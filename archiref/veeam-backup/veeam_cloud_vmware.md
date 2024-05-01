---

copyright:

  years: 2023, 2024

lastupdated: "2024-04-12"

keywords: veeam, IBM cloud for vmware, veeam in IBM Cloud for vmware

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Veeam in {{site.data.keyword.cloud_notm}} for VMware
{: #veeam_cloud_vmware}

## Overview 
{: #veeam_cloud_vmware_overview}

Veeam® in {{site.data.keyword.cloud_notm}} for VMware is an optional add-on service that can be ordered during the initial ordering of a vCenter Server instance or added to an existing vCenter Server instance.

The service can be deployed by using the following options:

* Windows Server virtual machine (VM) with iSCSI storage (selectable storage size and performance)
* Single Windows VSI with iSCSI storage (selectable storage size and performance)
* Bare metal server with local storage (selectable storage size)
* Linux hardened repository (selectable storage size)
* Number of VMs to license

Unless, the Linux® hardened repository is ordered then Veeam is deployed by using the Veeam simple deployment scenario. This deployment scenario is suitable for small environments. Otherwise, the purpose of the Veeam Backup and Replication evaluation and all services that are needed for data protection tasks are installed on a single Windows-based machine. If the Linux hardened repository option is selected, then the service is deployed by using the Veeam advanced deployment scenario with the backup repository on a Linux server. The other services that are required for data protection tasks are installed on the single Windows-based machine.

The simple scenario deployment can be changed to the advanced scenario deployment by following the Veeam documented guidance and recommendations. Also, within the advanced scenario deployment, components can be moved to their own dedicated resources to enable capacity and high availability.

In the simple deployment scenario, Windows Server hosts the following Veeam components:
* **Backup server** - Coordinates jobs, controls scheduling, and performs administrative activities.
* **Console** - A client-side component that provides access to the backup server. Log in to Veeam Backup and Replication and perform all data protection and disaster recovery operations on the backup server.
* **VMware backup proxy** - Handles job processing and transfers backup traffic.
* **Backup repository** - Backup files are stored in the repository.
* **Mount server** - Needed for restoring of Windows guest OS files.
* **Guest interaction proxy** - Needed for application-aware processing, indexing of guest file system, and transaction log processing.

After the initial provisioning of the service, the only Day 2 automations available are:
* Deprovision the service.
* Add or Remove licenses.

All other tasks are customer-managed with help of the Veeam documentation.

## Information on expanding your Veeam environment
{: #veeam_cloud_vmware_info}

The following steps show how to configure the post-service deployment to expand your Veeam environment in {{site.data.keyword.cloud}}:

* To order extra private subnets, see [Ordering secondary subnets and global IP addresses](/docs/subnets?topic=subnets-order-subnets).
* To order extra virtual server instance, see [Provisioning public instances](/docs/virtual-servers?topic=virtual-servers-ordering-vs-public).
* To order extra bare metal servers, see [Building a custom bare metal server](/docs/bare-metal?topic=bare-metal-ordering-baremetal-server).
* To order {{site.data.keyword.cloud_notm}} object storage, see:
   * [Choosing a plan and creating an instance](/docs/cloud-object-storage?topic=cloud-object-storage-provision)
   * [Endpoints and storage locations](/docs/cloud-object-storage?topic=cloud-object-storage-endpoints)
   * [Using storage classes](/docs/cloud-object-storage?topic=cloud-object-storage-classes)
   * [Using HMAC credentials](/docs/cloud-object-storage?topic=cloud-object-storage-uhc-hmac-credentials-main)
   * [Locking objects](/docs/cloud-object-storage?topic=cloud-object-storage-ol-overview)

* To use block storage for your Veeam Backup and Replication backup repository, see [Ordering block storage for classic](/docs/BlockStorage?topic=BlockStorage-orderingBlockStorage&interface=ui).
* To connect to your block storage, see [Connecting to iSCSI LUNs on Linux](/docs/BlockStorage?topic=BlockStorage-mountingLinux&interface=ui) and [Connecting to iSCSI LUNS on Microsoft Windows](/docs/BlockStorage?topic=BlockStorage-mountingWindows&interface=ui).
* To expand your block storage, see [Expanding Block Storage for Classic capacity](/docs/BlockStorage?topic=BlockStorage-expandingcapacity&interface=ui).

## Related links
{: #veeam_cloud_vmware-links}

* [Simple deployment](https://helpcenter.veeam.com/docs/backup/vsphere/simple.html?ver=120){: external}
* [Advanced deployment](https://helpcenter.veeam.com/docs/backup/vsphere/advanced.html?ver=120){: external}

