---

copyright:

  years:  2022, 2024

lastupdated: "2024-01-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.tg_full_notm}} overview
{: #interconnectivity-tgw-overview}

With {{site.data.keyword.tg_full}} (TGW), you can create a single or multiple transit gateways to connect VPCs together. You can also connect your {{site.data.keyword.cloud_notm}} classic infrastructure to a {{site.data.keyword.tg_short}} to provide seamless communication with Classic Infrastructure resources. Any new network that you connect to a {{site.data.keyword.tg_short}} is then automatically made available to every other network connected to it.

{{site.data.keyword.tg_full_notm}} supports local and global routing between VPCs and the {{site.data.keyword.cloud_notm}} classic infrastructure. Connections to and from an {{site.data.keyword.tg_full_notm}} on the IBM private network are not shown to the public internet. This arrangement reduces public egress and VPN costs and reduces security threats. {{site.data.keyword.tg_full_notm}} is a fully redundant, fault-tolerant service with no single point of failure within {{site.data.keyword.cloud_notm}} multizone regions.

{{site.data.keyword.tg_full_notm}} provisions and defines connections between resources on the {{site.data.keyword.cloud_notm}} network, providing private interconnectivity between {{site.data.keyword.cloud_notm}} data centers worldwide. It also provides a central hub for connectivity, making it easier to provision and manage your networks. With {{site.data.keyword.tg_full_notm}}, you can create a single {{site.data.keyword.tg_short}} or multiple transit gateways to connect {{site.data.keyword.vpc_short}}s. You can also connect your {{site.data.keyword.cloud_notm}} classic infrastructure to a {{site.data.keyword.tg_short}} to provide seamless communication with classic infrastructure resources. Any new resource that you connect to a {{site.data.keyword.tg_short}} is automatically made available to every other resource connected to it. All data remains within the private {{site.data.keyword.cloud_notm}} backbone and is optimized for performance.

For more information, see [About {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-about).

## Considerations with roll-your-own VMware solution on VPC
{: #interconnectivity-tgw-ryo-considerations}

When you use {{site.data.keyword.tg_short}} with your VMware® solution on VPC, the routing differs slightly between the two networking architectures.

When you use VMware virtual machines (VMs) on VPC subnets architecture, your VMs are attached to VPC subnets and the routing behaves in the same way as with VPC Virtual Servers. The VPC subnets are provisioned from the zone prefix, and when the VPC is attached to a {{site.data.keyword.tg_short}}, the routing works between other VPCs without any required changes. If you are using IANA-registered IP addresses in your VPC, see [Routing considerations for IANA-registered IP assignments](/docs/vpc?topic=vpc-interconnectivity#routing-considerations-iana).

![{{site.data.keyword.tg_short}} with VMware on VPC](../../images/vpc-ryo-diagrams-tgw-sub-arch.svg "{{site.data.keyword.tg_short}} with VMware on VPC"){: caption="Figure 1. {{site.data.keyword.tg_full_notm}} with VMware on VPC" caption-side="bottom"}

When you use NSX-T™ on your VMware solution on VPC, the VMs are attached on the NSX-T overlay segments. They use an IP address range or prefix, which is reachable through VPC route that points to the NSX-T Tier-0 private uplink VIP as described in [VMware NSX-T logical routing on VPC](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-nsx-t-vpc-routing). When you attach the VPC to a {{site.data.keyword.tg_short}}, you must create a VPC prefix that matches the VPC route, which points to the NSX-T overlay. You must not define any subnets on the prefix. However, the prefix must exist so that the {{site.data.keyword.tg_short}} can advertise the NSX-T overlay routes to other connections (VPCs, Classic, or Direct Link) that are attached to it.

![{{site.data.keyword.tg_short}} with VMware on VPC with NSX-T](../../images/vpc-ryo-diagrams-tgw-nsx-t-arch.svg "{{site.data.keyword.tg_short}} with VMware on VPC with NSX-T"){: caption="Figure 2. {{site.data.keyword.tg_full_notm}} with VMware on VPC with NSX-T" caption-side="bottom"}

## Related links
{: #interconnectivity-tgw-ryo-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
