---

copyright:

  years:  2020, 2024

lastupdated: "2024-03-26"

keywords: migrating to VMware as a Service

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Technical considerations about migrating from VMware Shared to {{site.data.keyword.vmware-service_short}}
{: #shared-vmwaas-migration}

{{site.data.content.shared-deprecated-note}}

{{site.data.keyword.vmware-service_full}} can be considered as an evolution to {{site.data.keyword.cloud_notm}} for VMware Shared. {{site.data.keyword.vmware-service_notm}} provides the same VMware Cloud Director™ platform, but with two flavors, either a dedicated or shared managed service. {{site.data.keyword.IBM}} performs the configuration, hosting, operations, and lifecycle management of the VMware® by Broadcom software in the same way, so you can quickly deploy your VMware-based cloud computing environments. Compute resources are available as either dedicated or multitenant hosts that use {{site.data.keyword.cloud_notm}} bare metal servers. Dedicated single-tenant VMware sites provide extra isolation and support multiple host configuration options to support flexible workload requirements.

{{site.data.keyword.vmware-service_short}} multitenant instances are deployed to all supported regions by {{site.data.keyword.IBM_notm}}. You can create your virtual data centers (VDCs) on the {{site.data.keyword.IBM_notm}} managed infrastructure. {{site.data.keyword.vmware-service_short}} single-tenant instances are provisioned and managed by your organization.

With the new versions for underlying VMware Cloud Director™ platform and its software defined networking, and due to changes to the add-on service options, you might need to change some components of the design. The following information describes the most significant changes to the platform and lists the design and implementation considerations for migrated virtual data centers. Review this information before migrating {{site.data.keyword.vmwaresolutions_full}} Shared virtual data centers to {{site.data.keyword.vmware-service_short}}.

## Network edge type
{: #shared-vmwaas-migration-edge-type}

VDCs connect to the public and IBM private networks through edges. Edges can also be used to connect multiple VDC networks together. You can create your VDC with or without a network edge. Network edge types include: Efficiency, Performance - M, Performance - L, and Performance - XL.

Performance edges are dedicated to a single virtual data center (VDC) and provide the most consistent performance. The larger size Performance edges offer support for more network service usage and throughput. The Efficiency edges can be shared by up to 64 separate virtual data centers and can be cost effective in large deployments with some sacrifice to network performance consistency. 

| Edge type | Details |
|:--------- |:------- |
| Efficiency | These edges allocate networking resources that can be used by up to 100 VDCs before another efficiency edge needs to be created. The first time an efficiency edge is selected new CPU, RAM, and storage resources are required. CPU and RAM are used from the single tenant site. New edge storage is allocated at a cost. Subsequent VDCs up to 100 can use this edge at no extra cost. This option is suitable for saving resources and costs with independent networking control per VDC. |
| Performance - M | This option is suitable when only L2 through L4 features such as NAT, routing, L4 firewall, L4 load balancer are required and the total throughput requirement is less than 2 Gbps. |
| Performance - L | This option is suitable when only L2 through L4 features such as NAT, routing, L4 firewall, L4 load balancer are required and the total throughput is in the range 2 - 10 Gbps. |
| Performance - XL | This option is suitable when the total throughput required is multiple Gbps for L7 and VPN. |
{: caption="Table 1. Network edge descriptions" caption-side="bottom"}

## Public network connectivity
{: #shared-vmwaas-migration-network-public}

When you deploy a new {{site.data.keyword.vmware-service_short}} VDC data center, you get new public IP addresses. Existing public IP addresses of the {{site.data.keyword.vmwaresolutions_full}} Shared VDC cannot be moved to the new {{site.data.keyword.vmware-service_short}} VDC.

* If you are accessing your VDC workloads by using NAT rules or other routing arrangements, you must reconfigure your DNS rules and other possible remote firewalls and their rules.
* If you are accessing your VDC workloads by using IPsec tunnels, you must reconfigure your VPN tunnels to the new public IP addresses.

## Private network connectivity
{: #shared-vmwaas-migration-network-private}

{{site.data.keyword.vmware-service_short}} multitenant and single-tenant virtual data centers (VDCs) can use {{site.data.keyword.tg_full}} to securely interconnect with other {{site.data.keyword.vmware-service_short}} virtual data centers, {{site.data.keyword.cloud_notm}} Classic and Virtual Private Cloud (VPC) IaaS infrastructures, and your on-premises locations by using {{site.data.keyword.tg_short}} attached Direct Link connections.

* {{site.data.keyword.tg_short}} uses Generic Routing Encapsulation (GRE) tunnels to connect your single-tenant and multitenant virtual data centers (VDCs) to a {{site.data.keyword.tg_short}} resource.
* Six unbound GRE tunnels and dynamic routing with BGP are used to establish redundant connectivity to each zone.
* This way, your private connectivity options are enhanced in the new virtual data centers.

To use this functionality, first use the VMware Solutions console to configure your GRE tunnel connections and add a connection group of six unbound GRE tunnels to your VDC. Then, you can add each GRE tunnel to the {{site.data.keyword.tg_short}} to attach the tunnels that belong to the connection group. For more information, see [Using {{site.data.keyword.tg_short}} to interconnect {{site.data.keyword.vmware-service_short}} with {{site.data.keyword.cloud_notm}} services](/docs/vmware-service?topic=vmware-service-tgw-adding-connections).

## NSX version change
{: #shared-vmwaas-migration-nsx-version}

{{site.data.keyword.vmware-service_short}} virtual data centers networking uses the most recent version of VMware NSX (also known as NSX-T), while VMware Shared is based on NSX-V. This change enhances the networking capabilities of your virtual data centers.

If you are using automation (such as Terraform), the API and Terraform resources are different. For more information, see [vCloud Director API](https://developer.vmware.com/apis/553/vcloud-director/){: external} and [Terraform VMware Cloud Director Provider](https://registry.terraform.io/providers/vmware/vcd/latest/docs){: external} documentation.
{: note}

## VDC gateways
{: #shared-vmwaas-migration-network-gateways}

With the NSX change, the gateway functions are split between two components: provider gateway and edge gateway. You can view the provider gateways that are dedicated to your VDC; however, no configuration options are available for these gateways. The gateways provide the connected edge gateway the logical and physical connection to the private and public networks.

The provider gateway supports BGP and the edge gateway supports static routing. No support is available for other routing protocols.

## VDC networks
{: #shared-vmwaas-migration-network-internal}

The VDC network concepts are the same, with no conceptual changes to routed or isolated VDC networks. IP address allocations that use manual, static IP pools, and DHCP configurations remain logically the same.

## Firewall rules
{: #shared-vmwaas-migration-network-firewall}

NSX firewall rules must be migrated to the new model. To allow or deny traffic from a specific source or destination, you must use firewall groups. Using IP addresses directly in the rules is not possible.

For more information, see:
* [Add an IP Set to an NSX Edge Gateway](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/VMware-Cloud-Director-Tenant-Portal-Guide/GUID-6A0E39F5-123C-4429-ACAC-31025A364411.html){: external}
* [Create a Static Security Group in a Data Center Group with an NSX Network Provider Type](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/VMware-Cloud-Director-Tenant-Portal-Guide/GUID-7EE6D6DE-5C09-4B88-AD13-0ACD6E7126DD.html){: external}.

## Virtual private networks
{: #shared-vmwaas-migration-network-vpn}

IPSec VPN offers site-to-site connectivity between an edge gateway and remote sites that also use NSX or that have either third-party hardware routers or VPN gateways that support IPsec.

Policy-based IPSec VPN requires a VPN policy to be applied to packets to determine which traffic is to be protected by IPsec before the traffic is passed through a VPN tunnel. This type of VPN is considered static because when a local network topology and configuration change, the VPN policy settings must also be updated to accommodate the changes.

{{site.data.keyword.vmware-service_short}} virtual data centers support only policy-based IPsec VPNs. Route-based IPsec VPNs are not supported. For more information, see [IPsec Policy-Based VPN for NSX Edge Gateways](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/VMware-Cloud-Director-Tenant-Portal-Guide/GUID-019E8BF7-8669-4A15-B1AE-CDFD04EA77CB.html){: external}.

## NAT rules
{: #shared-vmwaas-migration-network-nat}

To change the source IP address from a private to a public IP address, you create a source NAT (SNAT) rule. To change the destination IP address from a public to a private IP address, you create a destination NAT (DNAT) rule.

The following information lists the possible NAT options in the {{site.data.keyword.vmware-service_short}} Edge Gateway:

* When you configure a `SNAT` or a `DNAT` rule on an edge gateway in the VMware Cloud Director environment, you always configure the rule from the perspective of your organization VDC.
* An `SNAT` rule translates the source IP address of packets that are sent from an organization VDC network out to an external network or to another organization VDC network.
* A `NO SNAT` rule prevents the translation of the internal IP address of packets that are sent from an organization VDC out to an external network or to another organization VDC network.
* A `DNAT` rule translates the IP address and optionally, the port of packets that are received by an organization VDC network that are coming from an external network or from another organization VDC network.
* A `NO DNAT` rule prevents the translation of the external IP address of packets that are received by an organization VDC from an external network or from another organization VDC network.

For more information, see [Add an SNAT or a DNAT Rule to an NSX Edge Gateway](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/VMware-Cloud-Director-Tenant-Portal-Guide/GUID-9E43E3DC-C028-47B3-B7CA-59F0ED40E0A6.html){: external}.

When you access the {{site.data.keyword.cloud_notm}} service networks or you are using private network connectivity with {{site.data.keyword.tg_full}}, consider the following information:

* Create SNAT rules for the {{site.data.keyword.cloud_notm}} service networks (`161.26.0.0/16` and `166.8.0.0/14`) by using any public IP address of your VDC. The access uses private network despite the usage of public source IP.
* When you are using private network connectivity with {{site.data.keyword.tg_full}}, you might need to create `NO SNAT` rules for the private networks reachable though the private {{site.data.keyword.tg_short}} connection.

## Data center groups
{: #shared-vmwaas-migration-network-dc-groups}

Data center group networks that are backed by NSX provide level-2 network sharing, single active egress point configuration, and distributed firewall (DFW) rules that are applied across a data center group. A data center group acts as a cross-VDC router that provides centralized networking administration, egress point configuration, and east-west traffic between all networks within the group.

* After you create a data center group with an NSX network provider type, you can add data centers to the group, remove them, and edit the group settings.
* A data center group can include up to 16 virtual data centers.
* At least one virtual data centers in {{site.data.keyword.vmware-service_short}} must have edge networking enabled. You can choose between efficiency and performance edges. For more information, see [Network edge type](/docs/vmware-service?topic=vmware-service-tenant-plan-deploy#tenant-plan-deploy-edge).
* You can optionally order virtual data centers in {{site.data.keyword.vmware-service_short}} without edge networking. For more information, see [Ordering virtual data centers for {{site.data.keyword.vmware-service_short}} single-tenant](/docs/vmware-service?topic=vmware-service-vdc-adding).
* VDCs that you remove from the data center group must have no workloads attached to any of the networks that participate in the data center group.

## Migration tools
{: #shared-vmwaas-migration-tooling-migration}

You can use VMware Cloud Director Availability (VCDA) as a simple, secure, and cost-effective virtual machine migration from your {{site.data.keyword.vmwaresolutions_full}} Shared virtual data centers to new virtual data centers in your {{site.data.keyword.vmware-service_short}} Site.

The VCDA service is included by default in all multitenant virtual data centers (VDCs) and optionally included in your single-tenant {{site.data.keyword.vmware-service_short}} Cloud Director site order at no charge.

For more information, see [VMware Cloud Director Availability for {{site.data.keyword.vmware-service_short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-tenant-vcda).

## Protecting VMs in {{site.data.keyword.vmware-service_short}}
{: #shared-vmwaas-migration-tooling-protection}

The Veeam® Backup and Replication service are available and ready to use in your {{site.data.keyword.vmware-service_short}} instance. This service seamlessly integrates as a managed solution to help your enterprise achieve high availability and provides recovery points for your applications and data. By using this service, you control the backup of all virtual machines (VMs) for your infrastructure directly from the Veeam console.

* Existing backups are not moved from {{site.data.keyword.vmwaresolutions_full}} Shared virtual data centers.
* Re-configure backups in the new {{site.data.keyword.vmware-service_short}} VDC post migration.
* Veeam Cloud Connect Replication is not available in {{site.data.keyword.vmware-service_short}}.
* Zerto service is not available in {{site.data.keyword.vmware-service_short}}.

For more information, see [Managing Veeam for {{site.data.keyword.vmware-service_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-tenant-veeam).

## Related links
{: #shared-vmwaas-migration-related}

* [Planning the {{site.data.keyword.vmware-service_short}} deployment](/docs/vmware-service?topic=vmware-service-tenant-plan-deploy)
* [Managing Organization Virtual Data Center Networks](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/VMware-Cloud-Director-Tenant-Portal-Guide/GUID-B208CDD2-5D46-4841-8F3C-BED9E4F27F07.html){: external}
* [Using {{site.data.keyword.tg_short}} to interconnect {{site.data.keyword.vmware-service_short}} with {{site.data.keyword.cloud_notm}} services](/docs/vmware-service?topic=vmware-service-tgw-adding-connections)
* [Using VMware Cloud Director Availability with {{site.data.keyword.vmware-service_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-tenant-vcda).
* [VMware Cloud Director](https://www.vmware.com/products/cloud-director.html){: external}
* [vCloud Director API](https://developer.vmware.com/apis/553/vcloud-director/){: external}
* [Terraform VMware Cloud Director Provider](https://registry.terraform.io/providers/vmware/vcd/latest/docs){: external}
* [Network Edge Size](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/installation/GUID-22F87CA8-01A9-4F2E-B7DB-9350CA60EA4E.html){: external}
