---

copyright:

  years:  2023

lastupdated: "2023-10-10"
  
keywords: vmware cloud foundation, IBM Cloud, vpc

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deploying VMware validated solutions
{: #vpc-vcf-deploy-vvs}

A VMware validated solution is a technically validated implementation that is built and tested by VMware and VMware partners to help you resolve common business use cases. VMware validated solutions are operational, cost-effective, performant, reliable, and secure. 

Each solution contains a detailed design, implementation, and operational guidance. The following information provides a summary of the validated solutions on your VMware Cloud Foundation™ instance with some {{site.data.keyword.cloud_notm}} specific design and installation considerations and notes.

## Identity and Access Management for VMware Cloud Foundation
{: #vpc-vcf-deploy-vvs-iam}

The [Identity and Access Management for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-identity-and-access-management-v1/GUID-FF35966D-2225-4825-9E38-C7287B069D4D.html){: external} validated solution provides detailed design, implementation, configuration, and operation guidance on the use of Active Directory as an identity provider and authentication source, and on the use of role-based access control (RBAC) in VMware Cloud Foundation SDDC Manager™, VMware vCenter Server®, VMware ESXi™, and VMware NSX™.

This solution is intended for cloud architects and administrators who are familiar with VMware software and a role-based access control solution by using a central identity provider for VMware Cloud Foundation.

Solution-added products for this VMware validated solution include VMware Workspace ONE Access.

To deploy the Identity and Access Management for VMware Cloud Foundation validated solution in {{site.data.keyword.cloud_notm}}, follow the process in [Identity and Access Management for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-identity-and-access-management-v1/GUID-FF35966D-2225-4825-9E38-C7287B069D4D.html){: external}.

Use VMware Aria® Suite Lifecycle Manager (formerly known as VMware vRealize® Suite Lifecycle Manager) to deploy this VMware validated solution. Aria Suite Lifecycle Manager is deployed as part of the automation.
{: important}

If you are deploying a clustered or scaled out environment for Workspace ONE Access 3.3.7 X-Region, see [KB83928](https://kb.vmware.com/s/article/83928){: external}. If you need help, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: important}

## Developer Ready Infrastructure for VMware Cloud Foundation
{: #vpc-vcf-deploy-vvs-tanzu}

[The Developer Ready Infrastructure for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-developer-ready-infrastructure-v1/GUID-E3C98B72-EE54-491E-AC71-C07F52AAF5E2.html){: external} provides design, implementation, and operational guidance for a workload domain that runs vSphere with Tanzu workloads (TKG Runtime) in the Software-Defined Data Center (SDDC).

This solution is intended for cloud architects and administrators who are familiar with using VMware software to deploy and manage a workload domain that runs vSphere with Tanzu workloads in the SDDC.

The solution does not include any new solution-added products, but the VMware documentation provides a fast and efficient path to automating the Developer Ready Infrastructure for VMware Cloud Foundation implementation.

To deploy the Developer Ready Infrastructure for VMware Cloud Foundation validated solution in {{site.data.keyword.cloud_notm}}, follow the process in [Developer Ready Infrastructure for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-developer-ready-infrastructure-v1/GUID-E3C98B72-EE54-491E-AC71-C07F52AAF5E2.html){: external}.

Use Aria Suite Lifecycle Manager (formerly known as vRealize Suite Lifecycle Manager) to deploy this VMware validated solution. Aria Suite Lifecycle Manager is deployed as part of the automation.
{: important}

When you are deploying TKG Runtime in a VMware Cloud Foundation instance with {{site.data.keyword.cloud_notm}}, ensure that your edge cluster nodes appliance size is either Large or Extra Large. Currently, only the Active Standby edge cluster is supported in {{site.data.keyword.cloud_notm}}.
{: important}

To get the NSX edge cluster visible in compatible list under the SDDC Kubernetes deployment, before you deploy the TKG runtime, follow the steps in [Unable to get the NSX edge cluster visible in compatible list under the SDDC Kubernetes deployment](https://kb.vmware.com/s/article/83991){: external}.
{: important}

## Intelligent Logging and Analytics for VMware Cloud Foundation
{: #vpc-vcf-deploy-vvs-aria-operations-for-logs}

[The Intelligent Logging and Analytics for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-intelligent-logging-and-analytics-v1/GUID-42022E8E-7C84-4864-AE49-69D016EF5600.html){: external} provides information on the use of a log analysis tool that delivers highly scalable log management with intuitive and actionable dashboards, sophisticated analytics, and broad third-party extensibility. The solution provides deep operational visibility and fast troubleshooting for your VMware Cloud Foundation instance and workloads that are running on it.

Solution-added products for this VMware validated solutions include Aria Operations™ for Logs (formerly known as vRealize Log Insight). Aria Suite Lifecycle Manager (formerly known as vRealize Suite Lifecycle Manager) is deployed as part of the initial provisioning for your VMware Cloud Foundation instance, and you use this deployment method to deploy Intelligent Logging and Analytics for VMware Cloud Foundation.

To deploy the Intelligent Logging and Analytics for VMware Cloud Foundation validated solution in {{site.data.keyword.cloud_notm}}, follow the process in [Intelligent Logging and Analytics for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-intelligent-logging-and-analytics-v1/GUID-42022E8E-7C84-4864-AE49-69D016EF5600.html){: external}.

Use Aria Suite Lifecycle Manager (formerly known as vRealize Suite Lifecycle Manager) to deploy this VMware validated solution. Aria Suite Lifecycle Manager is deployed as part of the automation.
{: important}

## Intelligent Operations Management for VMware Cloud Foundation
{: #vpc-vcf-deploy-vvs-aria-operations}

[The Intelligent Operations Management for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-intelligent-operations-management-v1/GUID-31B18AB1-9E88-4355-BECF-A90F1E1F7C19.html){: external} provides instructions for implementing a centralized monitoring and alerting platform to deliver proactive management of system failures through a single interface to review and act on events and alerts for your VMware Cloud Foundation instance and workloads that are running on it.

This solution is intended for cloud architects and administrators who are familiar with and want to use VMware software and to provide a centralized monitoring and alerting platform to deliver proactive management of system failures.

Solution-added products for this VMware validated solutions include Aria Operations Manager (formerly known as vRealize Operations Manager). Aria Suite Lifecycle Manager (formerly known as vRealize Suite Lifecycle Manager) is deployed as part of the initial provisioning of your VMware Cloud Foundation instance. You can use this method to deploy Intelligent Operations Management for VMware Cloud Foundation.

To deploy the Intelligent Operations Management for VMware Cloud Foundation validated solution in {{site.data.keyword.cloud_notm}}, follow the process in [Intelligent Logging and Analytics for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-intelligent-operations-management-v1/GUID-31B18AB1-9E88-4355-BECF-A90F1E1F7C19.html){: external}.

Use Aria Suite Lifecycle Manager (formerly known as vRealize Suite Lifecycle Manager) to deploy this VMware validated solution. Aria Suite Lifecycle Manager is deployed as part of the automation.
{: important}

## Private Cloud Automation for VMware Cloud Foundation
{: #vpc-vcf-deploy-vvs-aria-automation}

[The Private Cloud Automation for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-private-cloud-automation-v1/GUID-33896484-4331-46F1-8875-B487BBEDCE05.html){: external} provides information about the use of Aria Automation (formerly known as vRealize Automation) for cloud automation services with the VMware Cloud Foundation platform.

This solution is intended for cloud architects and administrators who are familiar with implementation of cloud automation services that can use VMware Cloud Foundation.

Solution-added products for this VMware validated solution include Aria Automation (formerly known as vRealize Automation).

To deploy the Private Cloud Automation for VMware Cloud Foundation validated solution in {{site.data.keyword.cloud_notm}}, see [Private Cloud Automation for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-private-cloud-automation-v1/GUID-33896484-4331-46F1-8875-B487BBEDCE05.html){: external}.

Use Aria Suite Lifecycle Manager (formerly known as vRealize Suite Lifecycle Manager) to deploy this VMware validated solution. Aria Suite Lifecycle Manager is deployed as part of the automation.
{: important}

Before deployment, upgrade vRealize Operations Manager (also known as Aria Operations Manager) 8.10.0 to the most recent version and follow the procedure in [Deployment of vRealize Suite Lifecycle Manager and Workspace ONE Access for Private Cloud Automation for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-private-cloud-automation-v1/GUID-FD5C8968-55A8-463A-BE30-CC369A11EDCC.html){: external}.
{: important}

## Advanced Load Balancing for VMware Cloud Foundation
{: #vpc-vcf-deploy-vvs-nsx-advanced-load-balancing}

Deploying NSX Advanced Load Balancer Controllers require new {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) bare metal server VLAN interfaces and changes to {{site.data.keyword.vpc_short}} default routing tables. This configuration task is manual and it requires understanding of the {{site.data.keyword.vpc_short}} and its routing concepts.
{: important}

[The Advanced Load Balancing for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-nsx-advanced-load-balancer-v1/GUID-F8696F0A-D91B-46B1-A824-8FAE461E57B3.html){: external} provides information on the use of NSX Advanced Load Balancer as a load-balancing solution for VMware Cloud Foundation.

This solution is intended for cloud architects and administrators who want to use NSX Advanced Load Balancer for load balancing in VMware Cloud Foundation.

Solution-added products for this VMware validated solutions include NSX Advanced Load Balancer.

To deploy the Advanced Load Balancing for VMware Cloud Foundation validated solution in {{site.data.keyword.cloud_notm}}, see [Advanced Load Balancing for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-nsx-advanced-load-balancer-v1/GUID-F8696F0A-D91B-46B1-A824-8FAE461E57B3.html){: external}.

VMware recommends customers use [NSX Advanced Load Balancer](https://www.vmware.com/products/nsx-advanced-load-balancer.html){: external} for load balancing. NSX Advanced Load Balancer – Basic Edition is included with NSX Advanced (VMware Cloud Foundation Advanced Edition) and NSX Enterprise Plus (VMware Cloud Foundation Enterprise Edition).
{: note}

VMware NSX Advanced Load Balancer – Basic Edition offers L4–L7 load balancing with SSL offload and pass-through, server health checks, application rules for programmability, and traffic manipulation by using the GUI or REST API. Advanced features of NSX Advanced Load Balancer are available as an add-on license.
{: note}

NSX Advanced Load Balancer Controllers implement the control plane for the NSX Advanced Load Balancer. For high availability, it is typically deployed as a 3-node cluster. In a VMware Cloud Foundation, NSX Advanced Load Balancer Controllers run as VMs in the management domain.
{: important}

Deploying the Controller cluster nodes on the VMware Cloud Foundation management network requires 4 new {{site.data.keyword.cloud_notm}} bare metal server VLAN interfaces on the management network as shown in the following table. To create VLAN interfaces, see [Managing network interfaces for bare metal servers on {{site.data.keyword.vpc_short}}](/docs/vpc?topic=vpc-managing-nic-for-bare-metal-servers). 
{: important}

| Interface name | Interface type | VLAN ID | Subnet | Allow float | NSX interface | Distributed port group name |
| ---------------|----------------|---------|--------|-------------|---------------|---------------------------- |
| `vlan-nic-avi-0` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Advanced Load Balancer Controller 1 | `pg-mgmt` |
| `vlan-nic-avi-1` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Advanced Load Balancer Controller 2 | `pg-mgmt` |
| `vlan-nic-avi-2` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Advanced Load Balancer Controller 3 | `pg-mgmt` |
| `vlan-nic-avi-vip` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | NSX Advanced Load Balancer Controller VIP | `pg-mgmt` |
{: caption="Table 1. VLAN interfaces for NSX Advanced Load Balancer Controllers" caption-side="bottom"}

NSX Advanced Load Balancer Service Engine implements the data plane for the NSX Advanced Load Balancer. The NSX Advanced Load Balancer SEs perform load balancing for the configured applications. The NSX Advanced Load Balancer Controller cluster provides load-balancing services and it also manages the service engines that are deployed in the VI workload domain that is managed by the NSX-T Data Center.
{: important}

A new overlay management network is required to deploy the Service Engines in the VI workload domain's overlay with connectivity to the management domain's management network. This solution might require an {{site.data.keyword.vpc_short}} egress and ingress routes with a workload domain's Tier 0 Gateway HA VIP as the next hop.  
{: important}

## Related links
{: #vpc-vcf-deploy-vvs-links}

* [The Developer Ready Infrastructure for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-developer-ready-infrastructure-v1/GUID-641F8C25-CA4E-4F27-B467-484C849C7332.html){: external}
* [The Intelligent Logging and Analytics for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-intelligent-logging-and-analytics-v1/GUID-42022E8E-7C84-4864-AE49-69D016EF5600.html){: external}
* [The Intelligent Operations Management for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-intelligent-operations-management-v1/GUID-31B18AB1-9E88-4355-BECF-A90F1E1F7C19.html){: external}
* [The Private Cloud Automation for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-private-cloud-automation-v1/GUID-33896484-4331-46F1-8875-B487BBEDCE05.html){: external}
* [The Advanced Load Balancing for VMware Cloud Foundation validated solution](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-nsx-advanced-load-balancer-v1/GUID-F8696F0A-D91B-46B1-A824-8FAE461E57B3.html){: external}
