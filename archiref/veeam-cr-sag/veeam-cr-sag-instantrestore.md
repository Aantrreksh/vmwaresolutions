---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Instant restore
{: #veeam-cr-sag-instantrestore}

This document describes a use case where a cyberadmin uses a PowerShell script that uses Veeam®'s ability to do an instant restore of a production virtual machine (VM) from the cyberbackup.

Veeam's instant restore feature enables a VM to be started directly from the backup files. Veeam® vPower NFS service is used to access the backup files.

The script completes the following tasks:

* Runs from a PowerShell window on the Veeam backup server, or a PowerShell window on a different server where the Veeam PowerShell extension is installed. The Veeam backup server is also enabled for PowerShell remoting.
* Requires the following variables:
   * VM name `<vm_name>` from vCenter and the network name `<src_nw_name>` that the VM is connected to.
   * The VMware ESXi™ hostname `<esxi_hostname>` where the VM is restored.
   * A resource pool name `<resource_pool_name>` to which the restored VM belongs to.
   * The datastore `<datastore_name>` where the backup is restored.
   * A folder name `<folder_name>` in vCenter to which the restored VM belongs to.
   * The name of the target network `<tgt_nw_name>` that the restored VM is connected to.
* Retrieves the most recent retention point of the VM to be restored.
* Defines the restored VM name with a suffix of CR followed by a timestamp.
* Defines a description of the restore in the variable `$Reason`.
* Restores the VM:
   * The restored VM is powered on.
   * The PowerShell command is run asynchronously as the restore is a long-running process.
   * An anti-virus scan is initiated for Windows® OS and continues to scan after the first virus threat is found. If a virus is detected, the network on the VM is disabled.
* At the end of the instant restore, the VM is left powered on.

To find the VM names in the backup job, the following command can be used in a PowerShell window, where the JobName is set to a name of a Backup Job. In this example, the backup job is named `Cyber-backup - 1d1w30rp`:

```text
$JobName = "Cyber-backup - 1d1w30rp"
Get-VBRJob -Name $JobName | Get-VBRJobObject | Select-Object -Property Name
```
{: codeblock}

The following example shows some sample variables.

```text
$VMName           = "nrt01"
$SrcNetworkName   = "192-168-3-0-24"
$EsxiHostname     = "host002.test.ibmcloud.local"
$ResourcePoolName = "Cyber-restore-rp"
$DatastoreName    = "workload_share_LkXB6"
$FolderName       = "Cyber-restore"
$TgtNetworkName   = "cyber-veeam-recovery"
```
{: codeblock}

The PowerShell script is shown in the following example.

```text
# VM variables
$VMName = "<vm_name>"
$SrcNetworkName = "<src_nw_name>"

# Restore variables
$EsxiHostname = "<esxi_hostname>"
$ResourcePoolName = "<resource_pool_name>"
$DatastoreName = "<datastore_name>"
$FolderName = "<folder_name>"
$TgtNetworkName = "<tgt_nw_name>"

# Conversions
$LastRestorePoint = Get-VBRRestorePoint -Name $VMName | Sort-Object -Property CreationTime -Descending | Select-Object -First 1
$Esxi = Get-VBRServer -Type ESXi -Name $EsxiHostname
$ResourcePool = Find-VBRViResourcePool -Server $Esxi -Name $ResourcePoolName
$Datastore = Find-VBRViDatastore -Server $Esxi -Name $DatastoreName
$Folder = Find-VBRViFolder -Server $Esxi -Name $FolderName
$SrcNetwork = Get-VBRViServerNetworkInfo -Server $Esxi | Where-Object { $_.NetworkName -eq $SrcNetworkName }
$TgtNetwork = Get-VBRViServerNetworkInfo -Server $Esxi | Where-Object { $_.NetworkName -eq $TgtNetworkName }
$RestorePointDate = $LastRestorePoint.CreationTime
$RestoreDate = Get-Date -Format yyyy-MM-dd-HH:mm
$Reason = "Cyber-restore of $VMName retention point: $RestorePointDate at $RestoreDate"
$RestoredVMName = "$VMName-CR-$RestoreDate"

# Instant restore
Start-VBRInstantRecovery -RestorePoint $LastRestorePoint -Server $Esxi -ResourcePool $ResourcePool -Datastore $Datastore -Folder $Folder -SourceNetwork $SrcNetwork -TargetNetwork $TgtNetwork -VMName $RestoredVMName -PowerUp:$True -Reason $Reason -RunAsync -EnableAntivirusScan -EnableEntireVolumeScan -VirusDetectionAction DisableNetwork
```
{: codeblock}

## Log
{: #veeam-cr-sag-instantrestore-logs}

The following PowerShell commands display the log entries of the last restore session for the VM `<vm_name>`:

```text
$VMName = "<vm_name>"
$Session = Get-VBRRestoreSession -Name $VMName | Sort-Object -Property CreationTime -Descending | Select-Object -First 1
$Logs = $Session.logger.GetLog().GetRecordsSortedByOrdinalId()
foreach ($Log in $Logs) { Write-Host $Log.Title }
```
{: codeblock}

The following example shows the log entries for a VM called `nrt01`. The antivirus scan was skipped for this Linux® VM.

```text
Skipping nrt01: operating system is not supported for antivirus scan
Starting nrt01-CR-2021-11-19-12:50 recovery
Connecting to host host002.partner.ibmcloud.local
Restoring from Linux Hardened Repository - LHBR01
Checking if vPower NFS datastore is mounted on host
Locking backup files
Publishing backup files
Preparing change storage
Updating VM configuration
Checking free disk space available to Power NFS server
Registering VM
Creating VM snapshot
Powering on VM
Updating session history
nrt01-CR-2021-11-19-12:50 has been recovered successfully
Waiting for user to start migration
```
{: codeblock}

On the Linux hardened repository, the following ports were temporarily opened on the Linux firewall designated by the comment `Veeam rule 876f0752-7209-4e8b-8b34-fa0af7dbced4`.

```text
ufw status
Status: active
To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       10.38.207.142              # Allow SSH from trusted servers
6162/tcp                   ALLOW       10.38.207.157              # Allow Veeam Mgmt from Veeam BUR server
2500/tcp                   ALLOW       Anywhere                   # Veeam rule 876f0752-7209-4e8b-8b34-fa0af7dbced4
2501/tcp                   ALLOW       Anywhere                   # Veeam rule 876f0752-7209-4e8b-8b34-fa0af7dbced4

6162/tcp                   ALLOW OUT   Anywhere                   # Veeam transport rule
2500/tcp                   ALLOW OUT   Anywhere                   # Veeam rule 876f0752-7209-4e8b-8b34-fa0af7dbced4
2501/tcp                   ALLOW OUT   Anywhere                   # Veeam rule 876f0752-7209-4e8b-8b34-fa0af7dbced4
```
{: codeblock}

## Stopping the instant recovery
{: #veeam-cr-sag-instantrestore-stop}

The instant recovery session can be stopped by using the following command `Get-VBRInstantRecovery | Where-Object {$_.VMName -eq $RestoredVMName} | Stop-VBRInstantRecovery`.

For a use case where a cyberadmin uses the Veeam data integration API to access the cyberbackup, see [create a Veeam Linux managed server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lnxmgdsvr).

## Related links
{: #veeam-cr-sag-instantrestore-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
