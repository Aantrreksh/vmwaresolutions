---

copyright:

  years: 2023

lastupdated: "2023-10-16"

keywords: object storage, general considerations and limitations, direct backup to object storage, IBM cloud object storage, health check

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Object storage repositories
{: #veeam_repo_obj_storage}

An object storage repository is a repository that is intended for long-term data storage and based on either a cloud solution or an S3 compatible storage solution.

Veeam Backup and Replication supports the following types of object storage repositories:
* Amazon S3, Amazon S3 Glacier, and AWS Snowball Edge
* S3 compatible
* Google Cloud
* {{site.data.keyword.cloud_notm}}
* Wasabi Cloud Storage
* Microsoft Azure Blob, Azure Archive Storage, and Azure Data Box 

You can use object storage repositories as target repositories in the following ways:
* As target repositories for backup jobs and backup copy jobs.
* As target repositories for file share backup jobs.
* As a target repository for backups of VMware® Cloud Director virtual machines that are created by Veeam Backup and Replication.
* As target repositories for backups of virtual and physical machines that are created by Veeam® Agent for Microsoft Windows® or Veeam Agent for Linux®.
* As a target repository for backups of configuration database that is created by Veeam Backup and Replication.

You cannot keep backups created by file share backup jobs in object storage repositories if they are added as performance extents of the scale-out backup repository.
{: important}

You can also use object storage repositories as the following parts of the scale-out backup repository:
* As a part of the Performance tier, it helps you quickly access the stored data.
* As a part of Capacity tier, it helps you offload existing backup data directly to cloud-based object storage.
* As a part of the Archive tier, it helps you transport infrequently accessed data from the capacity tier for archive storage.

## Object storage repository deployment
{: #veeam_repo_obj_storage_dep}

To communicate with an object storage repository, Veeam Backup and Replication uses a VMware backup proxy to transfer data and a mount server to process guest OS applications and perform item recovery.

Depending on the type of a job, a VMware backup proxy connects to the object storage repository that uses one of the following options:
* Directly - in this case, a VMware backup proxy transfers data directly to the object storage repository.
* Using a gateway server - in this case, a VMware backup proxy transfers data to the object storage repository through a gateway server. 

### General considerations and limitations
{: #veeam_repo_obj_storage_lim}

Make sure to open required ports to communicate with object storage repositories in advance. For more information, see [Ports](https://helpcenter.veeam.com/docs/backup/vsphere/used_ports.html?ver=120#osrc){: external}.

Object storage gateway appliances that are used to store backup data in filer (CIFS/NFS) or block device mode (iSCSI) are not supported if the backup data is offloaded to object storage and is no longer stored directly on the appliance.

Such gateway appliances are only supported in the following cases:
* All of the backup data is stored on the appliance altogether (all of the backup chains are stored on the appliance as a whole and not scattered across multiple devices) and only extra copies of the backup data are transported to object storage.
* These appliances emulate a tape system (VTL) as an access protocol for Veeam Backup and Replication.
* Data in an object storage bucket or container must be managed solely by Veeam Backup and Replication, including retention and data management. Enabling lifecycle rules is not supported, and might result in backup and restore failures.
* Multi-factor authentication (MFA) is not supported for object storage repositories.

   Only one backup server must interact with an object storage repository. If you want to perform disaster recovery testing, you can add the object storage repository to another backup server. However, on the initial backup server, you must switch the object storage repository to the Maintenance mode. Otherwise, metadata on the object storage can get corrupted or out of sync, and you will not be able to restore data.
   {: important}

* Use one bucket per scale-out backup repository to reduce metadata. Creating folders for multiple scale-out backup repositories within a bucket slows down processing, as metadata operations within the object storage are handled per bucket.
* Object Storage Systems that offload data to tape devices or any other sequential storage devices is supported only if they are added as an archive tier in a scale-out backup repository.
* If a backup chain contains backup files that are marked as corrupted by Health Check, then such corrupted files, as well as all subsequent files that go after the corrupted one are never offloaded. In such a scenario, offload is only possible starting from the full backup file that succeeds the backup chain with corrupted backups.
* Different object storage repositories mapped to the same cloud folder can be used for storing both the capacity tier backups and the NAS backups.

   The same object storage repository (mapped to the same cloud folder) must not be used across multiple Veeam Backup and Replication servers for the same purposes as it leads to unpredictable system behavior and data loss. For the same reason, two object storage repositories that are mapped to the same cloud folder must not be added to different scale-out backup repositories within one Veeam Backup and Replication server.
   {: important}

* Within a scale-out backup repository, the mount server of a performance extent acts as a gateway server of the capacity extent if all of the following is true:
   * You can use SMB share/NFS share/deduplicating storage appliances as performance extents of your scale-out backup repository.
   * You have chosen Automatic selection for the gateway server at the Specify Shared Folder Settings step of the New backup repository wizard.
   * For the object storage that you use as the capacity extent, you have not selected to connect to object storage that uses a gateway server at the Account step of the New Object Repository wizard. 
* The backup proxy that processes backup data must meet the following requirements:
   * It must be an on-premises server as close as possible to a backup server.
   * It must have access to the cloud storage that you use as an object storage repository.
   * The backup proxy that processes VM data must be as close as possible to a backup server.
   * A backup server and a gateway server must have internet access to verify that the certificates that are installed on object storage repositories are valid.

### Considerations and limitations for direct backup to object storage
{: #veeam_repo_obj_storage_cons}

* Reverse incremental backup method for is not supported.
* A synthetic full backup method is not supported.
* Compact full backup file option is not supported.
* You cannot back up directly to object storage repositories backups created by [Veeam plug-ins for Enterprise Applications](https://helpcenter.veeam.com/docs/backup/plugins/overview.html?ver=120){: external}.

### Limitations for {{site.data.keyword.cloud_notm}} Object Storage
{: #veeam_repo_obj_storage_lim_storage}

For {{site.data.keyword.cloud_notm}} Object Storage on-premises, Veeam Backup and Replication supports versions 3.15.0.44 and later.

* Veeam Backup and Replication is supported on all {{site.data.keyword.cloud_notm}} Object Storage (Cloud Object Storage) deployment models. This includes on-premises, public cloud, and hybrid models. For the {{site.data.keyword.IBM_notm}} public cloud, the following storage classes are supported: Standard, Vault, Cold Vault and Smart Tier.
* Veeam Backup and Replication does not support Archive and Accelerated Archive storage classes in the {{site.data.keyword.IBM_notm}} public cloud.

### Health Check for Object storage repositories
{: #veeam_repo_obj_storage_health}

You can instruct Veeam Backup and Replication to periodically perform a health check for the latest restore point in the backup chain. An automatic health check can help you verify that VM data blocks are present in the object storage repository and check the integrity of these blocks. It helps you avoid a situation where a restore point gets corrupted, making all dependent restore points corrupted, too. 

The health check helps ensure that the restore point is consistent, and you are able to restore data from this restore point. During a health check, Veeam Backup and Replication performs a cyclic redundancy check (CRC) for metadata and a hash check for VM data blocks in the backup file to verify their integrity. 

If during the health check Veeam Backup and Replication detects corrupted data blocks in the latest restore point in the backup chain, it starts the health check retry. During the health check retry, Veeam Backup and Replication transport valid data blocks from the source data store to the object storage repository. After the health check retry completes, the transported data blocks are moved immediately to the latest backup in the backup chain.

The health check retry starts only if the backups job meets the requirements listed in [Health Check for Object Storage Repositories](https://helpcenter.veeam.com/docs/backup/vsphere/health_check_os.html?ver=120#conditions){: external}. Otherwise, Veeam Backup and Replication will add healthy blocks to a new backup file after the next job run.
{: note}

To allow Veeam Backup and Replication to perform the health check of data blocks that are located in the object storage repository, you must:
* Configure a proxy appliance located in the object storage at the **Mount server step** of the **New Object Repository wizard**.
* Enable the health check when you configure a backup job and define its schedule.

By default, the health check is performed on the last Friday of every month. You can change the schedule and run the health check weekly or monthly on specific days.

If you perform health check for encrypted backup files, Veeam Backup and Replication pass encryption keys to the regular backup repository or cloud repository. If you use Veeam Agent to back up machines and store their backups in object storage repositories, you can also perform the health check for Veeam Agent backups. For more information, see the [Health Check for Object Storage](https://helpcenter.veeam.com/docs/backup/vsphere/health_check_os.html?ver=120#conditions){: external} section of the User Guide for Veeam Agent that you use to back up data.
{: note}

### Completing the health check process
{: #veeam_repo_obj_storage_health_works}

The health check is performed in the following way:

1. The health check starts according to the schedule.
   * The health check runs only after all jobs and operations that process a backup are completed (for example, a backup job, a restore job, synthetic operations with backups, and so on). If some of these activities are started, the health check stops.
   * If a health check session does not complete until the next scheduled run, this session stops and a new session will start according to the schedule.
   * However, the health check skips verification of already processed data, Veeam Backup and Replication verifies the metadata of backup files that did not change between health check sessions. 

2. Veeam Backup and Replication performs CRC values check for backup metadata, verifies that blocks of data are present in the object storage repository and checks their integrity. During the health check, Veeam Backup and Replication verifies the latest restore point in the backup chain (restore point that is created with the current backup job session — the session during which the health check is performed). If the latest restore point in the backup chain is incomplete, Veeam Backup and Replication checks the restore point preceding the latest restore point. 

3. If the health check does not detect data corruption, the backup job session completes in a regular way. If the health check detects corrupted data, Veeam Backup and Replication starts the health check retry process. Depending on the revealed data corruption, Veeam Backup and Replication performs the following actions:
   * If the health check has detected corrupted backup metadata, Veeam Backup and Replication marks the whole backup chain as corrupted in the configuration database. In this case, you must detach the corrupted backup from the source job and you run a backup job again to create a new backup chain.
   * If the health check detects corrupted blocks of data, Veeam Backup and Replication performs the health check retry and attempts to repair the corrupted data blocks.

### Health check retry mode
{: #veeam_repo_obj_storage_health_check}

If the health check detects corrupted data, the backup job switches to the Retry mode and will start the health check retry process. During the health check retry,
Veeam Backup and Replication transports necessary data blocks of the whole VM image from the source data store and saves transported data blocks to the latest backup file in the object storage repository.

If Veeam Backup and Replication does not perform the health check retry, you must retry the job manually. In this case, Veeam Backup and Replication produces a new backup file with healthy data blocks. You can use this backup file to restore from the latest restore point. For scheduled jobs, the number of health check retries is equal to the number of job retries specified in the job settings. For jobs started manually, Veeam Backup and Replication performs 1 health check retry.

To allow Veeam Backup and Replication to add the repaired data blocks to the latest restore point after completing the health check, the backup job must meet the following requirements:
* The backup job must not be disabled.
* Schedule the backups job to run automatically.
* The target object storage is not set to the Maintenance mode.

   Backup window settings must allow a backup job to run after the health check completes. If the backup job does not meet these requirements, Veeam Backup and Replication will add the repaired data blocks to a new restore point, created during a next run of the backup job.
   {: important}

## Adding {{site.data.keyword.cloud_notm}} Object Storage
{: #veeam_repo_obj_storage_add}

For more information about {{site.data.keyword.cloud_notm}} Object Storage, see [{{site.data.keyword.cloud_notm}} Object Storage](https://www.ibm.com/cloud/object-storage){: external}. Before you add an {{site.data.keyword.cloud_notm}} Object Storage to the backup infrastructure, check these [considerations and limitations](https://helpcenter.veeam.com/docs/backup/vsphere/object_storage_repository_cal.html?ver=120){: external}. After that, use the **New Object Repository** wizard. 

To start the **New Object Repository** wizard, complete one of the following procedures:

* Open the **Backup Infrastructure** view. In the inventory pane, select the **Backup Repositories** and click **Add Repository**. In the **Add Backup Repository** window, select **Object Storage > {{site.data.keyword.cloud_notm}} Object Storage**.
* Open the **Backup Infrastructure** view. In the inventory pane, select **Backup Repositories** and click **Add Backup Repository**. In the **Add Backup Repository** window, select **Object Storage > {{site.data.keyword.cloud_notm}} Object Storage**.

To complete the steps in the **New Object Repository** wizard:

<!-- The {: #step-1} tag and the ordered list that has only 1s are intentional. Do not delete. This coding is necessary for proper indentation when the procedure is translated. -->

1. At the **Name** step of the wizard, enter a name for a new object storage repository and  provide a description for future reference in the **Name** and **Description** fields. {: #step-1}
1. If you want to limit the maximum number of tasks that can be processed at once, select the **Limit concurrent tasks to N** checkbox.
1. At the **Account** step of the wizard, specify the connection settings:
   
   1. In the **Service** point field, specify a service point address of your {{site.data.keyword.cloud_notm}} Object Storage.

   1. In the **Region** field, specify a region.

   1. From the **Credentials** list, select user credentials to access your {{site.data.keyword.cloud_notm}} Object Storage. If you already have a credential record that was configured in advance, select that record from the list. Otherwise, click **Add** and provide your access and secret keys, as described in [Cloud Credentials Manager](https://helpcenter.veeam.com/docs/backup/vsphere/cloud_credentials.html?ver=120){: external}. You can also click the **Manage cloud accounts** link to add, edit, or remove a credentials record.

1. To specify how Veeam Backup and Replication will access the object storage repository, click **Choose** and in the **Connection mode** window specify the following settings:

   * **Direct** — select this option if you want Veeam Backup and Replication to use a proxy server to transfer data from processed VMs or file share to object storage repositories. Review the following information:
      * Ensure that the backup proxy server that you plan to use meets the requirements listed in [System Requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#proxy){: external}.
      * Locate your proxy server as close as it is possible to the backup server.
      * The Veeam Agent that process backup policies that run in the Managed by agent mode transfers data directly to the object storage repositories. Ensure that you grant the Veeam Agent the necessary permissions. For more information, see [Access Permissions](https://helpcenter.veeam.com/docs/backup/vsphere/access_permissions.html?ver=120){: external}.
      {: note}

   * **Through gateway server** — select this option if you want Veeam Backup and Replication to use gateway servers to transfer data from processed machines or file shares to object storage repositories. From the **Name** list, select gateway servers that you want to use for data transfer operations. By default, the role of a gateway server is assigned to the Veeam Backup and Replication server. You can choose any Microsoft Windows or Linux server that is added to your backup infrastructure and has an internet connection. Add the server to the backup infrastructure beforehand. Before you add the server, check the following [Considerations and Limitations](https://helpcenter.veeam.com/docs/backup/vsphere/object_storage_repository_cal.html?ver=120){: external}. For more information about how to add a server, see [Virtualization Servers and Hosts](https://helpcenter.veeam.com/docs/backup/vsphere/setup_add_server.html?ver=120){: external}.

1. At the **Bucket** step of the wizard, specify the bucket and folder that will be used to store data:
   1. In the **Bucket** field, enter a name of the bucket or click **Browse** to get it. Create the bucket where you want to store your backup data beforehand.
   1. In the folder field, enter a cloud folder name to which you want to map your object storage repository. Alternatively, click **Browse** and either select an existing folder or click **New Folder**.  
   1. Select the **Limit object storage** consumption checkbox to define a soft limit that can be exceeded temporarily for your object storage consumption. Provide the value in TB or PB.
   1. Select the **Make recent backups immutable** checkbox to prevent deletion of blocks of data from object storage. Specify the immutability period. For more information, see [Immutability](https://helpcenter.veeam.com/docs/backup/vsphere/immutability_sobr.html?ver=120){: external}.

1. At the **Mount Server** step of the wizard, specify settings for the mount server that you plan to use for restore operations, and configure a helper appliance. The helper appliance is a temporary host that Veeam Backup and Replication deploys on your {{site.data.keyword.cloud_notm}} Object Storage to perform a health check of backup files and apply retention to NAS backup files. For more information, see [NAS Backup Retention Scenarios](https://helpcenter.veeam.com/docs/backup/vsphere/nas_retention_scenarios.html?ver=120){: external}. After Veeam Backup and Replication completes these operations, it removes the helper appliance from the {{site.data.keyword.cloud_notm}} Object Storage.

   Review the following information:
   * If you do not configure a helper appliance, Veeam Backup and Replication uses local resources to perform the health check and apply retention to NAS backup files. It consumes more cloud resources and can result in extra costs.
   * To perform the health check, you must enable this option when you configure a backup job. For more information, see [Health Check for Backup Files](https://helpcenter.veeam.com/docs/backup/vsphere/backup_health_check.html?ver=120){: external}.

1. Specify Mount Server settings.

   1. From the **Mount Server** drop-down list, select a server that you want to use as a mount server. Veeam Backup and Replication uses this server during restore operations to mount VM disks directly from objects located in object storage repositories. For more information, see [Mount Server](https://helpcenter.veeam.com/docs/backup/vsphere/mount_server.html?ver=120){: external}.

   1. The **Mount Server** list contains only Microsoft Windows servers that are added to the backup infrastructure. If the server is not added to the backup infrastructure yet, click **Add New** on the right to open the New Windows Server wizard. For more information, see [Adding Microsoft Windows Servers](https://helpcenter.veeam.com/docs/backup/vsphere/add_windows_server.html?ver=120){: external}.

      Veeam Backup and Replicationon does not use the mount server to restore data from capacity tier or archive tier. For more information, see [Restore from Capacity Tier](https://helpcenter.veeam.com/docs/backup/vsphere/restore_capacity_tier.html?ver=120){: external} and [Restore from Archive Tier](https://helpcenter.veeam.com/docs/backup/vsphere/restore_archive_tier.html?ver=120){: external}.
      {: note}

   1. In the **Instant recovery** write cache folder field, specify a folder to keep the cache that is created during mount operations.

   1. Select the **Enable vPower NFS** service on the mount server checkbox to allow the Veeam vPower NFS Service access the object storage repository. Veeam Backup and Replication enable the Veeam vPower NFS Service on the necessary mount server. For more information, see [Veeam vPower NFS Service](https://helpcenter.veeam.com/docs/backup/vsphere/vpower_nfs_service.html?ver=120){: external}.

1. Click **Ports** to customize network ports used by the Veeam vPower NFS Service. In the vPower NFS Port Settings window, specify the following settings:

   1. Next to the **Mount Port** section, specify the port that the Veeam vPower NFS Service uses to mount the vPower NFS data store to the ESXi host.

   1. Next to the **vPower NFS port** section, specify the port that the Veeam vPower NFS Service uses to connect to the target NFS share. For information on ports used by default, see [Ports](https://helpcenter.veeam.com/docs/backup/vsphere/used_ports.html?ver=120){: external}.

   1. To specify the helper appliance settings, click **Configure**. From the **Managed server** drop-down list, select a server that you want to use as the helper appliance.

      Do not enable Microsoft Windows NFS services on the machine where you install the Veeam vPower NFS Service. If Microsoft NFS services and Veeam vPower NFS Service are enabled on the same machine, both services might fail to work correctly.
      {: important}

1. At the **Review** step of the wizard, review what components will be processed on the mount server and their status.

   1. If the backup repository contains backups, select the **Search** the repository for existing backups and import them automatically checkbox. Veeam Backup and Replication scan the backup repository to detect existing backup files and display them in the Veeam Backup and Replication console under the **Backups > Object Storage (Imported)** node.
   1. If the backup repository contains guest file system index files, select the **Import** guest file system index data to the catalog checkbox. Veeam Backup and Replication import index files together with backup files, and you are able to search for guest OS files inside imported backups.

1. At the **Apply** step of the wizard, wait for Veeam Backup and Replication to complete saving your settings to the configuration database and create backup infrastructure objects.

1. At the **Summary** step of the wizard, review details of the newly created object storage repository and click **Finish**.

## Managing Object storage repositories
{: #veeam_repo_obj_storage_man}

You can manage your object storage repositories in various ways: edit the settings of an object storage repository, switch it to the maintenance or the Sealed mode or remove an object storage repository.

### Editing settings of Object storage repository
{: #veeam_repo_obj_storage_edit}

After you have added an object storage repository, you might want to edit its settings. To edit object storage settings, complete the following steps:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, select **Backup repositories**.
3. In the working area, select an object storage repository and click **Edit repository** on the ribbon or right-click an object storage repository and select **Properties**.
4. Follow the steps of the edit **Object Storage repository wizard** and edit settings as required.

   Some settings cannot be modified and will remain disabled while being edited.
   {: note}

### Removing Object storage repository
{: #veeam_repo_obj_storage_remove}

You can remove any object storage repository from the application scope if you no longer need it.

Review the following information:

* To remove such a repository, you must first exclude an object storage repository from the scale-out backup repository configuration. An object storage repository cannot be removed if backups located in this repository was imported. To remove such a repository, you must first detach object storage.
* An object storage repository cannot be removed if it is part of a scale-out backup repository.
* When an object storage repository is being removed from the environment, the data remains unaffected. 

To remove an object storage repository, complete the following steps:

1. Open the **Backup infrastructure** view.
2. In the inventory pane, select **Backup repositories**.
3. In the working area, select an object storage repository and click **Remove repository** on the ribbon or right-click an object storage repository and select **Remove**.

## Related links
{: #veeam_repo_obj_storage-links}

* [Adding backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_add_storage)
* [Managing backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage)
* [Scale-out backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_scale_backup)


