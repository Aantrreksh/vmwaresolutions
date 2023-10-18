---

copyright:

  years: 2023

lastupdated: "2023-10-17"

keywords: scale-out backup repositories, limitations for scale-out backup repositories, adding scale-out backup repositories, managing scale-out backup repositories, rescanning scale-out backup repositories

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Scale-out backup repositories
{: #veeam_repo_scale_backup}

A scale-out backup repository is a repository system with horizontal scaling support for multitier storage of data. A scale-out backup repository consists of one or more backup repositories or object storage repositories that are called performance tier, and can be expanded with object storage repositories for long-term and archive storage: capacity tier and archive tier. All the storage devices and systems inside the scale-out backup repository are joined into a system, with their capacities summarized.

A scale-out backup repository can comprise different tiers, or logical levels of storage.  
   * The performance tier is the level that is used for the fast access to the data. It consists of one or more backup repositories or object storage repositories called performance extents. For more information, see [Performance Tier](https://helpcenter.veeam.com/docs/backup/vsphere/backup_repository_sobr_extents.html?ver=120){: external}.
   * Capacity tier is an extra level for storing data that needs to be accessed less frequently. However, you can still restore your data directly from it. The capacity tier consists of cloud-based or on-premises object storage repositories called capacity extent. For more information, see [Capacity Tier](https://helpcenter.veeam.com/docs/backup/vsphere/capacity_tier.html?ver=120){: external}.
   * Archive tier is an extra level for archive storage of infrequently accessed data. Applicable data can be transported ether from the capacity or archive tier. For restoring from the archive tier, data must undergo a preparation process. For more information, see [Archive Tier](https://helpcenter.veeam.com/docs/backup/vsphere/archive_tier.html?ver=120){: external}.

A scale-out backup repository can be used for the following types of jobs and tasks:
* Backup jobs
* Backup copy jobs
* You can copy backups that reside in scale-out backup repositories and store backup copies in scale-out backup repositories.
* Veeam® backups for Amazon and Microsoft® Azure (via backup copy jobs)
* VeeamZIP tasks
* Backup jobs that are created by Veeam Agent for Linux® 2.0 or later
* Backup jobs that are created by Veeam Agent for Unix 2.0 or later
* Backup jobs that are created by Veeam Agent for Microsoft Windows® 2.0 or later
* Backup jobs created by Veeam Agent for Mac
* NAS backup jobs
* Backup jobs created by Veeam Backup for Nutanix AHV

## Limitations for scale-out backup repositories
{: #veeam_repo_scale_backup_limitations}

Scale-out backup repositories have the following limitations:
* You cannot use a scale-out backup repository as a target for the following types of jobs:
   * Configuration backup job
   * Replication jobs (including replica seeding)
   * VM copy jobs
   * Veeam Agent backup jobs that are created by Veeam Agent for Microsoft Windows 1.5 or earlier.
   * Veeam Agent backup jobs that are created by Veeam Agent for Linux 1.0 Update 1 or earlier.
* You cannot add a backup repository as an extent to the scale-out backup repository if any job of unsupported type is targeted at this backup repository or if the backup repository contains data that is produced by jobs of unsupported types (for example, replica metadata). To add such a backup repository as an extent, you must first target unsupported jobs to another backup repository and remove the job data from the backup repository in question.
* Scale-out backup repositories do not support rotator drives. If you enable this repository, it is backed by rotated hard disk drives setting on an extent. Veeam Backup and Replication ignore this setting and will work with such repository as with a standard extent.
* If a backup repository is added as an extent to the scale-out backup repository, you cannot use it as a regular backup repository. You cannot target jobs to this backup repository. Instead, you must target jobs to the configured scale-out backup repository.
* You cannot add a scale-out backup repository as an extent to another scale-out backup repository.
* You cannot add a backup repository as an extent if this backup repository is already added as an extent to another scale-out backup repository.
* You cannot add a backup repository as an extent if this backup repository is already used as a backup destination by VMware Cloud Director organizations.
* You cannot add a backup repository in which some activity is being performed (for example, a backup job or restore task) as an extent to the scale-out backup repository.
* You can add only one type of object storage repository as performance extent of one scale-out backup repository. For example, if a first extent is an Amazon S3 object storage repository, the second extent must also be an Amazon S3 object storage repository.
* You cannot use the backup repository and the direct object storage repository for the same performance tier.
* Data that is located in object storage repositories is organized into a separate backup chain for every machine in a job.
* If you use immutability and have several extents in your performance tier, you must enable it for all extents within this tier. You cannot use mixed configuration and have only one extent with immutability enabled.
* You cannot add as performance extents of one Wasabi bucket as an S3 Compatible Object Storage and another Wasabi bucket as a Wasabi Cloud Object Storage to the same type of tier (either performance tier or capacity tier) of a scale-out backup repository. For example, you cannot add Amazon S3 storage and Microsoft Azure Blob storage to one performance extent.
* If you apply the Forget or Remove from disk options to a missing restore point in a scale-out backup repository, the backup file that is associated with the missing restore point will be deleted from capacity tier and archive tier on the next offload and archiving job run.
* If you use Enterprise edition of Veeam Backup and Replication, you can create two scale-out backup repositories.

For each scale-out backup repository, you can have either backup repositories or object storage repositories added as a performance extent or a capacity extent. You can have 2
active, and 1 inactive (that is, put to the Maintenance mode) performance or capacity extents. You can add inactive extents, for example, if any of the active extents has no free space, and you want to evacuate backup data from it. If you add four performance extents and do not put any of them to the Maintenance mode, the jobs that are targeted at the scale-out backup repository will fail. Veeam Universal license and Enterprise Plus editions have no limitations on the number of scale-out backup repositories or performance extents and capacity extents.
* If you want to use the Extract utility to work with backup files on any of the extents of your scale-out backup repository, make sure that incremental and full backup files are on the same extent.
* You can use the Veeam Backup Validator utility only for backups that are stored in the performance tier, which consists of backup repositories (except object storage repositories). Make sure that incremental and full backup files are on the same extent.
* To let Veeam Backup and Replication automatically import backups during rescan of a scale-out backup repository, names of VBM files and paths to VBM files (starting from the backup repository root to VBM files, not including the root itself) must contain only allowed characters:

   * Alphanumeric characters: `a-zA-Z0-9`
   * Special characters: `_-.+=@^`

* Names of VBM files and paths to VBM files must not contain spaces. If a name of a VBM file or a path to a VBM file contains prohibited characters, Veeam Backup and Replication fail to import such backup during rescan of the scale-out backup repository. To import such backup, you can replace prohibited characters with the underscore character. For example: `C:\My Repository\Backup_Job\Backup_Job.vbm`. You do not need to rename the actual backup files.

* Veeam Backup and Replication do not split one backup file across multiple extents.
* An object storage repository added as a capacity tier in a scale-out backup repository can’t be used for storing [NAS backups](https://helpcenter.veeam.com/docs/backup/vsphere/file_share_support.html?ver=120){: external}. To archive NAS backup files to an object storage repository, assign the object storage repository as an archive repository when [you create a file share backup job](https://helpcenter.veeam.com/docs/backup/vsphere/file_share_backup_job_storage.html?ver=120){: external}.
* You cannot assign the role of a cache repository for file share backup to a scale-out backup repository and its extents. To learn more about cache repository, see [NAS Backup Support](https://helpcenter.veeam.com/docs/backup/vsphere/file_share_support.html?ver=120){: external}.
* If a repository is being used as a cloud repository, you cannot add it as an extent of a scale-out backup repository.

## Adding scale-out backup repositories
{: #veeam_repo_scale_backup_adding}

Before you add a scale-out backup repository to the backup infrastructure, check the following prerequisites:
* Backup repositories that you plan to add as performance extents to the scale-out backup repository must be added to the backup infrastructure.
* Check limitations for scale-out backup repositories.
* An object storage repository cannot be added as part of two or more different scale-out backup repositories at the same time.
* If the selected object storage contains offloaded backup data, you are offered to synchronize this data with your performance extents.
* Object storage that contains imported backups cannot be added as a capacity extent.
* You cannot add the same object storage repository as the performance extent and capacity extent.
* You cannot use object storage of different providers in the same type of tier. For example, you cannot add and use Amazon S3 storage and Microsoft Azure Blob storage to one performance extent.
* You cannot use the object storage repository and the backup repositories in the performance tier simultaneously.

To adding a scale-out backup repository, complete the following steps:

<!-- The {: #step-1} tag and the ordered list that has only 1s are intentional. Do not delete. This coding is necessary for proper indentation when the procedure is translated. -->

1. To start the **New scale-out backup repository wizard**, perform one of the following procedures. {: #step-1}
   * Open the **Backup infrastructure** view. In the inventory pane, select **Scale-out repositories** and click **Add scale-out repository** on the ribbon.
   * Open the Backup infrastructure view. In the inventory pane right-click **Scale-out repositories** and select **Add scale-out backup repository**. 

1. At the **Name step of the wizard**, specify a name and description for the scale-out backup repository.
   1. In the **Name** field, specify a name for the scale-out backup repository.
   1. In the **Description** field, provide a description for future reference. The default description contains information about the user who added the backup repository, the date, and time when the backup repository was added.

1. At the **Performance tier step** of the wizard, specify which backup repositories or object storage repositories you want to add as performance extents. Configure options for the scale-out backup repository.
   1. On the right of the Extents list, click **Add**.
   1. In the extents window, select check boxes next to backup repositories or object storage repositories that you want to add as performance extents.
   1. Click **OK**.
   1. At the lower right corner of the **Extents** list, click**Advanced**.
   1. Specify advanced options for the scale-out backup repository. If you want to create a separate backup chain for every machine in the job, check that the **Use per-machine backup files** checkbox is selected. With this option enabled, during one backup job session Veeam Backup and Replication will produce several backup files — one per every machine, and will write these files to the backup repository in multiple streams simultaneously. It is recommended that you enable this option to achieve better storage and compute resource utilization, especially if you use as a backup repository a deduplicating storage appliance that supports multiple write streams.
   1. To preserve the consistency of backup chains in the scale-out backup repository, select the **Perform full backup when required extent is offline** checkbox. If an extent that contains previous restore points from the current backup chain gets offline, the backup chain is broken. Veeam Backup and Replication will not be able to add a new incremental backup file. With this option enabled, Veeam Backup and Replication create a full backup file instead of an incremental backup file. If you enable this option, you must make sure that you have enough free space in the scale-out backup repository to host a full backup file.
   1. If a backup repository that you add as a performance extent is already used by jobs of the supported type or there are backups pointing at the backup repository (for example, independent backups that are created with VeeamZIP), Veeam Backup and Replication offer you to update a link to the backup repository in the job properties. Click **Yes** to update the link and target the jobs and backups at the scale-out backup repository. If you click **No**, you will not be able to pass to the next steps of the wizard.

1. Specify the backup placement policy.

   This step is not available if you use object storage repositories as performance extends.
   {: note}

   1. At the **Policy** step of the wizard, specify how you want to store backup files on performance extents of the scale-out backup repository.
   1. Set the backup file placement policy for the scale-out backup repository. Select **Data locality** if you want to store backup files that belong to the same backup chain together. In this case, a full backup file and subsequent incremental backup files are stored to the same performance extent of the scale-out backup repository. The new backup chain might be stored to the same performance extent or to another performance extent (unless you use a deduplicating storage appliance as a performance extent).
   1. Select **Performance** if you want to store full and incremental backup files to different performance extents of the scale-out backup repository. If you set the Performance policy, you must make sure that the network connection is fast and reliable so that Veeam Backup and Replication can access all backup files from the backup chain.
   1. If you select the **Performance** policy, you can restrict which types of backup files can be stored on a specific performance extent. For example, if you have added three performance extents to the scale-out backup repository, store full backup files on one extent and incremental backup files — on the other two extents.
   1. Click **Customize**.
   1. In the **Backup placement settings** window, select a performance extent and click **Edit**.
   1. Select a checkbox next to the type of backup files that you want to store on the extent: **Full backup files** or **Incremental backup files**. By default, Veeam Backup and Replication can store both full and incremental backup files on the same extent.
   1. If you select the **Strict placement policy enforcement** checkbox, Veeam Backup and Replication will not create a backup if it violates the backup placement policy and result in that a backup job might fail.

1. At the **Capacity tier step** of the wizard, select the object storage repositories that you want to add as capacity extents. Then specify when to move and copy data. To configure the capacity tier, complete the following steps:

   1. Select the **Extend scale-out backup repository capacity with object storage** checkbox.
   1. To select the object storage repositories to which you want to offload your data, click **Choose**.
   1. In the **Capacity tier extents** window, select the checkbox in front of the necessary object storage repositories.
   1. Ensure that these repositories are added to the backup infrastructure in advance. If the object storage repositories are not added, click **Add** and follow the steps in the [Adding object storage repository wizard](https://helpcenter.veeam.com/docs/backup/vsphere/new_object_storage.html?ver=120){: external}.
   1. Click **Window** and specify when it is allowed or prohibited to move or copy data to object storage.
   1. Select the **Copy backups to object storage when they are created** checkbox to copy new backups when they are created, as described in [copying backups to capacity tier](https://helpcenter.veeam.com/docs/backup/vsphere/capacity_tier_copy.html?ver=120){: external}.
   1. When you select this option, you are asked whether to copy all backup files that you might already have on any of the performance extents, or only those that have been created recently.
   1. If you select **Latest**, only the backup files that belong to the last active backup chain will be copied from each of the performance extents. If you select **All**, Veeam Backup and Replication copies all backup files that belong to all backup chains on any of the [specified extents](https://helpcenter.veeam.com/docs/backup/vsphere/sobr_add_extents.html?ver=120){: external}.
   1. Select the **Move backups to object storage as they age out of the operational restores window** checkbox to move inactive backup chains to the capacity extent, as described in [Moving backups to capacity tier](https://helpcenter.veeam.com/docs/backup/vsphere/capacity_tier_move.html?ver=120){: external}.
   1. Therefore, in the **Move backup files folder than X days** field, specify the operational restore window to define a period after which inactive backup chains on your performance extents are considered outdated and moved to the capacity extent. The value 0 is allowed to specify to offload inactive backup chains on the same day they are created.
   1. To override the behavior of moving old backups, click **Override**, select the **Move oldest backup files sooner if scale-out backup repository is reaching the capacity** checkbox and define a threshold in percent to force data transfer if a scale-out backup repository has reached the specified threshold.
   1. To offload data encrypted, select **Encrypt data that is uploaded to object storage** and provide a strong password. With this option selected, the entire collection of blocks along with the metadata will be encrypted while being offloaded.
   1. If you have not created the password beforehand, click **Add** or use the **Manage** passwords link to specify a new password.
   
1. At the **Summary** step of the wizard, complete the procedure of scale-out backup repository configuration. Wait for the scale-out backup repository to be added to the backup infrastructure. The process might take some time.

   1. Review details of the scale-out backup repository.
   1. Click **Finish** to exit the wizard.

## Managing scale-out backup repositories
{: #veeam_repo_scale_backup_managing}

You can manage your scale-out backup repositories and the data there in various ways: edit settings of the scale-out backup repository, rescan scale-out backup repositories automatically or manually, discover on which performance extent of the scale-out backup repository a particular backup file is stored, extend the scale-out backup repository or remove certain performance extents from it, perform service actions or remove the scale-out backup repository.

## Editing settings of scale-out backup repositories
{: #veeam_repo_scale_backup_editing}

To change the scale-out backup repository settings:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, click **Scale-out Repositories**.
3. In the working area, select the scale-out repository and click **Edit scale-out repository** on the ribbon or right-click the scale-out backup repository. Select **Properties**.
4. Follow the steps of the edit scale-out backup repository wizard and edit settings as required.

## Rescanning scale-out repositories
{: #veeam_repo_scale_backup_rescan}

Veeam Backup and Replication periodically rescan scale-out backup repositories. During the rescan process, it gets the following information:
* State of every performance extent added to the scale-out backup repository: online or offline.
* Status of Veeam Data Movers on extents: up-to-date or outdated.
* Space available in the scale-out backup repository.

To start the rescan process:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, select **Scale-out repositories**.
3. In the working area, select the scale-out repository and click **Rescan repository** or right-click the scale-out backup repository. Select **Rescan**.

## Extending scale-out repositories
{: #veeam_repo_scale_backup_extend}

You can add a backup repository or an object storage repository as a performance extent or a capacity extent to the scale-out backup repository at any time. For example, the scale-out backup repository may run low on space, and you need to add storage capacity to it. 

### Extending performance tier
{: #veeam_repo_scale_backup_extend_per}

To extend the performance tier, perform the following steps:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, click **Scale-out repositories**.
3. In the working area, select the scale-out repository and click **Edit scale-out repository** on the ribbon or right-click the backup repository. Select **Properties**.
4. Move to the performance tier step of the wizard.
5. Click **Add**.
6. In the **Extents** window, select the checkbox next to the backup repository that you want to add as a performance extent to the scale-out backup repository.
7. If a backup repository that you add as a performance extent is already used by jobs of the supported type or there are backups pointing at the backup repository (for example-independent backups that are created with VeeamZIP). Veeam Backup and Replication offers you to update a link to the backup repository in the job properties. Click **Yes** to update the link and target the jobs and backups at the scale-out backup repository. If you click **No**, you will not be able to continue with the wizard.
8. Go through the next wizard steps and finish working with the wizard. 

   The new performance extent is added to the scale-out backup repository.

### Extending capacity tier
{: #veeam_repo_scale_backup_extend_cap}

To extend the capacity tier, perform the following steps:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, click **Scale-out repositories**.
3. In the working area, select the scale-out repository and click **Edit scale-out repository** on the ribbon or right-click the backup repository. Select **Properties**.
4. Move to the capacity tier step of the wizard.
5. Click **Choose**.
6. In the **Capacity tier extents** window, select the checkbox next to the backup repository that you want to add as a performance extent to the scale-out backup repository.
7. If a backup repository that you add as a capacity extent is already used by jobs of the supported type or there are backups pointing at the backup repository (for example, independent backups created with VeeamZIP). Veeam Backup and Replication offers  to update a link to the backup repository in the job properties. Click **Yes** to update the link and target the jobs and backups at the scale-out backup repository. If you click **No**, you will not be able to continue with the wizard.
8. Go through the next wizard steps and finish working with the wizard. 

   The new capacity extent is added to the scale-out backup repository.

## Switching to maintenance mode
{: #veeam_repo_scale_backup_switch}

Veeam Backup and Replication allow you to put an object storage repository into maintenance mode. You can use this mode if you need to perform service actions with an object storage. 

To put an object storage into the Maintenance mode, do the following:

1. Open the **Backup infrastructure** view.
2. In the **inventory pane**, select the **Backup repositories** node.
3. In the working area, select an object storage and click **Maintenance mode** on the ribbon or right-click an object storage and select Maintenance mode. 
4. To remove the object storage repository from the **Maintenance mode**, select the extent and click **Maintenance Mode** on the ribbon or right-click the extent. 
5. Select **Maintenance mode** again.

## Removing scale-out backup repositories
{: #veeam_repo_scale_backup_remove}

You can remove a scale-out backup repository at any time. When you remove a scale-out backup repository, Veeam Backup and Replication unassign the extent role from all the
backup repositories that are configured into it, and they become individual backup repositories. Backup files are not removed from the backup repository — they remain on the disk or an object storage repository. You cannot remove a scale-out backup repository if at least one job is targeted at it. First, you must move all backup files to the new backup repository and then retarget the jobs.

To remove a scale-out backup repository:
1. Open the **Backup infrastructure** view.
2. In the inventory pane, click **Scale-out repositories**.
3. In the working area, select the scale-out repository and click **Remove repository** on the ribbon or right-click the backup repository. Select **Remove**.

## Related links
{: #veeam_repo_scale_backup-links}

* [Adding backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_add_storage)
* [Managing backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage)
* [Object storage repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_obj_storage)
