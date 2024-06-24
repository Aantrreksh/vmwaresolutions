---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the OS of the Linux hardened repository server
{: #veeam-cr-sag-lhbrcfg}

This step describes the Ansible® playbook that contains a number of operating system (OS) configuration tasks that prepares the server for its role as a Veeam® Linux® hardened backup server. The playbook is tested against the {{site.data.keyword.redhat_full}} distribution.

The playbook does the following tasks:

* [Upgrades the OS packages](#veeam-cr-sag-lhbrcfg-pkg)
* [Configures the time zone](#veeam-cr-sag-lhbrcfg-timezone)
* [Adds a user](#veeam-cr-sag-lhbrcfg-user) called `veeamlhbr` and change ownership of the file system to this user
* [Configures the Linux firewall](#veeam-cr-sag-lhbrcfg-fw)
* [Changes the DNS entry](#veeam-cr-sag-lhbrcfg-dns)

The playbook can be written locally on your laptop by using an editor, such as Visual Studio Code, and transferred to the automation server `\swlib\ansible` directory, or edited locally on the automation server in a text editor, such as vi or nano.

The server name and IP address must be registered in DNS in the AD/DNS server.
{: note}

## Creating the playbook
{: #veeam-cr-sag-lhbrcfg-play}

The playbook `create_lhbr.yml` starts with the following code.

```text
- hosts: lhbr
  vars_files:
    - vault
  vars:
    password: "{{ vault_lhbr_password }}"
    timezone: <timezone>
    vbr_ip: <vbr_ip>
    ansible_ip: <ansible_ip>
    dns_1: <addns1>
    dns_2: <addns2>

  tasks:
```
{: codeblock}

Replace `timezone`, `vbr_ip`, `ansible_ip`, `addns1`, and `addns2` in the previous code snippet with your values captured in the earlier steps. The previous code does the following actions:

* Defines that the playbook is run on the hosts that are defined as `lhbr` in the inventory file.
* Defines a file that contains other variables, called `vault`. The `vault` file that was created in the previous step is encrypted, and contains sensitive variables, such as passwords.
* Defines the time zone, the IP addresses of the VBR server and automation server to configure the firewall, and DNS IP addresses for the DNS change.

## Upgrading the OS packages
{: #veeam-cr-sag-lhbrcfg-pkg}

The following code snippet updates the package cache and upgrades the OS packages.

```text
tasks:
    - name: Update cache
      yum:
        update_cache: yes

    - name: Upgrade all packages
      yum:
        name: "*"
        state: latest
```
{: codeblock}

## Configuring the time zone
{: #veeam-cr-sag-lhbrcfg-timezone}

In the Red Hat distribution, the NTP server is configured and points to `servertime.service.softlayer.com`. Therefore, only the correct time zone must be configured.

```text
    - name: Set timezone
      community.general.timezone:
        name: "{{ timezone }}"
```
{: codeblock}

## Configuring the file system for the repository
{: #veeam-cr-sag-lhbrcfg-xfs}

The code snippet does the following actions:

* Unmounts the `/disk1` file system.
* Captures the UUID of the partition so that `fstab` can be configured.
* Mounts the `xfs` partition by using the UUID as `/mnt/veeamrepo01`.

```text
    - name: Unmount and remove from /etc/fstab
      ansible.posix.mount:
        path: /disk1
        state: absent

    - name: Unmount and remove from /etc/fstab
      ansible.posix.mount:
        path: /mnt/veeamrepo01
        state: absent

    - name: Get UUID of /dev/sdb1 and store in variable
      command: blkid -s UUID -o value /dev/sdb1
      register: uuid_dev_sdb1

    - name: Mount as /mnt/veeamrepo01 and add to /etc/fstab
      ansible.posix.mount:
        path: /mnt/veeamrepo01
        src: "UUID={{ uuid_dev_sdb1.stdout }}"
        fstype: xfs
        state: mounted
```
{: codeblock}

Before you run the previous code, if you run a `df -Th` command on the server, the output is shown as follows:

```text
Filesystem     Type      Size  Used Avail Use% Mounted on
devtmpfs       devtmpfs   32G     0   32G   0% /dev
tmpfs          tmpfs      32G     0   32G   0% /dev/shm
tmpfs          tmpfs      32G   42M   32G   1% /run
tmpfs          tmpfs      32G     0   32G   0% /sys/fs/cgroup
/dev/sda3      xfs       929G  9.2G  920G   1% /
/dev/sda1      xfs      1006M  273M  734M  28% /boot
/dev/sdb1      xfs        11T   80G   11T   1% /disk1
tmpfs          tmpfs     6.3G     0  6.3G   0% /run/user/1001
```
{: codeblock}

After you run the previous code, if you run the `df -Th` command, the output is shown as follows:

```text
Filesystem     Type      Size  Used Avail Use% Mounted on
devtmpfs       devtmpfs   32G     0   32G   0% /dev
tmpfs          tmpfs      32G     0   32G   0% /dev/shm
tmpfs          tmpfs      32G   42M   32G   1% /run
tmpfs          tmpfs      32G     0   32G   0% /sys/fs/cgroup
/dev/sda3      xfs       929G  9.2G  920G   1% /
/dev/sda1      xfs      1006M  273M  734M  28% /boot
/dev/sdb1      xfs        11T   80G   11T   1% /mnt/veeamrepo01
tmpfs          tmpfs     6.3G     0  6.3G   0% /run/user/1001
```
{: codeblock}

## Adding a user and changing ownership of the file system
{: #veeam-cr-sag-lhbrcfg-user}

The code snippet does the following actions:

* Adds a group, called `veeamlhbr`.
* Adds a user, called `veeamlhbr`.
* Changes the ownership of `/mnt/veeamrepo01`, and sets the permissions so that the owner can read, write, and run, and the group cannot read, write, and run. Other users cannot read, write, and run. Veeam uses this user to read and write to the file system.

Change file permissions for authentication certificates on the Linux server to maximize the repository security. For more information, see [Tips for enhanced security of hardened repository](https://helpcenter.veeam.com/docs/backup/vsphere/hardened_repository.html?ver=120){: external}.

```text
   - name: Create the veeamlhbr group
     ansible.builtin.group:
       name: veeamlhbr
       state: present

    - name: Add the user 'veeamlhbr' with a bash shell
      ansible.builtin.user:
        name: veeamlhbr
        shell: /bin/bash
        create_home: yes
        password: "{{ password | password_hash('sha512') }}"
        state: present
        groups: veeamlhbr,wheel
        append: yes

    - name: Change ownership of /mnt/veeamrepo01 to veeamlhbr
      ansible.builtin.file:
        path: /mnt/veeamrepo01
        state: directory
        owner: veeamlhbr
        group: veeamlhbr
        mode: "700"
```
{: codeblock}

## Configuring a Linux firewall
{: #veeam-cr-sag-lhbrcfg-fw}

The code snippet does the following actions:

* Allows SSH from the Veeam backup server on TCP port `22`. This rule is removed after the Veeam backup server is initially connected and the required Veeam services are installed.
* Allows SSH access from the automation server. This rule can be removed after the configuration task is complete. However, the future maintenance tasks might become more difficult.
* Allows the Veeam backup server access on TCP port `6162`. This port is the Veeam control channel that is used to communicate with the repository server.
* The firewall is started, enabled on startup, and enabled for logging.

```text
    - name: Enable firewalld on system reboot
      service:
        name: firewalld
        enabled: yes

    - name: Allow SSH
      ansible.posix.firewalld:
        service: ssh
        permanent: yes
        state: enabled

    - name: Allow incoming access from the vbr server for management
      ansible.posix.firewalld:
        port: 6162/tcp
        permanent: yes
        state: enabled

    - name: Reload firewall and enable firewall on boot
      service:
        name: firewalld
        state: restarted
```
{: codeblock}

## Changing the DNS
{: #veeam-cr-sag-lhbrcfg-dns}

The following code snippet changes the DNS from the {{site.data.keyword.cloud}} DNS resolvers - `10.0.80.11` and `10.0.80.12`, with the {{site.data.keyword.vcf-auto}} instances DNS - `addns1` and `addns2`.

```text
    - name: Change resolv nameserver_1
      replace:
        path: /etc/resolv.conf
        regexp: "10.0.80.11"
        replace: "{{ dns_1 }}"

    - name: Change resolv nameserver_2
      replace:
        path: /etc/resolv.conf
        regexp: "10.0.80.12"
        replace: "{{ dns_2 }}"
```
{: codeblock}

## Finalizing the playbook
{: #veeam-cr-sag-lhbrcfg-final}

Save the file. Ensure that the file is saved in the `\swlib\ansible` directory on the automation server.

## Related links
{: #veeam-cr-sag-lhbrcfg-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
