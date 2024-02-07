---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: veeam mover service, veeam data mover, nfs service, 

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Veeam Data Mover service
{: #veeam_mover_service}

The Veeam® Data Mover performs data processing tasks on behalf of Veeam Backup and Replication. It retrieves source machine data, performs data deduplication and compression, and stores backed-up data on the target storage. For Microsoft Windows® servers, Veeam Data Movers are persistent and are uploaded and installed only once. They are automatically installed when you add a Microsoft Windows server to the backup infrastructure. For Linux servers, Veeam Data Movers can be persistent or nonpersistent. A data mover is only manually installed if the Linux server fails. For more information, see [Veeam KB article](https://www.veeam.com/kb4298){: external}.

## Veeam Power NFS service
{: #veeam_mover_service_nfs}

The vPower NFS service is a Microsoft Windows service that runs on a Microsoft Windows machine and acts as an NFS server. The vPower technology enables the following features:

* SureBackup
* SureReplica
* Instant recovery
* Instant disk recovery
* Staged restore
* Universal Application-Item Recovery (U-AIR)
* Multi-OS guest OS file restore

Consider the following information when you use the previous features:

* Veeam Backup and Replication publishes VMDK files of the virtual machine (VM) from the backup on the vPower NFS data store. Veeam Backup and Replication emulates the presence of VMDK files on the vPower NFS data store. The VMDK files are still located in the backup file on the backup repository.
* The vPower NFS data store is then mounted to the ESXi host. As a result, the ESXi host can identify backed-up VM images with help of the vPower NFS data store and work with them as with regular VMDK files. The emulated VMDK files function as pointers to the real VMDK files in the backup repository.
* The vPower NFS data store stays mounted to the ESXi host. If the data store is unmounted, Veeam Backup and Replication remounts the data store. If you are using a Microsoft Windows backup repository, it is recommended that you enable the vPower NFS server on this backup repository. Therefore, you have a direct connection between the ESXi host and the backup repository, and the vPower NFS data store is mounted.

## Related links
{: #veeam_mover_service-links}

* [Veeam vPower NFS service](https://helpcenter.veeam.com/docs/backup/vsphere/vpower_nfs_service.html?ver=120){: external}
* [Adding Microsoft Windows Servers](https://helpcenter.veeam.com/docs/backup/vsphere/add_windows_server.html?ver=120){: external}
