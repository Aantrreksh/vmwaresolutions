---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-19"

keywords: vCenter Server Hybridity, hybridity, tech specs vCenter Server Hybridity

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# vCenter Server with Hybridity Bundle overview
{: #vc_hybrid_overview}

The VMware vCenter Server® with Hybridity Bundle is not supported for new installations. Instead, deploy the standard vCenter Server instance with the Hybrid Cloud Extension (HCX™) service.
{: deprecated}

The vCenter Server with Hybridity Bundle is a hosted private cloud that delivers the VMware vSphere® stack as a service. The VMware environment is built on top of a minimum of four {{site.data.keyword.cloud}} bare metal servers, includes VMware vSAN™ as dedicated storage, provides automatic deployment and configuration of an easy-to-manage logical edge firewall that is powered by VMware NSX®, and includes the HCX service.

The bare metal infrastructure can rapidly and elastically scale the compute capacity up and down as needed. To increase the vSAN-based storage capacity of a vSAN cluster, you can add more VMware ESXi™ servers to your instance.

You can upgrade the VMware NSX Advanced edition to the Enterprise edition, and you can purchase more VMware components, such as VMware Aria® Operations™.

You can add IBM-managed services if you want to offload the day-to-day operations and maintenance of the virtualization, guest OS, or application layers. The {{site.data.keyword.cloud_notm}} Professional Services team is also available to help you accelerate your journey to the cloud with migration, implementation, planning, and onboarding services.

## vCenter Server with Hybridity Bundle architecture
{: #vc_hybrid_overview-archi}

The following graphic depicts the high-level architecture and components of a three-node vCenter Server with Hybridity Bundle deployment.

![vCenter Server with Hybridity Bundle architecture](../images/hybrid_architecture.svg "vCenter Server with Hybridity Bundle architecture"){: caption="Figure 1. vCenter Server with Hybridity Bundle high-level architecture" caption-side="bottom"}

### Physical infrastructure
{: #vc_hybrid_overview-physical-infras}

This layer provides the physical infrastructure (compute, storage, and network resources) to be used by the virtual infrastructure.

### Virtualization infrastructure (Compute, Storage, and Network)
{: #vc_hybrid_overview-virtualization-infras}

This layer virtualizes the physical infrastructure through different VMware products:
* VMware vSphere virtualizes the physical compute resources.
* VMware Virtual SAN (vSAN) provides software-defined shared storage, based on the storage in the physical servers.
* VMware NSX is the network virtualization platform that provides logical networking components and virtual networks.

### Virtualization management
{: #vc_hybrid_overview-virtualization-mgmt}

This layer consists of vCenter Server Appliance with embedded Platform Services Controller (PSC), NSX Manager, two VMware NSX Edge™ Services Gateway (ESGs), three VMware NSX Controllers™, and the IBM CloudDriver virtual server instance (VSI). The CloudDriver VSI was deployed on demand as needed for certain operations such as adding hosts to the environment.

The base offering is deployed with a vCenter Server appliance that is sized to support an environment with up to 400 hosts and up to 4000 VMs. The same vSphere API-compatible tools and scripts can be used to manage the IBM-hosted VMware environment.

In total, the base offering requires 38 vCPU and 67 GB vRAM that are reserved for the virtualization management layer. The remaining host capacity for your VMs depends on several factors, such as oversubscription rate, VM sizing, and workload performance requirements.

For more management resource requirements when you deploy the HCX service, see [HCX overview](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations#hcx_considerations).

### Infrastructure hybridity
{: #vc_hybrid_overview-infras-hybrid}

This layer provides an abstraction of resources between the on-premises sites and {{site.data.keyword.cloud_notm}} sites so that you can move workloads back and forth securely and easily without the need to change VM characteristics such as their IP addresses.

Based on VMware HCX, you can create loosely coupled interconnects among on-premises and {{site.data.keyword.cloud_notm}} sites to enable bulk migration of VMs or live vMotion of VMs without downtime.

## Technical specifications for vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_overview-specs}

The following components are included in your vCenter Server with Hybridity Bundle instance:

The availability and pricing of standardized hardware configurations might vary based on the {{site.data.keyword.cloud_notm}} data center that is selected for deployment.
{: note}

### Bare metal server
{: #vc_hybrid_overview-bare-metal}

Your instance contains four or more {{site.data.keyword.cloud_notm}} bare metal servers with the server configuration that is selected at initial deployment.

### Networking
{: #vc_hybrid_overview-networking}

Your instance contains the following networking components:
*  10 Gbps dual public and private network uplinks.
*  Three VLANs (Virtual LANs): one public VLAN and two private VLANs.
*  One VXLAN (Virtual eXtensible LAN) with DLR (Distributed Logical Router) for potential east-west communication between local workloads that are connected to layer 2 (L2) networks. The VXLAN is deployed as a sample routing topology, which you can modify, build on it, or remove it. You can also add security zones by attaching more VXLANs to new logical interfaces on the DLR.
*  Two VMware NSX Edge Services Gateways (ESGs):
   * A secure management services ESG for outbound HTTPS management traffic, which is deployed by IBM as part of the management networking typology. This ESG is used by the IBM management VMs to communicate with specific external IBM management components that are related to automation. For more information, see [Configuring your network to use the customer-managed ESG](/docs/vmwaresolutions?topic=vmwaresolutions-vc_esg_config).

   This ESG is not accessible to you and you cannot use it. If you modify it, you might not be able to manage the vCenter Server with Hybridity Bundle instance from the {{site.data.keyword.vmwaresolutions_short}} console. In addition, when you use a firewall or disable the ESG communications to the external IBM management components cause {{site.data.keyword.vmwaresolutions_short}} to become unusable.
    {: important}

   * A secure customer-managed ESG for outbound and inbound HTTPS workload traffic, which is deployed by IBM as a template that can be modified by you to provide VPN access or public access. For more information, see [Does the customer-managed NSX Edge pose a security risk?](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions#faq-customer-nsx)

For more information about networking components that are ordered when you deploy the HCX service, see [HCX overview](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations#hcx_considerations).

### Virtual Server Instances
{: #vc_hybrid_overview-vsi}

Your existing instance contains the following virtual server instances (VSIs):
* A VSI for IBM CloudDriver.
* A single Microsoft® Windows® Server VSI for Microsoft Active Directory™ (AD) or two high availability Microsoft Windows VMs on the management cluster that was chosen at initial deployment.

### vSAN storage
{: #vc_hybrid_overview-vsan-storage}

vSAN storage offers customized configurations, with various options for disk type and quantity:
* Disk quantity: 2, 4, 6, 8, or 10
* Storage disk: 960 GB SSD SED, 1.9 TB SSD SED, or 3.8 TB SSD SED

   In addition, two cache disks of 960 GB are included per host.
* High Performance with Intel® Optane: this option provides two extra capacity disk bays. This option depends on the CPU model.

### IBM-provided licenses and fees
{: #vc_hybrid_overview-license-and-fee}

The following licenses are included in your instance.

* VMware vSphere Enterprise Plus 6.7u3
* VMware NSX Service Providers Edition (Advanced or Enterprise) 6.4
* VMware vSAN (Advanced or Enterprise) 6.6

More support and services fees might apply.

## Technical specifications for vCenter Server with Hybridity Bundle expansion nodes
{: #vc_hybrid_overview-expansion-node-specs}

Each vCenter Server with Hybridity Bundle expansion node deploys and incurs charges for the following components in your {{site.data.keyword.cloud_notm}} account.

### Hardware for expansion nodes
{: #vc_hybrid_overview-expansion-node-hardware}

One bare metal server with the configuration presented in [Technical specifications for vCenter Server with Hybridity Bundle instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_hybrid_overview#vc_hybrid_overview-specs).

### Licenses and fees for expansion nodes
{: #vc_hybrid_overview-expansion-node-license-and-fee}

* One VMware vSphere Enterprise Plus 6.73
* One VMware NSX Service Providers Edition (Advanced or Enterprise) 6.4
* One Support and Services fee
* VMware vSAN (Advanced or Enterprise) 6.6

You must manage the {{site.data.keyword.vmwaresolutions_short}} components that are created in your {{site.data.keyword.cloud_notm}} account only from the {{site.data.keyword.vmwaresolutions_short}} console, not the {{site.data.keyword.slportal}}, or any other means outside of the console. If you change these components outside of the {{site.data.keyword.vmwaresolutions_short}} console, the changes are not synchronized with the console.
{: important}

{{site.data.content.caution-component-management}}

   Exceptions to these activities include managing the shared storage file shares from the {{site.data.keyword.slportal}}. Such activities include: ordering, deleting (which might impact data stores if mounted), authorizing, and mounting shared storage file shares.

## Related links
{: #vc_hybrid_overview-related}

* [vCenter Server BOM](/docs/vmwaresolutions?topic=vmwaresolutions-vc_bom)
* [HCX overview](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations#hcx_considerations)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
