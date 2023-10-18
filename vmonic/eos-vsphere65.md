---

copyright:

  years:  2022, 2023

lastupdated: "2023-10-18"

keywords: end of support notice, vSphere 6.5 deployment, end of support vSphere 6.5, vSphere 6.5 deprecated, vSphere 6.5 support

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# End of Support for vSphere 6.5 instance deployments
{: #eos-vsphere65}

{{site.data.keyword.cloud_notm}} support for ordering all update levels of VMware vSphere® 6.5 ended on 10 October 2021. After that date, you can no longer order new VMware vCenter Server® instances with vSphere 6.5. Your existing vCenter Server instances with vSphere 6.5 are read–only in the VMware Solutions console.

For more information about upgrading to vSphere 7, see [Upgrading vCenter Server vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade) or [Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).

{{site.data.keyword.cloud_notm}} encourages that you migrate rather than upgrade to vSphere 7. Migration ensures that you are aligned with current and supported hardware, other {{site.data.keyword.cloud_notm}} features, and the vSphere 7 NSX–T topology, including the use of VMware vSphere Distributed Switches.

Before you upgrade, you must assess your environments for infrastructure and workload dependencies to ensure that they are supported for the current version.

vSphere 7 introduces the following features:
* HTML5 client
* Support for Intel Cascade Lake EVC level
* Enhanced vSphere Lifecycle Manager (LCM)
* Enhancements to DRS and vMotion
* Security enhancements such as multifactor authentication (MFA), vSphere Trust Authority (vTA), and in–flight encryption for vSAN

vSphere 7 is also the exclusive basis for VMware Regulated Workloads.

For more information about end of life procedures for {{site.data.keyword.cloud_notm}} infrastructure services and Third–Party software products, see [Lifecycle policy for {{site.data.keyword.cloud_notm}} products](https://www.ibm.com/cloud/cloud-prod-life). If you have any questions or need assistance, email clouddigitalsales@us.ibm.com or open a support ticket in the VMware Solutions console.

## Related links
{: #eos-vsphere65-related}

* [End of Support for NSX-V instance deployments](/docs/vmwaresolutions?topic=vmwaresolutions-eos-nsx-v)
* [End of Support for vSphere 6.7 instance deployments](/docs/vmwaresolutions?topic=vmwaresolutions-eos-vsphere67)
