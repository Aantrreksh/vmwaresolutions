---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Creating the airgap by using Juniper vSRX
{: #veeam-cr-sag-vsrx}

The following steps are needed only when you are creating an isolated recovery environment and you are using the Juniper® vSRX to isolate the environment.

An Ansible® playbook is used to configure the Juniper vSRX to allow traffic to the Veeam® Linux® Hardened repository in the isolated recovery environment from the Veeam backup proxies in the production environment. After the cyberbackup is completed, the Ansible playbook is used to block the traffic, isolating the Veeam Linux Hardened repository from the production environment. The Ansible playbook is initiated by a cron job on the automation server.

The document also describes a second Ansible playbook that can be used to schedule the opening and closing of the airgap.

The playbook might be extended to trigger the Veeam backup job instead of running the backup job on a schedule controlled by the Veeam backup server. For more information about using the Veeam PowerShell module, see [Start-VBRJob](https://helpcenter.veeam.com/docs/backup/powershell/start-vbrjob.html?ver=120){: external}.

As an alternative, scripts can be used before and after the backup job that connects to the automation server and initiates the Ansible playbook. For more information, see [Script settings](https://helpcenter.veeam.com/docs/backup/vsphere/backup_job_advanced_scripts_vm.html?ver=120){: external} and [New-PSSession](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/new-pssession?view=powershell-7.2){: external}.

The New-PSSession module requires PowerShell 7. For more information, see [Installing the MSI package](https://learn.microsoft.com/en-us/powershell/scripting/install/installing-powershell-on-windows?view=powershell-7.2#msi){: external}.
{: note}

Another option is to use the Posh-Junos® PowerShell module to interface with the vSRX directly from the Veeam backup server. For more information, see [Scripting how to: Windows® PowerShell](https://community.juniper.net/browse/blogs/blogviewer?blogkey=0903395c-8f62-433d-be52-ad636d75ed9c){: external}.

## Opening and closing the airgap
{: #veeam-cr-sag-vsrx-airgap}

The document does not describe the configuration of the Juniper vSRX. You must create the required configuration. The playbook assumes that the vSRX configuration includes the following items:

* A user, called `sa-ansible`, with an SSH key.
   * Set system login user sa-ansible `uid 2002`
   * Set system login user sa-ansible `class super-user`
   * Set system login user sa-ansible `authentication ssh-rsa <public_key>`
* NETCONF is enabled.
   * Set system services netconf ssh port `830`
   * Set firewall filter PROTECT-IN term NETCONF from destination-address `<vSRX_private_ip>/32`
   * Set firewall filter PROTECT-IN term NETCONF from protocol TCP
   * Set firewall filter PROTECT-IN term NETCONF from destination-port `830`
   * Set firewall filter PROTECT-IN term NETCONF then accept
* The security zones are configured as follows.
   * `IBM_CLOUD_PRIVATE` on `reth0` (untrusted network)
   * `IBM_CLOUD_PUBLIC` on `reth1` (untrusted network)
   * `IRE_PRIVATE` on `reth2` (trusted network)
   * `IRE_PUBLIC` on `reth3` (trusted network)
* Address book entries in an address book, called `CYBER`, for the Veeam proxies and the Veeam Linux hardened repository.
   * Set security address-book `CYBER` address PROXY_1 `<proxy_1_ip>/32`
   * Set security address-book `CYBER` address PROXY_2 `<proxy_2_ip>/32`
   * Set security address-book `CYBER` address LHBR_1 `<lhbr_ip>/32`
   * Set security address-book `CYBER` address-set CYBER_PROD address PROXY_1
   * Set security address-book `CYBER` address-set CYBER_PROD address PROXY_2
   * Set security address-book `CYBER` address-set CYBER_IRE address LHBR_1
   * Set security address-book `CYBER` attach zone `IBM_CLOUD_PRIVATE`
   * Set security address-book `CYBER` attach zone `IRE_PRIVATE`
* A custom application that defines the TCP ports `2500 - 3300`, which is the default range of ports that are used as data transmission channels by Veeam.
   * Set applications - application VEEAM_DATA protocol TCP
   * Set applications - application VEEAM_DATA destination-port 2500-3300
* A security policy is defined that denies traffic from the Veeam proxies to the Veeam Linux Hardened repositories.
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP match source-address CYBER_PROD
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP match destination-address CYBER_IRE
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP match application VEEAM_DATA
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP then deny
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP then log session-init
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP then log session-close
   * Set security policies from zone `IBM_CLOUD_PRIVATE` to zone `IRE_PRIVATE` policy AIRGAP then count

The Ansible playbook uses the `junipernetworks.junos.junos_config` module, which enables the management of the configuration on devices that run Juniper JUNOS. This module requires the NETCONF system service to be enabled on the remote device that is being managed. The module can be installed on the Ansible server by using the command `ansible-galaxy collection install junipernetworks.junos`.

The Ansible hosts file contains the following lines:

```text
[vsrx]
gateway01 ansible_host=<vsrx_private_ip> ansible_user=sa-ansible ansible_connection=ansible.netcommon.netconf ansible_network_os=junipernetworks.junos.junos
```
{: codeblock}

* `[vsrx]` needs to match the `- hosts: vsrx` entry in the airgap.yml file.
* `<vsrx_private_ip>` is the private IP address of the vSRX that is reachable from the automation server that runs Ansible.
* The ansible user needs to match the user configured on the vSRX, for example `set system login user sa-ansible`.

The Ansible playbook is run by using `ansible-playbook airgap.yml --tag open` or `ansible-playbook airgap.yml --tag close`.

* The script connects to the vSRX through the private IP address over NETCONF as the user sa-ansible and an SSH key for that user.
* The command `show security policies policy-name AIRGAP` is used and the output displayed.
* If the `--tag close` option is used, the command `set security policies from-zone IBM_CLOUD_PRIVATE to-zone IRE_PRIVATE policy AIRGAP then deny` is run.
* If the `--tag open` option is used, the command `set security policies from-zone IBM_CLOUD_PRIVATE to-zone IRE_PRIVATE policy AIRGAP then permit` is run.
* The command `show security policies policy-name AIRGAP` is used again and the output displayed.
* The `ansible - airgap opened` or `ansible - airgap closed` comment is used and can be seen when you use the `show system commit` on the vSRX appliance.

    ```text
    0   2022-04-22 10:48:40 UTC by sa-ansible via netconf
    ansible - airgap opened
    1   2022-04-22 10:30:21 UTC by sa-ansible via netconf
    ansible - airgap closed
    ```
    {: codeblock}

The Ansible playbook file `airgap.yml` contains the following lines:

```text
- hosts: vsrx
  connection: local
  gather_facts: no

  tasks:
    - name: Get show security policies policy-name AIRGAP
      junipernetworks.junos.junos_command:
        commands:
        - show security policies policy-name AIRGAP
      register: airgap_policy
      tags:
        - open
        - close

    - name: Display AIRGAP security policy
      debug:
        var: airgap_policy.stdout_lines
      tags:
        - open
        - close

    - name: Close airgap
      junipernetworks.junos.junos_config:
        lines:
          - set security policies from-zone IBM_CLOUD_PRIVATE to zone IRE_PRIVATE policy AIRGAP then deny
        comment: ansible - airgap closed
      tags: close

    - name: Open airgap
      junipernetworks.junos.junos_config:
        lines:
          - set security policies from-zone IBM_CLOUD_PRIVATE to zone IRE_PRIVATE policy AIRGAP then permit
        comment: ansible - airgap opened
      tags: open

    - name: Get show security policies policy-name AIRGAP
      junipernetworks.junos.junos_command:
        commands:
        - show security policies policy-name AIRGAP
      register: airgap_policy
      tags:
        - open
        - close

    - name: Display AIRGAP security policy
      debug:
        var: airgap_policy.stdout_lines
      tags:
        - open
        - close
```
{: codeblock}

## Scheduling
{: #veeam-cr-sag-vsrx-sched}

The following file `sched_airgap.yml` uses cron on the automation server to open and close the airgap based on a schedule. The `ansible-playbook sched_airgap.yml --tags set` command configures the cron job while `ansible-playbook sched_airgap.yml --tags cancel` command deletes the cron job. You can verify by using the `crontab -l` command. Ansible output is captured in a log file `/swlib/ansible/airgap.log`. The following example opens the airgap at 01:00 and closes the airgap at 05:00 each day.

```text
- hosts: localhost
  connection: local
  gather_facts: no

  tasks:
  - name: Create the airgap-open cron job
    ansible.builtin.cron:
      name: airgap-open
      weekday: "*"
      minute: "*"
      hour: "1"
      job: "ansible-playbook -i /swlib/ansible/hosts /swlib/ansible/airgap.yml --tags open >>/swlib/ansible/airgap.log"
    tags: set

  - name: Create the airgap-close cron job
    ansible.builtin.cron:
      name: airgap-close
      weekday: "*"
      minute: "*"
      hour: "5"
      job: "ansible-playbook -i /swlib/ansible/hosts /swlib/ansible/airgap.yml --tags close >>/swlib/ansible/airgap.log"
    tags: set

  - name: Delete the airgap-open cron job
    ansible.builtin.cron:
      name: airgap-open
      state: absent
    tags: cancel

  - name: Delete the airgap-close cron job
    ansible.builtin.cron:
      name: airgap-close
      state: absent
    tags: cancel
```
{: codeblock}

If you are creating the cyber-recovery isolated recovery environment solution architecture, then see [Production environment configuration](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-ireprod) for details.

## Related links
{: #veeam-cr-sag-vsrx-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
* [Juniper vSRX overview](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview)
* [Managing Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-managing)
* [Juniper Networks vSRX deployment and operation with {{site.data.keyword.vcf-auto-short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vcsvsrx-intro)
* [Managing VLANs with a gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-managing-vlans-and-gateway-appliances)
* [{{site.data.keyword.cloud_notm}} IP ranges](/docs/gateway-appliance?topic=gateway-appliance-ibm-cloud-ip-ranges)
* [VLANs and subnets in {{site.data.keyword.vmwaresolutions_full}}](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-vlans-subnets)
* [Ports that are used for deployment and Day 2 operations](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-deploy-day2ops)
* [Ports used by {{site.data.keyword.vmwaresolutions_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-vmwareuses)
* [Ports for services](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-services)
