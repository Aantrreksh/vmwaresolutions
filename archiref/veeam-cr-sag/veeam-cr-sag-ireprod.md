---

copyright:

  years:  2023, 2024

lastupdated: "2024-01-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the production environment
{: #veeam-cr-sag-ireprod}

The steps in this document are needed only when you want to connect the isolated recovery environment to the production environment.

## Active Directory Domain Name Services (AD/DNS) configuration
{: #veeam-cr-sag-ireprod-addns}

The steps are implemented on the AD/DNS server in the production environment and not on the AD/DNS server in the isolated recovery environment.

The Veeam® service in the isolated recovery environment needs to connect to the vCenter appliance in the production environment. Therefore, the Veeam service requires a service account that is configured in the active directory domain of the production environment.

1. Use the RDP client to access the AD/DNS server.
2. Open a PowerShell console with Administrator privileges.
3. Use the following commands to create a Veeam service account:

```text
$name = "sa-veeam-cyber-admin"
$sn = "sa-veeam-cyber-admin"
$descr = "Service Account for Veeam cyber-recovery"
$dname = "Cyber-recovery Admin"
$path = "CN=ic4v-vCenter,CN=Users,DC=partner,DC=ibmcloud,DC=local"
$pw = "<sa_veeam_cyber_admin_password>"
$grp = "ic4v-vCenter"
New-ADUser -Name $name -DisplayName $dname -Description $descr -SamAccountName $sn -AccountPassword (convertto-securestring $pw -AsPlainText -Force) -Enabled $true -PasswordNeverExpires $true -ChangePasswordAtLogon $false
Add-ADGroupMember -Identity $grp -Members $sn
```
{: codeblock}

## Creating a vCenter role
{: #veeam-cr-sag-ireprod-role}

Create a vCenter role and assign the required permissions so that the Veeam service account can create backups of the production virtual machines (VMs).

The steps are implemented on the vCenter appliance in the production environment and not on the vCenter appliance server in the isolated recovery environment.

The role requires a list of privileges. You can view the list of privileges in the variable list `$privileges` in the following PowerCLI script. For more information, see [Backup](https://helpcenter.veeam.com/docs/backup/vsphere/backup.html?ver=120){: external}.

The script completes the following tasks:

* Defines the required privileges.
* Loads the PowerCLI SnapIn and sets the configuration to ignore invalid certificates.
* Defines the vCenter IP/FQDN, admin user, and password.
* Defines a name for the Veeam user, such as `veeambur`.
* Connects to the vCenter.
* Creates a role with the required permissions.
* Creates the permissions for the user against the required inventory objects.

### Procedure to create role and assign permissions
{: #veeam-cr-sag-ireprod-role-procd}

1. Use the remote desktop client to connect to the jump server.
2. Open a PowerShell console with Administrator privileges.
3. Define the following variables for the script:
   * The `<vcsa_fqdn>` is the FQDN or IP address of the vCenter appliance in the production environment.
   * The `<vcsa_user>` is the username of the account in vCenter appliance that has necessary privileges to add roles.
   * The `<vcsa_user_password>` is the password for the `<vcsa_user>`.
   * The `<sub_domain>` is the subdomain of the root domain, that is, for `example.test.local`, `<sub_domain>` is `example` and `<root_domain>` is `test.local`.
4. Use the following commands to create the role and assign permissions:

```text
Add-PSSnapin VMware.VimAutomation.Core -ea "SilentlyContinue"
Set-PowerCLIConfiguration -InvalidCertificateAction Ignore -Confirm:$false | Out-Null
$vcsa = "<vcsa_fqdn>"
$vcsauser = "<vcsa_user>"
$vcsapassword = '<vcsa_user_password>'
$securevcsapassword = ConvertTo-SecureString -String $vcsapassword -AsPlainText -Force
$sn = "sa-veeam-cyber-admin"
$id = "<sub_domain>"
$role = "veeambur"
$principal = "$id\$sn"
$creds = New-Object System.Management.Automation.PSCredential -ArgumentList $vcsauser,$securevcsapassword
$privileges = @(
    'System.Anonymous',
    'System.View',
    'System.Read',
    'Global.ManageCustomFields',
    'Global.SetCustomField',
    'Global.LogEvent',
    'Global.Licenses',
    'Global.Settings',
    'Global.DisableMethods',
    'Global.EnableMethods',
    'Folder.Create',
    'Folder.Delete',
    'Datastore.Browse',
    'Datastore.DeleteFile',
    'Datastore.FileManagement',
    'Datastore.AllocateSpace',
    'Datastore.Config',
    'Network.Config',
    'Network.Assign',
    'DVPortgroup.Create',
    'DVPortgroup.Modify',
    'DVPortgroup.Delete',
    'Host.Config.Maintenance',
    'Host.Config.Storage',
    'Host.Config.Network',
    'Host.Config.AdvancedConfig',
    'Host.Config.Patch',
    'VirtualMachine.Inventory.Create',
    'VirtualMachine.Inventory.Register',
    'VirtualMachine.Inventory.Delete',
    'VirtualMachine.Inventory.Unregister',
    'VirtualMachine.Interact.PowerOn',
    'VirtualMachine.Interact.PowerOff',
    'VirtualMachine.Interact.Suspend',
    'VirtualMachine.Interact.ConsoleInteract',
    'VirtualMachine.Interact.DeviceConnection',
    'VirtualMachine.Interact.SetCDMedia',
    'VirtualMachine.Interact.SetFloppyMedia',
    'VirtualMachine.Interact.GuestControl',
    'VirtualMachine.GuestOperations.Query',
    'VirtualMachine.GuestOperations.Modify',
    'VirtualMachine.GuestOperations.Execute',
    'VirtualMachine.Config.Rename',
    'VirtualMachine.Config.AddExistingDisk',
    'VirtualMachine.Config.AddNewDisk',
    'VirtualMachine.Config.Annotation',
    'VirtualMachine.Config.RemoveDisk',
    'VirtualMachine.Config.RawDevice',
    'VirtualMachine.Config.AddRemoveDevice',
    'VirtualMachine.Config.EditDevice',
    'VirtualMachine.Config.Settings',
    'VirtualMachine.Config.Resource',
    'VirtualMachine.Config.AdvancedConfig',
    'VirtualMachine.Config.DiskLease',
    'VirtualMachine.Config.DiskExtend',
    'VirtualMachine.Config.ChangeTracking',
    'VirtualMachine.State.CreateSnapshot',
    'VirtualMachine.State.RevertToSnapshot',
    'VirtualMachine.State.RemoveSnapshot',
    'VirtualMachine.State.RenameSnapshot',
    'VirtualMachine.Provisioning.MarkAsTemplate',
    'VirtualMachine.Provisioning.MarkAsVM',
    'VirtualMachine.Provisioning.DiskRandomAccess',
    'VirtualMachine.Provisioning.DiskRandomRead',
    'VirtualMachine.Provisioning.GetVmFiles',
    'VirtualMachine.Provisioning.PutVmFiles',
    'Resource.AssignVMToPool',
    'Resource.CreatePool',
    'Resource.DeletePool',
    'Resource.HotMigrate',
    'Resource.ColdMigrate',
    'Extension.Register',
    'Extension.Unregister',
    'VApp.AssignVM',
    'VApp.AssignResourcePool',
    'VApp.Unregister',
    'StoragePod.Config',
    'Cryptographer.Access',
    'Cryptographer.EncryptNew',
    'Cryptographer.Encrypt',
    'Cryptographer.Migrate',
    'Cryptographer.AddDisk',
    'InventoryService.Tagging.AttachTag',
    'StorageProfile.Update',
    'StorageProfile.View')

Connect-VIServer -Server $vcsa -Credential $creds | Out-Null
New-VIRole -Name $role -Privilege (Get-VIPrivilege -Id $privileges) | Out-Null
Get-VIRole -Name $role | Select-Object Description, PrivilegeList, Server, Name | Format-List
New-VIPermission -Principal $principal -Role $role -Entity (Get-Datacenter) -Propagate:$true -Confirm:$false
Disconnect-VIServer -Confirm:$false
```
{: codeblock}

The steps are completed for creating the cyber-recovery isolated environment solution architecture.

For a use case where a cyberadmin uses a PowerShell script that uses Veeam to do an instant restore of a production VM from the cyberbackup, see [Instant restore](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-instantrestore).

Additionally, for a use case where a cyberadmin uses the Veeam data integration API to access the cyberbackup, see [create a Veeam Linux managed server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lnxmgdsvr).

## Related links
{: #veeam-cr-sag-ireprod-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
