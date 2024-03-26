---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Infrastructure management design
{: #vpc-ryo-infrastructuremgmt}

Infrastructure management refers to the components that manage the VMware® infrastructure.

* The VMware vCenter Server® with an embedded Platform Services Controller (PSC) is the centralized platform for managing VMware vSphere® environments. Also, it is one of the fundamental components in this solution.
* The PSC is used to provide a set of infrastructure services, which include VMware vCenter Single Sign On (SSO), license service, lookup service, and VMware certificate authority.

The design uses a PSC function that is integrated into an instance of vCenter Server. The PSC and vCenter Server are housed within the same virtual machine (VM).

![Infrastructure management](../../images/vpc-ryo-diagrams-overview-management.svg "Infrastructure management"){: caption="Figure 1. Infrastructure management" caption-side="bottom"}

The PSC located in the primary instance is assigned the default SSO domain of `vsphere.local`.

## vCenter Server design
{: #vpc-ryo-infrastructuremgmt-vcenter}

Beginning in vSphere 7.0, vCenter Server contains all PSC services, preserving the functionality and workflows, including authentication, certificate management, tags, and licensing. It is no longer necessary nor possible to deploy and use an external PSC. All PSC services are consolidated into vCenter Server, and deployment and administration are simplified.

When you deploy vCenter Server, you can select the size of the appliance.

Public Gateway attached to the management subnet can be used to download updates for vCenter Server and VMware ESXi™ hosts.

### vCenter Server cluster specification
{: #vpc-ryo-infrastructuremgmt-vcenter-cluster}

With this design, you can cluster the vSphere ESXi hosts that you use as part of your deployment in your VPC. However, before clusters can be created, a data center object must be created that signifies the location of the vSphere ESXi hosts and the Zone within a {{site.data.keyword.cloud}} MZR. A cluster can be created after the data center object is created. The cluster can be deployed with VMware vSphere High Availability (HA) and VMware vSphere Distributed Resource Scheduler (DRS) enabled when you use of the available shared storage options.

### vSphere Distributed Resource Scheduler
{: #vpc-ryo-infrastructuremgmt-vsphere-drs}

The design recommends that you use vSphere Distributed Resource Scheduling (DRS) in the clusters to place VMs. Also, you must use DRS in extra clusters to dynamically migrate VMs to achieve balanced clusters. The automation level can be set to fully automated so that initial placement and migration recommendations are run automatically by vSphere. Additionally, the migration threshold can be set to moderate so that vCenter applies priority 1, 2, 3 recommendations to achieve at least a decent improvement in the load balance of the cluster.

One of the available shared storage options is needed for clusters that are enabled for DRS.
{: note}

### vSphere High Availability
{: #vpc-ryo-infrastructuremgmt-vsphere-ha}

The design recommends that you use vSphere High Availability (HA) in the cluster to detect compute failures and recover VMs that run in a cluster. The vSphere HA feature is configured with both the Host Monitoring and Admission Control options that are enabled in the cluster. Additionally, the initial cluster reserves one node resources as spare capacity for the admission control policy.

One of the available shared storage options is needed for clusters that are enabled for HA.
{: note}

You are responsible to adjust the admission control policy when the cluster is later expanded or contracted.
{: note}

### Enhanced vMotion Compatibility
{: #vpc-ryo-infrastructuremgmt-evc}

To simplify vMotion compatibility across cluster nodes with potentially differing CPU capabilities, Enhanced vMotion Compatibility (EVC) mode can be enabled at the highest available level that is supported by the vSphere version. This setting ensures vMotion compatibility across cluster nodes when newer processors arrive within {{site.data.keyword.vpc_short}} inventory. The setting allows for cluster expansion in the future if the original processor is no longer in inventory.

## Related links
{: #vpc-ryo-infrastructuremgmt-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
