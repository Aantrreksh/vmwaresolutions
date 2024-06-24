---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# NSX deployment
{: #vpc-vcf-nsx-t}

The following information provides an introduction to VMware® NSX™ deployment details for VMware Cloud Foundation deployment architectures in {{site.data.keyword.vpc_short}}.

## NSX deployment architectures for VMware Cloud Foundation
{: #vpc-vcf-nsx-t-deployment-arch}

An overview of consolidated architecture is shown in the following diagram. The consolidated architecture deployment uses the management domain NSX components for the workloads as well.

![Architecture overview of consolidated VMware Cloud Foundation NSX deployment on {{site.data.keyword.vpc_short}}](../../images/vcf-vpc-v2-arch-net-cons.svg "Architecture overview of consolidated VMware Cloud Foundation NSX deployment on {{site.data.keyword.vpc_short}}"){: caption="Figure 1. Architecture overview of consolidated VMware Cloud Foundation NSX deployment on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

Standard architecture follows the same principles, but deploys dedicated NSX managers and NSX edge nodes for the VI workloads domain and uses dedicated TEP and Tier-0 gateway uplink subnets for the workload domain hosts and edge nodes. All NSX managers are deployed on the management domain.

![Architecture overview of standard VMware Cloud Foundation NSX deployment on {{site.data.keyword.vpc_short}}](../../images/vcf-vpc-v2-arch-net-std.svg "Architecture overview of standard VMware Cloud Foundation NSX deployment on {{site.data.keyword.vpc_short}}"){: caption="Figure 2. Architecture overview of standard VMware Cloud Foundation NSX deployment on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

## VMware vSphere distributed switch deployment
{: #vpc-vcf-nsx-t-vds}

In the VMware Cloud Foundation architecture for {{site.data.keyword.vpc_short}}, each {{site.data.keyword.cloud_notm}} bare metal server has two PCI interfaces and one vSphere Distributed Switch with two uplinks.

When you create {{site.data.keyword.cloud_notm}} bare metal server VLAN interfaces for NSX components that are attached to a VPC subnet, your Distributed Switch must contain a port group that matches the used VLAN IDs.
{: note}

Each physical host has a redundant 100 Gb network connection for network access to {{site.data.keyword.vpc_short}}. The 100 Gb bandwidth is shared by the network interfaces that are on the bare metal server.
{: note}

The high availability for physical network connectivity is handled by {{site.data.keyword.cloud_notm}}, which manages the aggregation. The multiple PCI interfaces, as seen in VMware Cloud Foundation deployment, do not add redundancy, but are required in VMware Cloud Foundation deployments and they are up the uplink migrations from vSphere Standard Switch to vSphere Distributed Switch.
{: note}

## NSX manager deployment
{: #vpc-vcf-nsx-t-managers}

NSX Manager Node hosts the API services, the management plane, and the agent services. It provides a graphical user interface (GUI) and REST APIs for creating, configuring, and monitoring NSX Data Center components, such as logical switches, gateways, and firewalls. It also provides a system view and it is the management component of NSX Data Center. For high availability, VMware Cloud Foundation deploys a management cluster of three NSX Manager virtual machines (VMs) and a virtual IP.

A VLAN interface is provisioned for each NSX manager in the management subnet (`vpc-mgmt-subnet`) of the VPC. This VPC subnet is designated for VMware management components of your solution. If you deploy the NSX managers on the same VPC subnet in a zone, and you plan to use the NSX internal network load balancer, you need an extra VLAN interface for this virtual IP (VIP). All created VLAN interfaces are allowed to float, which means that they can be vMotioned between the ESXi hosts. The following table summarizes the required VLAN interfaces in {{site.data.keyword.vpc_short}}.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | NSX interface | Distributed port group name |
| ---------------|----------------|---------|--------|-------------|---------------|---------------------------- |
| `vlan-nic-nsx-0` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Manager 1 | `pg-mgmt` |
| `vlan-nic-nsx-1` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Manager 2 | `pg-mgmt` |
| `vlan-nic-nsx-2` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Manager 3 | `pg-mgmt` |
| `vlan-nic-nsx-vip` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Manager VIP | `pg-mgmt` |
{: caption="Table 1. VLAN interfaces for NSX Managers" caption-side="bottom"}

When the initial NSX Manager is deployed into the host and cluster, you must register the vCenter as the compute manager to facilitate the deployment of other NSX Managers. You can use the Public Gateway that is attached to the management subnet to download updates for the NSX Managers through SDDC manager.

The principles for deploying NSX managers for consolidated and standard VMware Cloud Foundation deployment are the same.

## Host transport nodes
{: #vpc-vcf-nsx-t-hosts}

For NSX, each ESXi host must be set as a Transport Node so that it becomes capable of participating in an NSX Data Center overlay or NSX Data Center VLAN networking. Cloud builder and SDDC manager handle the deployment in VMware Cloud Foundation. VPC Bare Metal Server VLAN interfaces are prepared for the TEP vmks in the hosts.

The following table lists the required VLAN interfaces for NSX VMKs for each host. These interfaces are always local to the host and do not need to move, but are allowed to float to facilitate the use in NSX pools. They are provisioned on the `vpc-tep-subnet`.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | VMkernel adapter | Distributed port group name |
| ---------------|----------------|---------|--------|-------------|------------------|---------------------------- |
| `vlan-nic-tep-pool-<1>` | `vlan` | 1614 | `vpc-tep-subnet` | `false` | `vmk10` | `none` - set in NSX profile |
| `vlan-nic-tep-pool-<2>` | `vlan` | 1614 | `vpc-tep-subnet` | `false` | `vmk11` | `none` - set in NSX profile |
{: caption="Table 2. Host management networks and VMkernel adapters for consolidated architecture" caption-side="bottom"}

Host TEP VLAN ID is defined in the host transport profile.
{: note}

The previous table shows the naming and numbering principles. The actual deployment subnet or distributed port group names might vary.
{: note}


In the standard architecture, the VI workload domain deployment uses new VPC subnets and new VLAN IDs are used.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | VMkernel adapter | Distributed port group name |
| ---------------|----------------|---------|--------|-------------|------------------|---------------------------- |
| `vlan-nic-tep-pool-<1>` | `vlan` | 1614 | `vpc-tep-subnet` | `false` | `vmk10` | `none` - set in NSX profile |
| `vlan-nic-tep-pool-<2>` | `vlan` | 1614 | `vpc-tep-subnet` | `false` | `vmk11` | `none` - set in NSX profile |
| `vlan-nic-wl-tep-pool-<1>` | `vlan` | 1634 | `vpc-wl-tep-subnet` | `false` | `vmk10` | `none` - set in NSX profile |
| `vlan-nic-wl-tep-pool-<2>` | `vlan` | 1634 | `vpc-wl-tep-subnet` | `false` | `vmk11` | `none` - set in NSX profile |
{: caption="Table 3. Host management networks and VMkernel adapters for standard architecture" caption-side="bottom"}

The previous table shows the naming and numbering principles. The actual deployment subnet or distributed port group names might vary.
{: note}

## Edge transport nodes and gateway cluster
{: #vpc-vcf-nsx-t-edges}

In addition to NSX Managers, the NSX gateway cluster and NSX Edge nodes are required in an NSX deployment. The Edge Nodes are specific service appliances that are dedicated to running centralized network services. They cannot be distributed to the ESXi hypervisors, such as Network Address Translation or north-south traffic between NSX Geneve Segments and VPC subnets. NSX Edge Nodes are transport nodes that run local control plane daemons and forwarding engines that implement the NSX data plane.

VM form factor Edge Nodes are used in this architecture. Edge Nodes can be grouped in one or several clusters, representing a pool of capacity. NSX gateways, Tier-0 (also referred as T0) and Tier-1 (also referred as T1) can be hosted in the same or different gateway clusters. Also, in this architecture, a single gateway cluster is created for all T0 and T1 gateways. A T0 gateway provides north-south connectivity and connects to a VPC subnet. A T1 gateway connects to one T0 gateway, and it provides northbound connectivity to the NSX segments attached to it.

The following table summarizes the requirements for a Medium Form Factor Edge environment, which is the starting size for production workloads.

| Attribute            | Medium edge node |
|----------------------|------------------|
| NSX Edges            | 2 VMs            |
| Number of vCPUs      | 4                |
| Memory               | 8 GB             |
| Disk                 | 200 GB           |
| Network - Management | `vpc-mgmt-subnet` |
{: caption="Table 4. NSX Edge Node specifications" caption-side="bottom"}

You can change the size of the edge node in the deployment variables.
{: note}

As for the other NSX components, VLAN interfaces must be created in {{site.data.keyword.vpc_short}} for connectivity. The following table lists the required VLAN interfaces for Edge Nodes.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | NSX interface | Distributed port group or segment name |
| ---------------|----------------|---------|--------|-------------|---------------|----------------- |
| `vlan-nic-nsx-edge-1` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Edge 1 Mgmt | `pg-mgmt` |
| `vlan-nic-nsx-edge-2` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Edge 2 Mgmt | `pg-mgmt` |
| `vlan-nic-edge-tep-pool-1` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 1 TEP 1 | `none` - set in NSX profile |
| `vlan-nic-edge-tep-pool-2` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 1 TEP 2 | `none` - set in NSX profile |
| `vlan-nic-edge-tep-pool-3` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 2 TEP 1 | `none` - set in NSX profile |
| `vlan-nic-edge-tep-pool-4` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 2 TEP 2 | `none` - set in NSX profile |
{: caption="Table 5. Host management networks and VMkernel adapters for consolidated architecture" caption-side="bottom"}

Edge TEP VLAN ID is defined in the edge transport profile.
{: note}

This action provides the base for each NSX edge. NSX T0 gateway needs its own VLAN interfaces for its uplinks.
{: note}

The previous table shows the naming and numbering principles. The actual deployment subnet or distributed port group names might vary.
{: note}

In the standard architecture, the VI workload domain deployment uses new VPC subnets and new VLAN IDs are used.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | NSX interface | Distributed port group or segment name |
| ---------------|----------------|---------|--------|-------------|---------------|--------------------------------------- |
| `vlan-nic-nsx-edge-1` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Edge 1 Mgmt | `pg-mgmt` |
| `vlan-nic-nsx-edge-2` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Edge 2 Mgmt | `pg-mgmt` |
| `vlan-nic-edge-tep-pool-1` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 1 TEP 1 | `none` - set in NSX profile |
| `vlan-nic-edge-tep-pool-2` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 1 TEP 2 | `none` - set in NSX profile |
| `vlan-nic-edge-tep-pool-3` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 2 TEP 1 | `none` - set in NSX profile |
| `vlan-nic-edge-tep-pool-4` | `vlan` | 2713 | `vpc-tep-subnet` | `true` | NSX Edge 2 TEP 2 | `none` - set in NSX profile |
| `vlan-nic-nsx-wl-edge-1` | `vlan` | 1631 | `vpc-wl-mgmt-subnet` | `true` | NSX Edge 1 Mgmt | `pg-wl-mgmt` |
| `vlan-nic-nsx-wl-edge-2` | `vlan` | 1631 | `vpc-wl-mgmt-subnet` | `true` | NSX Edge 2 Mgmt | `pg-wl-mgmt` |
| `vlan-nic-edge-wl-tep-pool-1` | `vlan` | 2733 | `vpc-wl-tep-subnet` | `true` | NSX Edge 1 TEP 1 | `none` - set in NSX profile |
| `vlan-nic-edge-wl-tep-pool-2` | `vlan` | 2733 | `vpc-wl-tep-subnet` | `true` | NSX Edge 1 TEP 2 | `none` - set in NSX profile |
| `vlan-nic-edge-wl-tep-pool-3` | `vlan` | 2733 | `vpc-wl-tep-subnet` | `true` | NSX Edge 2 TEP 1 | `none` - set in NSX profile |
| `vlan-nic-edge-wl-tep-pool-4` | `vlan` | 2733 | `vpc-wl-tep-subnet` | `true` | NSX Edge 2 TEP 2 | `none` - set in NSX profile |
{: caption="Table 6. Host management networks and VMkernel adapters for standard architecture" caption-side="bottom"}

The previous table shows the naming and numbering principles. The actual deployment subnet or distributed port group names might vary.
{: note}

## Related links
{: #vpc-vcf-nsx-t-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} bare metal servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
