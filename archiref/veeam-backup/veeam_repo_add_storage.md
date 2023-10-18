---

copyright:

  years: 2023

lastupdated: "2023-10-16"

keywords: adding backup repositories, configuring setting for microsoft windows, configuring setting for linux server, SMB share, NFS share

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding backup repositories
{: #veeam_repo_add_storage}

This section describes how to add direct attached storage, network attached storage, and deduplicating storage appliances as backup repositories. Before you add a backup repository, make sure to [check prerequisites](https://helpcenter.veeam.com/docs/backup/vsphere/repo_before_you_begin.html?ver=120){: external}. Then use the **new backup repository** wizard to add the backup repository.

1. To start the new backup repository wizard, complete the following steps:

   1. Open the **Backup infrastructure** view.
   2. In the inventory pane, right-click **Backup repositories** and select **Add backup repository**. Alternatively, you can click **Add repository** on the ribbon.
   3. In the **Add backup repository** window, select the type of the backup repository you want to add.
   4. The **New backup repository** wizard guides you through steps for adding direct attached storage, network attached storage, and deduplicating storage appliances as backup repositories.

2. At the **Name** step of the wizard, specify a name and description for the backup repository.

   1. In the **Name** field, specify a name for the backup repository.
   2. In the **Description** field, provide a description for future reference. The default description contains information about the user who added the backup repository, the date, and time when the backup repository was added.
  
3. Specify server or shared folder settings.

Options that you can specify at the server step of the wizard depend on the type of backup repository you are adding.

## Configuring settings for Microsoft Windows and Linux Server
{: #veeam_repo_add_storage_mic_lin}

To configure settings for a Microsoft Windows® or Linux® server, follow the procedure:

1. From the **Repository server** list, select a Microsoft Windows or Linux server that you want to use as a backup repository. The **Repository server** list contains only those servers that are added to the backup infrastructure. If the server is not added to the backup infrastructure, you can click **Add new** on the right to open the **New windows server** or **New Linux server wizard**.

2. Click **Populate** to see a list of disks that are connected to the server, their capacity, and free space.


## SMB share
{: #veeam_repo_add_storage_smb}

To configure settings for an SMB share, complete the following steps:

1. In the **Shared folder** field, specify a UNC path to the SMB shared folder that you want to use as a backup repository. If you use the IPv6 address, specify the path in a literal format, for example, `\\[1080--8-800-200c-417a.ipv6-literal.net]\folder`. For more information, see [RFC 2732](https://www.rfc-editor.org/rfc/rfc2732){: external}. 

   You can use IPv6 addresses only if IPv6 communication is enabled as described in [IPv6 Support](https://helpcenter.veeam.com/docs/backup/vsphere/ipv6.html?ver=120){: external}.
   {: note}

2. If you must specify user credentials to access the shared folder, select the **This share requires access credentials** checkbox. From the **Credentials** list, select a credentials record for a user account that has Full Control permissions on the shared folder. 

   The username must be in the down-level logon name format. For example, `DOMAIN\username` or `HOSTNAME\username`.
   {: note}

3. If you have not set up credentials beforehand, click the **Manage accounts** link at the bottom of the list or click **Add** on the right to add the credentials.

4. In the **Gateway server** field, specify settings for the gateway server:
   * If you want Veeam Backup and Replication to select a gateway server automatically, leave **Automatic selection**.
   * If you want to select servers that can be used as gateway servers explicitly, click **Choose** next to the **Gateway server** field. In the **Gateway Server** window, click **Use the following gateway servers only** and select servers. The servers must have a direct access to the SMB shares and be located as close as possible. Veeam Backup and Replication chooses the most suitable server.

## NFS share
{: #veeam_repo_add_storage_nfs}

Complete the following steps:

1. Configure settings for an NFS share:
   1. In the **Shared folder** field, specify a path to the NFS shared folder that you want to use as a backup repository. You can specify the path that uses an IPv4 or IPv6 address.

      You can use IPv6 addresses only if IPv6 communication is enabled as described in [IPv6 Support](https://helpcenter.veeam.com/docs/backup/vsphere/ipv6.html?ver=120){: external}.
      {: note}

   2. In the Gateway server field, specify which server you want to use:
      * If you want Veeam Backup and Replication to select a gateway server automatically, leave **Automatic selection**.
      * If you want to select servers that can be used as gateway servers explicitly, click **Choose** next to the Gateway server field. In the **Gateway Server window**, click **Use the following gateway servers only** and select **servers**. The servers must have a direct access to the NFS share and must be located as close as possible. Veeam Backup and Replication choose the most suitable server.

2. Configure backup repository settings:

   1. At the **Repository step** of the wizard, specify path and load control repository settings.
   2. In the **Location section**, specify a path to the folder where backup files must be stored. Click **Populate** to check capacity and free space available in the selected location.
   3. For Linux repository and deduplicating storage appliances, except HPE StoreOnce and Dell Data Domain: Select the **Use fast cloning on XFS volumes** checkbox to enable copy-on-write functions. In terms of Veeam Backup and Replication, this function is known as **Fast clone**.
   4. Use the **Load control** section to limit the number of concurrent tasks and data ingestion rate for the backup repository. These settings help you control the load on the backup repository and prevent possible timeouts of storage I/O operations.
   5. Select the **Limit maximum concurrent tasks** checkbox and specify the maximum allowed number of concurrent tasks for the backup repository. If this value is exceeded, Veeam Backup and Replication will not start a new task until one of the current tasks finishes.
   6. Select the **Limit read and write data rates** checkbox and specify the maximum rate to restrict the total speed of reading and writing data in the backup repository disk.

3. Click **Advanced** to configure more settings for the backup repository:

   1. For Storage Systems that use a fixed block size, select the **Align backup file data blocks** checkbox. Veeam Backup and Replication align VM data that is saved to a backup file at a 4 KB block boundary.
   2. When you enable compression for a backup job, Veeam Backup and Replication compresses VM data at the source side, and then transports it to the target side. Writing compressed data to a deduplicating storage appliance results in poor deduplication ratios as the number of matching blocks decreases. To overcome this situation, select the **Decompress backup data blocks  before storing** checkbox. If data compression is enabled for a job, Veeam Backup and Replication compresses VM data on the source side, transports it to the target side, decompresses VM data on the target side, and writes raw VM data to the storage device to achieve a higher deduplication ratio.
   3. If you plan to use rotated drives for the backup repository, select the **Repository is backed by rotated hard disks** checkbox and choose how Veeam Backup and Replication will behave when a drive is swapped:
      * Continue an existing backup chain if present. Select this option to continue the backup chain found on the drive.
      * Delete backups belonging to this job. Select this option to delete all backups created by the currently running job.
      * Delete all backups on the drive. Select this option to delete all backups created by Veeam Backup and Replication and stored on the drive in the repository folder. Note that Veeam Backup and Replication will delete all backups, even backups created by other jobs.
   4. To create a separate backup file for every machine in the job, ensure that the **Use-per-machine backup files** checkbox is selected. If you clear the checkbox, Veeam Backup and Replication creates single-file backups.

4. Specify **Mount server** settings:

   1. At the **Mount server** step of the wizard, specify settings for the mount server that you plan to use for file-level and application items restore.
   2. From the **Mount Server** list, select a server that you want to use. The mount server is required for file-level and application items restore. During the restore process, Veeam Backup and Replication mount the VM disks from the backup file residing in the backup repository to the mount server. As a result, VM data will not travel over the network, which will reduce the load on the network and speed up the restore process. The **Mount server** list contains only Microsoft Windows servers that are added to the backup infrastructure. If the server is not added to the backup infrastructure yet, click **Add New** on the right to open the **New Windows Server wizard**.
   3. In the **Instant recovery write cache folder** field, specify a folder that is used for writing cache during mount operations.
   4. To make the backup repository accessible by the Veeam vPower NFS Service, select the **Enable vPower NFS service on the mount server** checkbox. Veeam Backup and Replication enables the vPower NFS Service on the mount server that you have selected.
   5. To customize network ports used by the vPower NFS Service, click **Ports**.

5. Review properties and components:

   1. At the **Review** step of the wizard, review details of the backup repository and specify importing settings.
   2. Review the backup repository settings and list of components that will be installed on the backup repository server.
   3. If the backup repository contains backups that were previously created with Veeam Backup and Replication, select the **Search the repository for existing backups and import them automatically** checkbox. Veeam Backup and Replication scans the backup repository to detect existing backup files and displays them in the Veeam Backup and Replication console under **Imported > Backups node**.
   4. If the backup repository contains guest file system index files that were previously created by Veeam Backup and Replication, select the **Import guest file system index** checkbox. Index files are imported with backup files, and you are able to search for guest OS files inside imported backups. 

6. Apply backup repository settings. At the **Apply** step of the wizard, wait for Veeam Backup and Replication to install and configure all required components. Click **Next** to complete the procedure of adding the backup repository to the backup infrastructure.

7. Finish working with the wizard. At the **Summary** step of the wizard, review details of the added backup repository. Click **Finish** to exit the wizard.

## Related links
{: #veeam_repo_add_storage-links}

* [Object storage repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_obj_storage)
* [Managing backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage)
* [Scale-out backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_scale_backup)
