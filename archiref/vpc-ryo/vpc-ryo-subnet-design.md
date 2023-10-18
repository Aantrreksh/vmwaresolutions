---

copyright:

  years:  2022, 2023

lastupdated: "2023-09-20"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware VMs on VPC subnets
{: #vpc-ryo-subnet}

The topic provides an introduction to {{site.data.keyword.vpc_full}} subnet-integrated VMware® virtual machines (VMs) architecture, as shown on the following diagram.

![Architecture overview of VMware on {{site.data.keyword.vpc_short}}](../../images/vpc-ryo-diagrams-aod-non-nsx-based.svg "Architecture overview of VMware on {{site.data.keyword.vpc_short}}"){: caption="Figure 1. Architecture overview of VMware on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

## Overview ov VMware virtual machine networking integration with VPC subnets
{: #vpc-ryo-subnet-intro}

The {{site.data.keyword.cloud_notm}} bare metal server for VPC fully supports VMware vSphere® networking capabilities with standard and distributed vSwitches. Before setting up networks in the vSphere environment, it is important to understand the networking concepts between {{site.data.keyword.cloud_notm}} bare metal server in {{site.data.keyword.vpc_short}} and vSphere networking.

When you provision a bare metal server, a primary PCI interface is created by default for every server. This primary PCI interface automatically becomes the bare metal server uplink on vSwitch0 in ESXi™. The PCI interface IP address is in the `vmk0` adapter, which is located in the management network port group on vSwitch0. The VLAN ID of the management network port group is automatically set to `0`.

VLAN interfaces in {{site.data.keyword.cloud_notm}} bare metal server can be used as virtual network adapters of the VMKernel adapters. Or also, as virtual machines (VMs) including management VMs, such as vCenter Server® and your VMs workload.

In this design, the standard vSwitches are migrated to distributed vSwitch in every host, and the default PCI interface is the uplink of the distributed vSwitch. When deploying VMkernel adapters in the ESXi™, you create a distributed port group for each System Traffic Type and VMK. Also, you configure the specific VMkernel adapter to a specific VPC subnet as described in the [Physical infrastructure design](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-infrastructure-physical) topic.

VLAN interfaces are always associated with a PCI interface through the VLAN ID. However, the VLAN ID is only local to the server. When VLAN interface traffic is traversing in VPC, the frames do not have the VLAN header, and therefore do not include the VLAN ID either. The VLAN interface in the bare metal server SmartNic automatically tags traffic that is routed through it with the VLAN ID. Inbound traffic that is tagged with a VLAN ID is directed to the appropriate VLAN interface.

## VLAN interfaces for VMware VMs on VPC subnets
{: #vpc-ryo-subnet-vlan-nic}

The following diagram presents an overview of the solution for hosting VMware VMs on VPC subnets with VLAN interfaces. In this design, the VMware infrastructure subnets are used to carry VMware System Traffic Types, and another set of subnets is used for VMs workloads. These subnets can be provisioned from the same VPC prefix, or you can use different prefixes for each type. As they are routed in the same VPC, the IP addresses must be unique for each traffic type.

![VLAN interfaces for VMware VMs on VPC subnets](../../images/vpc-ryo-diagrams-non-nsx-based-vms.svg "VLAN interfaces for VMware VMs on VPC subnets"){: caption="Figure 2. VLAN interfaces for VMware VMs on VPC subnets" caption-side="bottom"}

When you create a VLAN interface for either to a VMkernel adapter or to a VM, you must specify a VLAN ID for the VLAN interface. This VLAN ID maps to the VLAN ID that is used in a standard or a distributed port group in vSphere. VLAN ID `0` cannot currently be used for a VLAN interface. The following table provides an example mapping of VLAN interfaces and distributed port groups.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | VM network interface | Distributed Port Group name |
| -------------- |--------------- | ------- | ------ | ----------- | -------------------- | ---------------- |
| vlan-nic-vm001        | vlan           | 1000    | vpc-vm-subnet-192-168-100.0-24 | true         | vnic1                | dpg-vm-subnet-192-168-100-0-24 |
| vlan-nic-vm002        | vlan           | 1000    | vpc-vm-subnet-192-168-100.0-24 | true         | vnic1                | dpg-vm-subnet-192-168-100-0-24 |
| vlan-nic-vm003        | vlan           | 1001    | vpc-vm-subnet-192-168-100.0-24 | true         | vnic1                | dpg-vm-3-vlan-1001 |
| vlan-nic-vm004        | vlan           | 1002    | vpc-vm-subnet-192-168-100.0-24 | true         | vnic1                | dpg-vm-3-vlan-1002 |
{: caption="Table 1. VLAN interfaces for VMware VMs on VPC subnet example" caption-side="bottom"}

You can create VLAN interfaces with the same VLAN ID, or you can use different VLAN IDs mapped to the same VPC subnet. The distribution port group used for the VM's vNIC must match the provisioned VLAN interface's VLAN ID. For more information, see [Security groups with VMware workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-subnet#vpc-ryo-subnet-net-security-sg).
{: note}

Before you provision or migrate a VMware VM to a bare metal server in {{site.data.keyword.vpc_short}} subnet, you must create a VLAN interface for the VMs. A prerequisite for a VLAN interface creation is that you must define a VPC subnet in the VPC Zone prefix.

VLAN interfaces are provisioned with IP and MAC address. They are always provisioned to a specific subnet, and you can either use VPC to allocate the IP, or define the IP address of the available IP addresses in the VPC subnet. When configuring the network settings in VMs Operating System, you can use either static network configurations or DHCP. If you want to use DHCP, you must modify the VMs vNIC MAC address to match the provisioned VLAN interface MAC address. For static IP usage, no special changes are needed, and you might use VMware provided MAC address.

[VMware vSphere vMotion](https://www.vmware.com/fi/products/vsphere/vmotion.html){: external} refers to live migration of workloads from one ESXi host to another. If the VM needs to support vMotion, you must set the VLAN interface to `floatable` when provisioning it in VPC.

Floating configuration cannot be changed after the VLAN interface is created. However, you can re-create the VLAN interface, and use the same IP address to minimize required changes.
{: note}

When you introduce a new VLAN ID to be used by a VLAN interface in bare metal server, ensure that the used VLAN IDs are included in the PCI interface VLAN allowlist. In a distributed vSwitch topology and when vMotion is used for a VM, ensure that the VLAN ID of this port group is included in the VLAN allowlist of all the {{site.data.keyword.cloud_notm}} bare metal server part of the cluster.

## VPC access control lists (ACLs) and security groups (SGs) with VMware VMs on VPC subnets
{: #vpc-ryo-subnet-net-security}

Bare metal server for VPC provides full support for VPC networking features. Network security capabilities, such as security groups and Access Control Lists (ACL) can be used with bare metal server PCI and VLAN interfaces. In this design, both the VMware infrastructure subnets, which are used to carry VMware System Traffic Types, and VPC subnets for workloads VMs share the same routing domain. Best practices advice you to create required network security measures for this process.

### Access control list with VMware workloads
{: #vpc-ryo-subnet-net-security-acl}

An Access Control List can manage by allowing or denying inbound and outbound traffic for a subnet. An ACL is stateless, which means that inbound and outbound rules must be specified separately and explicitly. Each ACL consists of rules based on a source IP, source port, destination IP, destination port, and protocol. Every VPC has a default ACL that allows all inbound and outbound traffic. You can edit the default ACL rules, or create a custom ACL.

As ACLs are applied to a subnet. You can use them as with Virtual Servers to control traffic to and from the VPC subnets. Also, you can create isolated subnets, for example, for vSAN™, vMotion and TEP traffic.

For more information about ACLs, see [Security in VPC](/docs/vpc?topic=vpc-security-in-your-vpc). For more information about ACLs with {{site.data.keyword.cloud_notm}} bare metal server, see [Introduction to {{site.data.keyword.cloud_notm}} bare metal server networking](/docs/vpc?topic=vpc-bare-metal-servers-network).

### Security groups with VMware workloads
{: #vpc-ryo-subnet-net-security-sg}

A security group acts as a virtual firewall that controls the traffic for one or more virtual server network interfaces and {{site.data.keyword.cloud_notm}} bare metal server PCI or VLAN interfaces. A security group is a collection of rules that specify whether to allow or deny traffic for an associated interface. You can associate an interface with one or more security groups and edit the security group rules.

In this design, you can use security groups to create a logical grouping of management, vSAN, vMotion and TEP traffic types, and apply rules to allow required traffic flows. You can also use security groups as a source or destination in the rules to create more dynamic rules without specifying IP addresses.

When security groups are used with VLAN interfaces in VMware VMs, to avoid misconfigurations and misunderstandings, it is important to understand how traffic flows to and from standard and distributed vSwitches, and inside the hosts.

In a VMware environment, traffic between VLAN network interfaces that have the same VLAN ID on the same bare metal server is typically switched by the standard and distributed vSwitches within the ESXi host. Also, it never reaches the VPC network.

For example, on a vSphere Cluster that consists of multiple bare metal server hosts, and you configured a distributed vSwitch, or the hosts are using the default standard switch. In this case, you can create a port group with VLAN ID `100` and add it to the specific vSwitch or vSwitches. The traffic between vNICs of two VMs that are attached to Port Group `100` is controlled by the vSwitch.

The setting has the following consequences:

- Security Group rules that control traffic between the network interfaces in Port Group VLAN ID `100` are not applied.
- If you need Security Group to control traffic between the two VMs, you must use separate VLAN IDs for the VLAN interfaces to force traffic to traverse through VPC.
- If you use separate VLAN IDs for VMs, you must deploy multiple port groups with mapping VLAN IDs in standard distributed vSwitches.

For more information about security groups, see [Security in your VPC](/docs/vpc?topic=vpc-security-in-your-vpc). For more information about security groups with {{site.data.keyword.cloud_notm}} bare metal server, see [Introduction to {{site.data.keyword.cloud_notm}} bare metal server networking](/docs/vpc?topic=vpc-bare-metal-servers-network).

## Public connectivity with VMware VMs on VPC subnet
{: #vpc-ryo-subnet-vlan-public-connect}

Bare Metal Server for VPC provides full support for VPC public networking features. External connectivity can be achieved either by using a Public Gateway that is attached to a VPC subnet, or by using a floating IP address that is attached to a PCI or VLAN interface of bare metal server. Public gateway uses source network address translation (SNAT) and a floating IP uses destination network address translation (DNAT). These functionalities are identical to VPC virtual servers.

The following diagram depicts how VMware workloads that are attached to VPC subnets can use these two options, and shows the key differences between them. Each VM has a VLAN interface, and the external connectivity depends how the VLAN interface is provisioned.

![Public Gateways and floating IPs](../../images/vpc-ryo-diagrams-non-nsx-based-vms-pgw.svg "Public Gateways and floating IPs"){: caption="Figure 3. Public Gateways and floating IPs" caption-side="bottom"}

VLAN interfaces that are attached to a VPC subnet with a Public Gateway can initiate connections to the internet, but they cannot receive connections from the internet. Public Gateway provides connectivity for an entire subnet, and public traffic that originates from the VMs on this subnet considers the Public Gateway IP address as the source. If the subnet is not attached to a Public Gateway, the traffic is fully private. In this design, vSAN, vMotion, or TEP subnets can be examples.

A VLAN interface with a floating IP can initiate or receive connections to or from the internet. Floating IP provides connectivity for a single instance. This action overrides the Public Gateway of that specific VLAN interface in VPC subnet, if that is provisioned to a subnet with attached Public Gateway.

## Related links
{: #vpc-ryo-subnet-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
