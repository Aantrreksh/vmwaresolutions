---

copyright:

  years:  2022, 2024

lastupdated: "2023-01-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Virtual infrastructure design
{: #vpc-ryo-infrastructure-virtual}

The virtual infrastructure layer includes the VMware® software components that virtualize the compute, storage, and network resources provided in the physical infrastructure layer, such as VMware vSphere® ESXi™, VMware NSX-T™, and optionally VMware vSAN™. As with the roll-your-own VMware solution in VPC, you are responsible for configuring the virtual layer based on your needs.

![Virtual infrastructure](../../images/vpc-ryo-diagrams-overview-virtual.svg "Virtual infrastructure"){: caption="Figure 1. Virtual infrastructure" caption-side="bottom"}

## VMware vSphere design
{: #vpc-ryo-infrastructure-virtual-vsphere-design}

The vSphere ESXi configuration consists of the following aspects:

* Boot configuration
* Time synchronization
* Host access
* User access
* DNS configuration

The {{site.data.keyword.cloud}} bare metal server for {{site.data.keyword.vpc_short}} with ESXi includes a default configuration, for example, hostname, DNS, and NTP. With the {{site.data.keyword.cloud_notm}} bare metal servers boot configuration ([user data](/vpc?topic=vpc-user-data)), you can settle these configurations based on your preference. This design uses {{site.data.keyword.cloud_notm}} DNS service, and the IP addresses are configured automatically. Also, time synchronization uses {{site.data.keyword.cloud_notm}} NTP, which is automatically set. Although Secure Shell (SSH) and ESXi Shell are useful for provisioning and using various automation tools, they must be disabled after provisioning as a best practice.

With this design, you can manage the ESXi hosts through vSphere Web Client. The first thing to be done after the initial provisioning of your first {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} with ESXi is to deploy vCenter® Server.

Then, your vCenter Server is deployed and initially configured for the data center and cluster settings. You must add the {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} with ESXi to your vCenter Server and configure and manage them from there.

The vSphere cluster is located in the virtual machines (VMs) that manage the vCenter Server instance and the compute resources for user workloads.

* When your roll-your-own VMware solution in VPC uses vSAN, it is recommended that the minimum number of ESXi hosts in the initial deployment be four.
* When your roll-your-own VMware solution in VPC uses shared file–level storage, the minimum number of ESXi hosts in the initial deployment is two.

You can design your clusters and their sizes based on your need, and use VMware for best practices.

To support more user workloads, you can scale the environment by taking the following actions:

* Deploying more compute hosts of a same profile in your existing clusters.
* Deploying more compute hosts with same or different profile to be managed by the same vCenter appliance.
* Deploying new set of hosts and cluster in your {{site.data.keyword.vpc_short}}, but to another zone within the multizone region with a new vCenter Server appliance.

## VMware vSAN design
{: #vpc-ryo-infrastructure-virtual-vsan-design}

The VMware vSAN is a distributed layer of software that runs natively as a part of the ESXi hypervisor. It aggregates local or direct-attached capacity devices of a host cluster and creates a single storage pool that is shared across all hosts in the vSAN cluster. The VMware features that require shared storage, such as HA, vMotion, DRS, and vSAN eliminate the need for external shared storage. They also simplify storage configuration and virtual machine provisioning activities. However, if needed, you can combine these functions with {{site.data.keyword.vpc_short}} provided storage solutions.

Within vSAN design, the compute nodes contain local disk drives for the ESXi operating system (OS) and extra disk drives for the vSAN data store. In every bare metal server, two M.2 SSD mirrored drives are included in each node to house the ESXi installation, regardless of which type of cluster the host belongs to. The {{site.data.keyword.cloud_notm}} bare metal server profiles with letter `d` represent a number of additional attached NVMe U.2 SSDs, which can be used for vSAN.

With vSAN, you must specify each host and each device to be used for the vSAN data store. You can organize cache and capacity devices into disk groups. Each disk group contains one flash cache device and one or more capacity devices. When you create a disk group, consider the ratio of flash cache to used capacity. The ratio depends on the requirements and workload of the cluster. For more information about disk groups, see [Managing disk groups and devices](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vsan.doc/GUID-88790522-2FA0-476F-B874-6FE4E8E5B908.html){: external}. For more information about determining the cache ratio for all-flash clusters, see [Understanding vSAN architecture: disk groups](https://blogs.vmware.com/virtualblocks/2019/04/18/vsan-disk-groups/){: external}.

vSAN can be employed as follows:

* One or two-disk group vSAN designs.
* Each disk group with two or more disks.
* One NVMe drive in the group serves as the cache tier and the remaining SSDs serve as the capacity tier.
* A single vSAN data store is created from all storage.

The available vSAN features depend on the license edition that you select when you order the instance. For more information, see [VMware vSAN edition comparison](/docs/vmwaresolutions?topic=vmwaresolutions-solution-appendix#solution-appendix-vsan-editions).

### Virtual network setup for vSAN
{: #vpc-ryo-infrastructure-virtual-net-setup}

In this reference design, the vSAN traffic traverses between ESXi hosts on a dedicated VPC subnet. The PCI network adapter attached to the {{site.data.keyword.cloud_notm}} bare metal server is configured within vSphere as a vSphere Distributed Switch (vDS) with the network adapters as uplink. A dedicated vSAN kernel port group is configured for the vSAN VPC subnet and is located within the vDS. Jumbo frames (MTU 9000) are enabled for the private vDS.

vSAN does not load balance traffic across uplinks. High availability (HA) for the uplink is provided by the SmartNIC.
{: note}

For more information about physical NIC connections, see [Networking overview for {{site.data.keyword.cloud_notm}} Bare Metal Servers on VPC](/vpc?topic=vpc-bare-metal-servers-network&interface=ui).

### vSAN storage policy
{: #vpc-ryo-infrastructure-virtual-storage-policy}

When vSAN is enabled and configured, storage policies are configured to define the VM storage characteristics. Storage characteristics specify different levels of service for different VMs. With the roll-your-own VMware solution in VPC, you are responsible for configuring the storage policies based on your needs.

The default storage policy in this design tolerates a single failure. It is configured with erasure coding, with the Failure tolerance method set to RAID-5/6 (Erasure Coding) - Capacity and Primary level of failures set to 1. The RAID 5 configuration requires a minimum of four hosts.

Alternatively, you can choose the RAID 6 configuration with Failure tolerance method set to RAID-5/6 (Erasure Coding) - Capacity and Primary level of failures set to 2. The RAID 6 configuration requires a minimum of six hosts. Deduplication and compression are normally enabled in the default storage policy but can be disabled if needed.

An vSAN uses the default policy unless otherwise specified from the vSphere console. When a custom policy is configured, vSAN guarantees it when possible. However, if the policy cannot be guaranteed, it is not possible to provision a VM that uses the policy unless it is enabled to force provisioning.

Storage policies must be reapplied after adding new ESXi hosts or patching ESXi hosts.

### vSAN storage settings
{: #vpc-ryo-infrastructure-virtual-vsan-sett}

vSAN settings are configured based on best practices for deploying VMware solutions within {{site.data.keyword.cloud_notm}}. The vSAN configuration includes storage IO Control (SIOC) settings, explicit failover settings port group, and disk cache settings. With the roll-your-own VMware solution in VPC, you are responsible for configuring the storage policies based on your needs.

The following list includes an example design:

* SSD cache policy settings - No Read Ahead, Write Through, Direct (NRWTD)
* Network I/O control settings
   * Management - 20 shares
   * Virtual machine - 30 shares
   * vMotion - 50 shares
   * vSAN - 100 shares
* vSAN kernel ports - Explicit Failover

## NFS attached storage
{: #vpc-ryo-infrastructure-virtual-nfs-storage}

As described in [Shared file-level storage across hosts](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-infrastructure-physical#vpc-ryo-infrastructure-physical-storage-shared), {{site.data.keyword.filestorage_vpc_full_notm}} is a zonal file storage offering that provides NFS-based file storage services for VPC customers. File shares are created in an availability zone within a region. They can be shared with multiple server instances within the same zone across multiple VPCs.

If you choose to use this {{site.data.keyword.filestorage_vpc_full_notm}}, you can attach an NFS share to your selected hosts and VMware clusters. This share can be used for management components such as vCenter Server, VMware NSX-T managers, and NSX-T edge nodes. More data stores can be attached to a cluster for workload use, in various sizes and performance tiers.

The storage is attached by using the NFS v4.1 protocol to your hosts. To create an NFS mount path, you must create mount targets. A mount target for a file share is a network endpoint or path. When you create a mount target, an NFS mount path is created for the file share. You can create a mount target by providing a VPC or subnet information. If you want to connect a file share to instances that are running in multiple VPCs in the same zone, you can create multiple mount targets for different VPCs.

For more information about the shared storage, see [About {{site.data.keyword.filestorage_vpc_short}}](/docs/vpc?topic=vpc-file-storage-vpc-about&interface=ui).

Additionally, this architecture currently uses management `vmk` that hosts have for all NFS traffic for simplicity.

## Related links
{: #vpc-ryo-infrastructure-virtual-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
