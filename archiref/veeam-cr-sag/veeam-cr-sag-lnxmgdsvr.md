---

copyright:

  years:  2023, 2024

lastupdated: "2024-01-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Creating a Veeam Linux managed server
{: #veeam-cr-sag-lnxmgdsvr}

This step describes a use case where a cyberadmin uses the Veeam® data integration API to access the cyberbackup.

Create a Veeam Linux® managed server from an existing Linux server. When the server becomes managed by Veeam, Veeam can access the server. For this use case, use the Veeam data integration API.

The Veeam data integration API allows the mounting of backup files on a Microsoft® Windows® or Linux server. You designate a restore point of the backup file, mount it as a Windows folder or Linux mount point and access the files in the backup file. To mount a virtual machine (VM) file system on servers with the Microsoft Windows operating system, Veeam uses the iSCSI protocol. To mount a VM file system on servers with Linux operating system, Veeam uses FUSE (File system in User space). FUSE is a simple interface for user space programs to export a virtual file system to the Linux kernel.

Linux supports a special block device, called the loop device, which maps a normal file onto a virtual block device. It allows for the file to be used as a virtual file system inside another file. 

This use case has the following tasks:

* Add the Linux server's credentials to the Veeam's credential store.
* Publish the content of the backup that mounts the last restore point of the required VMs on to the Linux server.
* Unpublish.

## Adding VBR credentials
{: #veeam-cr-sag-lnxmgdsvr-creds}

The following PowerShell commands add a user on the Linux Managed Server to the Veeam credentials repository. Replace `username` and `password` with the credentials of the Linux server to be managed.

```text
$LinuxManagedServerUser = "<username>"
$LinuxManagedServerPassword = "<password>"
$LinuxManagedServerDescription = "Service Account for Linux Managed Server"
$LinuxManagedServerSSHPort = "22"
Add-VBRCredentials -User $LinuxManagedServerUser -Password $LinuxManagedServerPassword -Description $LinuxManagedServerDescription -Type Linux -SshPort $LinuxManagedServerSSHPort -ElevateToRoot -AddToSudoers
```
{: codeblock}

## Publishing
{: #veeam-cr-sag-lnxmgdsvr-publish}

In the following PowerShell commands, replace `managed_linux_server_ip_or_fqdn`, `username`, and `backup_job_name` with your required values.

```text
$TargetServer = "<managed_linux_server_ip_or_fqdn>"
$CredsName = "<username>"
$TargetServerCreds = Get-VBRCredentials -Name $CredsName
$BackupJobName = "<backup_job_name>"

# Build objects
$BackupJobObjects = Get-VBRJobObject -Job $BackupJobName

# Mount last restore point for each VM in the backup job
Foreach ($Job in $BackupJobObjects) { $RestorePoint = $Job | Get-VBRRestorePoint -Name *$($Job.Name)* | Sort-Object –Property CreationTime –Descending | Select-Object -First 1; $Session = Publish-VBRBackupContent -RestorePoint $Restorepoint -TargetServerName $TargetServer -TargetServerCredentials $TargetServerCreds -EnableFUSEProtocol -RunAsync }

# Show mounted disk location
$SessionArray = Get-VBRPublishedBackupContentSession
Foreach ($Session in $SessionArray) { $ContentInfo = Get-VBRPublishedBackupContentInfo -Session $Session; Foreach ($Disk in $ContentInfo.Disks.DiskName) { Write-Host $Disk } }
```
{: codeblock}

For understanding the examples of the mounted files systems and the underlying network connections, see [Examples](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lnxmgdsvr#veeam-cr-sag-lnxmgdsvr-examples).

## Unpublishing
{: #veeam-cr-sag-lnxmgdsvr-unpublish}

When you no longer require access to the published backup, the following PowerShell commands can be used to unpublish:

```text
$SessionArray = Get-VBRPublishedBackupContentSession
Foreach ($Session in $SessionArray) { Unpublish-VBRBackupContent -Session $Session -RunAsync } 
```
{: codeblock}

## Examples
{: #veeam-cr-sag-lnxmgdsvr-examples}

On the Linux managed server, no connections are there to any Veeam components.

```text
sudo netstat -nutlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      136174/sshd         
tcp        0      0 0.0.0.0:6162            0.0.0.0:*               LISTEN      13716/veeamtranspor 
tcp6       0      0 :::22                   :::*                    LISTEN      136174/sshd         
udp        0      0 127.0.0.1:323           0.0.0.0:*                           1663/chronyd        
udp6       0      0 ::1:323                 :::*                                1663/chronyd       
```
{: codeblock}

On the Linux managed server, the `veeamagent` opened TCP `2500 - 2502` ports:

```text
sudo netstat -nutlp
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name    
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      136174/sshd         
tcp        0      0 0.0.0.0:6162            0.0.0.0:*               LISTEN      13716/veeamtranspor 
tcp        0      0 0.0.0.0:2500            0.0.0.0:*               LISTEN      710143/veeamagent   
tcp        0      0 0.0.0.0:2501            0.0.0.0:*               LISTEN      711191/veeamagent   
tcp        0      0 0.0.0.0:2502            0.0.0.0:*               LISTEN      712309/veeamagent   
tcp6       0      0 :::22                   :::*                    LISTEN      136174/sshd         
udp        0      0 127.0.0.1:323           0.0.0.0:*                           1663/chronyd        
udp6       0      0 ::1:323                 :::*                                1663/chronyd 
```
{: codeblock}

On the Linux-managed server, the mount points to the published files, as shown in the following example.

```text
lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0     7:0    0  600M  0 loop /tmp/Veeam.Mount.FS.b2811b87-5bf4-4056-8134-21ce9555dca7/centos01-flat.vmdk_0
loop1     7:1    0 67.2M  1 loop /snap/lxd/21835
loop2     7:2    0 61.9M  1 loop /snap/core20/1242
loop3     7:3    0 55.5M  1 loop /snap/core18/2246
loop4     7:4    0 32.5M  1 loop /snap/snapd/13640
loop5     7:5    0 61.9M  1 loop /snap/core20/1169
loop6     7:6    0 42.2M  1 loop /snap/snapd/13831
loop7     7:7    0 67.2M  1 loop /snap/lxd/21803
loop8     7:8    0 55.5M  1 loop /snap/core18/2253
loop9     7:9    0    1G  0 loop /tmp/Veeam.Mount.FS.b2811b87-5bf4-4056-8134-21ce9555dca7/centos01-flat.vmdk_1
loop10    7:10   0  1.6G  0 loop 
loop11    7:11   0 12.8G  0 loop /tmp/Veeam.Mount.FS.b2811b87-5bf4-4056-8134-21ce9555dca7/cl-root
loop12    7:12   0  600M  0 loop /tmp/Veeam.Mount.FS.5f9917d0-cd25-4497-9c36-de21d5c93e23/centos02-flat.vmdk_0
loop13    7:13   0    1G  0 loop /tmp/Veeam.Mount.FS.5f9917d0-cd25-4497-9c36-de21d5c93e23/centos02-flat.vmdk_1
loop14    7:14   0  1.6G  0 loop 
loop15    7:15   0 12.8G  0 loop /tmp/Veeam.Mount.FS.5f9917d0-cd25-4497-9c36-de21d5c93e23/cl-root
loop16    7:16   0    1M  0 loop 
loop17    7:17   0    1G  0 loop /tmp/Veeam.Mount.FS.3b386d5e-9906-47ec-b8bd-7e17131f68a3/moss-web02-flat.vmdk_1
loop18    7:18   0 29.5G  0 loop /tmp/Veeam.Mount.FS.3b386d5e-9906-47ec-b8bd-7e17131f68a3/ubuntu-vg-ubuntu-lv
sda       8:0    0  931G  0 disk 
├─sda1    8:1    0    1G  0 part /boot
├─sda2    8:2    0    1G  0 part [SWAP]
└─sda3    8:3    0  929G  0 part /
sdb       8:16   0 10.9T  0 disk 
└─sdb1    8:17   0 10.9T  0 part /mnt/veeamrepo01 
```
{: codeblock}

On the Veeam backup server, the following connections can be seen, where:

* `10.38.207.157` is the Veeam backup server.
* `10.38.207.142` is the Veeam Linux managed server that is being used to mount the published files.
* `10.38.207.178` is the Veeam Linux hardened backup server.

```text
netstat -nt
Active Internet connections (w/o servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State      
tcp        0      0 10.38.207.137:22        10.38.207.142:58912     ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37784    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37786    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37788    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37790    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37792    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37794    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37796    ESTABLISHED
tcp        0      0 10.38.207.157:2500     10.38.207.142:37798    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57486    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57488    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57490    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57492    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57494    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57496    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57498    ESTABLISHED
tcp        0      0 10.38.207.157:2501     10.38.207.142:57500    ESTABLISHED
tcp        0      0 10.38.207.157:53207    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53219    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53255    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53273    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53313    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53323    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53463    10.38.207.178:6162     ESTABLISHED
tcp        0      0 10.38.207.157:53464    10.38.207.178:6162     ESTABLISHED
tcp        0      0 10.38.207.157:53466    10.38.207.178:2501     ESTABLISHED
tcp        0      0 10.38.207.157:53467    10.38.207.178:2501     ESTABLISHED
tcp        0      0 10.38.207.157:53468    10.38.207.178:2501     ESTABLISHED
tcp        0      0 10.38.207.157:53469    10.38.207.178:2501     ESTABLISHED
tcp        0      0 10.38.207.157:53471    10.38.207.178:6162     ESTABLISHED
tcp        0      0 10.38.207.157:53473    10.38.207.178:6162     ESTABLISHED
tcp        0      0 10.38.207.157:53475    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53476    10.38.207.178:2502     ESTABLISHED
tcp        0      0 10.38.207.157:53477    10.38.207.178:2502     ESTABLISHED
tcp        0      0 10.38.207.157:53482    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53486    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53491    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53492    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53493    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53498    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53499    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53500    10.38.207.142:22       ESTABLISHED
tcp        0      0 10.38.207.157:53502    10.38.207.142:2500     ESTABLISHED
tcp        0      0 10.38.207.157:53503    10.38.207.142:2500     ESTABLISHED
tcp        0      0 10.38.207.157:53505    10.38.207.142:2501     ESTABLISHED
tcp        0      0 10.38.207.157:53506    10.38.207.142:2501     ESTABLISHED
tcp        0      0 10.38.207.157:53508    10.38.207.142:2502     ESTABLISHED
tcp        0      0 10.38.207.157:53509    10.38.207.142:2502     ESTABLISHED
```
{: codeblock}

## Related links
{: #veeam-cr-sag-lnxmgdsvr-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
* [Veeam Data Integration API](https://helpcenter.veeam.com/docs/backup/vsphere/data_integration_api.html?ver=120){: external}
