---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the Linux hardened repository server
{: #veeam-cr-sag-lhbrmng}

This step describes the Ansible® playbook that adds the Linux® hardened backup repository as a Veeam® managed server into the Veeam backup infrastructure. The playbook does the following tasks:

* [Create Windows® firewall rules](#veeam-cr-sag-lhbrmng-fw).
* [Add the Linux hardened backup repository](#veeam-cr-sag-lhbrmng-linux-repo).
* (Optional) [Create a scale-out backup repository](#veeam-cr-sag-lhbrmng-scale-out-repo).

The playbook can be written locally on your laptop by using an editor, such as Visual Studio Code, and transferred to the automation server `\swlib\ansible` directory, or edited locally on the automation server in a text editor, such as vi or nano.

## Creating the playbook
{: #veeam-cr-sag-lhbrmng-play}

The playbook `create_lhbr.yml` starts with the following code:

```text
- hosts: vbr
  vars_files:
    - vault
  vars:
    lhbr_user: veeamlhbr
    lhbr_password: "{{ vault_lhbr_password }}"
    lhbr_vbr_name: <lhbr_vbr_name>
    lhbr_fqdn: <lhbr_fqdn>
    immutability_period: <immutability_period>
    max_concurrent_jobs: <max_concurrent_jobs>
```
{: codeblock}

Replace `<lhbr_vbr_name>`, `<lhbr_fqdn>`, and `<immutability_period>` in the previous code snippet with the values that you captured in the earlier steps. The previous code does the following actions:

* Defines that the playbook is run on the hosts that are defined as `vbr` in the inventory file.
* Defines a file that contains other variables, called `vault`. The `vault` file that was created in the previous step is encrypted, and contains sensitive variables, such as passwords.
* Defines the shortname that is used in designating the Linux hardened repository `<lhbr_vbr_name>`, and the FQDN of the server.


## Creating Windows firewall rules
{: #veeam-cr-sag-lhbrmng-fw}

The following code snippet adds Windows® firewall rules to allow inbound traffic to the Veeam backup server.

```text
  tasks:
    - name: Veeam firewall rule TCP 111 in
      community.windows.win_firewall_rule:
        name: Veeam port mapper service (TCP-in)
        group: Veeam
        localport: 111
        action: allow
        direction: in
        protocol: tcp
        state: present
        enabled: yes

    - name: Veeam firewall rule UDP 111 in
      community.windows.win_firewall_rule:
        name: Veeam port mapper service (UDP-in)
        group: Veeam
        localport: 111
        action: allow
        direction: in
        protocol: udp
        state: present
        enabled: yes

    - name: Veeam firewall rule TCP 1058 in
      community.windows.win_firewall_rule:
        name: Veeam Mount acceptor port of vPower NFS service (TCP-in)
        group: Veeam
        localport: 1058
        action: allow
        direction: in
        protocol: tcp
        state: present
        enabled: yes

    - name: Veeam firewall rule TCP 2049 in
      community.windows.win_firewall_rule:
        name: Veeam NFS acceptor port of vPower NFS service (TCP-in)
        group: Veeam
        localport: 2049
        action: allow
        direction: in
        protocol: tcp
        state: present
        enabled: yes

    - name: Veeam firewall rule TCP 2500-3300 in
      community.windows.win_firewall_rule:
        name: Veeam data transmission channels (TCP-in)
        group: Veeam
        localport: 2500-3300
        action: allow
        direction: in
        protocol: tcp
        state: present
        enabled: yes
```
{: codeblock}

In the code snippet, Veeam port mapper service, mount acceptor port and NFS acceptor port are used by vPower NFS service that presents the backup files to VMware ESXi™ hosts. Veeam data transmission channels are used between Veeam components that include the Veeam Hardened backup repository.

## Adding the Linux hardened backup repository
{: #veeam-cr-sag-lhbrmng-linux-repo}

The following code snippet adds the Linux hardened repository as a Veeam managed server, and then adds the managed server as a backup repository.

```text
    - name: Connect to the local VBR server
      win_shell: Connect-VBRServer

    - name: Add the server as a Veeam Managed Server
      win_shell: Add-VBRLinux -Name '{{ lhbr_fqdn }}' -SSHUser '{{ lhbr_user}}' -SSHPassword '{{ lhbr_password }}' -Description "Linux Hardened Repository - {{ lhbr_vbr_name }}" -SSHElevateToRoot:$true -SSHTempCredentials:$true -Confirm:$false

    - name: Add the Veeam Managed Server as a Linux Hardened Backup Repository
      win_shell: Add-VBRBackupRepository -Folder /mnt/veeamrepo01 -Type LinuxLocal -ImmutabilityPeriod '{{ immutability_period }}' -EnableBackupImmutability:$true -EnableXFSFastClone:$true -AlignDataBlocks:$true -UsePerVMFile:$true -MaxConcurrentJobs '{{ max_concurrent_jobs }}' -Server '{{ lhbr_fqdn }}' -Description "Linux Hardened Repository" -Name '{{ lhbr_vbr_name }}'
```
{: codeblock}

* `-SSHTempCredentials:$true` is used so that the SSH credentials are not entered into Veeam's credential store.
* `-EnableXFSFastClone:$true` defines that the Fast Clone technology is enabled for the backup repository.
* `-AlignDataBlocks:$true` indicates that the backup data blocks must be decompressed before you store to the repository.
* `-UsePerVMFile:$true` indicates that the backup repository must create per-virtual machine (VM) backup files.

## Creating a scale-out backup repository
{: #veeam-cr-sag-lhbrmng-scale-out-repo}

The following code snippet adds the Linux hardened repository as an extant to a scale-out backup repository. This step is optional. The code is extracted from [Protect against ransomware with Immutable Backups: a Veeam Guide](https://www.veeam.com/wp-guide-protect-ransomware-immutable-backups.html){: external}. The repository configuration must be a stand-alone repository (Scale-Out-Backup-Repository is technically compliant only if the “copy” policy is used for capacity tier).

```text
    - name: Create a Scale-Out Backup Repository
      win_shell: Add-VBRScaleOutBackupRepository -PolicyType DataLocality -Extent '{{ lhbr_vbr_name }}' -Name "Linux Hardened Repository - {{ lhbr_vbr_name }}" -Description "Linux Hardened Repository" -UsePerVMBackupFiles:$true
```
{: codeblock}

## Related links
{: #veeam-cr-sag-lhbrmng-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
* [Add-VBRLinux](https://helpcenter.veeam.com/docs/backup/powershell/add-vbrlinux.html?ver=120){: external}
* [Add-VBRBackupRepository](https://helpcenter.veeam.com/docs/backup/powershell/add-vbrbackuprepository.html?ver=120){: external}
* [Per-Machine Backup Files](https://helpcenter.veeam.com/docs/backup/vsphere/per_vm_backup_files.html?ver=120){: external}
* [Task Limitation for Backup Repositories](https://helpcenter.veeam.com/docs/backup/vsphere/limiting_tasks.html?ver=120){: external}

