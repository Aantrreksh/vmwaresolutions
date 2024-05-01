---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-15"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.dl_full_notm}} overview
{: #interconnectivity-dl}

{{site.data.keyword.dl_full}} offerings provide connectivity from an external source into a customer {{site.data.keyword.cloud_notm}} private network. {{site.data.keyword.dl_short}} can be viewed as an alternative to a site-to-site VPN solution, which is designed for customers that need more consistent, higher-throughput connectivity between a remote network and their {{site.data.keyword.cloud_notm}} environments.

The {{site.data.keyword.dl_full_notm}} service is a routed OSI Layer-3 service. It offers a direct connection to the {{site.data.keyword.cloud_notm}} private network backbone. Currently, two types of {{site.data.keyword.dl_short}} connections are available:

* **{{site.data.keyword.dl_short}} Dedicated** - Offers a single-tenant, fiber-based cross-connect into the {{site.data.keyword.cloud_notm}} network.
* **{{site.data.keyword.dl_short}} Connect** - Offers private access through various service providers into the {{site.data.keyword.cloud_notm}} network and to any other clouds.

For more information, see [About {{site.data.keyword.dl_full_notm}} (2.0)](/docs/dl?topic=dl-dl-about).

## Considerations with VMware Cloud Foundation solution in VPC
{: #interconnectivity-dl-vcf-considerations}

When you use the VMware® virtual machines (VMs) on the VPC subnet architecture, your VMs are attached to VPC subnets and the routing behaves in the same way as with VPC Virtual Servers. The VPC subnets are provisioned from the zone prefix, and when the VPC is attached to a {{site.data.keyword.dl_short}}, the routing works between on-premises without any required changes. If you are using IANA-registered IP addresses in your VPC, see [Routing considerations for IANA-registered IP assignments](/docs/vpc?topic=vpc-interconnectivity#routing-considerations-iana).

![Direct Link with VMware on VPC](../../images/vpc-vcf-diagrams-dl-sub-arch.svg "Direct Link with VMware on VPC"){: caption="Figure 1. {{site.data.keyword.dl_short}} with VMware on VPC" caption-side="bottom"}

When you use NSX-T™ on your VMware® solution on VPC, the VMs are attached on the NSX-T overlay segments. They use an IP address range or prefix, which is reachable through VPC route. The IP address range or prefix points to the NSX-T Tier-0 private uplink VIP as described in the [VMware NSX-T logical routing on VPC](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-nsx-t-vpc-routing) topic. When you attach the VPC to a {{site.data.keyword.dl_short}}, you must create a VPC prefix that matches the VPC route, which points to the NSX-T overlay. You must not define any subnets on the prefix. However, the prefix must exist so that {{site.data.keyword.dl_short}} can advertise the NSX-T overlay routes to the on-premises network.

![Direct Link with VMware on VPC with NSX-T](../../images/vpc-vcf-diagrams-dl-nsx-t-arch.svg "Direct Link with VMware on VPC with NSX-T"){: caption="Figure 2. {{site.data.keyword.dl_short}} with VMware on VPC with NSX-T" caption-side="bottom"}

## Related links
{: #interconnectivity-dl-vcf-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
