---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware Solutions infrastructure domain
{: #adds-infra-domain}

The {{site.data.keyword.vmwaresolutions_full}} infrastructure domain holds the resource objects and user accounts for the administration of the {{site.data.keyword.vcf-auto}} instance only. Using this domain to hold resource objects and user accounts for your workload VMs is not recommended.

Within the vCenter Server design, the {{site.data.keyword.vmwaresolutions_short}} infrastructure Active Directory™ (AD) domain is used for:

* DNS - The appliances provisioned as part of the services have DNS entries in the AD. These entries enable the functions of the vCenter Server instance to use FQDN and do name lookups.
* Authentication services - An AD security group is added, and a number of accounts are added to enable the automation.

In {{site.data.keyword.vmwaresolutions_short}}, every primary instance deploys a forest root domain and configures the site topology. The {{site.data.keyword.vmwaresolutions_short}} AD/DNS is always going to be its own forest and domain, you cannot remove this forest or domain because it might break the {{site.data.keyword.vmwaresolutions_short}} automation. You can't migrate the users and resources to one of your existing domains or create a new domain, as you can't create the credentials for the IBM user named `automation`.

During the ordering process of a vCenter Server instance, the hostname prefix and the domain name are collected from the user that is pertinent to the Active Directory Domain Services (AD DS) and DNS configuration.

These values are then used to generate the username and server names of the instance. For more information, see [Ordering vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req).

## Domain controllers
{: #adds-infra-domain-controllers}

All AD domain controllers that are used in the {{site.data.keyword.vmwaresolutions_full}} infrastructure domain are exclusively yours and nothing is shared with other customers. You must provide operational management to monitor, update, back up, and recover these domain controllers.

These domain controllers are authoritative for the domain name that you selected for your instance. Ensure that you select a domain name that is unique within your domain space so that the DNS responsibility can be delegated completely to these controllers.

You must administer users, groups, computer and group policies, in the same manner as you do with your on-premises AD by using standard AD tools. You have full administrative control of the operating system and the AD environment that gets deployed as part of the vCenter Server instance provisioning. You can set up custom configurations and create simple or complex topology as needed.

During the ordering process, you can deploy:

* A single Microsoft® Windows® Server VSI for AD DS
* Two highly available Microsoft Windows VMs in the cluster

Currently, Microsoft Windows Server 2019 Standard is deployed for the operating system. The domain-functional level 2008 is set to allow for compatibility with an earlier version with any potential secondary instances. If compatibility with earlier (2008) secondary instances is not a consideration in your environment, you can upgrade the domain-functional level to a higher version.

For more information, see [Forest and domain functional levels](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/active-directory-functional-levels){: external}.

### Single VSI domain controller
{: #adds-infra-domain-controllers-vsi}

The following diagram shows the deployment pattern of the single VSI domain controller.

![Single VSI domain controller diagram](../../images/adds-advsi.svg "Single VSI domain controller diagram"){: caption="Figure 1. Single VSI domain controller diagram" caption-side="bottom"}

If you order the single VSI, it is recommended that you manually order a second VSI of the same type. Configure this VSI as a second domain controller to enable AD DS as a highly available service.

The following table describes the VSI configuration.

| Parameter          | Specification                                 |
|:-------------------|:----------------------------------------------|
| Operating System   | Windows Server 2019 Standard Edition (64-bit) |
| CPU                | 2 x 2.0 GHz or higher cores                   |
| RAM                | 8 GB                                          |
| Disk               | 100 GB (SAN)                                  |
| Uplink Port Speeds | 1 Gbps Private Network Uplink                 |
{: caption="Table 1. VSI specifications" caption-side="bottom"}

The domain controller is provisioned with a name of `ADNS<instance_name>.<root_domain>`, for example, `ADNSoncloud.cloud-east.myroot.local`. This server is the global catalog (GC) instance for the domain.

### Two highly available Microsoft Windows VMs in the cluster
{: #adds-infra-domain-controllers-ha}

The following diagram shows the deployment pattern of the two highly available VM domain controllers.
![Two highly available VM domain controllers diagram](../../images/adds-adha.svg "Two highly available VM domain controllers"){: caption="Figure 2. Two highly available VM domain controllers" caption-side="bottom"}

If you order the two high availability Microsoft Windows VMs, you must provide two Microsoft Windows Server 2019 licenses. For more information, see [Domain Name System configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-network-interface-settings#vc_orderinginstance-dns-config).

After the provisioning of the vCenter Server instance, you have 30 days to activate the VMs. The cluster is configured with a VM-VM anti-affinity rule. Therefore, Distributed Resource Scheduler (DRS) tries to keep the VMs apart by placing them on different physical vSphere ESXi hosts. The following table describes the VM configuration.

| Parameter        | Specification                                 |
|:-----------------|:----------------------------------------------|
| Operating System | Windows Server 2019 Standard Edition (64-bit) |
| CPU              | 2                                             |
| RAM              | 8 GB                                          |
| Disk             | 100 GB                                        |
{: caption="Table 2. HA VM specifications" caption-side="bottom"}

## Domain configuration
{: #adds-infra-domain-config}

After the domain controllers are provisioned, AD DS is configured as follows:

1. The domain name is set as <root_domain>, collected from the order process.
2. The `ic4V-vCenter` AD security group is added to the domain.
3. The following AD users are created in the domain:

   * `automation` - member of Administrators, Domain Admins, Domain Users, Enterprise Admins, `ic4V-vCenter`, Schema Admins, and Users AD groups.
   * `cloudbase-init` - member of the Administrators and Domain Users AD groups (this user is created by the VSI automation for use during initial provisioning of the VSI).
   * Add-on service accounts, for example, `prod-Caveonix-19765` or `prod-Zerto-5c9cb035` - member of `ic4V-vCenter` and `Domain Users` AD groups.

As the customer, you have full access to add more system administrators to the `ic4V-vCenter` AD security group to allow each administrator with access to vCenter. It is recommended that this domain holds only the resources and user accounts for administration of the vCenter Server instance only.

## User IDs
{: #adds-infra-domain-ids}

The {{site.data.keyword.cloud_notm}} automation initially configures some customer and IBM user IDs when the vCenter Server instance is created. The IBM user IDs are used by the automation for operations, such as adding clusters, vSphere ESXi hosts, or storage to your vCenter Server instance. These operations might fail if the IBM user IDs are deleted, disabled, or if their passwords are changed.

For more information, see [IBM user IDs](/docs/vmwaresolutions?topic=vmwaresolutions-audit_user_ids).

## Multisite topology
{: #adds-infra-domain-multisite}

As an option in {{site.data.keyword.vmwaresolutions_short}}, you can provision vCenter Server instances in a multisite topology. Your first instance is the primary instance, but subsequent orders can be either primary or secondary depending on the topology you want to create. By using a primary instance and then selecting secondary instances, you create a multisite topology.

You can have a maximum of 15 instances (one primary and 14 secondary) in a multisite configuration:

* Primary instance - To deploy the first instance, you define that instance as primary during the instance order process.
* Secondary instances - The instances that are attached to the primary instance are defined as secondary instances during the order process.

AD and DNS replication is automatically set up between the domain controllers on the primary and secondary instances. If you are using a single AD domain controller at each site, configure the DNS settings manually, as follows:

* Primary instance components - use the secondary instance DNS as the secondary DNS server.
* Secondary instance components - use the primary instance DNS as the secondary DNS server.

A multisite configuration has the following key aspects:

* Enhanced Linked Mode
* Cross vCenter NSX

Enhanced Linked Mode and Cross-vCenter NSX are complementary but separate from each other. For more information, see [Multisite configuration for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_multisite).

### Enhanced-linked mode
{: #adds-infra-domain-multisite-elm}

With Enhanced Linked Mode (ELM), you can view and search across all linked vCenter Server systems and replicate roles, permissions, licenses, policies, and tags.

ELM provides the following benefits:

* A single-pane-of-glass view into the environment with multiple vCenter Servers
* Simplified primary-secondary relationship creation by using single sign-on (SSO) credentials
* vCenter Server automation configuration for DNS name resolution for all the sites that are linked together
* In a cross-vCenter NSX environment, you can manage all NSX managers from a single vSphere Web Client
* Single pane of glass management across all sites for both NSX and normal vCenter functions

ELM simplifies the management of multiple vCenters, but it does not bring high availability for vCenter services. ELM is configured by the {{site.data.keyword.vmwaresolutions_short}} automation when a secondary instance is deployed.

### Cross vCenter NSX
{: #adds-infra-domain-multisite-nsx}

In cross-vCenter NSX, you have a primary NSX Manager and multiple secondary NSX managers. Each of these NSX managers is linked to a separate vCenter Server. On the primary NSX Manager, you can create universal NSX components such as switches and routers that are viewable from the secondary NSX managers.

Cross-vCenter NSX includes the following features:

* The same logical networks are available in the cross-vCenter environment, so it's possible for VMs on any cluster on any vCenter Server system to be connected to the same logical network.
* Firewall rules are managed from one centralized location, and apply to the VM regardless of location or vCenter Server system.
* Centralized management of universal objects, reducing administration effort.
* VMs can be migrated by using vMotion across vCenter Servers without having to reconfigure the VM or change firewall rules.

When cross-vCenter NSX is combined with ELM, you can view and manage any of the NSX managers and all of the universal NSX components from any of the linked vCenter Servers. ELM is not a prerequisite or requirement for cross-vCenter NSX. Without ELM, you can still create cross-vCenter universal transport zones, universal switches, universal routers, and universal firewall rules. However, without ELM in place, you must log in to the individual vCenter Servers to access each NSX Manager instance.

Cross vCenter NSX is not automatically deployed. You must deploy it manually by following the tasks in [Configuring the primary NSX manager](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.4/com.vmware.nsx.cross-vcenter-install.doc/GUID-0B74FB40-1D90-4A6A-B7CE-B4EF3B923452.html){: external}.

### Active Directory, SSO, and DNS in a multisite topology
{: #adds-infra-domain-multisite-ad}

AD, DNS, and SSO are configured slightly differently in a primary and secondary instance.

The primary instance has the following configuration:

* AD and DNS root domain and SSO domain
* vCenter Server belonging to root domain with instance-specific name
* Hosts belonging to root domain with instance-specific prefix

The secondary instances have the following configuration:

* Same root domain and SSO domain as primary instance
* DNS and AD replication setup between the domain controllers on the primary and secondary instances
* vCenter Server belonging to root domain and SSO domain with instance-specific name
* Hosts belonging to root domain with instance-specific prefix
* Enhanced Linked Mode (ELM) setup between the secondary instance vCenter to the vCenter in the primary instance

## Customer user IDs
{: #adds-infra-domain-userid}

The customer user IDs and passwords for the vCenter Server instance are available through the instance details on the VMware Solutions console. For more information, see [vCenter and Platform Services Controller user IDs](/docs/vmwaresolutions?topic=vmwaresolutions-audit_user_ids).

## Domain Name System configuration
{: #adds-infra-domain-dns}

The vCenter Server instance design integrates DNS services on the AD domain controllers:

* The domain structure is specified during the instance order process.
* The domain controllers are configured to be authoritative for the DNS domain.
* The domain controllers servers are configured to point to the {{site.data.keyword.cloud_notm}} DNS servers for all other zones.
* Any secondary vCenter Server instances that are integrated to the primary instance use the same DNS name structure.

When a secondary vCenter Server instance is linked to the primary instance, the vCenter Server instance appliances are configured:

* DNS is configured with the primary instances AD DNS server IP address.
* Secondary DNS is configured with the secondary instances AD DNS server IP address.

AD DS DNS is configured with a forward lookup zone with the name of <root_domain>, and populated with the following host (A) records:

* `clouddriver`
* `<instance_name>-vc`
* `<instance_name>-nsx`
* Add-on services when ordered. For example, HCX, Caveonix RiskForesight, Veeam, or Zerto, with instance-specific names

Reverse lookup zones with the start of authority (SOA), name server (NS), and the required pointer (PTR) records for the appliances are configured in the following subnets:

* Management subnet
* `Internal-mgmt` subnet
* Add-on services subnets. For example, HCX subnet, risk foresight subnet.

The forwarder section is configured with:

* 10.0.80.12
* 10.0.80.11

Forwarders are DNS servers that the AD DNS server can use to resolve DNS queries for records that the AD server cannot resolve. 10.0.80.12 and 10.0.80.11 are the two addresses for {{site.data.keyword.cloud_notm}} Resolving Name Servers. Resolving name servers are located on the private network and act as DNS resolvers. The private resolvers query the Internet root name servers for domain lookups and resolve this information over the private network to keep your bandwidth usage down, reduce the load on the authoritative servers, and offer quick resolution. Private network resolvers are a convenience service for our customers.

All deployed appliances (vCenter Server Appliance, NSX Manager and Controllers, and vSphere ESXi hosts) have their DNS settings configured to point to the AD DNS server as their default DNS. You can customize the DNS zone configuration if it does not interfere with the configuration of the deployed components.

## Related links
{: #adds-infra-domain-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
* [Getting started with VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-getting-started)

