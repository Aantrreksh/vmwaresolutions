---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Virtual Private Cloud overview
{: #vpc-ryo-vpc}

The {{site.data.keyword.vpc_full}} is a virtual network that is linked to your customer account. It gives you cloud security, with the ability to scale dynamically, by providing fine-grained control over your virtual infrastructure and your network traffic segmentation.

Each VPC is deployed to a single region. Within that region, the VPC can span multiple zones.

{{site.data.keyword.cloud_notm}} virtual or {{site.data.keyword.cloud_notm}} bare metal server presented in your VPC is attached to subnets. Subnets within the VPC offer private connectivity, thus your servers can communicate within and between the subnets by using an implicit router. Subnets in your VPC can connect to the public internet through an optional public gateway, or you can assign floating IP addresses to any network interface of the servers.

The following diagram shows an overview of {{site.data.keyword.vpc_short}}.

![IBM VPC connectivity and security](../../images/vpc-ryo-diagrams-overview-virtual.svg "IBM VPC connectivity and security"){: caption="Figure 1. {{site.data.keyword.vpc_short}} connectivity and security" caption-side="bottom"}

Review the following concepts to understand how {{site.data.keyword.vpc_short}} is constructed. The terminology is used throughout this architecture solution.

A region is an abstraction that is related to the geographic area in which a VPC is deployed. Each region contains multiple zones, which represent independent fault domains. A VPC can span multiple zones within its assigned region. A region is also often referred to a multizone region or MZR.

A zone is an abstraction that refers to the physical data center, which hosts the compute, network, storage resources, and the related cooling and power, which provides services and applications. Zones are isolated from each other, so to create no shared single point of failure, improved fault tolerance, and reduced latency. Each zone is assigned a default address prefix, which specifies the range of addresses in which subnets can be created. If the default address scheme does not suit your requirements, such as if you want to bring your own public IPv4 address range, you can customize the address prefixes. A zone is also known as an availability zone or AZ.

Virtual Private Clouds or VPCs are deployed to a single region. Within that region, the VPC can span multiple zones. You can have multiple VPCs in your {{site.data.keyword.cloud_notm}} account.

Subnets within the VPC offer private connectivity. They can communicate to each other over a private link by using the implicit router. Setting up routes is not necessary. Subnets are provisioned from prefixes, which are defined per zone and assigned to {{site.data.keyword.cloud_notm}} virtual server or bare metal server instance vNICs.

Subnets in your VPC can connect to the public internet through an optional public gateway. You can assign floating IP addresses to any virtual server or bare metal server instance vNICs to enable it to be reachable from the internet, independent of whether its subnet is attached to a public gateway. Floating IP addresses can be either NATed to private VPC subnet IPs, or routed to NSX-T logical routers without NAT. Currently, only one or more single IP addresses can be routed, but as the solution develops, it's possible to route entire subnets. When the VPC NAT is disabled, the packet is passed unmodified to or from the network interface, allowing for instance the NSX-T logical routers to perform any needed NAT or routing operations. This capability can also be used with public IP addresses assigned to NSX-T overlay services and later with subnets on NSX-T segments.

An Access Control List (ACL) can allow or deny inbound and outbound traffic for a subnet. It is stateless, which means that inbound and outbound rules must be specified separately and explicitly. Each ACL consists of rules based on a source IP, source port, destination IP, destination port, and protocol. Every VPC has a default ACL that allows all inbound and outbound traffic. You can edit the default ACL rules, or create a custom ACL and attach it to your subnets. A subnet can have only one ACL attached to it at any time, but one ACL can be attached to multiple subnets.

A security group operates as a virtual firewall that controls the traffic for one or more virtual server instances. It is a collection of rules that specify whether to allow or deny traffic for an associated instance. You can associate an instance with one or more security groups and edit the security group rules.

Interconnectivity between VPCs can be established by using {{site.data.keyword.tg_full_notm}}. When a VPC is attached to a Transit Gateway as a connection, the VPC prefixes (not the subnets) are advertised to the Transit Gateway instance. The connectivity to on-premises networks can be established through {{site.data.keyword.dl_full_notm}}, where you can bring your WAN or MPLS connection to one of {{site.data.keyword.cloud_notm}} PoPs and connect to your resources.

For more information, see [About networking](/docs/vpc?topic=vpc-about-networking-for-vpc).

## Related links
{: #vpc-ryo-vpc-links}

* [Getting started with {{site.data.keyword.vpc_short}} (VPC)](/docs/vpc?topic=vpc-getting-started)
* [Planning for Bare Metal Servers on VPC](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [Architecture overview of roll-your-own VMware solution on VPC](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [Getting started with {{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [Getting started with {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
