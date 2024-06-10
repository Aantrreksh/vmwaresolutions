---

copyright:

  years: 2023, 2024

lastupdated: "2024-06-05"

keywords: backup repository, direct attached storage, network attached storage

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Backup repositories
{: #backup_repos}

A backup repository is a storage location where Veeam® keeps backup files, virtual machine (VM) copies, and metadata for replicated VMs.

At service order, choose from the following options:
* Direct attached storage, through iSCSI block storage on a Microsoft Windows® server.
* A Linux® hardened repository that uses local hard disks.

To add extra repositories, Veeam supports the following storage types:

* **Direct attached storage** - The following virtual and physical servers can be used as backup repositories:
   * [Microsoft Windows Server](https://helpcenter.veeam.com/docs/backup/vsphere/ms_server.html?ver=120){: external}
   * [Linux server](https://helpcenter.veeam.com/docs/backup/vsphere/linux_server.html?ver=120){: external}
   * [Hardened repository](https://helpcenter.veeam.com/docs/backup/vsphere/hardened_repository.html?ver=120){: external}

* **Network attached storage** - Add the following network shares as backup repositories:
   * [SMB (CIFS) share](https://helpcenter.veeam.com/docs/backup/vsphere/smb_share.html?ver=120){: external}
   * [NFS share](https://helpcenter.veeam.com/docs/backup/vsphere/nfs_share.html?ver=120){: external}

* **Deduplicating storage appliances** - While you can add the following deduplicating storage appliances as backup repositories in Veeam, you are only able to deploy virtual appliances in {{site.data.keyword.cloud}}. Be aware of the type of storage and locations of both primary (the VMs being backed up) and secondary data (the storage that is used by the appliance to hold backup files) as these might be the same underlying storage:
   * [Dell Data Domain](https://helpcenter.veeam.com/docs/backup/vsphere/dell_dd.html?ver=120){: external}
   * [ExaGrid](https://helpcenter.veeam.com/docs/backup/vsphere/deduplicating_appliance_exgrid.html?ver=120){: external}
   * [Fujitsu ETERNUS CS800](https://helpcenter.veeam.com/docs/backup/vsphere/fujitsu.html?ver=120){: external}
   * [HPE StoreOnce](https://helpcenter.veeam.com/docs/backup/vsphere/deduplicating_appliance_storeonce.html?ver=120){: external}
   * [Infinidat InfiniGuard](https://helpcenter.veeam.com/docs/backup/vsphere/infinidat_infiniguard.html?ver=120){: external}
   * [Quantum DXi](https://helpcenter.veeam.com/docs/backup/vsphere/deduplicating_appliance_quantum.html?ver=120){: external}

* **Object storage** - You can use cloud storage services as backup repositories. For more information, see [Object storage repository](https://helpcenter.veeam.com/docs/backup/vsphere/object_storage_repository.html?ver=120){: external}.  

To add {{site.data.keyword.cloud_notm}} object storage, see:
* [Choosing a plan and creating an instance](/docs/cloud-object-storage?topic=cloud-object-storage-provision)
* [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main)
* [Locking objects](/docs/cloud-object-storage?topic=cloud-object-storage-ol-overview)
* [Adding {{site.data.keyword.cloud_notm}} Object Storage](https://helpcenter.veeam.com/docs/backup/vsphere/adding_ibm_object_storage.html?ver=120){: external}

To add a Linux Hardened repository, see:
* [Building a custom bare metal server](/docs/bare-metal?topic=bare-metal-ordering-baremetal-server)
* [Veeam on bare metal server introduction](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-bms-archi-intro)
* [Provisioning the Linux hardened repository server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lhbr)
* [Hardened repository](https://helpcenter.veeam.com/docs/backup/vsphere/hardened_repository.html?ver=120){: external}

When you add a Linux hardened repository, consider:
* Recommendations from the Security Technical Implementation Guides (STIGs) created and maintained by the Defense Information Systems Agency (DISA) for Ubuntu 20.04 LTS. For more information, see [DISA STIGs Document Library](https://public.cyber.mil/stigs/downloads/){: external}.
* To be compliant with [DISA STIG UBTU-20-010414](https://www.stigviewer.com/stig/canonical_ubuntu_20.04_lts/2022-12-06/finding/V-238335){: external}, you do not need to enable disk encryption for the operating system. To protect data in backups, use Veeam Backup and Replication built-in encryption instead.

For postinstallation, consider the following Veeam recommendations:
   * To be compliant with [DISA STIG UBTU-20-010009](https://www.stigviewer.com/stig/canonical_ubuntu_20.04_lts/2022-12-06/finding/V-238204){: external}, set a password for GRUB.
   * To be compliant with [DISA STIG UBTU-20-010012](https://www.stigviewer.com/stig/canonical_ubuntu_20.04_lts/2022-12-06/finding/V-238206){: external}, you must have only two users:
      * The `root` account, which has a blank password and cannot be used for connection.
      * The user account that you create during the installation. This account is used to connect to the Linux server and deploy the required Veeam Backup and Replication components.

For {{site.data.keyword.cloud_notm}}, consider:
* The choice of storage regarding the location of primary data. If your {{site.data.keyword.vcf-auto}} instance has an NFS cluster, then an NFS share for backup data might place the primary and secondary data on the same storage appliance.
* No SMB (CIFS) share is available as a service in {{site.data.keyword.cloud_notm}}.
* Only virtual appliances versions of deduplicating storage appliances can be installed in {{site.data.keyword.cloud_notm}}. Furthermore, consider what storage that these appliances use.
* For object storage, see [Considerations and Limitations](https://helpcenter.veeam.com/docs/backup/vsphere/object_storage_repository_cal.html?ver=120){: external}.
* For Direct Backup to Object Storage, see [Considerations and limitations for direct backup to Object Storage](https://helpcenter.veeam.com/docs/backup/vsphere/object_storage_repository_cal.html?ver=120#considerations-and-limitations-for-direct-backup-to-object-storage){: external}.
