---

copyright:

  years:  2023, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VPC design for VMware deployment
{: #vpc-ryo-vpc-vmw}

The topic provides an overview to the VPC architecture for a VMware® deployment. You might alter this architecture for your needs, but it is important to understand the separation of VMware infrastructure networking requirements and the need to separate it from other workload traffic.

## VPC subnets
{: #vpc-ryo-vpc-vmw-subnets}

The VMkernel networking in VMware provides connectivity to hosts and handles the standard system traffic of vSphere® vMotion, IP storage, Fault Tolerance, vSAN™, and others. You can also create VMkernel adapters (VMK) on the source and target vSphere Replication hosts to isolate the vSphere replication data traffic.

It is recommended to take appropriate security measures to prevent unauthorized access to the management and system traffic in your vSphere environment, such as:

* Isolate the vMotion traffic in a separate network that includes only the ESXi hosts that participate in the migration.
* Isolate the management traffic in a network that only network and security administrators can access.
* Isolate the NSX-T™ TEP traffic only to the Transport Nodes and to interfaces that need access to TEP traffic.

As there are various System Traffic Types in VMware, it is recommended to dedicate a separate VMkernel adapter for every System Traffic Type. And also, isolate traffic in logical segments in the underlying network infrastructure and dedicate a distributed port group in distributed switches.

In {{site.data.keyword.vpc_short}}, there are multiple ways to do logical segmentation or isolation. The architecture represented here uses a traditional VLAN segmentation analogy. Each System Traffic Type or VMK has its own VPC subnet that can then be controlled with subnet ACLs.

![VPC design for VMware deployment](../../images/vpc-ryo-diagrams-vpc-physical.svg "VPC design for VMware deployment"){: caption="Figure 1. VPC network design for VMware deployment" caption-side="bottom"}

For this architecture, a new VPC is created for VMware workloads for simplicity. To connect to other workloads, you can use {{site.data.keyword.cloud}} interconnectivity solutions. If needed, you might customize and create your own design, and also integrate the {{site.data.keyword.cloud_notm}} bare metal servers with your existing VPCs.

The following table lists the recommended subnets in VPC. It is based on the recommendation to separate System Traffic Types logically and a dedicated VPC subnet for each user used. As each VMK host needs its own IP, it is recommended to keep the PCI interfaces (management) hosts on their own subnet. Also, place other management instances (such as vCenter®, NSX-T managers, NSX-Edge management interfaces) on their own subnet. It allows easier segmentation, sizing, and provides better scalability.

| Subnet name         | System traffic type          | Subnet sizing guidance |
| --------------------| ---------------------------- |----------------------- |
| vpc-mgmt-subnet       | Management appliance traffic | Number of Management Appliances |
| vpc-host-subnet       | Host management traffic      | Number of Hosts |
| vpc-vmot-subnet       | vMotion traffic              | Number of Hosts |
| vpc-vsan-subnet       | vSAN traffic                 | Number of Hosts |
| vpc-tep-subnet        | TEP traffic                  | Number of Hosts + \n 2 x Edge Nodes |
{: caption="Table 1. VPC subnets for System Traffic Types" caption-side="bottom"}

To be able to create subnets in VPC, you must create a VPC prefix. VPC prefixes are defined per zone. To simplify routing, it is recommended to allocate the recommended subnets from a single prefix. Which means that to be able to accommodate 5 subnets, you need one `/21` prefix to cater addresses for about 120 hosts per zone. If you want to use a prefix with `/22`, you can add about 60 hosts per zone. By selecting a large enough prefix, it will leave you growth for scalability and future needs, such as dedicated VMKs for NFS replication and for NSX-T Tier-0 uplinks.

### Physical host connections in VPC
{: #vpc-ryo-vpc-vmw-host-connect}

The {{site.data.keyword.cloud_notm}} bare metal server in {{site.data.keyword.vpc_short}} uses SmartNICs to support all VPC network capabilities. Each physical host has a redundant 100 Gb network connection for network access to {{site.data.keyword.vpc_short}}. The high availability for physical network connectivity is handled by {{site.data.keyword.cloud_notm}}, and you do not have to configure anything special. All network interfaces are backed by two redundant physical ports that are on the TORs (top-of-rack) switch. {{site.data.keyword.cloud_notm}} manages the aggregation, and you do not have to create multiple PCI interfaces for redundancy, for example. The 100 Gb bandwidth is shared by the network interfaces that are configured and currently active on the bare metal server.

A network interface in a {{site.data.keyword.cloud_notm}} bare metal server is an abstract representation of a network interface card, and a network interface connects a {{site.data.keyword.cloud_notm}} bare metal server to a VPC subnet.

In {{site.data.keyword.vpc_short}}, you can create two types of network interfaces on a bare metal server:

* **PCI (Peripheral Component Interconnect) interface** represents a physical network interface. It is possible to include up to 8 PCI interfaces on a bare metal server.
* **VLAN (Virtual LAN) interface** represents an interface that is associated with a PCI interface through the VLAN ID. The VLAN interface automatically tags traffic that is routed through it with the VLAN ID. Inbound traffic that is tagged with a VLAN ID is directed to the appropriate VLAN interface.

PCI interface in a {{site.data.keyword.cloud_notm}} bare metal server is a physical PCI device that can be created or deleted only when the {{site.data.keyword.cloud_notm}} bare metal server is stopped. PCI interface has an `allowed_VLANs` property, which controls the VLANs that permit to use the PCI interface. VLAN interface is a virtual device, which is used through a PCI device that has the VLAN in its array of `allowed_VLANs`.

The allowed VLANs list must be updated for all PCI interfaces hosts separately if you start using new VLAN IDs in your solution.
{: note}

Every VLAN interface must use an IEEE 802.1q tag. It is important to understand that these VLAN tags have only local significance to the server. They can be used internally to isolate or separate the traffic, for example, in Distributed Virtual Switches. While each VLAN interface can attach to only one subnet, you can create multiple VLAN interfaces in a bare metal server. Each of these interfaces can be attached to a specific subnet.

VLAN interfaces are created for every virtual machine (VM) which needs to be attached to a VPC subnet. For example, VLAN interface that is created for vCenter can use VLAN tag `100` and this VLAN interface can be provisioned to a management subnet in VPC. When deploying a vCenter VM, it is attached to vSphere vSwitch and uses a port group that is defined with VLAN tag `100`. When the vCenter uses the IP of the vLAN interface as provided by VPC, it is logically attached to a management subnet in VPC just like any other VPC Virtual Server.

You can set VLAN interfaces to be `floatable`. This action is important with VMware workloads that require vMotion between the {{site.data.keyword.cloud_notm}} bare metal server. This capability is used with VMware management workloads such as vCenter or NSX managers to allow them to be moved between hosts for High Availability (HA) or Distributed Resource Scheduler (DRS).

Both PCI and VLAN interfaces can be attached to a VPC security group. A VLAN interface does not inherit the security groups of the PCI interface through which the VLAN interface traffic flows. Also, VPC ACLs can be used to control inbound and outbound traffic for a subnet to which these PCI and VLAN interfaces are attached.

For more information about the networking concepts, see [Networking overview for {{site.data.keyword.cloud_notm}} bare metal server on VPC](/docs/vpc?topic=vpc-bare-metal-servers-network).

### Host management networks and VMkernel adapters
{: #vpc-ryo-vpc-vmw-mgmt-net}

As mentioned earlier, it is recommended to dedicate a separate VMkernel adapter for every VMware System Traffic Type. Also, to isolate this traffic in logical segments in the underlying network infrastructure and dedicate a Distributed Port Group in the Distributed Virtual Switch.

In {{site.data.keyword.vpc_short}}, each {{site.data.keyword.cloud_notm}} bare metal server is connected to a VPC subnet by using its primary PCI interface. This interface is used by the default management VMkernel adapter `vmk0`. For the other System Traffic Types in VMware, VLAN interfaces are used and one VLAN interface is created for each VMkernel adapter type.

The following table lists the VMK key that is required in this architecture for each ESXi host. Depending on your design and planned capabilities, you might not need all VMKs listed here. However, when you plan the deployment and VPC infrastructure automation with, for example Terraform, it is recommended to take a note of these requirements.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | VMkernel adapter | Distributed Port Group name |
| -------------- | -------------- | ------- | ------ | ----------- | ---------------- | --------------------------- |
| pci-nic-vmnic0-vmk0   | pci            | 0       | vpc-host-subnet     | false        | vmk0             | dpg-hosts |
| vlan-nic-vmotion-vmk2 | vlan           | 200     | vpc-vmot-subnet     | false        | vmk2             | dpg-vmotion |
| vlan-nic-vsan-vmk3    | vlan           | 300     | vpc-vsan-subnet     | false        | vmk3             | dpg-vsan |
| vlan-nic-tep-vmk10    | vlan           | 400     | vpc-tep-subnet      | false        | vmk10            | dpg-tep |
{: caption="Table 2. Host management networks and VMkernel adapters" caption-side="bottom"}

If you are not using NSX-T, you do not need `vlan-nic-tep-vmk10` interface.
{: note}

If you are not using vSAN, you do not need `vlan-nic-vsan-vmk3` interface.
{: note}

The following diagram presents how PCI and VLAN interfaces, Distributed Virtual Switch and Distributed Port Groups are created and used with basic deployment architecture without NSX-T.

![{{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups](../../images/vpc-ryo-diagrams-vpc-hosts-vmk.svg "{{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups"){: caption="Figure 2. {{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups" caption-side="bottom"}

The following diagram presents how PCI and VLAN interfaces, Distributed Virtual Switch, and Distributed Port Groups are used with NSX-T based deployment architecture.

![{{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups with NSX-T](../../images/vpc-ryo-diagrams-vpc-hosts-vmk-tep.svg "{{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups with NSX-T"){: caption="Figure 3. {{site.data.keyword.cloud_notm}} bare metal server network interfaces and Distributed PortGroups with NSX-T" caption-side="bottom"}

When provisioning a host, make sure you provision the required VLAN interfaces for each, and that the PCI interface allowed VLANs lists include the used VLAN IDs.
{: note}

As VMkernel adapters do not need to move between hosts, they are provisioned with `Allow Float` set to `false`.
{: note}

## Related links
{: #vpc-ryo-vpc-vmw-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
