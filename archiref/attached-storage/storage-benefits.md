---

copyright:

  years:  2016, 2022

lastupdated: "2022-04-28"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# About attached storage for vCenter Server
{: #storage-benefits}

Attached storage is an extension of the VMware vCenter Server® offering. The attached storage solution architecture for the vCenter Server details the components of the solution and the high-level configuration of each component in the design.

For more information about the vCenter Server design, see [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview).

## Key benefits of attached storage for vCenter Server
{: #storage-benefits-key-benefits}

While attached storage isn't a prerequisite for VMware® environments, its use as a shared storage device provides many benefits to users for IT operations. Using shared storage devices can help you achieve high availability, distributed resource scheduler, efficient use of storage capacity, and simplified management through enabling the vSphere functions described in the following table.

| Function | Description |
|:------- |:----------- |
| vSphere Distributed Resource Scheduler and Resource Pools | This feature allows for abstraction and flexible management of resources through load balancing and virtual machine (VM) placement. Resource pools can be grouped into hierarchies and used to hierarchically partition available CPU and memory resources. |
| vSphere High Availability | This feature provides HA for VMs (by pooling them) and for the hosts in a cluster. The hosts in the cluster are monitored. If a failure occurs, the VMs on a failed host are restarted on alternative hosts. |
| vSphere Datastore Clusters | This feature provides a collection of datastores with shared resources and a shared management interface. |
| vSphere Fault Tolerance | This feature provides continuous availability to VMs, by eliminating downtime and disruption, even if a complete host failure occurs. |
{: caption="Functions description for attached storage for vCenter Server" caption-side="bottom"}

## Related links
{: #storage-benefits-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
