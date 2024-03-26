---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Physical infrastructure design
{: #vpc-ryo-infrastructure-physical}

The physical infrastructure consists of the following components:

* **Physical compute** - The physical compute provides the physical processing and memory that is used by the virtualization infrastructure. For this design, the compute components are provided by {{site.data.keyword.cloud}} bare metal server for {{site.data.keyword.vpc_short}}.
* **Physical network** - The physical network provides the network connectivity into the environment that is used by the network virtualization. The network is provided by the {{site.data.keyword.vpc_short}}.
* **Physical storage** - The physical storage provides the raw storage capacity that is used by the virtualization infrastructure. Storage components are provided either by NVMe U.2 SSDs attached to {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} or by {{site.data.keyword.vpc_short}} file share that uses NFS v4.1.

![Physical infrastructure](../../images/vpc-ryo-diagrams-overview-physical.svg "Physical infrastructure"){: caption="Figure 1. Physical infrastructure" caption-side="bottom"}

## Physical compute design
{: #vpc-ryo-infrastructure-physical-host-design}

Each VMware® deployment begins with a minimum of two hosts, depending on the choice of storage solution and High Availability (HA) architecture that you want. You are responsible to design your VMware deployment and its clusters to meet your HA goals.

The server configurations available in the solution meet or exceed the minimum requirements to install, configure, and manage vSphere® ESXi™. The {{site.data.keyword.cloud_notm}} bare metal server for VPC on {{site.data.keyword.vpc_short}} uses second Generation Intel® Xeon® Platinum 8260 processors.

Various configurations for CPU, RAM, and storage are available to satisfy different requirements. These predefined configurations are called profiles, for example `bx2d-metal-192x768`. The following information describes the naming rule of the profiles:

* **b** represents a Balanced family profile.
* **x** represents the x86_64 CPU architecture.
* **2** represents the current generation of processors (Cascade Lake).
* **d** represents NVMe U.2 SSDs.
* The field between the two hyphen (-) characters is "metal" for {{site.data.keyword.cloud_notm}} bare metal server.
* The field after the second hyphen (-) contains information about the number of vCPU and the memory size (in GB). For example, "192x768" means that this profile has 192 vCPU and a memory of 768 GB.

The previous example shows a **Balanced bare metal** profile with **192 vCPU** and **768 GB memory**. The profile has the **Cascade Lake processors** and **NVMe U.2 SSDs for additional storage**. For a detailed listing of available profiles with their specifications for the VMware {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}}, see the [x86-64 bare metal server profiles](/docs/vpc?topic=vpc-bare-metal-servers-profile&interface=ui).

Each bare metal server for {{site.data.keyword.vpc_short}} is located in the {{site.data.keyword.vpc_short}} in {{site.data.keyword.cloud_notm}} multizone region in a specified zone.
{: note}

## Physical network design
{: #vpc-ryo-infrastructure-physical-net}

Physical networking is provided by {{site.data.keyword.vpc_short}}. Each bare metal server for VPC provides full support for VPC networking capabilities and features. The VPC network is fully software-defined, so you can configure it through the GUI, CLI, API, or by using {{site.data.keyword.cloud_notm}} Terraform provider.

## Physical network segmentation
{: #vpc-ryo-infrastructure-physical-net-segment}

The VMkernel networking in VMware provides connectivity to hosts, and handles the standard system traffic of vSphere vMotion, IP storage, Fault Tolerance, vSAN™, and others. It is recommended to take appropriate security measures to prevent unauthorized access to the management and system traffic in your vSphere environment. In {{site.data.keyword.vpc_short}}, you can do logical segmentation or isolation in many ways. The built-in capabilities in VPC and the bare metal server network interfaces are used to secure VMkernel networking by following the VMware best practices.

## {{site.data.keyword.cloud_notm}} bare metal server network interfaces
{: #vpc-ryo-infrastructure-physical-net-nics}

The {{site.data.keyword.cloud_notm}} bare metal server and the VMware workloads that are hosted on the bare metal server can connect with {{site.data.keyword.cloud_notm}} virtual server instances on the VPC. The {{site.data.keyword.cloud_notm}} bare metal server for VPC supports vMotion (for live migration of instances between ESXi hosts), IP failover capabilities and the use of VMware vSphere Distributed Resource Scheduler (DRS).

The {{site.data.keyword.cloud_notm}} bare metal server in {{site.data.keyword.vpc_short}} uses SmartNICs. Each physical host has a redundant 100 Gb network connection for network access to {{site.data.keyword.vpc_short}}. The high availability for physical network connectivity is handled by {{site.data.keyword.cloud_notm}}, and you do not have to configure anything additional. The 100 Gb bandwidth is shared by the network interfaces that are configured and currently active on the bare metal server.

A network interface in a bare metal server is an abstract representation of a network interface card, and a network interface connects a bare metal server to a VPC subnet.

In {{site.data.keyword.vpc_short}}, you can create two types of network interfaces on a bare metal server.

* **PCI (Peripheral Component Interconnect) interface** represents a physical network interface. It is possible to include up to 8 PCI interfaces on a bare metal server.
* **VLAN (Virtual LAN) interface** represents an interface that is associated with a PCI interface through the VLAN ID. The VLAN interface automatically tags traffic that is routed through it with the VLAN ID. Inbound traffic that is tagged with a VLAN ID is directed to the appropriate VLAN interface. You can have as many VLAN interfaces as you want.

In a VMware solution, PCI interface is used as the vSwitch uplink and as a management VMkernel adapter. An important difference between PCI interfaces and VLAN interfaces is that a VLAN interface can be set to `floatable`. The key function of the VMware workloads requires vMotion between the {{site.data.keyword.cloud_notm}} bare metal server. This capability is used with VMware management workloads such as vCenter® or NSX® managers to allow them to be moved between hosts for high availability (HA) or distributed resource scheduler (DRS).

In this architecture, VLAN interfaces are used in many ways:

* For VMkernel adapters, such as vMotion, vSAN, and NSX-T™ TEPs.
* For VMware management appliances, such as vCenter and NSX-T managers.
* For VMware virtual machines (VMs) attached to VPC subnets.

Both PCI and VLAN interfaces can be attached to a VPC security group, and security group rules can be applied to these interfaces. Also, VPC ACLs can be used to control inbound and outbound traffic for a subnet to which these PCI and VLAN interfaces are attached.

For more information about the networking concepts, see [Networking overview for Bare Metal Servers on VPC](/docs/vpc?topic=vpc-bare-metal-servers-network).

## Storage design
{: #vpc-ryo-infrastructure-physical-storage}

Physical storage design consists of configuring the disks that are locally attached to the {{site.data.keyword.cloud_notm}} bare metal server and configuring the shared network-attached storage.

The disks attached to the physical hosts include the operating system (vSphere ESXi) and a variable number of extra disks. These SSDs can be used, for example, to virtualize storage with VMware vSAN, with which you can create a software-defined virtual storage of these locally attached SSDs.

With this architecture, you can use either VMware vSAN or shared network-attached storage that is provided by {{site.data.keyword.vpc_short}} as the data store options for the hosted VMs. While shared storage for VMs isn't a prerequisite for VMware environments, a shared storage device provides many benefits for IT operations. Using shared storage devices can help you achieve high availability, distributed resource scheduler, efficient use of storage capacity, and simplified management through enabling the vSphere functions.

### Operating system disks
{: #vpc-ryo-infrastructure-physical-storage-os}

The vSphere ESXi hypervisor is installed in a persistent location in {{site.data.keyword.vpc_short}}. Each bare metal server or ESXi host employs at minimum two locally attached SATA M.2 mirrored drives that are allocated to the vSphere ESXi hypervisor.

You do not need to configure RAID for M.2 mirrored drives. The configuration is provided as part of the bare metal server provisioning.
{: note}

### vSAN disks
{: #vpc-ryo-infrastructure-physical-storage-vsan}

When provisioning a server for vSAN, select it from a profile, which includes the additional U.2 NVMe SSDs to match the required vSAN storage size.

When provisioning a server, you can select it from multiple profiles with a variable number of U.2 NVMe SSDs required for vSAN building.
{: note}

When you configure vSAN, depending on the bare metal server profile and included SSDs, you can use one or more vSAN disk groups, with one solid-state disk (SSD) for cache and one or more SSDs for capacity.

For more information about vSAN design, see [Virtual infrastructure design](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-infrastructure-virtual).

### Shared file-level storage across hosts
{: #vpc-ryo-infrastructure-physical-storage-shared}

The {{site.data.keyword.filestorage_vpc_full_notm}} is a zonal file storage offering that provides NFS-based file storage services for VPC customers. File shares are created in an availability zone within a region. They can be shared with multiple server instances within the same zone across multiple VPCs.

The network attached storage for this architecture is limited to the {{site.data.keyword.vpc_short}} storage, which is available in the same {{site.data.keyword.vpc_short}} zone as the {{site.data.keyword.cloud_notm}} bare metal server.
{: note}

If you choose to use this {{site.data.keyword.filestorage_vpc_full_notm}}, you can attach an NFS share to your selected ESXi hosts and VMware clusters. This share can be used for management components such as vCenter Server, VMware NSX-T managers and NSX-T edge nodes, or for other VMware workloads and VMs.

These file shares are accessible only within the zone in which you created them, for example `us-south-1`. They are identified by name and associated with a resource group in your {{site.data.keyword.cloud_notm}} customer account.

You have two options for creating file shares, by using an IOPS tier profile or by using a custom IOPS profile.

IOPS tiers provide a guaranteed level of performance for your workloads. You can select from three tiers:

* 3 IOPS/GB
* 5 IOPS/GB
* 10 IOPS/GB

With custom IOPS profiles, you can choose the performance that you want, by selecting custom allocated I/O operations per second (IOPS). You can increase the file share size from its original capacity in GB increments up to 32,000 GB capacity, depending on your file share profile.

The storage is attached by using the NFS v4.1 protocol to your hosts. To create an NFS mount path, you need to create mount targets. A mount target for a file share is a network endpoint or path. When you create a mount target, an NFS mount path is created for the file share. You can create a mount target by providing a VPC or subnet information. If you want to connect a file share to instances that are running in multiple VPCs in the same zone, you can create multiple mount targets for different VPCs.

For more information about the shared storage, see [About {{site.data.keyword.filestorage_vpc_short}}](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui).

## Related links
{: #vpc-ryo-infrastructure-physical-links}

* [Getting started with Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-getting-started)
* [Planning for Bare Metal Servers on VPC](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [Architecture overview of roll-your-own VMware solution on VPC](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [Getting started with {{site.data.keyword.cloud_notm}} Direct Link](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [Getting started with {{site.data.keyword.cloud_notm}} Transit Gateway](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
