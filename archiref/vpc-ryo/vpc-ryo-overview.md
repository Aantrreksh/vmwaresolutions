---

copyright:

  years:  2022, 2023

lastupdated: "2023-08-17"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Overview of roll-your-own VMware solution on VPC
{: #vpc-ryo-overview}

The {{site.data.keyword.vmwaresolutions_full}} offerings help you extend your existing VMware® virtualized data center into {{site.data.keyword.cloud_notm}}. The {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} provides you compute capacity to host VMware workloads in the {{site.data.keyword.vpc_short}}.

With this solution, you have the flexibility to design a VMware deployment for your needs, which is integrated with {{site.data.keyword.vpc_short}}. The following diagram shows an overview of the solution.

![Overview of VMware on {{site.data.keyword.vpc_short}}](../../images/vpc-ryo-diagrams-overview.svg "The solution virtualizes compute, network, and optionally storage resources to be used by VMs where you can run your applications."){: caption="Figure 1. Overview of VMware on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

The {{site.data.keyword.cloud_notm}} bare metal server is integrated with the VPC network, and you can take advantage of the network, storage, and security capabilities provided by {{site.data.keyword.vpc_short}}. Use VMware vSAN™ for storage and VMware NSX-T™ for network capabilities. You can easily and quickly add and remove ESXi hosts. Also, add, configure, and remove VMware vSphere® clusters as you like. If your storage needs grow, you can add and attach {{site.data.keyword.vpc_short}} file shares.

After the bare metal server provisioning and initial VMware configurations, you can access and manage the IBM-hosted environment. To do this step, you can use VMware clients, command line interface (CLI), existing scripts, or other familiar vSphere API-compatible tools. These options can be combined with {{site.data.keyword.cloud_notm}} automation solutions, such as using {{site.data.keyword.cloud_notm}} Terraform provider with Schematics.

For the required common services, such as NTP and DNS, you can use {{site.data.keyword.vpc_short}} basic services and solutions. For Active Directory™, you can use {{site.data.keyword.vpc_short}} compute resources to build your Active Directory in {{site.data.keyword.vpc_short}}, or interconnect with your existing Active Directory infrastructure.

For connectivity needs, you can use {{site.data.keyword.vpc_short}} and {{site.data.keyword.cloud_notm}} interconnectivity solutions. For public internet network access capabilities, the options include floating IP addresses and Public Gateway configurations within your VPC.

On-premises connectivity over public internet can be arranged by using {{site.data.keyword.vpc_short}} VPN services (site-to-site and client-to-site), or alternatively NSX-T built-in capabilities. For private networking, you can use {{site.data.keyword.cloud_notm}} interconnectivity services to connect your VMware workloads with {{site.data.keyword.cloud_notm}} classic infrastructure, other VPCs, and on-premises networks.

## Key responsibilities
{: #vpc-ryo-overview-responsibilities}

With the roll-your-own VMware Solutions in {{site.data.keyword.vpc_short}}, you are responsible for ordering the VPC, prefixes, and subnets for it. Also, ordering the {{site.data.keyword.cloud_notm}} bare metal server and setting up the vSphere clusters, including installing and configuring VMware vCenter Server®, vSAN, NSX-T, attaching file storage.

The {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} has the VMware ESXi™ 7.x hypervisor preinstalled.

For day two of operation, it is your responsibility to monitor and manage the vCenter and NSX-T, including backups, patching, configuration, and monitoring of the VMware software and the underlying vSphere hypervisor.

## Key benefits
{: #vpc-ryo-overview-benefits}

The architecture provides fundamental building blocks, which include VMware vSphere, vCenter Server, VMware NSX-T, and shared storage options, such as VMware vSAN or {{site.data.keyword.vpc_short}} file share. These building blocks are needed to flexibly design a VMware software-defined data center solution that best fits your workloads.

VMware Solutions in {{site.data.keyword.vpc_short}} have the following key benefits over {{site.data.keyword.cloud_notm}} classic deployments:

* {{site.data.keyword.vpc_short}} gives you the ability to easily and rapidly define and control a virtual network, which is logically isolated from all other tenants. The logical isolation is implemented by using virtual network functions and security that is built into the platform.
* Provisioning the {{site.data.keyword.cloud_notm}} bare metal server on {{site.data.keyword.vpc_short}} takes minutes instead of hours when compared to the {{site.data.keyword.cloud_notm}} bare metal server on {{site.data.keyword.cloud_notm}} classic.
* VMware workloads by running in {{site.data.keyword.vpc_short}} can take advantage of all original functions for VPC networking capabilities and other {{site.data.keyword.cloud_notm}} interconnectivity services.

With this single-tenant {{site.data.keyword.cloud_notm}} bare metal server infrastructure that is provided in {{site.data.keyword.vpc_short}}, you can quickly deploy network, compute, and storage capacity for your VMware environment to the {{site.data.keyword.cloud_notm}} in minutes.

Unlike the managed service offerings, this architecture gives you flexibility to design a solution for your needs, and provides you full and complete access to all components.

## Related links
{: #vpc-ryo-overview-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
