---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for using {{site.data.keyword.dl_short}} with NSX edge cluster in colocation
{: #arch-pattern-direct-link-edge}

On [{{site.data.keyword.vcf-auto}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) instance in {{site.data.keyword.cloud}} classic infrastructure, your workloads are deployed and run on VMware NSX™ overlay networks. As part of the deployment, the automation deploys an example NSX topology. You can use the provisioned examples as your base or build your own topologies on overlay. These overlay networks are not automatically advertised to {{site.data.keyword.cloud_notm}} classic infrastructure network. 

This architecture pattern presents private connectivity for {{site.data.keyword.vcf-auto}} that uses [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-dl-about) and deploying an NSX edge transport node at the colocation. This solution is applicable for [NSX-based {{site.data.keyword.vcf-auto-short}} instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview), which is provisioned in {{site.data.keyword.cloud_notm}} classic infrastructure. 

This solution relies on the principle that you can advertise NSX TEP traffic through {{site.data.keyword.dl_short}} to the colocation. Therefore, you can extend your NSX overlays over {{site.data.keyword.dl_short}}. You are responsible for deploying the edge transport nodes in colocation on your own x86 hardware and for creating the NSX edge cluster and configuring Tier-0 (T0) Gateway on the edge cluster.

You can use Gateway Appliance or vCenter Server gateway cluster with Juniper vSRX or other device as part of the solution. This is optional.

## Deploying {{site.data.keyword.dl_short}} with NSX edge cluster in colocation
{: #arch-pattern-direct-link-edge-overview}

The following diagram presents an overview of an architecture pattern for deploying {{site.data.keyword.dl_short}} with NSX edge cluster in colocation.

![{{site.data.keyword.dl_short}} with NSX edge cluster in colocation](../../images/arch-pattern-vcs-nsx-t-direct-link-edge.svg "{{site.data.keyword.dl_short}} with NSX edge cluster in colocation."){: caption="Figure 1. {{site.data.keyword.dl_short}} with NSX edge cluster in colocation" caption-side="bottom"}

This architecture pattern deployment is summarized as follows: 

1. {{site.data.keyword.vcf-auto-short}} instance is deployed at {{site.data.keyword.cloud_notm}} classic infrastructure. Two {{site.data.keyword.cloud_notm}} private VLANs and one {{site.data.keyword.cloud_notm}} public VLAN (optional) are deployed. Each of these VLANs host multiple subnets. You can see the details through {{site.data.keyword.vmwaresolutions_short}} portal.
2. NSX T0 is deployed with two interfaces - private and public (optional). If you opt for a public one, this interface is attached to your Public VLAN and has direct internet access. Your T0's private interface is attached to the Private VLAN and it uses {{site.data.keyword.cloud_notm}} portable private IP.
3. If vCenter Server gateway cluster with vSRX (or other third-party device) or {{site.data.keyword.cloud_notm}} Gateway Appliance is deployed to your classic infrastructure, you must configure your {{site.data.keyword.vcf-auto-short}} instance private primary VLAN. It is routed through the vSRX or Gateway Appliance and allows TEP traffic through it.
4. Create a {{site.data.keyword.dl_short}} at your {{site.data.keyword.cloud_notm}} data center or zone location and attach your classic network as a connection. All your classic networks in the region are advertised with Local routing option (or all with Global Option). Use BGP between your colocation router and {{site.data.keyword.dl_short}}. Ensure that the networks planned for NSX edge transport node management and TEP traffic are advertised through this BGP session to {{site.data.keyword.dl_short}}.
5. Deploy an NSX edge cluster at colocation and create a T0 at the colocation cluster. Create routes on edge nodes for management and TEP traffic through the {{site.data.keyword.dl_short}} path.
6. Configure an NSX overlay transit segment between T0 VRFs and configure routing between the T0 VRFs.
7. Each tenant has their own WANs or MPLS. You must design and configure how to secure and separate the tenants and connect to tenant WANs.

## Considerations
{: #arch-pattern-direct-link-edge-considerations}

When you design or deploy this architecture pattern, consider the following steps:

* This pattern requires BYOL for the colocation solution VMware licensing. Contact VMware or your Business Partner for licensing details.
* This pattern requires you to bring your own x86 hardware at colocation to host the NSX edge transport nodes.

## Related links
{: #arch-pattern-direct-link-edge-links}

* [Getting started with {{site.data.keyword.dl_full_notm}} (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Installing NSX Edge](https://docs.vmware.com/en/VMware-NSX-Data-Center/3.1/installation/GUID-5EF2998C-4867-4DA6-B1C6-8A6F8EBCC411.html){: external}
