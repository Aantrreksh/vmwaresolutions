---

copyright:

  years:  2022, 2024

lastupdated: "2024-10-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for using IPsec over {{site.data.keyword.dl_short}} with a vCenter Server with NSX instance
{: #arch-pattern-nsx-t-direct-link-ipsec}

On [{{site.data.keyword.vcf-auto}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) instance in {{site.data.keyword.cloud}} classic infrastructure, your workloads are deployed and run on VMware NSX™ overlay networks. As part of the deployment, the automation deploys an example NSX topology. You can use the provisioned examples as your base or build your own topologies on overlay. These overlay networks are not automatically advertised to {{site.data.keyword.cloud_notm}} classic infrastructure network.

This architecture pattern presents private connectivity for {{site.data.keyword.vcf-auto}} that uses [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-dl-about) and tunneling. This solution is applicable for [NSX-based {{site.data.keyword.vcf-auto-short}} instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview), which is provisioned in {{site.data.keyword.cloud_notm}} classic infrastructure. You can use Gateway Appliance or vCenter Server gateway cluster with Juniper® vSRX or other device as part of the solution as an option.

The tunnel is established between NSX T0 and a customer router routable through {{site.data.keyword.dl_short}}. If vSRX or other third-party device is used in a gateway cluster, you can terminate the tunnel in these devices as well. In this case, NSX T0 advertises routes in the vSRX (or other third-party device) through BGP or Static Routes.

## Deploying IPsec over {{site.data.keyword.dl_short}} with vCenter Server and NSX
{: #arch-pattern-nsx-t-direct-link-ipsec-overview}

The following diagram presents an overview for an architecture pattern for deploying IPsec over {{site.data.keyword.dl_short}} with vCenter Server and NSX.

![Using IPsec over {{site.data.keyword.dl_short}} with {{site.data.keyword.vcf-auto}}](../../images/arch-pattern-vcs-nsx-t-direct-link.svg "Using IPsec over {{site.data.keyword.dl_short}} with {{site.data.keyword.vcf-auto}}."){: caption="Using IPsec over {{site.data.keyword.dl_short}} with {{site.data.keyword.vcf-auto}}" caption-side="bottom"}

This architecture pattern deployment is summarized as follows:

1. {{site.data.keyword.vcf-auto-short}} instance is deployed at {{site.data.keyword.cloud_notm}} classic infrastructure. Two {{site.data.keyword.cloud_notm}} private VLANs and one {{site.data.keyword.cloud_notm}} public VLAN (optional) are deployed. Each of these host multiple subnets. You can see the details on {{site.data.keyword.vmwaresolutions_short}} portal.
2. NSX T0 is deployed with two interfaces - private and public (optional). If you opt for a public, this interface is attached to your Public VLAN and has direct internet access. Your T0's private interface is attached to the Private VLAN and uses {{site.data.keyword.cloud_notm}} portable private IP.
3. If vCenter Server gateway cluster with vSRX (or other third-party device) or {{site.data.keyword.cloud_notm}} Gateway Appliance is deployed to your classic infrastructure, you must configure your {{site.data.keyword.vcf-auto-short}} instance private primary VLAN. It must be routed through the vSRX or Gateway Appliance. Also, establish routing between your NSX T0 and vSRX, such as BGP.
4. Create a {{site.data.keyword.dl_short}} at your {{site.data.keyword.cloud_notm}} data center or zone location and attach your classic network as a connection. All your classic networks in the region are advertised with local routing option (or all with Global option).
5. Configure a Policy or Route Based IPsec connection between your customer router to vSRX or Gateway Appliance private IP ({{site.data.keyword.cloud_notm}} private portable). Ensure that your T0, vSRX, or Gateway Appliance has a route to this tunnel end point. Large MTU is supported in {{site.data.keyword.cloud_notm}} private network and {{site.data.keyword.dl_short}}.
6. You can exchange routes through BGP, or static between your overlay and the on-premises customer router through the tunnel.
7. You can attach any other required VPC connections to the {{site.data.keyword.dl_short}}, for example, VPCs. Your VPC IP address allocation design must ensure that you do not overlap with the attached classic network nor with the NSX overlay networks.

{{site.data.keyword.dl_short}} does not provide direct connectivity between the VPC and classic. But, depending on your routing setup, it is possible to do a hair pinning on the customer router. Alternatively, use transit gateway for this use case.
{: note}

## Considerations
{: #arch-pattern-nsx-t-direct-link-ipsec-considerations}

When you design or deploy this architecture pattern, consider the following steps:

* Route-based IPsec VPN is recommended for dynamic routing.
* IPsec tunnels can also be terminated to Tier-1 gateways. In this case, only policy-based VPNs are supported. Also, ensure that the VPN endpoint is known and routed in {{site.data.keyword.cloud_notm}} classic network (for example, use a `/32` from the private portable subnet for the T1 VPN endpoint).

## Related links
{: #arch-pattern-nsx-t-direct-link-ipsec-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Getting started with {{site.data.keyword.dl_full_notm}} (2.0)](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [Virtual Private Network (VPN)](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-A8B113EC-3D53-41A5-919E-78F1A3705F58.html){: external}
