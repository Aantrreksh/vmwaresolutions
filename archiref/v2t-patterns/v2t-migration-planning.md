---

copyright:

  years:  2022, 2023

lastupdated: "2023-09-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Migration planning
{: #v2t-planning}

Migration planning and preparation are the key to a successful migration project. It is imperative that the migration complexity is fully understood so that timescales, required tools, skills, and knowledge are available. An overview migration flow is shown in the following diagram.

![Migration flow](../../images/v2t-diagrams-tree.svg "Make sure that the migration complexity is fully understood so that timescales, required tools, skills, and knowledge are available."){: caption="Figure 1. Migration flow" caption-side="bottom"}

## Classify migration complexity
{: #v2t-planning-complexity}

In the initial stage, the complexity of the migration is estimated. An aspect of this complexity is based on the source environment. Therefore, a review of the current NSX-V environment must be undertaken and documented so the following details are understood:

* Logical network topology - A series of diagrams that document the external and internal networking.
* Logical networking and security configurations - Detailed parameters that are used in the configuration of the NSX-V network and security. Logical switches, routing, distributed firewall, edge firewall, NAT, VPNs, and load balancing are included.
* Clusters and hosts - Information on the clusters and their hosts.
* Workload virtual machines - Placement of VMs, and their relationships to each other.
* Integration - External tools that integrate with vCenter or NSX-V Manager, such as Veeam®, VMware Aria® Operations™ Manager, VMware Aria® Automation™, custom scripts, and other tools.

The following factors govern the complexity of migration:

* Project-based factors - such as how is the project that is being staffed.
* Architecture factors - such as changes to the existing NSX-V environment since deployment.
* Micro-segmentation factors - such as the use of distributed firewall rules and the use of tagging in these rules.
* Integration factors - what systems are integrating with NSX-V Manager and vCenter as both these components are replaced in the migration. Integrated systems can include VMware Aria Automation, VMware Aria Operations, VMware Aria Orchestrator, SEIM or security tools, backup and recovery, replication, F5, vSRX, FortiGate, or other third-party network applications.

For more information, see [Assess migration complexity](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-complexity).

Classifying or assessing migration complexity is just an informative step to provide you guidance. So that you can estimate the migration timescales, required tools, skills and knowledge, and you can prepare in the best possible way.
{: important}

## Required skills
{: #v2t-planning-skills}

When you assess the complexity, you must focus on skills and resource availability. You must assess:

* If existing resources have time to participate in migration activities while they are delivering their existing duties.
* If existing resources have the skills, knowledge and experience that are needed to successfully deliver the required tasks.

If it is deemed that in-house skills need to be supplemented, then it is advised to engage a migration services provider as soon as possible. 

In addition, to ensure successful Day 2 operations, improve the core VMware NSX-T™ skills by using the available [VMware Learning for NSX-T education](https://www.vmware.com/learning.html){: external}.

## Engage a migration services provider
{: #v2t-planning-serviceprovider}

You can engage PrimaryIO’s experienced Professional Services team through the IBM Catalog. For more information, see [HDM Cloud Connect NSX-V to NSX-T](https://cloud.ibm.com/catalog/services/hdm-cloud-connect-nsx-v-to-nsx-t).

PrimaryIO’s Fasttrack Migration Service is optimized to move customers away from NSX-V and onto NSX-T through short form engagements that continually drive progress by focusing on critical path objectives.

## Source environment complexity patterns
{: #v2t-planning-complexitypatterns}

The output of the [Assess migration complexity](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-complexity) step is a complexity status of low, medium, or high. 

This status can be used to help the selection as follows:

* A target platform.
* A configuration migration pattern.
* A workload migration pattern.
* A network L2 extension pattern.

You are not able to neatly classify every source environment due to the multiple number of variations. Also, client requirements into one of these three categories by a set of rules or a defined set of parameters. Therefore, an analytical approach is required with a consensus gained across your team.

## Target platforms
{: #v2t-planning-targetplatforms}

Based on the source environment complexity, you must consider the following target platform:

* Single site VMware vCenter Server® instance - An automated provisioning offering that deploys hardware and software in a defined pattern. After initial deployment, you must add capacity and additional services to a number of automated workflows as needed. For more information, see [vCenter Server overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview). The types of vCenter Server instances include:
   * Regulated Workloads. For more information, see [VMware Regulated Workloads overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-overview).
   * Security and Compliance Readiness Bundle. For more information, see [Security and Compliance Readiness Bundle overview](/docs/vmwaresolutions?topic=vmwaresolutions-scb-overview).
* Multisite or location vCenter Server instance - The vCenter Server offering can be deployed in multiple locations to create a multisite or location vCenter Server instance. The vCenter Server multisite deployment pattern is two or more instances that are deployed into a common root domain and single sign-on domain with vCenters in Enhanced Link Mode. Each site or location has its own NSX-T instance. For more information, see [Multisite configuration for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_multisite).

The vCenter Server multizone offering is now deprecated. For more information, see [vCenter Server multizone BOM](/docs/vmwaresolutions?topic=vmwaresolutions-mcv-archi-bom).
{: note}

For more information about comparisons of the previous available offerings to enable a selection, see [Target platforms in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-targets).

## Configuration migration
{: #v2t-planning-configmigration}

Configuration migration covers all the NSX-V settings and parameters that must be transferred to the NSX-T environment to provide similar functions of the NSX-V environment. Configurations can be applied by one of the following approaches:

* Manual or scripted
* VMware Migration Coordinator
* Third-party tool

If the configurations are simple, or don't have too many rules or definitions, manual, or scripted is typically the simplest way to migrate the configuration. A benefit of following this approach is also that you have a better understanding of how the target is configured. If the configurations are complex or have many firewall rules, consider the use of third-party tool to ease up duplicate manual work.
{: note}

## Workload migration
{: #v2t-planning-workloadmigration}

After the configuration migration, the workload VMs can be migrated by using either a Layer 3 or Layer 2 connection between workload VMs awaiting migration on the NSX-V environment. Also, those workload VMs that migrated to the NSX-T environment. To migrate your workloads from NSX-V to the NSX-T environment, consider the following steps:

* Bridge the NSX-T and NSX-V overlays and use the [available L2 extension methods](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-planning#v2t-planning-nwl2ext), by allowing for gradual migration of individual or small batches of VMs.
* Migrate all the VMs on a subnet by using your preferred migration method or tool and move the default gateway to NSX-T.

Considerations include the following questions:

* Do you need to move workload VM with or without limited downtime?
* Do you need to move workload VMs individually or in small batches but cannot move a subnet at a time?
* Do you need to extend Layer 2 between the existing and new vCenter Server environments?
   * How many networks do you need to extend at one time?
   * Do you need high availability?
   * How much spare capacity do you have on the NSX-V prepared host to deploy the required number of NSX-T Edge node VMs for L2 Bridge edge VMs?

The following migration patterns for workload migration must be considered:

* HCX™ - VMware HCX application migration enables the scheduling and migration of thousands of VMs. For more information, see [VMware HCX Migration Types](https://docs.vmware.com/en/VMware-HCX/4.3/hcx-user-guide/GUID-8A31731C-AA28-4714-9C23-D9E924DBB666.html){: external}.
* Advanced vCenter vMotion - From vSphere 7.0 Update 1c (Patch 02), vCenter supports the import of VMs from another vCenter Server that is not part of the same SSO Domain. The source vCenter Server must be version 6.5 or later. For more information, see [Introducing the Advanced Cross vCenter Server vMotion Capability](https://core.vmware.com/resource/introducing-advanced-cross-vcenter-server-vmotion-capability#){: external}.
* Zerto or Veeam® - You might have Zerto or Veeam installed on your NAX-V environment and be competent in their usage. These products can be used to replicate VMs from the source data store to the target data store and then initiate a fail-over. And also to replicate a backup from the source cluster to a recovery on the target cluster.

## Network L2 extension
{: #v2t-planning-nwl2ext}

From a network perspective, the requirement for Layer 3 and Layer 2 connectivity during the migration must be understood. L2 extension allows bridging the NSX-T logical switches to NSX-T segments. You can move the workloads between the NSX-V and NSX-T environments, while you keep the default gateway either on the NSX-V or move it to the new NSX-T. This action allows a smoother network migration. However, it is not mandatory if your environment can tolerate downtime.

Consider the following details for Layer 3 network migration:
* VM by VM migration – This approach moves a VM at a time and /32 route for that host is injected into the NSX-T environment. Therefore, a specific route is defined to this IP address to the NSX-T environment while all other IP addresses in the subnet are still routed to the NSX-V environment.
* Subnet by subnet migration – This approach moves all the VMs on a subnet at a time. The subnet is advertised out of the NSX-T environment and not advertised from the NSX-V environment.
* Big-bang - All subnets and their connected VMs are moved and then all subnets advertised from the NSX-T environment.

Consider the following details for Layer 2 network extension during migration:
* NSX-T L2 bridge - In this approach an NSX-T Edge VM or preferably a pair of NSX-T Edge VMs, are deployed on the NSX-V prepared hosts. These Edge VMs are registered with NSX-T Manager and a L2Bridge configured to connect the required NSX-V VXLAN (virtual wire) to an NSX-T segment. For more information, see [Migration that uses vMotion or third-party tools and NSX-T L2 bridge](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-l2-nsx-t).
* VMware HCX - VMware HCX is a solution that is primarily used for migrating workloads between environments, and consists of a number of services to achieve workload mobility. HCX integrates into both NSX-V and NSX-T. HCX Network Extension (NCX-NE) allows simultaneous bridging of multiple networks. The solution is useful in cases where the applications are spread across multiple segments and need inter-app connectivity for extended periods of time during the migration. Using HCX allows bridging of eight segments at a time per HCX-NE pair. This action is especially useful if a workload spans multiple segments. For more information, see [Workload migration with HCX](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-hcx).

A third possible Layer 2 approach is to use NSX-T L2VPN. In this approach, the NSX-V environment acts as the L2VPN client and the NSX-T environment acts as the L2VPN server. The L2 VPN connection is secured with a route-based IPsec tunnel between the L2 VPN server and the L2 VPN client. This approach is not recommended in {{site.data.keyword.cloud_notm}} between two vCenter Server instances for V2T migration as NSX-T L2 Bridge offers better performance. And also because {{site.data.keyword.cloud_notm}} private network supports large MTU (jumbo frames).
{: note}

## Related links
{: #v2t-planning-links}

* [Terraform by Hashicorp](https://www.terraform.io/){: external}
* [The NSX Terraform Provider](https://registry.terraform.io/providers/vmware/nsxt/latest/docs){: external}
* [NSX-V to NSX-T 3.x Migration Coordinator](https://nsx.techzone.vmware.com/resource/nsx-v-nsx-t-3x-migration-coordinator#_Toc57645169){: external}
* [NSX-V to NSX-T fast track migration service](https://hdm.primaryio.com/lp/nsxvtot){: external}
* [HDM Cloud Connect NSX-V to NSX-T](https://cloud.ibm.com/catalog/services/hdm-cloud-connect-nsx-v-to-nsx-t#about)
