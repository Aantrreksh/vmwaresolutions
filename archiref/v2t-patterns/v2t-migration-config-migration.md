---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-04"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuration migration
{: #v2t-config-migration}

Configuration migration covers all the NSX-V settings and parameters that must be transferred to the VMware NSX-T™ environment to provide similar functions of the NSX-V environment.

Depending on the complexity of your network, it can include the following configurations:

* VLAN and overlay-backed logical switches
* L2 Bridges, routing, and NAT
* Transport zones
* Distributed and edge firewall
* L2 and L3 VPNs
* Load balancer, DHCP, and DNS
* Service composer, guest, and network introspection
* Grouping objects, IP and MAC sets, security groups, tags, services and service groups

Configurations can be applied by one of the following approaches:

* Manual or scripted - By using the NSX-T UI or scripting tools like Terraform, the NSX-T configuration can be applied to the required overlay pattern.
* Migration Coordinator - Migration Coordinator is a built-in and automated migration tool, which is designed to help migrate from NSX-V to NSX-T. This tool is fully supported by VMware® and is built into NSX-T Manager Appliance. Migration Coordinator might also be used as an assessment tool to check whether the existing NSX-V environment is suitable for migration with Migration Coordinator. This is nondisruptive and doesn't change the NSX-V infrastructure.
* Third-party tool - It provides UI based scripts to enable the assessment, migration, and rollback of configurations. For more information, see [NSX-V to NSX-T migration tools](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-l2-nsx-t).

If the configurations are simple, or there are not too many rules or definitions, manual, or scripted is typically the simplest way to migrate the configuration. If the configurations are complex, consider the use of a third-party tool.
{: note}

Migration Coordinator supports other migration approaches such as "in-place migration", which is not supported in {{site.data.keyword.cloud}}. Therefore, consider the documentation at [NSX-V to NSX-T 3.x Migration Coordinator](https://nsx.techzone.vmware.com/resource/nsx-v-nsx-t-3x-migration-coordinator#_Toc57645169){: external}.
{: note}

## Understanding distributed firewall complexity
{: #v2t-config-migration-understandingdfw}

It is important to understand the complexity of your distributed firewall configuration.

* If you are not using distributed firewall, then you must not migrate the configuration.
* If in your distributed firewall configuration "Applied To" is set to "DFW" and all the rules are IP-based, then by migrating workload virtual machines is a single stage process.
* If in your DFW configuration has the following, then a multistage approach for workload VMs is needed:
   * If "Applied To" is set to "DFW" in all the rules, and there are rules with Security Groups with dynamic memberships based on Security Tags or with static memberships.
   * If "Applied To" is set to a universal security group or a universal logical switch in any rule. Also, if there are rules with Security Groups with dynamic memberships based on Security Tags or with static memberships.
   * If "Applied To" is set to a universal security group or a universal logical switch in any rule, and all the rules are IP-based.

## Distributed firewall migration guidance
{: #v2t-config-migration-migratingdfw}

When you migrate the workload VMs to the NSX-T environment in waves, it is imperative that the distributed firewall does not break communications between the workload VMs during the migration. Therefore, the configuration migration for the distributed firewall has two stages:

1. The first stage migrates the firewall rules and the groups to NSX-T.
2. The second stage creates specific VIFs for each VM that is migrated. And also includes the creation of IP Set-based rules for every VM that is migrated to ensure that there are no security gaps when you move to NSX-T.

It is important to note that:

* Tags cannot be applied before you move the VM over to the NSX-T.
* A VM moved without tags can create a gap in security.
* Temporary IP Sets are used to allow for a gradual migration while micro-segmentation is enforced for flows between the two NSX environments.
* If workload VMs must be migrated by using vMotion, then the vMotion must be initiated through the API. So that, the VMs are connected to the pre-created logical ports.
* When workload VMs are migrated, there is a post-migration step to remove temporary IP Set group and tag the VMs that migrate.

## Load balancer migration guidance
{: #v2t-config-migration-migratinglb}

The approach is to configure load balancing in NSX-T in parallel to the existing NSX-V configuration. This action allows testing and then, when verified, cut-over to NSX-T load balancing. To migrate the load-balancing service from NSX-V to NSX-T, consider the following steps:

* Deploy a new NSX-T Edge cluster that contains two Edge node VMs with active or standby configurations.
* Deploy a T1 router into the Edge cluster with centralized service ports (CSP).
* Deploy a load balancer, with the same configuration as the NSX-V load balancer, into the Edge cluster and linked with the T1 router.
* Assign a new VIP for each server pool to allow the testing of connectivity from the client to the servers.
* Add the new NSX-T segment that is created for the VIPs to any security group rules. At this stage, you have:
   * NSX-V load balancers are active as the DNS records point to the VIP on the NSX-V load balancer.
   * NSX-T load balancers can be used for testing the configurations.
* To cut over from the NSX-V to NSX-T load balancers, point DNS record to NSX-T VIP.

## Considerations for configuration migration
{: #v2t-config-migration-considerations}

When you plan and design configuration migration, consider the following aspects:

* Are you using vCenter-specific objects (for example, clusters, folders) in NSX-V distributed firewall rules? While micro-segmentation is similar in NSX-V and NSX-T, there are differences that must be considered for during the migration. Customers that write distributed firewall rules for NSX-V might use vCenter-specific objects (for example, clusters, folders) which are not available in NSX-T. Those rules must be rewritten to ensure that the overall micro-segmentation design and granularity are maintained after NSX-T migration.
* Are you using IP Sets and Security Groups? You must create new security groups in NSX-T based on the security groups in NSX-V. You must identify IP sets and security groups with exclusions, and security groups with the dynamic inclusion rule that contains multiple criteria.
* Are you using firewall rules based on security groups that dynamically include VMs based on security tags? In NSX-T, security tags are entirely managed by NSX-T. The firewall rules based on security groups that dynamically include VMs based on security tags are not effective until the security tags are applied to the VMs.
* What types of NSX Edge services, such as firewall, L2VPN, load balancing, are in use? These services must be re-created in the NSX-T environment.
* Are you using the NSX-V IPFIX feature to capture traffic flows that are sourced from and destined to the VMs running on NSX-V logical switches? You must analyze the ability of NSX-T to replace the packet flow forwarding feature.
* Are you using OSPF as dynamic routing protocol? You must assess the use of BGP to replace OSPF.
* Are you using DLR native L2 bridging to bridge L2 traffic between VMs and bare metal servers through a distributed virtual switch? Search for alternative solutions of bridging in NSX-T.
* Do you need gradual migration of VMs from NSX-V to NSX-T, and not a full subnet migration? By using an NSX-V to NSX-T bridge, allows VMs in the same L2 domain to be migrated from an NSX-V logical switch to NSX-T segment. Alternatively, L2VPN or VMware HCX™ can be used to provide L2 connectivity.

## Related links
{: #v2t-config-migration-links}

* [cITopus for NSX](https://spjsolutions.com){: external}
* [ReSTNSX's Migration Assistance Tool (M.A.T.)](https://www.restnsx.com/post/migration-assistance-tool-mat){: external}
* [PrimaryIO NSX-V to NSX-T Fasttrack Migration Service](https://hdm.primaryio.com/lp/nsxvtot){: external}
* [VMware Cloud Migration Services (VMwaaS VPC NSX-T)](https://cloud.ibm.com/catalog/services/vmware-cloud-migration-services-vmwaas-vpc-nsx-t)
