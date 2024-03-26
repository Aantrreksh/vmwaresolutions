---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware NSX-T logical routers on VPC deployments
{: #vpc-ryo-nsx-t-logical-routers}

As defined earlier, a single NSX-T™ gateway cluster with two virtual edge nodes is used in this architecture. It is required to create a Tier-0 (T0) logical router or a Tier-1 (T1) router to provide stateful services such as NAT or load balancer.

When you deploy a VMware NSX Edge™, you can consider it as an empty container. The edge nodes do not change until you create logical routers. The NSX Edge Node provides the compute capacity that is backing the T0 and T1 logical routers. Each logical router contains a services router (SR) and a distributed router (DR). A DR is essentially a router with logical interfaces that are connected to multiple subnets (NSX-T segments). It runs as a kernel module and is distributed in ESXi hypervisors across all transport nodes, including edge nodes.

A services router is instantiated on a gateway cluster as a virtual routing and forwarding (VRF) when a service that cannot be distributed is enabled, such as:

* Physical infrastructure connectivity
* NAT
* DHCP server
* VPN
* Gateway Firewall

In this architecture, the single gateway cluster hosts both T0 and T1s as shown in the following diagram. You can deploy multiple gateway clusters to scale the solution up, if needed.

![VPC gateway cluster](../../images/vpc-ryo-diagrams-nsx-t-edges.svg "VPC gateway cluster"){: caption="Figure 1. VPC gateway cluster" caption-side="bottom"}

For more information about NSX designs, see the [NSX Reference Design Guide](https://nsx.techzone.vmware.com/resource/nsx-reference-design-guide){: external}.

## Tier-0 logical router
{: #vpc-ryo-nsx-t-logical-routers-edge-tier-0}

An NSX-T Tier-0 logical gateway provides a gateway service between the logical NSX-T overlay segments and VPC subnets, for example, for north-south traffic. In this architecture, a highly available T0 gateway is deployed in the NSX-T gateway cluster. Because of a VMware® NSX-T limitation, this gateway cluster can host only a single T0 Logical Router, which runs in Active-Standby mode. Active-Standby mode is required, for example, to have High Availability VIPs in the T0.

![T0 Logical Router in VPC gateway cluster](../../images/vpc-ryo-diagrams-nsx-t-edges-routing.svg "T0 Logical Router in VPC gateway cluster"){: caption="Figure 2. T0 Logical Router in VPC gateway cluster" caption-side="bottom"}

Currently, Active-Active mode with T0 is not supported in {{site.data.keyword.vpc_full}}.
{: note}

When T0 is run in Active-Standby mode, both participating Edge Transport Node has their own uplink. High availability between these uplinks uses a High Availability VIP.
{: note}

The T0 is configured with **two uplink types**: two uplinks for **private** use and two uplinks for **public** use. HA VIPs are assigned to both public and private uplinks for high availability. For public and private uplinks, two VPC subnets are needed. These subnets are provisioned from the Zone prefix, and they can both use RFC 1918 private addresses, including the public subnet.

| Subnet name | System traffic type | Subnet sizing guidance |
|:----------- |:------------------- |:---------------------- |
| vpc-t0-public-uplink-subnet | T0 public uplink subnet | `/29` or larger |
| vpc-t0-private-uplink-subnet | T0 private uplink subnet | `/29` or larger |
{: caption="Table 1. VPC subnets for NSX-T T0 uplinks" caption-side="bottom"}

If you do not need inbound traffic from the internet, you do not need public uplink subnet.
{: note}

The following VLAN interfaces are required in VPC for each T0 uplink. It is important to separate the public and private uplinks as specified previously. VLAN interfaces with `Allow IP spoofing` and `Enable Infrastructure NAT` set to `false` allow public floating IP addresses to traverse non-NATted to the public uplinks of the T0 logical router. VLAN interfaces with `Allow IP spoofing` and `Enable Infrastructure NAT` set to `true` allow VMware workloads on NSX-T overlay with private IP addresses to be routed to {{site.data.keyword.vpc_short}}. These functionalities cannot be combined into one.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | Allow IP spoofing | Enable infra NAT | NSX-T interface | Segment name |
|:-------------- |:-------------- |:------- |:------ |:----------- |:----------------- |:---------------- |:----- | :----------------------- |
| vlan-nic-t0-pub-uplink-1 | vlan | 700 | vpc-t0-public-uplink-subnet | true | false | false | T0 Public Uplink * Edge 1 | vpc-zone-t0-public-*vlanid* |
| vlan-nic-t0-pub-uplink-2 | vlan | 700 | vpc-t0-public-uplink-subnet | true | false | false | T0 Public Uplink * Edge 2 | vpc-zone-t0-public-*vlanid* |
| vlan-nic-t0-pub-uplink-vip | vlan | 700 | vpc-t0-public-uplink-subnet | true | false | false | T0 Public Uplink VIP | vpc-zone-t0-public-*vlanid* |
| vlan-nic-t0-priv-uplink-1 | vlan | 710 | vpc-t0-private-uplink-subnet | true | true | true | T0 Private Uplink * Edge 1 | vpc-zone-t0-private-*vlanid* |
| vlan-nic-t0-priv-uplink-2 | vlan | 710 | vpc-t0-private-uplink-subnet | true | true | true | T0 Private Uplink * Edge 2 | vpc-zone-t0-private-*vlanid* |
| vlan-nic-t0-priv-uplink-vip | vlan | 710 | vpc-t0-private-uplink-subnet | true | true | true | T0 Private Uplink VIP | vpc-zone-t0-private-*vlanid* |
{: caption="Table 2. VLAN interfaces for T0 uplinks" caption-side="bottom"}

If you do not need inbound traffic from internet, you might not need either public uplinks on T0 or the public VLAN interfaces for the bare metal server.
{: note}

Routing in T0 needs to take the previous note into consideration. If you have public uplinks, your default route `0.0.0.0/0` must be routed through the public uplinks and any private routes must be routed through private uplinks. Configure your static routes to the gateway of your VPC subnet.
{: note}

You can provision only one pair of uplinks from the T0 Logical Router from the same gateway cluster in the same VPC subnet. This limitation also includes T0 VRFs. Each T0 uplink pair must have its own VPC subnet.
{: note}

## Tier-1 logical router
{: #vpc-ryo-nsx-t-logical-routers-edge-tier-1}

An NSX-T T1 logical router has downlink connections to the attached NSX-T segments and uplink connections to a single T0 logical router. The NSX Edge Nodes provide the compute capacity for the T1 logical routers. Each T1 logical router contains a service router (SR) and a distributed router (DR), same as with T0s. A DR runs as a kernel module distributed in hypervisors and SR is instantiated as a VRF on a gateway cluster when a service is enabled and cannot be distributed.

In this design, one or more T1 logical routers can be created for the needs of your chosen topologies.

You can deploy multiple T1s in the same gateway cluster, but that gateway cluster can have only one T0.
{: note}

## VPC routing with Tier-0 logical routers
{: #vpc-ryo-nsx-t-logical-routers-edge-tier-0-routing}

When designing logical network topologies in {{site.data.keyword.vpc_short}} hosted NSX-T, it is important to decide how to route the traffic of NSX-T segment attached workloads between NSX-T, {{site.data.keyword.vpc_short}}, and public internet.

The following diagram presents an overview of the routing between NSX-T Logical Routers and VPC.

![VPC routing with NSX-T Logical Routers](../../images/vpc-ryo-diagrams-nsx-t-vpc-routing.svg "VPC routing with NSX-T Logical Routers"){: caption="Figure 3. VPC routing with NSX-T Logical Routers" caption-side="bottom"}

If your design does not need direct inbound public access, you can customize this architecture. Various customization aspects of the connectivity architecture are discussed in the following topics.

### Routing between Tier-0 and Tier-1 logical routers
{: #vpc-ryo-nsx-t-logical-routers-edge-tier-0-routing-t1}

The first architectural decision to be made for your solution is routing between T1 and T0. You can configure various route advertisements and static routes on a T1 logical router.

In this design, the workloads are connected to NSX-T overlay segments behind T1, and when T1 is connected to its parent T0, it has a default route that points to the T0. By default, T0 does not know about the segments that are attached to T1, and this is where route advertisement is needed.

If you want to route natively with {{site.data.keyword.vpc_short}} subnets and other connected service without using NAT in T1, enable route advertisement of "All Connected Segments & Service Ports" in the specific T1. You must not configure a routing protocol or static routes between T1 and T0 logical routers. After you enable the route advertisement, NSX-T creates routes automatically. With this approach, you have all connected segments on your T1 routed to T0, and then you can decide how to proceed with the public and private traffic in T0.

### Public traffic between Tier-0 and VPC
{: #vpc-ryo-nsx-t-logical-routers-edge-tier-0-routing-public}

The second architectural decision to be made for your solution is public traffic. If your workloads need direct public traffic and have inbound public traffic without using any network translation, you must provision the public uplink subnet and public T0 uplink VLAN interfaces. Also, you must configure your T0 with public uplinks as described in the topic [Tier-0 logical router](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-nsx-t-logical-routers#vpc-ryo-nsx-t-logical-routers-edge-tier-0) previously. As the NSX-T T0 uses Active-Standby, the HA VIP provides high availability for the routing of public traffic between VPC, T0 and your NSX-T workloads. When you need public IPs, you can order floating IP address to the HA VIP VLAN interface. Each floating IP is a single `/32` IP address, and you can order as many as you need within VPC [Quotas](/docs/vpc?topic=vpc-quotas).

| Interface name | Interface type | VLAN ID | Subnet | Allow float | Allow IP spoofing | Enable infra NAT | NSX-T interface | Segment name |
|:-------------- |:-------------- |:------- |:------ |:----------- |:----------------- |:---------------- | :--- | :----------------------- |
| vlan-nic-t0-pub-uplink-vip | vlan | 700 | vpc-t0-public-uplink-subnet | true | false | false | T0 Public Uplink VIP | vpc-zone-t0-public-*vlanid* |
{: caption="Table 3. Public uplink HA VIP to be used for Public floating IPs" caption-side="bottom"}

VLAN interfaces with `Allow IP spoofing` and `Enable Infrastructure NAT` set to `false` allow public floating IP address to traverse non-NATted to the public uplinks of the T0 logical router. For high availability with NSX-T T0 logical router, HA VIPs can be used. When you order floating IP address for public uplinks, always use the VIP VLAN interface instead of the uplinks that are reserved for the actual Edge Nodes.
{: note}

You can currently use the public IPs, for example:

* To perform destination NAT done in either Tier-0 or Tier-1 Logical Routers for **inbound** public traffic to NSX-T overlay.
* To perform source NAT done in either Tier-0 or Tier-1 Logical Routers for **outbound** public traffic from NSX-T overlay.
* To establish VPNs in either Tier-0 or Tier-1.

For more information, see the [Network Services provided by Tier-0 and Tier-1 Logical Routers](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-nsx-t-logical-routers#vpc-ryo-nsx-t-logical-routers-edge-gateway).

For public IPs, you can currently use one or more `/32` IP address, but you cannot have subnets, such as `/29` or `/26`.
{: note}

In this case, your default route `0.0.0.0/0` in NSX-T T0 Logical Router must be pointed to the default gateway of the `vpc-t0-public-uplink-subnet`.

| Route description | Device | CIDR | Next-hop |
| ----------------------------| -------------------- | ------------------ | ---------------------------------------------- |
| Default route | T0 Logical Router | 0.0.0.0/0 | Default GW of `vpc-t0-public-uplink-subnet` |
{: caption="Table 4. Default route in T0 Logical Router with Public Uplinks" caption-side="bottom"}

If you do not need **inbound** traffic from internet, you do not need public uplinks on T0 nor the public VLAN interfaces. Alternatively, you can use Public Gateway in {{site.data.keyword.vpc_short}}, which provides you the outbound internet access from NSX-T overlay segments, and use the T0s private uplinks for this traffic. In this case, your default route `0.0.0.0/0` in NSX-T T0 Logical Router must be pointed to the default gateway of the `vpc-t0-private-uplink-subnet`.

| Route description | Device | CIDR | Next-hop |
| ------------------| -------------------- | ------------------ | ---------------------------------------------- |
| Default route | T0 Logical Router | 0.0.0.0/0 | Default GW of |`vpc-t0-private-uplink-subnet` |
{: caption="Table 5. Default route in T0 Logical Router with Private Uplinks Only" caption-side="bottom"}

### Private traffic between Tier-0 and VPC
{: #vpc-ryo-nsx-t-logical-routers-edge-tier-0-routing-private}

The third architectural decision to be made for your solution is private traffic. Routing between T1 and T0 was discussed previously, and this approach assumes that your T0 knows how to reach the IP subnets/prefixes configured for the segments that are attached to either T1 and T0.

If you have both Public and Private Uplinks, the first step is to create a route in NSX-T T0 pointing to the Private networks you must connect to from the VMware workloads that are attached to NSX-T overlay segments. These networks must be reachable through the VPC, or DL/TGW to which the VPC is attached to. The following table shows an example, when private prefix `172.16.0.0/16` is used elsewhere and this prefix is known by VPC, either directly or through attached Direct Link (DL) or Transit Gateway (TGW).

| Route description | Device | CIDR | Next-hop |
| ------------------| -------------------- | ------------------ |---------------------------------------------- |
| Private networks | T0 Logical Router | 172.16.0.0/16 | Default GW of `vpc-t0-private-uplink-subnet` |
{: caption="Table 6. Private routes in T0 Logical Router with Public Uplinks" caption-side="bottom"}

If you use only private route, then your default route `0.0.0.0/0` in NSX-T T0 Logical Router routes all traffic to the VPC.
{: note}

You must define inbound traffic from VPC. Then, you must create a VPC route in the Zone to the IP subnet or prefix that you are using in the NSX-T overlay. As the NSX-T T0 uses Active-Standby, the HA VIP provides high availability for the routing of private traffic between VPC and your NSX-T overlay. Therefore, the next-hop for the VPC route must be the HA VIP, as specified on the following table.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | Allow IP spoofing | Enable infra NAT | NSX-T interface | Segment name |
| ---------------------------- | ---------------- | --------- | ------------------------------ | -------------- | ------------------- | ------------------- | ----------------------------|------------------------------ |
| vlan-nic-t0-priv-uplink-vip | vlan | 710 | vpc-t0-private-uplink-subnet | true | true | true | T0 Private Uplink VIP | vpc-zone-t0-private-*vlanid* |
{: caption="Table 7. VLAN interfaces for T0 uplinks" caption-side="bottom"}

VLAN interfaces with `Allow IP spoofing` and `Enable Infrastructure NAT` set to `true` allow VMware workloads on NSX-T overlay with private IP addresses to be routed to {{site.data.keyword.vpc_short}}. To enable it, a VPC route is created with IP address of private uplink HA VIP/vlan-nic-t0-priv-uplink-vip as the next-hop configured in the {{site.data.keyword.vpc_short}} Zone.
{: note}

When planning routing, try to summarize the NSX-T overlay subnets/prefixes to keep the number required routes minimal. When creating a route pointing to the NSX-T overlay, the following table provides an example for the required parameters for an NSX-T overlay subnets `192.168.4.0/24`, `192.168.5.0/24`, `192.168.6.0/24`, and `192.168.7.0/24` attached to T1. Further summarized to a prefix `192.168.4.0/22` and using NSX-T HA VIP `192.168.0.10` in Zone `us-south-2` as the next-hop. For more information about VPC routes, see [VPC routing tables and routes](/docs/vpc?topic=vpc-about-custom-routes).

| Route description | Zone | Traffic type | CIDR | Action | Type | Next-hop |
| ----------------------------| ----------------| ----------------| ------------------| -----------| --------| ------------------- |
| NSX-T overlay networks | us-south-2 | Egress | 192.168.4.0/22 | Deliver | IP | 192.168.0.10 |
{: caption="Table 8. VPC routes" caption-side="bottom"}

VPC routes are Zone specific.
{: note}

Creating a VPC route enables traffic within the Zone, and within the VPC depending on how the VPC route is created. If you use any of the interconnectivity options, such as Direct Link or Transit Gateway, and you need connectivity from another VPC attached to a TGW, in addition to the VPC route, you can create a VPC prefix matching the NSX-T overlay subnet or prefix. This action allows both DL and TGW to advertise your NSX-T overlay subnet or prefix to the attached TGW connections or DL. By using the previous example, you can create a VPC prefix matching the route `192.168.4.0/22`, which enables TGW to advertise this prefix to the other attached VPCs, or Classic. For more information about VPC prefixes and about creating them, see [Bring your own subnet](/docs/vpc?topic=vpc-configuring-address-prefixes).

## Network services provided by Tier-0 and Tier-1 logical routers
{: #vpc-ryo-nsx-t-logical-routers-edge-gateway}

NSX-T Data Center supports network services such as IPsec Virtual Private Network (IPsec VPN), Network Address Translation (NAT) and Firewalls as shown in the following diagram.

![Network Services provided by Tier-0 and Tier-1 Logical Routers](../../images/vpc-ryo-diagrams-nsx-t-edge-services.svg "Network Services provided by Tier-0 and Tier-1 Logical Routers"){: caption="Figure 4. Network Services provided by Tier-0 and Tier-1 Logical Routers" caption-side="bottom"}

This topic gives a brief introduction to these capabilities and how they can be used in {{site.data.keyword.vpc_short}}.

### VPN services
{: #vpc-ryo-nsx-t-logical-routers-edge-gateway-vpn}

IPsec Virtual Private Network (IPsec VPN) and Layer 2 VPN (L2 VPN) run on an NSX Edge node. IPsec VPN offers site-to-site connectivity between an NSX Edge node and remote sites. With L2 VPN, you can extend your data center by enabling virtual machines (VMs) to keep their network connectivity across geographical boundaries while using the same IP address.

When you configure NSX-T VPN service in {{site.data.keyword.vpc_short}}, you can use the public `/32` floating IP addresses as the VPN Endpoints both Tier-0 and Tier-1 Logical Routers. You can have multiple VPN endpoints, if needed. When VPN service is configured on Tier-1 Logical Router, ensure that the floating IP is correctly advertised between Tier-0 and Tier-1 Logical Routers.

For more information about the VPN service, see the [VMware documentation](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-A8B113EC-3D53-41A5-919E-78F1A3705F58.html){: external}.

### Network Address Translation
{: #vpc-ryo-nsx-t-logical-routers-edge-services-nat}

Network Address Translation (NAT) is supported on Tier-0 and Tier-1 Logical Routers.

As example, the following types of NAT are supported.

* **Source NAT (SNAT)** translates a source IP address of outbound packets so that packets are shown as originating from a different network.
* **Destination NAT (DNAT)** translates the destination IP address of inbound packets so that packets are delivered to a target address into another network.

You can also disable SNAT or DNAT for an IP address or a range of addresses. If an address has multiple NAT rules, the rule with the highest priority is applied.

When configuring NSX-T NAT in {{site.data.keyword.vpc_short}}, you can use the public `/32` floating IP addresses as the public NAT IP addresses in both Tier-0 and Tier-1 Logical Routers. You can have multiple NAT IPs, if needed. When NAT is configured on Tier-1 Logical Router, ensure that the floating IP is correctly advertised between Tier-0 and Tier-1 Logical Routers.

For more information about NAT and NSX-T, see the [VMware documentation](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-7AD2C384-4303-4D6C-A44A-DEF45AA18A92.html){: external}.

### Firewall
{: #vpc-ryo-nsx-t-logical-routers-edge-gateway-fw}

You can configure East-West and North-South firewall policies in your NSX-T platform.

Gateway firewall represents rules that are applied to the perimeter firewall for North-South traffic connected to {{site.data.keyword.vpc_short}}. Gateway firewall can be applied to both Tier-0 and Tier-1 Logical Routers.

Distributed firewall monitors all the East-West traffic on your VMs. Grouping of objects simplifies rule management. Groups include different objects that are added both statically and dynamically, and can be used as the source and destination of a firewall rule. They can be configured to contain a combination of VMs, IP sets, MAC sets, segment ports, segments, AD user groups, and other groups. Dynamic inclusion of groups can be based on tag, machine name, OS name, or computer name.

For more information about firewalls and NSX-T, see the [VMware documentation](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-F206A4B8-0F33-482D-8727-E71FE253BBCD.html){: external}.

## Related links
{: #vpc-ryo-nsx-t-logical-routers-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
