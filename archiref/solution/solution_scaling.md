---

copyright:

  years:  2016, 2023

lastupdated: "2023-12-07"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Scaling capacity
{: #solution_scaling}

After initial deployment, you can scale out the compute capacity from the {{site.data.keyword.vmwaresolutions_full}} console. The design supports the following scale-out paths:
* Addition of new sites managed by separate VMware vCenter Servers®
* Addition of new clusters
* Addition of new hosts to an existing cluster

## Adding more sites
{: #solution_scaling-sites}

{{site.data.keyword.vmwaresolutions_short}} can use the {{site.data.keyword.cloud_notm}} worldwide data center presence and integrated network backbone to allow for various cross-geographies use cases to be deployed and functioning within a fraction of the time that it would take to build such an infrastructure from scratch.

In this design, the definition of a multisite deployment consists of the following items.
* An initial or primary VMware deployment that contains a new DNS/AD root domain, SSO domain, and SSO site name to be provided.
* Single or multiple secondary sites that are provisioned into the primary sites SSO domain that requires the following configuration:
   * New SSO site name
   * Shared DNS root domain with primary instance
   * DNS and AD replication setup between the secondary and primary site AD VMs
   * vCenter setup with Enhanced Linked Mode to the primary site vCenter

Additionally, the NSX Manager in secondary sites can be set up as secondary NSX managers for the NSX Manager on the primary site. You must complete this as a manual process.

## Adding new clusters
{: #solution_scaling-clusters}

You can also scale out the compute capacity by creating a new cluster from the {{site.data.keyword.vmwaresolutions_short}} console and ordering new hosts that are automatically added to the new cluster.

This method enables you to achieve the following things:
* Creating an additional, separate cluster in the environment.
* Separating management workloads from application workloads physically and logically.
* Separating workloads based on other characteristics, for example, Microsoft® SQL database cluster.
* Deploying applications in highly available topologies.

When the initial cluster is converted into a management-only cluster, you must complete manual steps for the migration of existing workloads. This might involve the reattachment of data stores to the new cluster or alternately storage migration. The IP addresses of the workloads might need to be changed if the new cluster resides in a different {{site.data.keyword.cloud_notm}} pod or if the cluster is assigned to a different VLAN ID.
{: note}

## Adding ESXi hosts into existing clusters
{: #solution_scaling-hosts}

You can scale out an existing cluster by ordering hosts from the {{site.data.keyword.vmwaresolutions_short}} console. The new hosts are automatically added to the cluster. You might need to adjust the HA reservation policy for the cluster based on your reservation requirements.

## Related links
{: #solution_scaling-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
* [Design overview](/docs/vmwaresolutions?topic=vmwaresolutions-design_overview)
