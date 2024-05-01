---

copyright:

  years:  2023, 2024

lastupdated: "2024-04-03"

keywords: cyber recovery, add hosts cyber recovery, add servers cyber recovery, remove hosts cyber recovery

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Expanding and contracting capacity for {{site.data.keyword.cr}} instances
{: #cr-addingremovingservers}

Expand or contract the capacity of your {{site.data.keyword.cr}} instances according to your business needs, by adding or deleting VMware vSphere® ESXi™ servers or Network File System (NFS) storage.

## Before you add or delete ESXi servers
{: #cr-addingremovingservers-before}

You must migrate the VMware vCenter Server® virtual machines (VMs) before you delete a server. This requirement applies to the vCenter Server VM and to the additional vCenter HA VMs on the management cluster.

## Adding or deleting ESXi servers
{: #cr-addingremovingservers-add-delete-esxi}

The processes to add and delete servers for {{site.data.keyword.cr}} instances are similar to the ones for Automated instances. For more information, see the following topics:
* [Adding ESXi servers to Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Deleting ESXi servers from Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_removingservers)

## Adding or removing NFS storage
{: #cr-addingremovingservers-add-delete-nfs}

The processes to add and remove NFS storage for {{site.data.keyword.cr}} instances are similar to the ones for Automated instances. For more information, see the following topics:
* [Adding NFS storage to Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs)
* [Removing NFS storage from Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_removingnfs)

## Related links
{: #cr-addingremovingservers-related}

* [Planning for {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_planning)
* [Requirements for {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
* [Adding, viewing, and deleting clusters for {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_addingviewingclusters)
