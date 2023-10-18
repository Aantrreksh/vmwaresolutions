---

copyright:

  years:  2022, 2023

lastupdated: "2023-09-20"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware NSX-T design on VPC
{: #vpc-ryo-nsx-t}

The topic provides an introduction to VMware® NSX-T™ deployment architecture that uses {{site.data.keyword.cloud}} bare metal server for {{site.data.keyword.vpc_short}}. An overview of this architecture is shown in the following diagram.

![Architecture overview of VMware with NSX-T on {{site.data.keyword.vpc_short}}](../../images/vpc-ryo-diagrams-aod-nsx-t-based.svg "Architecture overview of VMware with NSX-T"){: caption="Figure 1. Architecture overview of VMware with NSX-T on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

## VMware NSX-T overview
{: #vpc-ryo-nsx-t-overview}

VMware NSX-T is designed to address application frameworks and architectures that have heterogeneous endpoints and technology stacks. In addition to VMware vSphere®, these environments can include other hypervisors, KVM, containers, and {{site.data.keyword.cloud_notm}} bare metal server. NSX-T is designed to span a software defined network and security infrastructure across platforms other than just vSphere alone. While it is possible to deploy NSX-T components without needing vSphere, this architecture focuses on NSX-T Data Center and its integration within a roll-your-own VMware vSphere Solution on {{site.data.keyword.vpc_short}}. This deployment architecture focuses on NSX-T version 3.1 and later.

NSX-T consists of the following key components:

* **NSX Manager** provides a graphical user interface (GUI) and REST APIs for creating, configuring, and monitoring NSX-T Data Center components such as segments, logical routers, and firewalls. NSX Manager provides a system view and it is the management component of NSX-T Data Center.
* **NSX Host Transport Nodes** participate in an NSX-T Data Center overlay or NSX-T Data Center VLAN networking. Each provisioned ESXi host in the VPC must be enabled to be a Transport Node.
* **NSX Edge Transport Nodes** are service appliances, which are dedicated to running centralized network services that cannot be distributed to the hypervisors. Edge Nodes are grouped in one or several gateway clusters, representing a pool of capacity.

When deployed on {{site.data.keyword.vpc_short}}, the VMware virtual machines (VMs) hosted on {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} can be connected to NSX-T overlay segments. NSX-T segments are logically abstracted network segments in a defined Transport Zone. A Transport Zone is a container that defines the potential reach of Transport Nodes, Hosts, or Edges. The NSX-T segments support line-rate switching and distributed routing in the ESXi hosts. Also, it uses Geneve encapsulation for this overlay traffic to identify and isolate L2 segments over a common L3 infrastructure. In this design, Geneve traffic traverses between the defined Transport Nodes that use {{site.data.keyword.vpc_short}} as the underlying transport network.

In addition to basic software defined overlay networks, NSX-T brings many embedded advanced features. The features are Network Address translation, site to site IPsec VPNs, firewall policies, inclusion of guest introspection within firewall policies, and advanced netflow tracking. Describing these features in detail is beyond the scope of this document. For more information, see [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}.

## NSX-T data center deployment architecture
{: #vpc-ryo-nsx-t-dplarch-managers}

### vSphere distributed switch deployment
{: #vpc-ryo-nsx-t-dplarch-vds}

In this architecture for {{site.data.keyword.vpc_short}}, each {{site.data.keyword.cloud_notm}} bare metal server has only one PCI interface. Therefore, only one vSphere Distributed Switch is used in the ESXi hosts. Note the different to deployments Classic, two vSphere Distributed Switches are currently used, one for private and one for public. Although it is possible to provision multiple PCI interfaces for each {{site.data.keyword.cloud_notm}} bare metal server also in {{site.data.keyword.vpc_short}}, this architecture uses a minimum number of vDS Switches. It also takes advantage of running the vSphere VDS switch version 7.0.x, which allows a converged NSX-T architecture. The following diagram presents how PCI and VLAN interfaces, Distributed Virtual Switches, and Distributed Port Groups are used with NSX-T based deployment.

![Bare Metal Server network interfaces and Distributed PortGroups with NSX-T](../../images/vpc-ryo-diagrams-vpc-hosts-vmk-tep.svg "{{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups with NSX-T"){: caption="Figure 2. {{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups with NSX-T" caption-side="bottom"}

When you create {{site.data.keyword.cloud_notm}} bare metal server VLAN interfaces for NSX-T components that are attached to a VPC subnet, your Distributed Switch must contain a port group that matches the used VLAN ID.
{: note}

Each physical host has redundant 100 Gb network connection for network access to {{site.data.keyword.vpc_short}}. The high availability for physical network connectivity is handled by {{site.data.keyword.cloud_notm}}, which manages the aggregation. In that way, you must not create multiple PCI interfaces for redundancy. The 100 Gb bandwidth is shared by the network interfaces that are on the bare metal server.
{: note}

### NSX-T manager deployment
{: #vpc-ryo-nsx-t-dplarch-managers-depl}

NSX Manager Node hosts the API services, the management plane, and the agent services. It provides a graphical user interface (GUI) and REST APIs for creating, configuring, and monitoring NSX-T Data Center components such as logical switches, logical routers, and firewalls. It also provides a system view and is the management component of NSX-T Data Center. For high availability, NSX-T Data Center supports a management cluster of three NSX Manager VMs. For a production environment, deploying a management cluster is recommended.

For a proof-of-concept environment, you can deploy a single NSX Manager VM. It does not provide high availability for the management and control planes. This action is not suitable for any solution that requires high availability.
{: note}

If you deploy the NSX Managers on the same VPC subnet in a zone, they can use the internal network load balancer. This architecture assumes a deployment in a single zone, and uses single VPC subnet for all management appliances. In other cases, you must use other load balancers, which are beyond the scope of this document.

In this architecture, you deploy three NSX-T Manager VMs on the initial hosts, in the cluster you created of the {{site.data.keyword.cloud_notm}} bare metal server. Architecturally, this is a converged Management and gateway cluster. The following figure shows the logical network placement of the NSX managers in relation to the other components in this architecture.

![NSX-T Manager network overview](../../images/vpc-ryo-diagrams-nsx-t-managers.svg "NSX-T Manager network overview"){: caption="Figure 3. NSX-T Manager network overview" caption-side="bottom"}

The following table shows the specifications for the Manager Nodes. You might select between Small, Medium and Large, depending on the size of your solution.

| Attribute         | Small           | Medium          | Large           |
|:------------------|:----------------|:----------------|:----------------|
| NSX managers      | 3 VMs           | 3 VMs           | 3 VMs           |
| Number of vCPUs   | 4               | 6               | 12              |
| Memory            | 16 GB           | 24 GB           | 48 GB           |
| Disk              | 300 GB          | 300 GB          | 300 GB          |
| Disk type         | Thin            | Thin            | Thin            |
| Network           | vpc-mgmt-subnet | vpc-mgmt-subnet | vpc-mgmt-subnet |
{: caption="Table 1. NSX-T Manager specifications" caption-side="bottom"}

A VLAN interface is provisioned for each NSX-T manager in the management subnet (`vpc-mgmt-subnet`) of the VPC. This VPC subnet is designated for VMware management components of your solution. If you deploy the NSX-T managers on the same VPC subnet in a zone, and you plan to use the NSX-T internal network load balancer, an additional VLAN interface is needed for this Virtual IP (VIP). All created VLAN interfaces are allowed to float, which means that they can be vMotioned between the ESXi hosts. The following table summarizes the required VLAN interfaces in {{site.data.keyword.vpc_short}}.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | NSX-T interface | Distributed Port Group name |
| -------------- | -------------- | ------- | ------ | ----------- | --------------- | --------------------------- |
| vlan-nic-nsx-0 | vlan           | 100     | vpc-mgmt-subnet     | true         | NSX-T Manager 1   | dpg-mgmt |
| vlan-nic-nsx-1 | vlan           | 100     | vpc-mgmt-subnet     | true         | NSX-T Manager 2   | dpg-mgmt |
| vlan-nic-nsx-2 | vlan           | 100     | vpc-mgmt-subnet     | true         | NSX-T Manager 3   | dpg-mgmt |
| vlan-nic-nsx-vip | vlan         | 100     | vpc-mgmt-subnet     | true         | NSX-T Manager VIP | dpg-mgmt |
{: caption="Table 2. VLAN interfaces for NSX-T Managers" caption-side="bottom"}

When the initial NSX Manager is deployed into the host and cluster, you must register the vCenter as the compute manager to facilitate the deployment of other NSX Managers. Public Gateway attached to the management subnet can be used to download updates for the NSX Managers.

For more information about deploying NSX Managers, see [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}.

### Host transport nodes
{: #vpc-ryo-nsx-t-dplarch-hosts}

For NSX-T, each ESXi host must be set as a Transport Node so that it becomes capable of participating in an NSX-T Data Center overlay or NSX-T Data Center VLAN networking. As of version 3, NSX-T can run on the vSphere Distributed Switch version 7.0, and each host if provisioned as described in the [Physical infrastructure design](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-infrastructure-physical) can be added as a Transport Node.

The following table lists the required VLAN interfaces for NSX-T VMKs for each host. These interfaces are always local to the host and are not allowed to float. They are provisioned on the `vpc-tep-subnet`. You can provision these VLAN interfaces in {{site.data.keyword.vpc_short}} either when you provision the host, or when you configure and deploy NSX-T.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | VMkernel adapter | Distributed Port Group name |
| ---------------------- | ---------------- | --------- | --------------------- | -------------- | ------------------ | ------------------------------ |
| vlan-nic-tep-vmk10    | vlan           | 400     | vpc-tep-subnet      | false        | vmk10            | dpg-tep |
{: caption="Table 3. Host management networks and VMkernel adapters" caption-side="bottom"}

Host TEP VLAN ID is defined in the host transport profile. The `dpg-tep` creation is optional, and for consistency only. It might help you to identify the VLAN ID used when operating the environment later.
{: note}

### Edge transport nodes and gateway cluster
{: #vpc-ryo-nsx-t--dplarch-edges}

In addition to NSX Managers, NSX-T gateway cluster and NSX Edge Nodes are required in an NSX-T deployment. The Edge Nodes are specific service appliances that are dedicated to running centralized network services. They cannot be distributed to the ESXi hypervisors, such as Network Address Translation or north-south traffic between NSX-T Geneve Segments and VPC subnets. NSX Edge Nodes are transport nodes that run local control plane daemons and forwarding engines that implement the NSX-T data plane.

VM form factor Edge Nodes are used in this architecture. Edge Nodes can be grouped in one or several clusters, representing a pool of capacity. NSX-T Logical Routers, Tier-0 (also referred as T0) and Tier-1 (also referred as T1) can be hosted in the same or different gateway clusters. Also, in this architecture, a single gateway cluster is created for all T0 and T1 Logical Routers. A T0 Logical Router provides north-south connectivity and connects to a VPC subnet. A T1 logical router connects to one T0 logical router, and it provides northbound connectivity to the NSX-T segments attached to it.

The following table summarizes the requirements for a Medium Form Factor Edge environment, which is the recommended starting size for production workloads.

| Attribute            | Medium Edge Node |
|:---------------------|:-----------------|
| NSX Edges            | 2 VMs            |
| Number of vCPUs      | 4                |
| Memory               | 8 GB             |
| Disk                 | 200 GB           |
| Network: Management | vpc-mgmt-subnet  |
{: caption="Table 4. NSX-T Edge Node specifications" caption-side="bottom"}

As for the other NSX-T components, VLAN interfaces must be created in {{site.data.keyword.vpc_short}} for connectivity. The following table lists the required VLAN interfaces for Edge Nodes.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | NSX-T interface | DPG/Segment name |
| ---------------------- | ---------------- | --------- | --------------------- | -------------- |------------------- | ------------------------------ |
| vlan-nic-nsx-edge-1   | vlan           | 100     | vpc-mgmt-subnet     | true         | NSX-T Edge 1 Mgmt | dpg-mgmt |
| vlan-nic-nsx-edge-2   | vlan           | 100     | vpc-mgmt-subnet     | true         | NSX-T Edge 2 Mgmt | dpg-mgmt |
| vlan-nic-tep-edge-1   | vlan           | 400     | vpc-tep-subnet      | true         | NSX-T Edge 1 TEP  | vpc-zone-edge-tep |
| vlan-nic-tep-edge-2   | vlan           | 400     | vpc-tep-subnet      | true         | NSX-T Edge 2 TEP  | vpc-zone-edge-tep |
{: caption="Table 5. Host management networks and VMkernel adapters" caption-side="bottom"}

The edge TEP traffic must traverse in VLAN backed NSX-T segment `vpc-zone-edge-tep` with the specified VLAN ID, and `dpg-tep` cannot be used for action.
{: note}

This action provides the base for each NSX-T edge. NSX-T T0 Logical Router needs its own VLAN interfaces for its uplinks.
{: note}

## Naming conventions
{: #vpc-ryo-nsx-t-naming}

The following naming conventions are used for deployment. You might use your own naming convention if preferred.

| Description | Naming Standard |
|:---------------------|:-----------------|
| Management VMs | `vpc-nsxt-0`  \n `vpc-nsxt-1`  \n `vpc-nsxt-2` |
| Uplink profiles | `vpc-esxi-vpc-profile`  \n `vpc-edge-vpc-profile` |
| NIOC profiles | `vpc-cluster-nioc-vpc-profile` |
| Gateway cluster profiles | `vpc-zone-cluster-edge-cluster-profile` |
| Transport zones | `nsx-overlay-transportzone`  \n `nsx-vlan-transportzone` |
| Segments | `vpc-zone-customer-t0-172-16-16-0`  \n `vpc-zone-customer-t1-192-168-0-0`  \n `vpc-zone-t0-private-*vlanid*`  \n `vpc-zone-t0-public-*vlanid*`  \n  `vpc-zone-edge-tep` |
| Tier-0 and Tier-1 gateways | `vpc-zone-T0` \n `vpc-zone-T1` |
{: caption="Table 6. NSX-T design naming convention" caption-side="bottom"}

### Transport zones
{: #vpc-ryo-nsx-t-naming-transport-zones}

A Transport Zone is a container that defines the potential reach of Transport Nodes, Hosts, or Edges. Default NSX-T transport zones are used in this architecture.

| Transport node type | Naming Standard             |
|:---------------------|:-----------------|
| Overlay             | `nsx-overlay-transportzone` |
| VLAN                | `nsx-vlan-transportzone`    |
{: caption="Table 7. NSX-T transport zones" caption-side="bottom"}

### Transport nodes
{: #vpc-ryo-nsx-t-naming-transport-nodes}

Transport nodes define the physical server objects or VMs that participate in the virtual network fabric. Uplink profiles provide a shared configuration for each transport node that uses it.

| Transport node type   | Uplink profile | IP assignment |
|:---------------------|:-----------------|:-----------------|
| ESXi | `vpc-esxi-vpc-profile`  | `Static IP list` |
| Gateway cluster | Overlay : `vpc-edge-vpc-profile`  \n VLANs : `vpc-edge-vpc-profile` | `Static IP list` |
{: caption="Table 8. NSX-T transport nodes" caption-side="bottom"}

The IP addresses for each NSX-T transport node must be defined manually, which maps to provisioned {{site.data.keyword.cloud_notm}} bare metal server VLAN interface IPs.
{: note}

### Uplink profiles and teaming
{: #vpc-ryo-nsx-t-naming-uplink-profiles}

An uplink profile defines policies for the links from hypervisor hosts to NSX-T logical switches or from NSX Edge nodes to top-of-rack switches.

| Uplink profile name | VLAN | Teaming policy | Active uplinks | Standby links | MTU |
|:------------------- |:---- |:-------------- |:-------------- |:------------- |:--- |
| `vpc-esxi-vpc-profile` | 400 | Failover order | uplink-1 |   | Managed by vCenter Server |
| `vpc-edge-vpc-profile` | default | Failover order | uplink-1 |   | 9000 |
{: caption="Table 9. NSX-T uplink profiles" caption-side="bottom"}

The VLAN ID used for Host TEPs is defined here. If you use a different VLAN ID, change the profile. The VLAN ID used for Edge TEPs is defined in the Edge TEP Segment (`vpc-zone-edge-tep`).
{: note}

### VNI pools
{: #vpc-ryo-nsx-t-vni-pools}

Virtual Network Identifiers (VNIs) are similar to VLANs for a physical network. VNIs are created automatically when a logical switch is created from a pool or range of IDs. This architecture uses the default VNI pool that is deployed with NSX-T.

### Segments
{: #vpc-ryo-nsx-t-logical-switches}

An NSX-T segment reproduces switching functions, broadcast, unknown unicast, multicast (BUM) traffic, in a virtual environment that is decoupled from the underlying hardware.

| Segment name | VLAN | Transport zone | Uplink teaming policy |
|:------------ |:---- |:-------------- |:--------------------- |
| `vpc-zone-edge-tep` | default | `nsx-vlan-transportzone` | TEP * Failover order |
| `vpc-zone-t0-public` | default | `nsx-vlan-transportzone` |   |
| `vpc-zone-t0-private` | default | `nsx-vlan-transportzone` |   |
| `vpc-zone-customer-t0-172-16-16-0` |   | `nsx-overlay-transportzone` |   |
| `vpc-zone-customer-t1-192-168-0-0` |   | `nsx-overlay-transportzone` |   |
| `vpc-zone-customer-t1-192-168-1-0` |   | `nsx-overlay-transportzone` |   |
{: caption="Table 10. NSX-T segments" caption-side="bottom"}

## Related links
{: #vpc-ryo-nsx-t-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
