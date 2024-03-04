---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-04"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deployment considerations for the roll-your-own VMware solution on VPC
{: #vpc-ryo-considerations}

Roll-your-own VMware® solution in VPC is not a managed service. You can use {{site.data.keyword.cloud}} services to build your own VMware solution in {{site.data.keyword.vpc_short}}.

You are responsible for the VPC deployment and related networking resources, {{site.data.keyword.cloud_notm}} bare metal server in VPCs and for the deployment, configuration, security, management, and monitoring of all VMware software components. With complete administrative access to the solution, you have great power and flexibility that requires significant technical, administrative, and operational expertise across various domains.

Managing a VMware in the {{site.data.keyword.cloud_notm}} requires the same planning and expertise as planning for an on-premises instance. Software-defined technologies such as VMware NSX-T™ and VMware vSAN™ greatly simplify some aspects of instance management. However, management in {{site.data.keyword.vpc_short}} might require new skills and tools for proper operation. For example, a proper understanding of {{site.data.keyword.cloud_notm}} concepts and {{site.data.keyword.vpc_short}} solutions and services are required.

## Sizing your VMware vSphere clusters
{: #vpc-ryo-considerations-sizing}

A vSphere cluster is typically the boundary of shareable resources for VMware workloads. By definition, a vSphere High Availability (HA) cluster consists of two or more hosts. VMware vSphere® HA protects your virtual machines (VMs) if a VMware ESXi™ host failure occurs by restarting VMs on other hosts in the cluster when an ESXi host fails. When you are planning the sizing for your VMware vSphere clusters in {{site.data.keyword.cloud_notm}} VPC, consider the VMware best practices that are documented in [VMware validated designs](https://core.vmware.com/vmware-validated-solutions){: external} to meet your capacity and high availability targets.

Theoretically, as each {{site.data.keyword.vpc_short}} Bare Metal Server is deployed individually, you can build a solution as small as one ESXi host per {{site.data.keyword.vpc_short}} zone. However, you need to take the high availability aspects into account. To protect your VMware workloads from host failures, for example in case one host stops functioning, you need to have a cluster with at least two hosts. To keep the workloads running, you need to size enough reserve capacity in each cluster even if a host would fail. In most use cases, a 3-node cluster is far more appropriate because you have the option of running maintenance tasks on ESXi hosts (such as host updates) without having to disable HA.

As the central point of SDDC management (vCenter Server and NSX-T Managers) runs on the same {{site.data.keyword.vpc_short}} Bare Metal Servers, protecting them is key. You can use vSphere HA and anti-affinity rules (to prevent specific VMs from running on a same host) for these in the vSphere HA cluster. As your initial cluster is typically a management cluster, VMware best practice is to build a management cluster of four hosts or more allowing the cluster to tolerate host failures better and you to perform maintenance tasks easily, especially with NSX-T and vSAN deployments. Typically, it's not suitable to have three or fewer hosts for a management or a converged management and workload cluster in production.

In general, when you are deploying vSphere HA clusters, it is also important to consider the overall size of the cluster. Smaller-sized clusters require a larger relative percentage of all the available cluster resources to be reserved to handle failures. For example, a cluster of three nodes requires at least 33% of the cluster resources to be held on reserve for failover where a cluster of eight nodes requires 12.5% of cluster resources that are reserved for failover. In a production environment, always consider at least one host as a failover minimum per 8 to 10 ESXi hosts to achieve N+1 redundancy.

It is also considered the best practice to build the cluster out of identical server hardware. In {{site.data.keyword.vpc_short}}, use the same Bare Metal Server profiles for hosts in the same cluster. This practice greatly simplifies the management and configuration of servers. It also reduces resource fragmentation and increases the ability to handle server failures. The use of different hardware in a cluster might make the cluster unbalanced and less productive.

## {{site.data.keyword.cloud_notm}} account access
{: #vpc-ryo-considerations-acct-access}

To manage access to your {{site.data.keyword.cloud_notm}} account, ensure that you have proper access to provision and manage required assets. Depending on your solution design, you might need proper {{site.data.keyword.cloud_notm}} IAM access to the following services:

* [Deploy and manage services in {{site.data.keyword.vpc_short}}](/docs/vpc?topic=vpc-managing-user-permissions-for-vpc-resources)
* [Deploy and manage {{site.data.keyword.cloud_notm}} DNS Services](/docs/dns-svcs?topic=dns-svcs-iam)
* Deploy and manage {{site.data.keyword.cloud_notm}} Interconnectivity Services:
   * [{{site.data.keyword.dl_short}}](/docs/dl?topic=dl-iam)
   * [{{site.data.keyword.tg_short}}](/docs/transit-gateway?topic=transit-gateway-iam)

For more information, see [How {{site.data.keyword.cloud_notm}} IAM works](/docs/account?topic=account-iamoverview).

## VMware licensing
{: #vpc-ryo-considerations-licensing}

The bare metal servers are licensed through the ESXi 7.x image, which provides ESXi in licensed mode. The license is activated during the provisioning process.

For more information about how to license ESXi, see [Licensing ESXi hosts](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.esxi.install.doc/GUID-28D25806-748B-49C0-97A1-E7DE5CB335A9.html){: external}.

For other VMware licenses, for example, vCenter Server and NSX-T, see [FAQ about BYOL for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-faq_byol).

Billing applies to all IBM-provided licenses.
{: note}

## Network design and connectivity
{: #vpc-ryo-considerations-net-design}

To manage access to your {{site.data.keyword.cloud_notm}} network and VMware management components, and to plan your {{site.data.keyword.cloud_notm}} network topology, you must complete the following steps:

* Devise a strategy for public versus private network connectivity to and from your VMware workloads.
* You can provide access to your VPC that hosts the VMware ESXi hosts and workloads by using the various VPC connectivity options, for example:
   * Access to your VMware workloads attached directly to VPC subnets by using VPC network functions, such as floating IP addresses, security groups, and subnet ACLs.
   * Access to your VMware workloads hosted on NSX-T software-defined networking (SDN) by using NSX-T Edge Nodes and Clusters and NSX-T Tier-0 Logical Routers.
   * Private access by using VPC VPNaaS, Transit Gateway, or Direct Link.
* Access your VPC by using the various VPC connectivity options.

## Security planning and hardening
{: #vpc-ryo-considerations-sec-planning}

You are responsible for securing, encrypting, and monitoring your VMware hosts, vCenter Server, NSX-T, and the workloads that are running in the hosts or cluster. In that way, you can meet your corporate, industry, and regulatory standards. The following steps provide generic guidelines to ensure proper security:

* The default host root UID passwords are stored and encrypted in the {{site.data.keyword.cloud_notm}}. You can have them with the SSH key that you must provide by provisioning the bare metal server. It is recommended to change all host root IDs passwords after you finish the provisioning activities and configurations.
* Review password policies, such as complexity and expiration period, across all components.
* Review encryption settings across all components.
* Plan and implement appropriate physical or virtual firewall solutions, such as VPC subnet ACLs and Security Groups, and also NSX-T East-West and North-South firewalls.
* Plan and implement appropriate application load balancing and security solutions.
* Plan and implement appropriate security information and event management (SIEM) solutions.
* Plan and implement appropriate vulnerability scanning.

## Active Directory
{: #vpc-ryo-considerations-ad}

Complete the following steps to ensure proper Single Sign On (SSO) configuration and management:

* If you deployed your Active Directories in VPC or into the VMware vSphere® cluster, configure the Active Directory™ (AD) server update and restart schedule.
* If you choose the option to deploy AD servers into the VMware vSphere cluster, provide Microsoft® Windows® licensing and activation for the servers to ensure compliance and availability.
* Establish mutual trust between the instance and your on-premises AD server.
* Integrate NSX-T, if applicable, with your AD SSO.
* Integrate ESXi hosts with your AD SSO.

## Maintenance planning
{: #vpc-ryo-considerations-maint-planning}

Complete the following steps to ensure proper planning for software maintenance:

* [Set up VMware Update Manager (VUM)](/docs/vmwaresolutions?topic=vmwaresolutions-vum-intro) through a Public Gateway to obtain VMware updates.
* If applicable, set up vSAN through a proxy to maintain the vSAN Hardware Compatibility List (HCL) database.
* Plan regular maintenance for VMware components that are not supported by VUM. For example, VMware vCenter, PSC, and NSX.
* Review vSphere Enhanced vMotion Compatibility (EVC) configuration. Your cluster might not be configured with EVC enabled if the current version of vSphere does not support EVC for your hardware level.

## Monitoring
{: #vpc-ryo-considerations-monitoring}

Ensure to plan for and implement the following solutions for monitoring your instance and instance components:

* A logging server that includes log forwarding or collection for all instance components and adequate log retention. The [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) offering can help you with log management and visibility.
* An alert infrastructure, including configuration of the SMTP server and short message service (SMS) gateway, as needed.
* Proactive monitoring of hosts, drives, management software, and network, including vSAN monitoring if applicable. The [VMware Aria Operations on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) offering can help you operate and monitor the performance, health, and capacity of your VMware environment.
* Monitoring your backup infrastructure and backup jobs.
* vSphere Distributed Switch Health Check is enabled by default. It can generate a significant number of MAC addresses for testing team policy, MTU size, and VLAN configuration, which results in extra network traffic. Disable this health check and re-enable only as needed for network troubleshooting. For more information, see [vSphere Distributed Switch Health Check](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.networking.doc/GUID-4A6C1E1C-8577-4AE6-8459-EEB942779A82.html){: external}.

## Business continuity and availability
{: #vpc-ryo-considerations-business-cont}

Considering your VMware instance is running on {{site.data.keyword.cloud_notm}} bare metal server, complete the following steps to ensure that you make adequate plans for high availability and business continuity:

* Review vSphere HA and vSphere Distributed Resource Scheduler (DRS) configuration against your requirements.
* Review network and storage I/O control configuration against your requirements.
* Configure the virtual machine startup order against your requirements.
* Configure resource pools, as needed, for management and workload.
* Plan, implement, and monitor a backup solution for both management components and workload.
* Plan for high availability of instance management, including the possibility of multiple instances, multiple clusters, and vCenter HA.
* Use backup solutions such as Veeam to plan for business continuity for your workloads.

## Storage planning
{: #vpc-ryo-considerations-storage}

In addition to capacity planning, complete the following to ensure that your storage configuration meets your performance and availability requirements:

* Storage performance depends on various factors. This action includes RAID configuration and disk striping, network configuration, block size, IOPS configuration (input/output operations per second) for network-attached storage. Also, VM hardware configuration and methods of storage attachment, clustering and replication methods, and use of storage policies such as encryption, deduplication, and compression. Plan time to test and adjust your configuration to meet your storage performance needs.
* Review your vSAN storage policy:
   * RAID 1 provides better performance and smaller windows of susceptibility to sequential failure, such as shorter rebuild time, than RAID 5. However, RAID 5 has less storage overload.
   * RAID 6 provides protection against dual failures, but requires a minimum of six hosts compared to four hosts for RAID 5.
* To add more storage to your vSAN cluster, you must add new hosts to the cluster or add {{site.data.keyword.filestorage_vpc_full_notm}} instead. Adding disks to the existing hosts is not currently supported.

## Related links
{: #vpc-ryo-considerations-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
* [VMware validated designs](https://core.vmware.com/vmware-validated-solutions){: external}.
