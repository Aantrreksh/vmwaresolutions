---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-31"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# KMIP for VMware overview
{: #kmip-overview}

This solution architecture describes the KMIP™ on VMware architecture for protecting your VMware® instances. Many storage encryption options are available to protect your VMware workload. KMIP for VMware works together with VMware native vSphere encryption and vSAN™ encryption. The vSphere and vSAN encryption provides simplified storage encryption management together with the security and flexibility of {{site.data.keyword.cloud}} Key Protect or {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services customer-managed keys.

This solution is considered to be an extra component and extension of the {{site.data.keyword.vcf-classic}} offerings on {{site.data.keyword.cloud_notm}}. As a result, this document doesn't cover the existing configuration of these foundation solutions on {{site.data.keyword.cloud_notm}}. To understand more about the foundation solution architecture, see [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview).

## Key benefits
{: #kmip-overview-benefits}

While many storage encryption solutions are available for your VMware workload, KMIP for VMware offers the following benefits:

* Integration with VMware vSAN encryption and vSphere encryption, both of which are implemented in the hypervisor layer rather than the storage or virtual machine layer. This approach allows easy management and transparency to your storage solution and application.
* Fully managed key management server available in many {{site.data.keyword.cloud_notm}} multizone regions (MZRs).
* Integrating your VMware cluster with {{site.data.keyword.cloud_notm}} Key Protect or {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services provides you with fully customer-managed keys that you can revoke at any time.

## Related links
{: #kmip-overview-related}

* [Solution design](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-design)
* [Implementation and management](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-implementation)
* [High availability and disaster recovery](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-hadr)
