---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the Veeam backup server
{: #veeam-cr-sag-vbrcfg}

For the immutable backup and isolated recovery environments, the Veeam® backup server is configured by PowerShell. PowerShell is run locally on the Veeam backup server through an Ansible® playbook that is run on the automation server. Ansible uses WinRM to access Microsoft® Windows® servers. The following items are required by Ansible:

* PowerShell 3.0 or newer and at least .NET 4.0 to be installed.
* A WinRM listener that is created and activated.

Both these requirements are enabled by default in the {{site.data.keyword.cloud}} build of Windows 2019.

In this step, the following tasks are required to configure the Veeam backup server so that it can be accessed by the automation server:

* [Create a firewall rule](#veeam-cr-sag-vbrcfg-fw) that allows WinRM inbound on TCP port `5986`.
* [Create a service account for ansible automation](#veeam-cr-sag-vbrcfg-sa), and add to the local administrator group.

## Creating an inbound firewall rule
{: #veeam-cr-sag-vbrcfg-fw}

1. From the jump server, use the Remote Desktop Protocol (RDP) client to access the Veeam backup server.
2. On the Veeam backup server, open a PowerShell window with **Run as administrator** option.
3. Run the following command `New-NetFirewallRule -DisplayName "WinRM (HTTPS-In)" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 5986` to create the required firewall rule.

## Creating a service account for ansible automation
{: #veeam-cr-sag-vbrcfg-sa}

1. From the jump server, use the RDP client to access the Veeam backup server.
2. On the Veeam backup server, open a PowerShell window with **Run as administrator** option.
3. Use the following commands and enter a password at the prompt:

   ```text
   $n = "sa-ansible"
   $d = "Service Account for ansible control node"
   $pw = Read-Host -AsSecureString
   New-LocalUser -AccountNeverExpires -Description $d -Name $n -Password $pw -PasswordNeverExpires -Confirm:$false
   Add-LocalGroupMember -Group "Administrators" -Member $n
   ```
   {: codeblock}

4. Verify with `Get-LocalUser` and `Get-LocalGroupMember -Group "Administrators"`.

For more information, see [Setting up a Windows host](https://docs.ansible.com/ansible/latest/os_guide/windows_setup.html){: external}.

## Related links
{: #veeam-cr-sag-vbrcfg-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
