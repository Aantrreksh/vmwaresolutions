---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-03"

keywords: vmware cloud foundation BOM, bill of materials vmware cloud foundation, BOM

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.vcf-vpc-short}} BOM
{: #vpc-vcf-ovw-bom}

Review the Bill of Materials (BOM) information for {{site.data.keyword.vcf-vpc}} instances.

## VPC Infrastructure BOM for {{site.data.keyword.vcf-vpc-short}}
{: #vpc-vcf-ovw-bom-vpc}

Review the BOM information for Bare Metal Servers on {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}).

| Type | Details |
| ---- | ------- |
| Bare Metal Servers | Provides compute capacity, a minimum of 4 hosts for the consolidated architecture, and a minimum of 7 hosts for the standard architecture. |
| VLANs | Assigned to physical VMware ESXi servers for traffic of VMware vSphere management, VMware vSAN, vSphere vMotion, and VMware NSX TEP. |
| Subnets | Created for vSphere management traffic, vSAN, vSphere vMotion, NSX TEP, and NSX-T Tier-0 Gateway. |
| Security Groups | To create logical groups and apply rules to traffic of vSphere management, vSAN, vSphere vMotion, and NSX TEP. |
| Virtual Server Instances | Optional. Windows Server 2019 Standard Edition (AMD64), 2 vCPU, 8 GB RAM, and a bandwidth cap of 4 Gbps. |
{: caption="Table 1. BOM for {{site.data.keyword.vpc_short}} infrastructure in {{site.data.keyword.vcf-vpc-short}} instances" caption-side="bottom"}

## Software BOM for {{site.data.keyword.vcf-vpc-short}}
{: #vpc-vcf-ovw-bom-software}

Review the BOM information for {{site.data.keyword.vcf-vpc-short}} software components.

| Component | Version | Build number |
| --------- | ------- | ------------ |
| Cloud Builder VM | 4.5.2 | 22223457 |
| SDDC Manager | 4.5.2 | 22223457 |
| VMware vCenter Server Appliance | 7.0 Update 3o | 22357613 |
| VMware ESXi | 7.0 Update 3p | 23307199 |
| VMware Virtual SAN Witness Appliance | 7.0 Update 3l | 21424296 |
| VMware NSX-T | 3.2.3.1 | 22104592 |
| VMware Aria® Suite Lifecycle Manager | 8.12.0.9 | 22652426 |
{: caption="Table 2. BOM for software components in {{site.data.keyword.vcf-vpc-short}} instances" caption-side="bottom"}

## Network MTU configuration settings
{: #vpc-vcf-ovw-bom-mtu-config}

The vSphere cluster has a single vSphere Distributed Switches (vDS) for public and for private network connectivity.

The private network connections are configured to use Jumbo Frames MTU (Maximum Transmission Unit) with a size of 9000 (when applicable), which improves performance for large data transfers such as storage and vMotion. This value is the maximum MTU allowed within VMware and by {{site.data.keyword.cloud_notm}}.

The public network connections use a standard Ethernet MTU of 1500, which must be maintained. Any changes might cause packet fragmentation over the internet.

Review the following table for an overview of the Network MTU configuration settings that are applied to the Virtual Distributed Switch, VMkernel adapters, and NSX Tier 0 uplinks.

| Configuration setting | Value |
| --------------------- | ----- |
| Virtual Distributed Switch | 9000 (Jumbo Frames) |
| VMkernel adapters for management | 1500 (Default) |
| VMkernel adapters for VSAN | 9000 (Jumbo Frames) |
| VMkernel adapters for vMotion | 9000 (Jumbo Frames) |
| VMkernel adapters for TEP traffic | 9000 (Jumbo Frames) |
| Tier 0 private uplinks | 9000 (Jumbo Frames) |
| Tier 0 public uplinks | 1500 (Default) |
{: caption="Table 3. MTU configuration settings for {{site.data.keyword.vcf-vpc-short}}" caption-side="bottom"}

NSX Global Gateway Configuration is set to MTU of 1500 for the router links and interfaces at the overlay.

## Related links
{: #vpc-vcf-ovw-bom-links}

* [{{site.data.keyword.vcf-vpc-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw)
* [Planning for {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-plan)
