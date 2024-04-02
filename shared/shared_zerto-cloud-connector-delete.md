---

copyright:

  years:  2021, 2024

lastupdated: "2024-04-02"

keywords: zerto, delete zerto cloud connector

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting Zerto Cloud Connector
{: #shared_zerto-cc-delete}

{{site.data.content.shared-deprecated-note}}

You can delete the Zerto Cloud Connector (ZCC) when it is no longer needed.

## Before you begin
{: #shared_zerto-cc-delete-prereq}

* Review the following considerations before you delete Zerto Cloud Connector:
   * The on-premises site is unpaired from the {{site.data.keyword.cloud}} site and all workloads that are moved from the on-premises site are deleted.
   * All Virtual Protection Groups and the VMs replicated from the on-premises site to the {{site.data.keyword.cloud_notm}} site are deleted.
* When you delete the ZCC, you unpair the on-premises workloads from {{site.data.keyword.cloud_notm}}.

## Procedure to delete Zerto Cloud Connector
{: #shared_zerto-cc-delete-procedure}

1. Under the **Enabled services** on the virtual data center details page, click **Delete ZCC** in the Zerto Cloud Connector details table.
2. In the **Delete Zerto Cloud Connector** window, review, and accept the delete confirmation and click **Delete**. The status of the ZCC is changed to **Deleting**. When the ZCC is deleted successfully, the status is changed to **Deleted**.

## Related links
{: #shared_zerto-cc-delete-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [Accessing the Zerto self-service portal](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-portal)
* [Ordering a Zerto Cloud Connector](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-order)
* [Viewing Zerto Cloud Connector details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-view)
* [Zerto for VMware vSphere](https://www.zerto.com/solutions/workloads-and-applications/vmware-vsphere/){: external}
* [Zerto Support and Services](https://www.zerto.com/support-and-services/){: external}
