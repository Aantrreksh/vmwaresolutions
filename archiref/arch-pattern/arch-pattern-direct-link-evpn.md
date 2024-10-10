---

copyright:

  years:  2022, 2024

lastupdated: "2024-10-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for using {{site.data.keyword.dl_short}} with NSX and EVPN
{: #arch-pattern-direct-link-evpn}

On [{{site.data.keyword.vcf-auto}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) instance in {{site.data.keyword.cloud}} classic infrastructure, your workloads are deployed and run on VMware NSX™ overlay networks. As part of the deployment, the automation deploys an example NSX topology. You can use the provisioned examples as your base or build your own topologies on overlay. These overlay networks are not automatically advertised to {{site.data.keyword.cloud_notm}} classic infrastructure network.

This architecture pattern presents private connectivity for {{site.data.keyword.vcf-auto}} that uses [{{site.data.keyword.dl_short}}](/docs/dl) and EVPN. EVPN (Ethernet VPN) is a standard-based BGP control plane that extends Layer 2 and Layer 3 connectivity between different data centers. Multi-Protocol BGP (MP-BGP) EVPN is established between NSX T0 and a Customer Router through {{site.data.keyword.dl_short}}. {{site.data.keyword.cloud_notm}} private network and {{site.data.keyword.dl_short}} are used as L3 transport network for VXLAN traffic. VXLAN is the used encapsulation between NSX and the Customer Router.

You can use Gateway Appliance or vCenter Server gateway cluster with Juniper vSRX or other device as part of the solution. This is optional.

## Deploying {{site.data.keyword.dl_short}} with NSX and EVPN
{: #arch-pattern-direct-link-evpn-overview}

The following diagram presents an overview for an architecture pattern for using {{site.data.keyword.dl_short}} with NSX and EVPN.

![{{site.data.keyword.dl_short}} with NSX and EVPN](../../images/arch-pattern-vcs-nsx-t-direct-link-evpn.svg "{{site.data.keyword.dl_short}} with NSX and EVPN."){: caption="{{site.data.keyword.dl_short}} with NSX and EVPN" caption-side="bottom"}

This architecture pattern deployment is summarized as follows:

1. {{site.data.keyword.vcf-auto-short}} instance is deployed at {{site.data.keyword.cloud_notm}} classic infrastructure. Two {{site.data.keyword.cloud_notm}} private VLANs and one {{site.data.keyword.cloud_notm}} Public VLAN (optional) are deployed. Each of these VLANs host multiple subnets. You can see the details through {{site.data.keyword.vmwaresolutions_short}} portal.
2. NSX T0 is deployed with two interfaces - private and public (optional). If you opt for a public one, this interface is attached to your Public VLAN and has direct internet access. Your T0's private interface is attached to the Private VLAN and it uses {{site.data.keyword.cloud_notm}} portable private IP.
3. If vCenter Server gateway cluster with vSRX (or other third-party device) or {{site.data.keyword.cloud_notm}} Gateway Appliance is deployed to your classic infrastructure, you must configure your {{site.data.keyword.vcf-auto-short}} instance private primary VLAN. It is routed through the vSRX or Gateway Appliance. Ensure that you allow BGP and VXLAN traffic though the firewall.
4. Create a {{site.data.keyword.dl_short}} at your {{site.data.keyword.cloud_notm}} data center or zone location and attach your classic network as a connection. All your classic networks in the region are advertised with Local routing option (or all with Global Option). Ensure that you advertise the required networks for establishing the BGP session and VXLAN traffic.
5. Configure MP-BGP with eBGP multihop and EVPN on your T0 router. Create a T0 VRF for each tenant as an EVPN tenant in NSX.
6. VXLAN or VNI are used for each tenant. Transport between your colocation router and NSX transport nodes and Tier-0 traverse through {{site.data.keyword.cloud_notm}} classic infrastructure network and {{site.data.keyword.dl_short}}.
7. Each tenant can have their own WANs or MPLS. You must arrange the network separation at colocation by using your routers and switches. Also, you must design and configure how to secure and separate the tenants and connect to tenant WANs.

## Considerations
{: #arch-pattern-direct-link-evpn-considerations}

When you design or deploy this architecture pattern, consider the following steps:

* You are responsible for configuring EVPN between your T0 gateways and the routers in colocation.
* You can deploy more NSX edge transport nodes manually on {{site.data.keyword.cloud_notm}} side, if needed.
* EVPN uses its own address family in MP-BGP and NSX advertises EVPN type-5 routes.
* If you use `vpnv4 unicast address-family` in the connecting router to connect to MPLS VPNs, your router must be able to convert the advertisements between these two address families.
* Refer to your router vendor and VMware NSX documentation for EVPN interoperability and EVPN configuration details.

## Related links
{: #arch-pattern-direct-link-evpn-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Getting started with {{site.data.keyword.dl_full_notm}} (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [Configuring EVPN](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-D8186088-6C8F-4553-B859-B9499D9FB559.html){: external}
