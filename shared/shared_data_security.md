---

copyright:

  years:  2020, 2023

lastupdated: "2023-08-22"

keywords: personal data, data deletion, PHI, data, data security, high availability, ha, disaster recovery, vmware solutions shared, compliance

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing your data in VMware Shared
{: #shared_data}

Review the following data storage, high availability, and disaster recovery considerations before you order {{site.data.keyword.vmwaresolutions_full}} Shared.

## Data security
{: #shared_data-security}

VMware Shared supports data storage in the form of:

* VMware Cloud Director virtual machine (VM) instances
* VMware Cloud Director customer media uploads
* VMware Cloud Director customer templates
* VMware Cloud Director independent disks
* Veeam® backups

All VMware Cloud Director data is stored in multitenant datastores where the datastores are secured by VMware Cloud Director. A significant portion of VMware Cloud Director security, especially in protecting cloud tenants from internal threats, comes from the security of the underlying virtualization layer. It includes VMware vSphere®, the additional security of VMware Cloud Director, and the security of the ESXi™ hosts themselves. The VMware Cloud Director abstraction separates different organizations from each other. Different organizations cannot modify or see each other's organizations data at rest or data in motion.

VMware Cloud Director data storage uses {{site.data.keyword.cloud_notm}} Infrastructure Endurance {{site.data.keyword.filestorage_short}}, which is encrypted at rest to Endurance {{site.data.keyword.filestorage_short}} specifications. When VMware Cloud Director data is deleted, it becomes available for reallocation where it is then zeroed out and instantiated for the next use case.

Veeam service backups are to both {{site.data.keyword.cloud_notm}} Infrastructure Endurance {{site.data.keyword.filestorage_short}} and Cloud Object Storage for longer term storage. When the first VMware Shared virtual data center is created, a unique encryption key is generated for each customer organization. It is used to encrypt all Veeam backups for that specific customer's organization. The encryption key is not stored and is unavailable to IBM. After the VMware Cloud Director Data Center is deleted, all backups are deleted, and cannot be recovered.

## High availability and disaster recovery
{: #shared_data-ha-dr}

The VMware Shared management service is initially only offered in the {{site.data.keyword.cloud_notm}} NA South and Europe regions. Recovering from potential disasters that affect an entire location requires planning and preparation.

* You are responsible for understanding your configuration, customization, and usage of the service.
* You are responsible for enabling your VMs or virtual applications (vApps) to participate in the provided backup service.
* You are responsible for being ready to restore all instances of your VMs or vApps used in the service in the restored location or new location.

### High availability
{: #shared_data-ha}

VMware Shared supports high availability of the VMware Cloud Director service itself. The service achieves high availability automatically and transparently by using the Multizone region (MZR) feature that is provided by {{site.data.keyword.cloud_notm}}.

However, you cannot configure workloads that are running VMs and vApps in a high availability manner across multiple {{site.data.keyword.cloud_notm}} data center sites. VMware Shared currently allows workloads to operate in only one {{site.data.keyword.cloud_notm}} data center site.

Use VMware Shared with vCenter Server to achieve high availability. You can deploy vCenter Server in multiple {{site.data.keyword.cloud_notm}} data center regions.

### Disaster recovery
{: #shared_data-dr}

Disaster recovery can become an issue if an {{site.data.keyword.cloud_notm}} location experiences a significant failure that includes the potential loss of data. Because MZRs are not available across locations, you must wait for IBM to bring a location back online if it becomes unavailable. If underlying data services are compromised by the failure, you must also wait for IBM to restore those data services.

If a catastrophic failure occurs, IBM might not be able to recover data from database backups. In this case, you need to restore your data to return your service instance to its most recent state. You can restore the data to the same or to a different location, including a vCenter Server instance.

Your disaster recovery plan includes knowing, preserving, and being prepared to restore all data that is maintained on {{site.data.keyword.cloud_notm}}.

## Related links
{: #shared_data-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
