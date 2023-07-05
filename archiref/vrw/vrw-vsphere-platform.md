---

copyright:

  years:  2020, 2023

lastupdated: "2023-06-19"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# vSphere components
{: #vrw-vsphere-platform}

The {{site.data.keyword.cloud}} for VMware® Regulated Workloads is built with vSphere technology, which includes the VMware ESXi™ hypervisors and vCenter appliance.

## Management cluster
{: #vrw-vsphere-platform-management}

The management software stack consists of vCenter Server, AD/DNS, and VMware Aria® Operations™ tooling. vCenter Server manages all hosts in the vCenter Server instance. AD/DNS provide Domain Name Services (DNS) and management authentication services, a local NTP source, and role-based access control (RBAC) for access to the vCenter, VMware Aria operations tooling, and NSX-T™ administration portal. The VMware Aria operations tooling includes VMware Aria Operations Manager, and VMware Aria Operations™ for Logs. These components collectively provide a native console for vSphere operations, ability to automate management of the cloud platform, centralized log collection and analysis, and network visibility and optimization up to the hypervisor. SaaS consumer workloads are not monitored by default.

Within the Management cluster, shared storage is used to provide enhanced resiliency to the management stack. The use of shared storage provides rapid restoration of management components if an ESXi host is lost. vSAN based storage is used to keep all management stack data in the account boundary. vSAN requires a minimum cluster size of four ESXi hosts.

The vCenter appliance provides the necessary interfaces to the virtualization administrators, which include a robust RESTful API. Resilience of the vCenter appliance is delivered by using vSphere native DRS functions such as vMotion. More management components are deployed to the management cluster but only the vCenter appliance is responsible for direct operation of the platform.

### Active Directory and DNS
{: #vrw-vsphere-platform-management-ad}

Active Directory serves to authenticate accesses to manage the VMware® instance only and not to house users of the workloads in the deployed instances. The forest root domain name of the Active Directory server equals to the Domain Name Services (DNS) domain name that you specify during initial deployment.

Domain name services (DNS) in this design support cloud management and infrastructure components only. The DNS zone files are also replicated on the Active Directory servers.

### Veeam management backup
{: #vrw-vsphere-platform-management-veeam}

Veeam is used to continuously back up the management stack for protection against disasters and rapid restoration to known good states. Veeam is also available for use in the workload cluster to provide back up and disaster recovery services for the SaaS consumer workloads.

### vCenter
{: #vrw-vsphere-platform-management-vcenter}

The vCenter Server with an embedded PSC is installed on a portable subnet on the private VLAN that is associated with management VMs. Its default gateway is set to the IP address assigned on the perimeter gateway.

One vCenter Server is deployed to manage the management cluster, the gateway cluster, and the SaaS consumer workload clusters.

### NSX-T
{: #vrw-vsphere-platform-management-nsxt}

NSX-T™ provides a highly secure and flexible software-defined network to support the application requirements. NSX-T controllers are hosted in the management cluster.

NSX-T is configured with three controllers, which provide a highly available and redundant configuration. Additionally a virtual IP (VIP) address is used to access the cluster to provide fault tolerance and high availability to NSX Manager nodes. Each controller manager is assigned a VLAN–backed IP address from the private portable address block that is designated for management components.

Hosting the NSX-T controllers in the management cluster ensures that network and security changes are not possible by anyone other than the designated administrators.

### VMware Aria Operations Manager
{: #vrw-vsphere-platform-management-vrops}

The VMware Aria Operations analytics cluster contains the nodes that analyze and store data from the monitored components in this deployment.

The analytics cluster consists of the following components:
- Primary node – The primary node is the initial node in a VMware Aria Operations cluster. In a large environment, this node manages all the other nodes.
- Primary node replica – This node enables high availability of the primary node.
- Data nodes – The data node enables scale out of VMware Aria Operations in larger environments.

For more information, see [VMware Aria Operations Manager design](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-vrops).

### VMware Aria Operations for Logs
{: #vrw-vsphere-platform-management-vrli}

The VMware Aria Operations for Logs environment consists of four virtual machines (VMs) with an integrated load balancer.

VMware Aria Operations for Logs enables real-time logging for components in the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads environment. The design deploys a VMware Aria Operations for Logs cluster that consists of four nodes in each instance. This configuration provides continued availability and increased log ingestion rates.

VMware Aria Operations for Logs collects log events from the following virtual infrastructure and cloud management components (logging clients):

- vCenter Server
- ESXi hosts
- NSX controllers
- NSX routers
- NSX distributed firewall ESXi kernel module
- VMware Aria Operations Manager analytics cluster nodes and remote collectors
- VMware Aria Operations for Logs instance in the other instances as a result of event forwarding (MZR configuration)

For more information, see [VMware Aria Operations for Logs design](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-vrli).

### Backup server
{: #vrw-vsphere-platform-management-backupserver}

This server is a Linux® VM that is manually deployed to provide a location for file-based backups. It is used by the vCenter Server Appliance to perform a file-based backup of the vCenter Server core configuration, inventory, and historical data. Similarly, NSX controller backups are done to this server.

### Caveonix server
{: #vrw-vsphere-platform-management-caveonix}

The Caveonix RiskForesight service manages cyberrisk and compliance risk with proactive monitoring and automated defense controls to protect against threats and to meet industry or government regulations.

## Gateway cluster
{: #vrw-vsphere-platform-edge}

No vSphere management components are deployed to the gateway cluster. The tooling in the management cluster is used to manage the gateway cluster ESXi hosts.

## Workload cluster
{: #vrw-vsphere-platform-workload}

THe NSX-T gateway cluster VMs that house the Tier-0 and Tier-1 routers are on the workload clusters. No vSphere management components are deployed to the workload cluster. The tooling in the management cluster is used to manage the workload cluster ESXi hosts.

## Related links
{: #vrw-vsphere-platform-related}

* [IBM Cloud compliance programs](https://www.ibm.com/cloud/compliance)
