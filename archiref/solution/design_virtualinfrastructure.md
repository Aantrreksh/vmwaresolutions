---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-31"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Virtual infrastructure design
{: #design_virtualinfrastructure}

The virtual infrastructure layer includes the VMware® software components that virtualize the compute, storage, and network resources provided in the physical infrastructure layer: VMware vSphere ESXi®, VMware NSX-T™, and optionally VMware vSAN™.

![Virtual infrastructure](../../images/nsx-t-3-ra-diagrams-virtual-infrastructure.svg "Virtual infrastructure"){: caption="Figure 1. Virtual infrastructure" caption-side="bottom"}

## VMware vSphere design
{: #design_virtualinfrastructure-vsphere-design}

The vSphere ESXi configuration consists of the following aspects:
* Boot configuration
* Time synchronization
* Host access
* User access
* DNS configuration

The following table outlines the specifications for each aspect. After the configuration and installation of ESXi, the host is added to a VMware vCenter Server® and is managed from there.

With this design, you can access the virtual hosts through Direct Console User Interface (DCUI) and vSphere Web Client. Secure Shell (SSH) and ESXi Shell are disabled after provisioning as a best practice.

By default, the only users who can log in directly are the _root_ and _ibmvmadmin_ users for the physical machine of the host. The administrator can add users from the Microsoft® Active Directory™ (MSAD) domain to enable user access to the host. All hosts in the {{site.data.keyword.vcf-auto}} solution design are configured to synchronize with a central NTP server.

| Attribute              | Configuration parameter |
|:---------------------- |:----------------------- |
| ESXi boot location     | Different host configurations might be deployed with: \n * Local disks configured with RAID-1 \n * A pair of M.2 boot drives in a mirrored configuration \n * A single M.2 boot drive |
| Time synchronization   | Uses {{site.data.keyword.cloud}} NTP server |
| Host access            | Supports DCUI. SSH and ESXi Shell are supported but not enabled by default |
| User access            | Local authentication and MSAD |
| Domain name resolution | Uses DNS as described in [Common services design](/docs/vmwaresolutions?topic=vmwaresolutions-design_commonservice). |
| EVC Mode | Highest available level supported by vSphere version. However, for a management cluster with Intel® Cascade Lake processors, no EVC is set where Cascade Lake EVC is not supported by the vSphere version. |
{: caption="Table 1. vSphere ESXi configuration" caption-side="bottom"}

The vSphere cluster houses the virtual machines (VMs) that manage the {{site.data.keyword.vcf-auto}} instance and the compute resources for user workloads.

* When a {{site.data.keyword.vcf-auto}} instance uses vSAN, the minimum number of ESXi hosts at initial deployment is four.
* When a {{site.data.keyword.vcf-auto}} instance uses shared file–level or block-level storage, the minimum number of ESXi hosts at initial deployment is three.

You can deploy up to 20 ESXi hosts in this cluster during initial deployment. After initial deployment, you can scale the cluster up to a maximum of 50 hosts in increments of up to 20 hosts at a time.

To support more user workloads, you can scale the environment by taking the following actions:
* Deploying more compute hosts in existing clusters.
* Deploying more clusters that are managed by the same vCenter Server appliance.
* Deploying new {{site.data.keyword.vcf-auto}} instances with their own vCenter Server appliance.

## VMware vSAN design
{: #design_virtualinfrastructure-vsan-design}

In this design, VMware vSAN storage is employed in {{site.data.keyword.vcf-auto}} instances to provide shared storage for the vSphere hosts.

As shown in the following figure, vSAN aggregates the local storage across multiple ESXi hosts within a vSphere cluster and manages the aggregated storage as a single VM datastore. Within this design, the compute nodes contain local disk drives for the ESXi operating system (OS) and the vSAN datastore. 

Different host configurations might be deployed with:
* local disks configured with RAID-1
* a pair of M.2 boot drives in a mirrored configuration
* a single M.2 boot drive

![vSAN concept](../../images/vcsv4radiagrams-ra-vsan.svg "vSAN aggregates the local storage across multiple ESXi hosts within a vSphere cluster and manages the aggregated storage as a single VM datastore"){: caption="Figure 2. vSAN concept" caption-side="bottom"}

vSAN employs the following components:
* Two-disk group vSAN design; each disk group with two or more disks. One SSD or NVMe drive of the smallest size in the group serves as the cache tier and the remaining SSDs serve as the capacity tier.
* The onboard RAID controller is configured in a RAID 0 array for each individual drive that is used for vSAN cache or capacity.
* A single vSAN datastore is created from all storage.

### Virtual network setup for vSAN
{: #design_virtualinfrastructure-net-setup}

For this design, the vSAN traffic traverses between ESXi hosts on a dedicated private VLAN. The two network adapters attached to the private network switch are configured within vSphere as a vSphere Distributed Switch (vDS) with both network adapters as uplinks. A dedicated vSAN kernel port group that is configured for the vSAN VLAN resides within the vDS. Jumbo frames (MTU 9000) are enabled for the private vDS.

vSAN does not load balance traffic across uplinks. As a result, one adapter is active while the other is in standby to support high availability (HA). The network failover policy for vSAN is configured as **Explicit Failover** between physical network ports.

For more information about physical NIC connections, see [Physical host NIC connections](/docs/vmwaresolutions?topic=vmwaresolutions-design_physicalinfrastructure#design_physicalinfrastructure-host-connect).

### vSAN policy design
{: #design_virtualinfrastructure-storage-policy}

When vSAN is enabled and configured, storage policies are configured to define the VM storage characteristics. Storage characteristics specify different levels of service for different VMs.

The default storage policy in this design tolerates a single failure. The default policy is configured with erasure coding, with **Failure tolerance method** set to **RAID-5/6 (Erasure Coding) - Capacity** and **Primary level of failures** set to 1. The RAID 5 configuration requires a minimum of four hosts.

Alternatively, you can choose the RAID 6 configuration with **Failure tolerance method** set to **RAID-5/6 (Erasure Coding) - Capacity** and **Primary level of failures** set to 2. The RAID 6 configuration requires a minimum of six hosts. **Deduplication** and **compression** are normally enabled in the default storage policy but can be disabled if needed.

An instance uses the default policy unless otherwise specified from the vSphere console. When a custom policy is configured, vSAN guarantees it when possible. However, if the policy can't be guaranteed, it's not possible to provision a VM that uses the policy unless it is enabled to force provisioning.

Storage policies must be reapplied after addition of new ESXi hosts or patching of the ESXi hosts.

### vSAN settings
{: #design_virtualinfrastructure-vsan-sett}

vSAN settings are configured based on best practices for deploying VMware solutions within {{site.data.keyword.cloud_notm}}. The vSAN settings include SIOC settings, explicit failover settings port group, and disk cache settings.

* SSD cache policy settings - No **Read Ahead**, **Write Through**, **Direct** (NRWTD)
* Network I/O control settings
   * Management - 20 shares
   * Virtual machine - 30 shares
   * vMotion - 50 shares
   * vSAN - 100 shares
* vSAN kernel ports - **Explicit Failover**

## NFS attached storage
{: #design_virtualinfrastructure-nfs-storage}

NFS server LIF migrations might cause excessive latency when they use NFS v4.1. When you use NFS network-attached storage, this architecture prescribes the use of NFS v3 rather than NFS v4.1. Each vSphere host is connected to the NFS storage by using its hostname.

One 2-TB NFS data store is attached to a cluster for use by management components with a performance tier of 4 IOPS/GB. More data stores can be attached to a cluster for workload use, at various sizes and performance tiers.

Additionally, this architecture requires that all hosts have a subnet route that is created for the subnet where the NFS storage resides. The purpose of this subnet route is to direct all NFS traffic to use the port group, subnet, and VLAN designated for NFS traffic by this design. If multiple NFS data stores are attached, multiple routes might be required to be configured since those data stores might be located in different remote subnets.

Management virtual machines can be located on an NFS data store. This approach creates a bootstrapping problem since some of the management machines might be responsible for DNS services, which are used to resolve the NFS hostname. Therefore, this architecture specifies that at least one of the IP addresses for the management data store to be hardcoded in `/etc/hosts` on each of the hosts.

## Related links
{: #design_virtualinfrastructure-related}

* [VMware NSX-T design](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design)
