---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-31"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware Solutions components
{: #design_overview}

{{site.data.keyword.vmwaresolutions_full}} provides automation to deploy VMware® technology components into {{site.data.keyword.cloud}} data centers across the globe.

The offerings in this solution portfolio include VMware Cloud Foundation™ products within an automatically deployed and configured cluster: VMware vSphere ESXi™, VMware vCenter Server® Appliance, VMware NSX-T™, and optionally, VMware vSAN™.

The architecture consists of a single cloud region. You can extend into more cloud regions that are located in another geography and in another {{site.data.keyword.cloud_notm}} pod within the same data center. A region is defined as a unique {{site.data.keyword.vcf-auto}} instance. This design also allows for automated expansion and contraction of virtual capacity within a {{site.data.keyword.vcf-auto}} instance.

![Solution components of {{site.data.keyword.vmwaresolutions_short}}](../../images/vcsv4radiagrams-ra-full.svg "The solution comprises physical infrastructure, virtual infrastructure, infrastructure management, and common services."){: caption="Solution components of {{site.data.keyword.vmwaresolutions_short}}" caption-side="bottom"}

## Related links
{: #design_overview-related}

* [Virtual infrastructure design](/docs/vmwaresolutions?topic=vmwaresolutions-design_virtualinfrastructure)
* [Common services design](/docs/vmwaresolutions?topic=vmwaresolutions-design_commonservice)
* [Infrastructure management design](/docs/vmwaresolutions?topic=vmwaresolutions-design_infrastructuremgmt)
