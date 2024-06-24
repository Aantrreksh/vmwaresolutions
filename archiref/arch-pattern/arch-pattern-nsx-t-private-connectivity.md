---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture patterns for vCenter Server deployment with private connectivity options
{: #arch-pattern-nsx-t-private-connectivity}

When you deploy a [{{site.data.keyword.vcf-auto-short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) instance in your {{site.data.keyword.cloud}} classic infrastructure, the deployment consists of a number of network constructs and VMware® management components.

These architecture patterns give an overview for a few private connectivity options for {{site.data.keyword.vcf-auto}} deployments.

## Private connectivity deployed by automation
{: #arch-pattern-nsx-t-private-connectivity-depl-auto}

When you deploy a {{site.data.keyword.vcf-auto-short}} instance in your {{site.data.keyword.cloud_notm}} classic infrastructure, you obtain the default private network topology as presented in the following diagram.

![Access to {{site.data.keyword.cloud_notm}} Private network](../../images/arch-pattern-nsx-t-private-access.svg "Access to {{site.data.keyword.cloud_notm}} Private network"){: caption="Figure 1. Access to {{site.data.keyword.cloud_notm}} private network" caption-side="bottom"}

The following list summarizes the private connectivity pattern.

1. The automation deploys an NSX Tier 0 (T0) Gateway in the NSX workload edge cluster. The T0 gateway provides connectivity to {{site.data.keyword.cloud_notm}} private network. 
2. The deployed T0 gateway has a route to {{site.data.keyword.cloud_notm}} private network `10.0.0.0/8` and {{site.data.keyword.cloud_notm}} Services networks `166.8.0.0/14` and `161.26.0.0/16` with BCR as a next-hop.
3. The automation deploys an example NSX overlay topology with a Tier 1 (T1) Gateway and a few example segments attached both to the T1 and T0 Gateways. You might customize the topology based on your needs.
4. {{site.data.keyword.cloud_notm}} Services can be reached through {{site.data.keyword.cloud_notm}} private network by using Cloud Services Endpoints when it uses {{site.data.keyword.cloud_notm}} private network addresses.
5. When you use BYOIP on NSX overlay networks, you must use SNAT at T0 or T1. If you use SNAT at T1, you can advertise the NAT IP addresses from T1 to T0, where proxy ARP is used.
6. You can create DNAT rules on T0 Gateway to access your workloads from {{site.data.keyword.cloud_notm}} private networks.
7. You can use IP addresses from {{site.data.keyword.cloud_notm}} private portable subnet that is deployed for NSX Edge uplinks for the NAT. Alternatively, you can order [{{site.data.keyword.cloud_notm}} Private static subnets](/docs/subnets?topic=subnets-getting-started) that are routed toward your T0's private HA VIP to be used for NAT-ing or on segments.

## Ingress private connectivity
{: #arch-pattern-nsx-t-private-connectivity-ingress}

Private ingress connectivity to NSX overlay is enabled through NAT or though using overlay tunnels. You can use IP addresses from the private portable subnet that is provisioned for T0 private uplinks for these use cases.

![Private ingress access to {{site.data.keyword.cloud_notm}} NSX overlay](../../images/arch-pattern-nsx-t-private-access-ingress.svg "Private ingress access to {{site.data.keyword.cloud_notm}} NSX overlay"){: caption="Figure 2. Private ingress access to {{site.data.keyword.cloud_notm}} NSX overlay" caption-side="bottom"}

The following steps summarize this architecture pattern deployment.

1. The automation deploys an NSX T0 Gateway in the NSX workload edge cluster. The T0 gateway provides connectivity to the {{site.data.keyword.cloud_notm}} private network.
2. The automation deploys an example NSX overlay topology with a T1 Gateway and a few example segments attached both to the T1 and T0 Gateways. You can customize the topology based on your needs.
3. Workload T0 Gateway has a private uplink that is attached to the {{site.data.keyword.cloud_notm}} private VLAN with three IP addresses, two for uplinks in edge 1 and edge 2 and one for HA VIP. Interfaces are configured with the network mask of the private portable subnet.

   The NSX T0 uplink does not support secondary IP addresses.
   {: note}

4. You can configure DNAT rules on T0 or T1 for ingress access, or SNAT for egress access from NSX overlay by using the IP addresses from the private portable subnet configured in the T0 uplinks. You can also configure load balancer VIPs, IPsec, or L2 VPN. Each of these are advertised as `/32` host IP addresses. You need to enable route advertisements on T1 Gateways so that T0 is aware of these IP addresses, and they must appear on T0s routing table.
5. T0 Gateway uses proxy ARP on the uplink subnet for each `/32` IP address that is aware of (that is, which exists in its routing table). BCR can route ingress traffic only to these IP addresses. To check the routing table of T0, use the NSX GUI or log in to the NSX edge node and its T0 Service Router (SR) VRF. With [{{site.data.keyword.cloud_notm}} Private static subnets](/docs/subnets?topic=subnets-getting-started), the whole subnet is routed to the overlay.

## Ingress private connectivity with gateway cluster
{: #arch-pattern-nsx-t-private-connectivity-edge-gateway-cluster}

Private ingress connectivity to NSX overlay is enabled through NAT or though using overlay tunnels. You can use IP addresses from the private portable subnet that is provisioned for T0 private uplinks for these use cases. With Juniper vSRX running on the [gateway cluster](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters#vc_orderinginstance-addl-clusters-gate), you can alternatively route portable IP addresses to the T0 HA VIP and use the portable IP subnets in the overlay.

![Private ingress access to {{site.data.keyword.cloud_notm}} NSX overlay with gateway cluster](../../images/arch-pattern-nsx-t-private-access-ingress-vsrx.svg "Private ingress access to {{site.data.keyword.cloud_notm}} NSX overlay with gateway cluster"){: caption="Figure 3. Private ingress access to {{site.data.keyword.cloud_notm}} NSX overlay with gateway cluster" caption-side="bottom"}

The following list summarizes this architecture pattern deployment.

1. The automation deploys an NSX T0 Gateway in the NSX workload edge cluster. The T0 gateway provides connectivity to {{site.data.keyword.cloud_notm}} private network. With gateway cluster, this uplink VLAN can be routed through the firewall, for example Juniper vSRX.
2. The automation deploys an example NSX overlay topology with a T1 Gateway and a few example segments attached both to the T1 and T0 Gateways. You can customize the topology based on your needs.
3. Workload T0 Gateway has a private uplink that is attached to the {{site.data.keyword.cloud_notm}} private VLAN with three IP addresses, two for uplinks in edge 1 and edge 2 and one for HA VIP. Interfaces are configured with the network mask of the private portable subnet.

   The NSX T0 uplink does not support secondary IP addresses.
   {: note}

4. When you order a private portable subnet to a private VLAN that is routed by vSRX, BCR routes this subnet to the vSRX though its transit VLAN.
5. Instead of configuring the subnet as a secondary IP address in the interface in vSRX, you can route this subnet to the NSX T0 HA VIP.
6. You can then use this subnet in segments or specific IP addresses from it for NAT rules, load balancer VIPs, or VPN endpoints.

## Private connectivity through direct link
{: #arch-pattern-nsx-t-private-connectivity-direct-link}

Private connectivity for vCenter Server can use [{{site.data.keyword.dl_full_notm}}](/docs/dl?topic=dl-dl-about) and tunneling. This solution is applicable for [NSX-based {{site.data.keyword.vcf-auto-short}} instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview), which is provisioned in {{site.data.keyword.cloud_notm}} classic infrastructure. You can use Gateway Appliance or vCenter Server gateway cluster with Juniper vSRX or other device as part of the solution as an option.

The tunnel is established between NSX T0 and a customer router routable through {{site.data.keyword.dl_short}}. If vSRX or other third-party device is used in a gateway cluster, you can terminate the tunnel in these devices as well. In this case, NSX T0 advertises routes in the vSRX (or other third-party device) through BGP or Static Routes.

For more information about this architecture pattern, see [Architecture pattern for using IPsec over {{site.data.keyword.dl_short}} with a vCenter Server with NSX instance](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-nsx-t-direct-link-ipsec).

## Private connectivity through transit gateway
{: #arch-pattern-nsx-t-private-connectivity-transit-gateway}

Hybrid cloud connectivity can be established by using [{{site.data.keyword.tg_full}}](/docs/transit-gateway?topic=transit-gateway-about). This solution is applicable for NSX-based {{site.data.keyword.vcf-auto-short}} instance, which is provisioned in {{site.data.keyword.cloud_notm}} classic infrastructure. This pattern requires a [gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-about#firewall) or [gateway cluster](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters) with Juniper vSRX or other third-party device, which supports GRE. In this solution, a GRE tunnel is established between this device and Transit GW Router in a specific Zone. NSX T0 advertises routes through vSRX (or other device) to Transit Gateway.

For more information about this architecture pattern, see [Architecture pattern for using Transit Gateway with a vCenter Server with NSX instance](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-nsx-t-transit-gw).

## Related links
{: #arch-pattern-nsx-t-private-connectivity-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [VMware NSX design](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design)
