---

copyright:

  years:  2022, 2023

lastupdated: "2023-05-19"

keywords: vCenter Server delete clusters, delete clusters, delete vCenter Server cluster, vmware multizone, vCenter Server multizone delete clusters, delete vCenter Server cluster

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting clusters from vCenter Server instances
{: #vc_deletingclusters}

You can delete clusters from VMware vCenter Server® instances when you do not need them.

Deleting clusters from vCenter Server instances with VMware vSphere® 6.5 is not supported.
{: note}

## Before you delete clusters from vCenter Server instances
{: #vc_deletingclusters-before}

* {{site.data.content.para-vcenterremoveclusters}}
* You can delete any cluster except for the first cluster (the one that is created during initial deployment).
* You can delete multiple clusters at a time. You can also delete a cluster while another cluster is being created or deleted.
* Ensure that all nodes in a cluster are powered on and operational before you delete the cluster.
* When you delete a cluster, all VMs from the cluster are also deleted and they can't be recovered. If you want to keep the VMs, migrate them to other clusters.
* When you delete a cluster, all storage and subnets that are associated with the cluster are deleted as well. To view the storage and subnets that are associated with a cluster, see the cluster details page.
* You do not have to delete any services that are installed on the cluster, including services on a gateway cluster. The services are automatically deleted when you delete the cluster.

## Procedure to delete clusters from vCenter Server instances
{: #vc_deletingclusters-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance that you want to delete clusters from.

   Ensure that the instance status is **Available**. Otherwise, you can't delete clusters from the instance.
   {: important}

3. Click the **Infrastructure** tab. In the **Clusters** table, locate the cluster that you want to delete and click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to the **Status** column.
4. In the **Delete cluster** window, confirm that you completed the migration of VMs to other clusters, if needed, and that you want to delete the cluster. Click **Delete**.

## Related links
{: #vc_deletingclusters-related}

* [Viewing vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Expanding and contracting capacity for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
