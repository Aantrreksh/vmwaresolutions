---

copyright:

  years:  2020, 2023

lastupdated: "2023-06-02"

keywords: vmware regulated workloads, regulated workloads, workloads instance, regulated instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware Regulated Workloads overview
{: #vrw-overview}

The VMware® Regulated Workloads offering includes a secure-by-default architecture that follows the {{site.data.keyword.IBM}} unique policy controls framework. It also includes continuous compliance monitoring and the highest level of data encryption FIPS 140-2 Level 4.

Review the following specifications before you begin.
* VMware Regulated Workloads is only available for single-zone topology.
* VMware Regulated Workloads are based on VMware NSX-T™ and VMware vSphere® 7.
* [Hyper Protect Crypto Services](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services), [KMIP for VMware](https://cloud.ibm.com/infrastructure/vmware-solutions/console/servicestandalonenew/KMIPAdapter), and [Direct Link Dedicated](https://cloud.ibm.com/interconnectivity/direct-link) are required for VMware Regulated Workloads. Ensure that you order these services before you start your VMware Regulated Workloads order.
* Some of the services require configuration setup. Review each service and ensure that you configure its settings properly, as indicated.
* The **Private network only** option is available for all clusters. The **Public and private network** option is available only for the gateway cluster.

## Options not available for VMware Regulated Workloads
{: #vrw-overview-before-not-avail-options}

The following options or settings are not available for VMware Regulated Workloads:
* Local disks
* High performance with Intel® Optane
* vSAN™ deduplication and compression
* Selection of existing VLANs. Only the option to order new VLANs is available.
* Single public Windows® VSI for Active Directory™ DNS configuration. Only the option to order two highly available dedicated Windows server virtual machines (VMs) on the management cluster is available.

## Related links
{: #vrw-overview-related}

* [VMware Regulated Workloads reference architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview)
* [Planning for VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-planning)
* [Ordering VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-req)
* [Viewing and deleting VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-view-delete-instance)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
