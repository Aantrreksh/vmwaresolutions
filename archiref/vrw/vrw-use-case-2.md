---

copyright:

  years:  2020, 2023

lastupdated: "2023-09-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Use case 2
{: #vrw-use-case-2}

{{site.data.keyword.cloud}} for VMware® Regulated Workloads delivers high security for sensitive workloads such as those run by users in the healthcare or financial sectors.

The architecture of the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads is designed for isolation of sensitive workloads.

Compute and storage resources are offered in a dedicated workload region where the deployment of multiple clusters allows isolation of workloads by business unit or other designation, such as PCI workloads, further enhancing the security of the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads.

Network isolation is maintained between the workload region, the management plane, and the edge region by using a gateway appliance at the physical plant level. The workloads also benefit from the inclusion of an SDN overlay that is delivered with NSX-T™. NSX-T uses micro-segmentation to enforce traffic isolation. Micro-segmentation policies applied to workload VMs are configured by the user to meet business requirements.

The use of shared resources, such as VSIs or shared storage options, is prohibited to prevent any data leakage out of the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads. All resources necessary to support the workloads are delivered from within the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads dedicated instance.

Data and VM encryption options are included in the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads. The preferred option is `keep your own key (KYOK)` by using IBM Hyper Protect Crypto Services (HPCS). Connecting HPCS to the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads is either accomplished by through the {{site.data.keyword.cloud_notm}} KMIP adapter that is required to integrate with the vCenter directly.

{{site.data.keyword.cloud_notm}} for VMware Regulated Workloads is designed with high security throughout the platform, which makes it an option for user workloads that demand the highest level of protection.

## Related links
{: #vrw-use-case-2-related}

* [{{site.data.keyword.cloud_notm}} compliance programs](https://www.ibm.com/cloud/compliance)
