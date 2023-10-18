---

copyright:

  years: 2023

lastupdated: "2023-10-16"

keywords: managing backup repositories, editing backup repositories, managing permissions for S3 compatible object storage, fast clone

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Managing backup repositories
{: #veeam_repo_man_storage}

You can manage your backup repositories and the data that is stored in them in various ways: edit settings of the backup repositories, set up access permissions, rescan backup repositories or remove backup repositories. 

## Editing settings of backup repositories
{: #veeam_repo_man_storage_editing}

You can edit the settings of backup repositories that you have added to the backup infrastructure. To edit the settings of a backup repository, complete the following steps:

1. Open the **Backup infrastructure** view.
2. Open the inventory pane, select the **Backup repositories** node.
3. Open the working area, select the backup repository and click **Edit repository** on the ribbon or right-click the backup repository and select **Properties**.
4. Edit the backup repository settings as required. 

You cannot change the selected repository server and path to the folder used for storing backups.
{: note}

## Access permissions
{: #veeam_repo_man_storage_access}

If you want to store in the backup repository backups of virtual and physical machines that are created with Veeam Backup and Replication extra solutions, for example, Veeam Agent for Microsoft Windows®, Veeam® Agent for inux®, and so on, you must set up access permissions to backup repositories. Access permissions are granted to security principals such as users and AD groups by the backup administrator who works with Veeam Backup and Replication. Users with granted access permissions can target Veeam Agent backup jobs at this backup repository and perform restore from backups that are located in this backup repository.

If you plan to create backups in a Veeam backup repository with Veeam Agent backup jobs that are configured in Veeam Backup and Replication, you don't need to grant access permissions on the backup repository to users. In the Veeam Agent management scenario, to establish a connection between the backup server and protected computers, Veeam Backup and Replication uses a TLS certificate.
{: note}

Right after installation, access permissions on the default backup repository are set to Allow to everyone for testing and evaluation purposes. If necessary, you can change these settings. After you create a new backup repository, access permissions on this repository are set to Deny to everyone. To allow users to store backups in the backup repository, you must grant users with access permissions to this repository.

## Managing permissions of backup server
{: #veeam_repo_man_storage_permissions}

To grant access permissions to a security principal:

1. In Veeam Backup and Replication, open the **Backup infrastructure** view.
2. In the inventory pane, click one of the following nodes:
   * The backup repository node: if you want to grant access permissions on a regular backup repository.
   * The scale-out repository node: if you want to grant access permissions on a scale-out backup repository.
3. In the working area, select the necessary backup repository and click **Set access** permissions on the ribbon or right-click the backup repository and select **Access permissions**. If you do not see the set access permissions button on the ribbon or the access permissions command is not available in the menu, press and hold the `[Ctrl]` key, right-click the backup repository and select **Access permissions**.
4. In the **Standalone applications** window, specify whom you want to grant access permissions on this backup repository:
   
   * Allow to everyone: select this option if you want all users to be able to store backups. Setting access permissions to everyone is equal to granting access rights to the everyone Microsoft Windows group (anonymous users are excluded). 

      This scenario is recommended for demo environments only.
      {: important}

   * Allow to the following accounts or groups only: select this option if you want only specific users to be able to store backups in this backup repository. Click **Add** to the necessary users and groups to the list.

5. To encrypt backup files that are created in the backup repository by Veeam Agents operating in the stand-alone mode, select the **Encrypt backups that are stored in this repository** checkbox and choose the necessary password from the field. If you have not specified a password beforehand, click **Add** on the right or the **Manage passwords** link to add a new password. Veeam Backup and Replication encrypt files at the backup repository side that uses its built-in encryption mechanism.

If you want to encrypt backup files that are created by Veeam Agents operating in the managed mode, you must configure encryption in the backup job settings. For more information about how to encrypt backup files created by managed Veeam Agent for Microsoft Windows, see [Storage Settings](https://helpcenter.veeam.com/docs/backup/agents/agent_job_advanced_storage.html?ver=120){: external}.

## Managing Permissions for S3 Compatible object storage
{: #veeam_repo_man_storage_compatible}

If you plan to use an S3 Compatible object storage as an object storage repository, you must set up access permissions to the object storage. These permissions are used if you keep in object storage repositories backups created by Veeam Agent or by Veeam Cloud Connect tenant. For more information, see [Backup to Object Storage](https://helpcenter.veeam.com/docs/backup/agents/object_storage.html?ver=120){: external} in the Veeam Agent Management Guide and [Backup to Object Storage](https://helpcenter.veeam.com/docs/backup/cloud/cc_object_storage.html?ver=120){: external} in the Veeam Cloud Connect Guide.

To manage permissions for S3 Compatible object storage, perform the following:
1. In Veeam Backup and Replication, open the **Backup infrastructure** view.
2. In the inventory pane, click the **Backup repositories** node.
3. In the working area, select the necessary S3 compatible backup repository and click **Set access permissions** on the ribbon or right-click the backup repository and select **Access permissions**. If you do not see the set access permissions button on the ribbon or the access permissions command is not available in the menu, press and hold the `[Ctrl]` key. Then, right-click the backup repository and select **Access permissions**.
4. On the security tab, specify how Veeam Agent or an SP access an S3 Compatible object storage repository:

   * Agents share credentials to the the object storage repository — use this option if you want directly access the S3 Compatible object storage repository. In this case, the the Veeam agent uses credentials that you specified when added the S3 Compatible object storage repository to the backup infrastructure. This option is not secure since Veeam Backup and Replication will have access permissions on the bucket where you keep your folders with backups.
   * Provided by the backup server — use this option if you want to access the S3 Compatible object storage repository through a gateway server.
   * Provided by IAM/STS object storage capabilities — use this option if you want directly access the S3 Compatible object storage repository. In this case, Veeam Backup and Replication create service tokens that Veeam Agent or an SP will use to access the S3 Compatible object storage repository.

5. To specify credentials, complete the following steps:
   1. In the **Identity and access management (IAM) endpoint** field, specify the endpoint of your S3 Compatible object storage repository.
   2. In the **Security token service (STS) endpoint** field, specify the security token.

## Rescanning backup repositories
{: #veeam_repo_man_storage_rescanning}

You can rescan a backup repository that is configured in the backup infrastructure. Backup repository rescan might be required, if you have archived backups from a backup repository to tape and deleted backup files or you have copied backups to the backup repository manually and want to work with them in Veeam Backup and Replication. During the rescan operation, Veeam Backup and Replication gathers information about backups that are available in the backup repository and updates the list of backups in the configuration database. After the rescan operation, backups that were not in this configuration database will be shown on the Home view in the Backups > Disk (Imported) node. If backups are encrypted, they are shown in the Backups > Disk (Encrypted) node.

To rescan a backup repository, complete the following steps:
1. Open the **Backup infrastructure** view.
2. In the inventory pane, select the **Backup repositories node**.
3. In the working area, select the backup repository and click **Rescan repository** on the ribbon or right-click the backup repository and select **Rescan repository**.

## Removing backup repositories
{: #veeam_repo_man_storage_rem_backup}

You can permanently remove a backup repository from the backup infrastructure. When you remove a backup repository, Veeam Backup and Replication unassign the backup repository role from the server and this server is no longer used as a backup repository. The actual server remains in the backup infrastructure. Veeam Backup and Replication do not remove backup files and other data that is stored in the backup repository. You can reconnect the backup repository at any time and import backups from this backup repository to Veeam Backup and Replication. You cannot remove a backup repository that is used by any job. To remove such a backup repository, you first need to delete a reference to this backup repository in the job settings.

To remove a backup repository, complete the following steps:
1. Open the **Backup infrastructure** view.
2. In the inventory pane, select the **Backup repositories node**.
3. In the working area, select the backup repository and click **Remove repository** on the ribbon or right-click the backup repository and select **Remove**.

## Fast clone
{: #veeam_repo_man_storage_fast}

Fast clone is the Veeam Backup and Replication technology that helps create quick file copies. It increases the speed of synthetic backup creation and transformation, reduces disk space requirements and decreases the load on storage devices. With this technology, Veeam Backup and Replication references existing data blocks on volumes instead of copying data blocks between files. Data blocks are copied only when files are modified.

Veeam Backup and Replication uses Fast Clone for the following operations:
* In backup jobs: to merge backup files, create synthetic full backups (including GFS backups), transform reverse incremental backups, and compact full backup files.
* In backup copy jobs: to merge backup files, create GFS backups (synthetic method), and compact full backup files.
- To [migrate (evacuate) backups between performance extents](https://helpcenter.veeam.com/docs/backup/vsphere/sobr_evacuate.html?ver=120){: external}.
- To [migrate (evacuate) Veeam Cloud Connect tenant backups between performance extents](https://helpcenter.veeam.com/docs/backup/powershell/start-vbrcloudtenantbackupevacuation.html?ver=120){: external}.
- To [rebalance SOBR extents](https://helpcenter.veeam.com/docs/backup/vsphere/sobr_rebalance.html?ver=120){: external}.
- To [move backups to another repository](https://helpcenter.veeam.com/docs/backup/vsphere/move_backup.html?ver=120){: external}.
- To [copy backups to another repository](https://helpcenter.veeam.com/docs/backup/vsphere/copy_backup.html?ver=120){: external}.
- To [export backups into standalone.VBK files](https://helpcenter.veeam.com/docs/backup/vsphere/exporting_backups.html?ver=120){: external}.
- To [upgrade the backup chain format](https://helpcenter.veeam.com/docs/backup/vsphere/backup_copy_change_type.html?ver=120#periodic_copy_mode){: external} for backup copies created in the periodic copy mode.

### Fast clone for Linux repositories
{: #veeam_repo_man_storage_fast_linux}

For Linux backup repositories, Fast Clone is based on the relink technology.

### Requirements for Linux repositories
{: #veeam_repo_man_storage_fast_linux_req}

To use Fast Clone, Veeam Backup and Replication requires that Linux backup repositories
meet the following conditions:
* File system is XFS.
* The Linux distribution is supported.
* The Linux kernel supports reflinks.
* Cyclic redundancy check (CRC) is enabled.
* The minimum supported data block size is 1 KB. The maximum supported block size is 4 KB.

### Configuring a Linux repository
{: #veeam_repo_man_storage_fast_linux_conf}

To configure a Linux backup repository for work with Fast Clone, perform the following
procedure:

1. Format the disk where backups are stored that uses the following XFS volume format string:
   ```psh
   mkfs.xfs -b size=4096 -m reflink=1,crc=1 /dev/sda1
   ```
   {: pre}

   Consider the following:
   * size=4096 sets file system block size to 4096 bytes.
   * reflink=1 enables reflinking for the XFS instance (disabled by default).
   * crc=1 enables checksums, which are required for reflink=1 (enabled by default).
2. Mount the disk to a specific directory:
   ```psh
   mkdir /backups
   mount /dev/sda1 /backups
   ```
   {: pre}

3. Run the following command to ensure that the disk is properly configured:
   ```psh
   df -hT
   ```
   {: pre}

4. To permanently mount the disk, add the entry to the `/etc/fstab configuration` file. It is recommended to use the UUID to specify the disk.
   ```psh
   # <file system> <mount point> <type> <options> <dump> <pass>
   UUID=<UUID> /backups xfs defaults 0 0
   ```
   {: pre}

5. To get the UUID, run the following command:
   ```psh
   blkid /dev/sda1
   ```
   {: pre}

### Limitations
{: #veeam_repo_man_storage_fast_linux_limitations}

After you have moved backup chains to a Linux backup repository with Fast clone support, you must create active full backups for these chains to activate it. You can also schedule the backup file compact operation instead of active full backup.

### Fast clone for Microsoft Windows and SMB Repositories
{: #veeam_repo_man_storage_fast_windows}

For Microsoft Windows and SMB backup repositories, Fast Clone is based on block cloning technology of Microsoft. For more information about block cloning, see [Microsoft Docs](https://learn.microsoft.com/en-us/windows/win32/fileio/block-cloning){: external}.

By default, Veeam Backup and Replication uses Fast Clone for all Microsoft Windows and SMB backup repositories that meet the requirements. You can disable this option with a registry value. For more information, contact Veeam Customer Support. 

### Requirements for Microsoft Windows and SMB repositories
{: #veeam_repo_man_storage_fast_windows_req}

To use Fast Clone, Veeam Backup and Replication requires that Microsoft Windows backup repositories meet the following conditions:

   * The OS is Microsoft Windows Server 2016 (or later) or Microsoft Windows 10 Pro for Workstations (or later).
   * File system is Re-FS 3.1 (or later).

   All Re-FS supported configurations must use [Windows Server catalog](https://www.windowsservercatalog.com/){: external} certified hardware. For other requirements, limitations, and known issues, see [Veeam KB article](https://www.veeam.com/kb2792){: external}.
   {: note}

   * Shared folder backup repository 

   To use Fast Clone, Veeam Backup and Replication requires that SMB backup repositories support [FSCTL_DUPLICATE_EXTENTS_TO_FILE](https://learn.microsoft.com/en-gb/windows/win32/api/winioctl/ni-winioctl-fsctl_duplicate_extents_to_file?redirectedfrom=MSDN){: external} and [FSCTL_SET_INTEGRITY_INFORMATION](https://learn.microsoft.com/en-gb/windows/win32/api/winioctl/ni-winioctl-fsctl_set_integrity_information?redirectedfrom=MSDN){: external}. SMB shares that are configured on Microsoft Windows machines must also support the SMB 3.1.1 protocol and the Re-FS 3.1 (or later) file system.

Depending on the type of the job performed, Veeam Backup and Replication also imposes the following requirements on backup infrastructure components. 

| Type of job | Requirements to back up infrastructure components |
|:----------- |:------------------------------------------------ |
| Backup job | Protocol: SMB 3.1.1 |
| Backup copy job | Protocol: SMB 3.1.1 |
{: caption="Table 1. Shared folder backup repository" caption-side="bottom"}

### Limitations for Microsoft Windows or SMB backup repositories
{: #veeam_repo_man_storage_fast_windows_limitations}

The following limitations apply when Veeam Backup and Replication uses Fast Clone for Microsoft Windows or SMB backup repositories:
* Veeam Backup and Replication does not use Fast Clone for backup repositories that are configured with Veeam Backup and Replication 9.5 or an earlier version. After upgrade, such backup repositories will work as backup repositories without Fast Clone support. To use Fast Clone, edit the settings of such backup repositories and complete the **Edit Backup Repository wizard** without changing settings.
* After you have enabled Fast Clone for existing repositories as described in the previous paragraph or have moved backup chains to backup repositories with Fast Clone support, you must create active full backups for backup chains that are stored in or moved to the repositories to activate Fast Clone. You can also schedule the backup file compact operation instead of performing active full backup.
* Due to Microsoft limitations, the source and destination files must be stored on the same Re-FS volume. For more information, see Restrictions and Remarks at [Microsoft Docs](https://learn.microsoft.com/en-gb/windows/win32/fileio/block-cloning?redirectedfrom=MSDN){: external}.
* If you add a backup repository with Fast Clone support as an extent to a scale-out backup repository, make sure that you enable the Data Locality placement policy for this scale-out backup repository. If backup files are stored on different extents, Fast Clone will not be used.
* Veeam Backup and Replication automatically aligns data blocks at a 4 KB or 64 KB block boundary depending on the volume configuration or SMB share-used storage.

It is recommended that you use Re-FS volume that is formatted with 64 KB cluster size to provide better performance with large data volumes.
   * When you copy data from a Re-FS volume to another location, the file system downloads cloned data blocks. For this reason, copied data occupies more space in the target location than it used to occupy in the source location. This can happen, for example, if you evacuate an extent that supports block cloning from a scale-out backup repository and migrate VM backup data to another extent: copied data require more space than it originally took.
   * If you plan to assign the role of a backup repository to Microsoft Windows Server 2016 version 1709 (or later) or Microsoft Windows 10 Pro for Workstations (or later), consider the following limitations:
   * Fast Clone and Windows data deduplication cannot be used simultaneously. Thus, if you target a backup job to a repository supporting Fast Clone and enable Windows data deduplication, the Fast Clone technology will not be used for this job.
   * If you target a backup job to a CIFS Re-FS repository and enable Windows data deduplication, the job fails. Veeam Backup and Replication does not support such a scenario.

## Proxy affinity
{: #veeam_repo_man_storage_proxy}

By default, Veeam Backup and Replication assigns backup proxies and repositories for jobs or tasks independently of each other. If you need to bind backup proxies to specific backup repositories and use them together, you can define proxy affinity settings. Proxy affinity determines what backup proxies are eligible to access a specific backup repository, and read or write data from and to this backup repository.

Proxy affinity can be set up for the following types of backup repositories:

* Backup repositories
* Scale-out backup repositories
* Cloud repositories (proxy affinity settings are configured on the tenant side)

Proxy affinity rules are applied to the following types of jobs and tasks that engage backup proxies and repositories:
* Backup jobs, including VMware Cloud Director backup and backup jobs from storage snapshots on primary and target storage arrays
* VeeamZIP
* VM copy
* Entire VM restore
* Hard disk restores

Proxy affinity rules are not applied to replication jobs and are not restrictive. You can think of affinity rules as a priority list. If backup proxies from the proxy affinity list cannot be used for some reason, for example, these backup proxies are inaccessible, Veeam Backup and Replication automatically fails over to the regular processing mode. It displays a warning in the job or task session and picks the most appropriate backup proxy from the list of proxies that are selected for the job or task.

When you target a job at a backup repository for which proxy affinity settings are configured, you must ensure that you assign a backup proxy from the proxy affinity list for job or task processing. If you assign a backup proxy that is not bound to this backup repository, Veeam Backup and Replication display a warning. For job processing, Veeam Backup and Replication uses the backup proxy that you define in the job settings, which might result in degraded job performance.

For every backup repository, you can configure proxy affinity settings — define a list of backup proxies that can work with this backup repository. Proxy affinity binds backup
proxies to specific backup repositories. When transporting data to and from the backup repository, Veeam Backup and Replication picks a VMware backup proxy from the proxy affinity list rather than VMware backup proxies specified in job or task settings.

Follow the steps to configure a proxy affinity list for a backup repository:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, select **Backup repositories**.
3. In the working area, select the backup repository and click **Proxy affinity** or right-click the backup repository and select Proxy affinity.
4. In the Proxy affinity window, select **Prefer the following backup proxies** for this repository and select check boxes next to the backup proxies that you want to bind to the backup repository.

## Related links
{: #veeam_repo_man_storage-links}

* [Adding backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_add_storage)
* [Scale-out backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_scale_backup)
* [Object storage repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_obj_storage)
