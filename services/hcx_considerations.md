---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-20"

keywords: VMware HCX, HCX, tech specs HCX

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware HCX on {{site.data.keyword.cloud_notm}} overview
{: #hcx_considerations}

VMware HCX™ on {{site.data.keyword.cloud}} extends the networks of on-premises data centers into {{site.data.keyword.cloud}}, and it helps you migrate virtual machines (VMs) to and from {{site.data.keyword.cloud_notm}} without any conversion or change. HCX creates an abstraction layer that enables application mobility and infrastructure hybridity through securely stretched networks. You can modernize your VMware® environment without the need to refactor or modify your existing application, as HCX enables a seamless transformation. With HCX, you can bring your IP subnet ranges into {{site.data.keyword.cloud_notm}} and ensure the IP consistency through a hybrid deployment and by providing high-level security with end-to-end Suite B encryptions. VMware HCX on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from VMware, not IBM.
{: shortdesc}

The HCX version available for deployment is periodically updated to the most recent version of HCX. VMware® by Broadcom requires you to be on one of their supported versions in order for you to open a support request for HCX. For more information, see the [VMware HCX release notes](https://docs.vmware.com/en/search/#/VMware%20HCX%20Release%20Notes){: external}.
{: note}

For {{site.data.keyword.vcf-auto}} with NSX-T™ instances, HCX is supported for NSX-T 3.1 or later and for VMware vSphere® 7.

For {{site.data.keyword.vcf-auto-short}} with NSX-V instances (VMware Solutions V4.7 and earlier), HCX is supported for vSphere 6.7.

{{site.data.content.para-promotion-services}}

A {{site.data.keyword.vcf-auto-short}} instance with HCX is limited to three simultaneous connections from on-premises sites.
{: restriction}

## Technical specifications for HCX
{: #hcx_considerations-specs}

The following components are ordered and included in the HCX service.

On-premises HCX instances include only licensing and activation.
{: restriction}

### HCX Management Appliance VM
{: #hcx_considerations-vm}

* CPU - 4 CPUs
* RAM - 12 GB
* Disk - 60 GB VMDK

More HCX appliances are deployed during configuration as necessary for L2 connectivity, WAN optimization, and gateway connections.

{{site.data.content.impnote-deploymanual-hcx}}

### Networking
{: #hcx_considerations-networking}

* One public portable subnet with 16 IP addresses
* Two private portable subnets with 64 IP addresses
* Eight IP addresses from private portable vMotion subnet

For more information about resource requirements and capacity checking, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

### NFS storage
{: #hcx_considerations-nsf-storage}

If the service mesh target cluster is not a vSAN™ cluster, NFS storage (with 500 GB and 10 IOPS/GB) is ordered.

For {{site.data.keyword.vcf-auto-short}} with NSX-V instances, the service mesh target cluster is the default cluster.
{: note}

### VMware NSX Edge Services Gateways for HCX management (NSX-V only)
{: #hcx_considerations-nsx}

An active-passive pair of VMware NSX Edge Services Gateways for HCX management is ordered.
* CPU - 6 CPUs
* RAM - 8 GB
* Disk - 3 GB VMDK

## Related links
{: #hcx_considerations-related}

* [Ordering HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering)
* [Managing HCX](/docs/vmwaresolutions?topic=vmwaresolutions-managinghcx)
* [Glossary of HCX terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_glossary)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [VMware HCX documentation](https://docs.vmware.com/en/VMware-HCX/index.html){: external}
