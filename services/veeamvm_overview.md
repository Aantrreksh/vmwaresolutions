---

copyright:

  years:  2020, 2023

lastupdated: "2023-10-06"

keywords: Veeam, Veeam Backup and Replication 12, Veeam install, tech specs Veeam, Veeam overview

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Veeam on {{site.data.keyword.cloud_notm}} overview
{: #veeamvm_overview}

Veeam® on {{site.data.keyword.cloud}} seamlessly integrates directly with your VMware® hypervisors to help your enterprise achieve high availability. This service provides recovery points and time objectives for your applications and data. The recovery points and time objectives can be provided in less than 15 minutes after configuration is completed. 

By using this service, you control both the backup and restore of all virtual machines (VMs) for your infrastructure directly from the Veeam console. Veeam on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from Veeam, not IBM.
{: shortdesc}

{{site.data.content.para-promotion-services}}

The Veeam service that is installed is Veeam Availability Suite™ 12 (known as Veeam 12).
{: note}

If you have Veeam 9.5u4b, you can continue to use it. However, you cannot install Veeam 9.5u4b on a new or existing instance.
{: restriction}

## Veeam on a bare metal server
{: #veeamvm_overview-baremetal-server}

You can install Veeam Backup and Replication 12 on a bare metal server. This installation is supported only for VMware vSphere® 7.0 with VMware NSX-T™.

* For VMware Regulated Workloads, the Veeam bare metal server is the only option. For Security and Compliance Readiness Bundle, the Veeam bare metal server is the default option with a choice of switching to Veeam VM.
* Veeam is always deployed on the management cluster.
* No migration path is available for existing Veeam 9.5u4b users.

For more information about Veeam on bare metal server, see the following topics.

* [Veeam on bare metal server introduction](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-bms-archi-intro)
* [Veeam on bare metal server overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-bms-archi-overview)

## Technical specifications for Veeam
{: #veeamvm_overview-specs}

You can choose one of the following deployment types with Veeam:
* Microsoft Windows® Server VM on the management cluster or the consolidated cluster
* Single Public Windows VSI
* Bare metal server

For more information about resource requirements and capacity checking for some services, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

The following components are ordered and included in the Veeam service.

### VMs for Veeam
{: #veeamvm_overview-specs-vms}

The following components are included if you deploy Veeam as a Windows Server VM on the management cluster:

* VM with Veeam Backup and Replication 12 OS Add-on and Veeam Availability Suite™ 12
* Windows Server 2019 Standard Edition (64-bit)
* 8 CPUs, 32 GB RAM
* 100 GB disk (SAN)

### VSIs for Veeam
{: #veeamvm_overview-specs-vsi}

The following components are included if you deploy Veeam as a single public Windows VSI:

* Single VSI with Veeam Backup and Replication 12 OS Add-on and Veeam Availability Suite 12
* Windows Server 2019 Standard Edition (64-bit)
* 4 x 2.0 GHz Cores
* 8 CPUs, 32 GB RAM
* 1 Gbps private network uplink
* 100 GB disk (SAN)

### Bare metal servers for Veeam
{: #veeamvm_overview-specs-baremetal}

The following components are included if you deploy Veeam on a bare metal server:

* Bare metal server with Veeam Backup and Replication 12 OS Add-on and Veeam Availability Suite 12
* Windows Server 2019 Standard Edition (64-bit)
* 2 x 2.2 GHz CPU
* 64 GB RAM
* 10 Gbps private redundant network uplink
* 2 x 1 TB, RAID 1, OS drive
* 2 x 1 TB, RAID 1, database config drive
* Customizable sizes for backup data drive

### Storage for backups for Veeam
{: #veeamvm_overview-specs-storage}

#### Endurance iSCSI storage (VM or VSI option)
{: #veeamvm_overview-specs-storage-vm-or-vsi}

The following options for storage size are available:
* 2,000 GB
* 4,000 GB
* 8,000 GB
* 12,000 GB

The following options for storage performance (IOPS/GB) are available:
* 0.25
* 2
* 4

#### Local HDD storage (Bare metal server option)
{: #veeamvm_overview-specs-storage-bm-server}

The following options for storage size are available:
* 8 x 2 TB, RAID 6, 12 TB total estimated usable storage
* 8 x 6 TB, RAID 6, 36 TB total estimated usable storage
* 8 x 12 TB, RAID 6, 72 TB total estimated usable storage

#### Repositories created
{: #veeamvm_overview-specs-storage-repositories-created}

As part of the Veeam service installation and configuration, the following repositories are created:
* For the Veeam configuration backup files - a repository named `IC4V Default Config Backup Repository`. The path to the folder where the Veeam backups are stored is `<Drive>:\ConfigBackup\`.
* For scale-out - a repository named `IC4V Scale-Out Repository`. For more information, see [Adding a scale-out repository](/docs/vmwaresolutions?topic=vmwaresolutions-icos_ordering#icos_ordering-scale-repo).
* For the VM backups - a repository named `IC4V Default VM Backup Repository`. The path to the folder where the VM backups are stored is `<Drive>:\VMBackup\`. This repository is added as an extent to `IC4V Scale-Out repository`.

### Linux hardened repository for immutable storage
{: #veeamvm_overview-specs-linux-storage}

When you order Veeam, you can optionally order a Linux hardened repository (LHR). You can use the repository for immutable storage.

* If you order an LHR, an extra bare metal server with Red Hat Enterprise Linux (RHEL) 8.x installed is deployed. The same bare metal hardware is deployed as the Veeam Backup and Replication server.
* The disk options are similar to the Veeam Backup and Replication server. The size options are 2 TB, 6 TB, and 12 TB.
* You can order an LHR for any of the Veeam deployment types: VM, VSI, or bare metal server.
* There is no charge for LHR beyond the cost of the bare metal infrastructure.

See the following information:
* [Cyber recovery with Veeam architecture](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview), which describes two solution architectures to help you with cyber recovery.
* [Cyber recovery with Veeam guide](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-overview), which describes how to create two cyber-recovery solution architectures.
* [Hardened repository](https://helpcenter.veeam.com/docs/backup/vsphere/hardened_repository.html?ver=120){: external} in the Veeam Backup and Replication 12 - User Guide for VMware vSphere.

### Networking for Veeam
{: #veeamvm_overview-specs-networking}

One primary private IP address. Bare metal and VSI options use one primary private IP address. However, the VM option uses one primary portable IP address.

The Veeam® VSI and Veeam bare metal services are not configured with an {{site.data.keyword.cloud_notm}} infrastructure portable IP address or with a NAT connection to the public network, even if you have public interfaces in your instance. This implementation helps to avoid the possibility of asymmetric routing when it uses a network gateway appliance.

When you deploy Veeam as a bare metal server or VSI, you can optionally configure your own proxy or NAT connection to the public network to connect to Veeam support for updates.

When you deploy Veeam as a VM, if your instance has public interfaces, VMware Solutions still creates a NAT connection for Veeam to the public network through the NSX-T services edge.

### Licenses and fees for Veeam
{: #veeamvm_overview-specs-licenses}

For Veeam Availability Suite 12, you can order any number of VM licenses.

If you choose the option to install Veeam as a VM, you must provide a Microsoft® Windows Server 2019 Standard edition license.
{: important}

## Related links
{: #veeamvm_overview-related}

* [Ordering Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering)
* [Managing Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-managingveeam)
* [Ordering Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering_licenses)
* [Managing Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses)
* [Ordering and configuring {{site.data.keyword.cloud_notm}} Object Storage with Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-icos_ordering)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Veeam Backup and Replication](https://www.ibm.com/cloud/architecture/architectures/virtualization_backup_veeam){: external}
* [Veeam Help Center (Technical Documentation)](https://www.veeam.com/documentation-guides-datasheets.html){: external}
