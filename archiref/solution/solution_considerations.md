---

copyright:

  years:  2016, 2024

lastupdated: "2024-01-31"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Post-deployment considerations for your VMware instance
{: #solution_considerations}

{{site.data.keyword.vmwaresolutions_full}} offerings are not managed services. You are responsible for the configuration, security, management, and monitoring of all software components. With complete administrative access to the solution, you have great power and flexibility that requires significant technical, administrative, and operational expertise across various domains. Managing a VMware® instance in the {{site.data.keyword.cloud_notm}} requires the same planning and expertise as planning for an on-premises instance. Software-defined technologies such as VMware NSX® and VMware vSAN™ greatly simplify some aspects of instance management, but might require new skills and tools to be properly managed and operated. Combining the power, speed, and reliability of {{site.data.keyword.cloud_notm}} automated VMware deployment with the appropriate operational planning and testing ensures quick and successful navigation to hybrid cloud.

Review the following considerations to understand your responsibilities for managing and operating the instance before and after it is deployed.

## {{site.data.keyword.cloud_notm}} account access
{: #solution_considerations-acct-access}

To manage access to your {{site.data.keyword.cloud_notm}} account, permit other members of your team to access your instance in the {{site.data.keyword.vmwaresolutions_short}} console. For more information, see [Inviting users to access services and resources](/docs/vmwaresolutions?topic=vmwaresolutions-useraccount#useraccount-iamuserinv).

## Limitations
{: #solution_considerations-limitations}

Familiarize yourself with the following limitations for your instance:

- [Impacts of changing vCenter artifacts](/docs/vmwaresolutions?topic=vmwaresolutions-vcenter_chg_impact)
- [Networking considerations and limitations](/docs/vmwaresolutions?topic=vmwaresolutions-vc_networkingonvcenterserver)
- [Frequently asked questions](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)

## Network design and connectivity
{: #solution_considerations-net-design}

Complete the following steps to manage access to your {{site.data.keyword.cloud_notm}} network and to your VMware management components and to plan your {{site.data.keyword.cloud_notm}} network topology.

- Access instance management endpoints by using the [{{site.data.keyword.cloud_notm}} VPN](/docs/iaas-vpn?topic=iaas-vpn-getting-started) or your [{{site.data.keyword.cloud_notm}} Direct Link](https://www.ibm.com/products/direct-link){: external}.
- Devise a strategy for public network connectivity from within your instance. Your options include the sample customer VMware NSX Edge™ Services Gateway (ESG), gateway appliances such as Vyatta and FortiGate, and proxy servers deployed in the {{site.data.keyword.cloud_notm}} network or on your own network accessed through Direct Link.
- Plan whether to deploy your workload on {{site.data.keyword.cloud_notm}} VLANs with [{{site.data.keyword.cloud_notm}} portable IP addresses](/docs/subnets?topic=subnets-getting-started) or [on NSX-T logical switches using your own IP addresses](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design). When you use NSX software-defined networking (SDN), it gives you the greatest flexibility to manage and secure your workload network in the {{site.data.keyword.cloud_notm}}.
- Use NSX ESGs, [{{site.data.keyword.cloud_notm}} Vyatta](https://cloud.ibm.com/catalog/infrastructure/virtual-router-appliance), and Direct Link peering to plan for connectivity to workloads (Network Address Translation, Virtual Private Network, routing).
- If you implement Cross-vCenter NSX, ensure that your local segment ID ranges are not overlapping before you deploy any local workloads.

## Security planning and hardening
{: #solution_considerations-sec-planning}

You are responsible for securing, encrypting, and monitoring your VMware instance and workloads to meet your corporate, industry, and regulatory standards. Complete the following steps to ensure proper security.

- Change all passwords displayed in the {{site.data.keyword.vmwaresolutions_short}} console and use your own password management system. IBM retains distinct user IDs needed for ongoing automation and support.
- Review password policies, such as complexity and expiration period, across all components.
- Review encryption settings across all components.
- Plan and implement appropriate physical or virtual firewall solutions, such as NSX Distributed Firewall (DFW), NSX ESGs, [FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations), and [{{site.data.keyword.cloud_notm}} Vyatta](https://cloud.ibm.com/catalog/infrastructure/virtual-router-appliance).
- Plan and implement appropriate application load balancing and security solutions, such as [F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations).
- Plan and implement appropriate security information and event management (SIEM) solutions, such as [IBM Security QRadar SIEM](https://www.ibm.com/products/qradar-siem){: external}.
- Plan and implement appropriate vulnerability scanning.

## Customization
{: #solution_considerations-custom}

Complete the following steps to customize the base VMware instance installation to fit your requirements.
- Use your own certificate authority (CA) to generate certificates for components such as vCenter (with embedded PSC) and NSX Manager.
- Configure deployed services. For example,
   - For Zerto, plan for IP addressing and routing of Zerto Virtual Replication Appliance (VRA) communications since network address translator (NAT) traversal is not supported. Consider either tunneling or redeployment of your VRAs for appropriate addressing and routing.
   - For backup services such as Veeam® and IBM Spectrum® Protect Plus, configure your backup job, optionally configure additional storage, and configure monitoring alerts.
   - For networking and security services such as F5® BIG-IP and FortiGate Virtual Appliance, configure network interfaces, certificates, high availability (HA) configuration, and rules according to your network topology and other requirements.

## Active Directory
{: #solution_considerations-ad}

Complete the following steps to ensure proper single sign-on (SSO) configuration and management.
- Configure the Active Directory® (AD) server update and restart schedule.
- If you choose the option to deploy AD servers into the VMware vSphere® cluster, provide Microsoft® Windows® licensing and activation for the servers to ensure compliance and availability.
- Establish mutual trust between the instance and your on-premises AD server.
- Integrate NSX VPN, if applicable, with AD SSO.
- Integrate VMware ESXi® hosts with AD SSO.

## Maintenance planning
{: #solution_considerations-maint-planning}

Complete the following steps to ensure proper planning for software maintenance.
- [Set up VMware Update Manager (VUM)](/docs/vmwaresolutions?topic=vmwaresolutions-vum-intro) through a proxy to obtain VMware updates.
- If applicable, set up vSAN through a proxy to maintain the vSAN Hardware Compatibility List (HCL) database.
- Plan regular maintenance for VMware components that are not supported by VUM. For example, VMware vCenter, PSC, and NSX.
- Review vSphere Enhanced vMotion Compatibility (EVC) configuration. Your cluster might not be configured with EVC enabled if the current version of vSphere does not support EVC for your hardware level.
- Plan regular maintenance for add-on services such as Veeam, Zerto, and F5 BIG-IP.

## Monitoring
{: #solution_considerations-monitoring}

Ensure to plan for and implement the following solutions for monitoring your instance and instance components.
- A logging server that includes log forwarding or collection for all instance components and adequate log retention. The [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) offering can help you with log management and visibility.
- An alert infrastructure, including configuration of the SMTP server and short message service (SMS) gateway, as needed.
- Proactive monitoring of hosts, drives, management software, and network, including vSAN monitoring if applicable. The [VMware Aria Operations on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) offering can help you operate and monitor the performance, health, and capacity of your VMware environment.
- Capacity monitoring and planning. You can [add clusters](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingclusters), [remove clusters](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingclusters), [add hosts](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers), and [remove hosts](/docs/vmwaresolutions?topic=vmwaresolutions-vc_removingservers) for your instance from the {{site.data.keyword.vmwaresolutions_short}} console.
- Monitoring your backup infrastructure and backup jobs.
- vSphere Distributed Switch Health Check is enabled by default and can generate a significant number of MAC addresses for testing team policy, MTU size, and VLAN configuration, which results in extra network traffic. Disable this health check and re-enable only as needed for network troubleshooting. For more information, see [vSphere Distributed Switch Health Check](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.networking.doc/GUID-4A6C1E1C-8577-4AE6-8459-EEB942779A82.html){: external}.

## Business continuity and availability
{: #solution_considerations-business-cont}

Your VMware instance is running on {{site.data.keyword.cloud_notm}} bare metal servers.

Complete the following steps to ensure that you make adequate plans for high availability and business continuity.
- Review vSphere HA and vSphere Distributed Resource Scheduler (DRS) configuration against your requirements.
- Review network and storage I/O control configuration against your requirements.
- Configure the virtual machine startup order against your requirements.
- Configure resource pools, as needed, for management and workload.
- Plan, implement, and monitor a backup solution for both [instance management components](/docs/vmwaresolutions?topic=vmwaresolutions-solution_backingup) and workload.
- Plan for high availability of instance management, including the possibility of multiple instances, multiple clusters, vCenter HA, and PSC HA.
- Use solutions such as [Zerto Disaster Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr) or [Veeam Backup and Replication](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) to plan for business continuity for your workloads.

## Storage planning
{: #solution_considerations-storage}

In addition to capacity planning, complete the following to ensure that your storage configuration meets your performance and availability requirements.

- Storage performance depends on various factors, including RAID configuration and disk striping, network configuration, block size, configured IOPS (input/output operations per second) for network-attached storage, VM hardware configuration and method of storage attachment, clustering and replication methods, and use of storage policies such as encryption, deduplication, and compression. Plan time to test and tune your configuration to meet your storage performance needs.
- Review your vSAN storage policy
   - RAID 1 provides better performance and smaller windows of susceptibility to sequential failure, such as shorter rebuild time, than RAID 5. However, RAID 5 has less storage overhead.
   - RAID 6 provides protection against dual failures, but requires a minimum of six hosts compared to four hosts for RAID 5.
- To add more storage to your vSAN cluster, you must add new hosts to the cluster or add {{site.data.keyword.cloud_notm}} Endurance NFS storage instead. Adding disks to the existing hosts is not currently supported.
- If you mount additional {{site.data.keyword.cloud_notm}} Endurance NFS storage to your cluster, ensure that you follow the architecture guidance and configure host routes to the storage that uses the cluster's NFS port group addresses. You must authorize these addresses, rather than the hosts themselves, to the storage. For more information, see [Attached storage infrastructure management](/docs/vmwaresolutions?topic=vmwaresolutions-storage-infra-mgmt#storage-infra-mgmt-vsphere-routing).

## Related links
{: #solution_considerations-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
* [Design overview](/docs/vmwaresolutions?topic=vmwaresolutions-design_overview)
* [Scaling capacity](/docs/vmwaresolutions?topic=vmwaresolutions-solution_scaling)
