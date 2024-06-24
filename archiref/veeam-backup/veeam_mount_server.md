---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-04"

keywords: mount servers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Mount servers
{: #veeam_mount_server}

The mount server is required for restoring of guest OS files and application items. To access files or items that are stored in a backup file, Veeam Backup and Replication mount the content of the backup to the mount server. Only after the content is mounted, Veeam Backup and Replication can get files and copy them to the restore destination. The mount server is required for performing the following operations:

* [Guest OS file restore](https://helpcenter.veeam.com/docs/backup/vsphere/guest_file_recovery.html?ver=120){: external}
* [Application items restore](https://helpcenter.veeam.com/docs/backup/vsphere/restore_veeam_explorers.html?ver=120){: external}
* [Secure restore](https://helpcenter.veeam.com/docs/backup/vsphere/av_scan_about.html?ver=120){: external}
* [Instant file share recovery](https://helpcenter.veeam.com/docs/backup/vsphere/performing_instant_file_share_recovery.html?ver=120){: external}
* [Restore of specific files and folders from NAS backup](https://helpcenter.veeam.com/docs/backup/vsphere/file_share_recovery_restore_files_folders.html?ver=120){: external}

To reduce the load on the network and speed up the restore process, the mount server must be located in the same site as the backup repository, where backup files are stored. If you have several sites, it is recommended you configure at least one mount server in each site. During service deployment, the automation deploys a mount server onto the Veeam Backup and Replication server. 

If required, additional mount servers can be added. The mount server is defined for each backup repository, when you configure a backup repository, you specify which server you want to assign the role of the mount server. You can assign the mount server role to any 64-bit Microsoft Windows® machine added to the backup infrastructure. This machine and the backup repository must be located as close as possible. For cloud repositories, the mount server role is assigned to the backup server, but you cannot assign the mount server role to a different machine.

The mount server must have access to the backup repository and the virtual machine (VM) to where you restore files or application items to.
{: note}


## Related links
{: #veeam_mount_server-links}

* [Configuring a backup repository](https://helpcenter.veeam.com/docs/backup/vsphere/repository_mount_server.html?ver=120){: external}
* [Adding Microsoft Windows Servers](https://helpcenter.veeam.com/docs/backup/vsphere/add_windows_server.html?ver=120){: external}
* [System requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#mount){: external}



