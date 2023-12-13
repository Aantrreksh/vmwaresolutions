---

copyright:

  years:  2016, 2023

lastupdated: "2023-11-15"

keywords: vCenter Server delete instance, delete vCenter Server, remove vCenter Server, vmware multizone, vcenter server multizone, delete vCenter Server multizone

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting vCenter Server instances
{: #vc_deletinginstance}

To release the components that you ordered in a VMware vCenter Server® instance, delete the instance.

{{site.data.content.deletinginstance-components-list}}

{{site.data.content.deletinginstance-delete-vlans}}

{{site.data.content.deletinginstance-delete-info}}

{{site.data.content.deletinginstance-important-note}}

The instance remains in **Deleting** status and the monthly ESXi servers are available for the remainder of the account monthly billing cycle. After the billing cycle ends, the status of the device changes from **ACTIVE** to **RECLAIM** until the reclaim process completes which can take days or weeks into the following month.

After the ESXi server reclaim process completes, the subnets and VLANs are deleted and the instance deletion is completed.

You can review the next account invoice to confirm that you are no longer billed for this instance. From the {{site.data.keyword.cloud_notm}} console, click **Manage > Billing and usage** and click **Invoices**.

## Procedure to delete vCenter Server instances from the Resources page
{: #vc_deletinginstance-procedure1}

1. From the VMware Solutions console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, find the instance to delete.
3. Click the vertical overflow menu next to the **Status** column and click **Delete instance**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

4. If you want to delete the instance record from the VMware Solutions console, complete the following steps:
   1. Click the vertical overflow menu next to the **Status** column and click **Delete from the console**.
   2. In the **Delete instance** window, click **Delete**.

## Procedure to delete vCenter Server instances from the instance details page
{: #vc_deletinginstance-procedure2}

1. From the VMware Solutions console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance to delete.
3. Click **Actions** next to **vCenter console** and click **Delete instance**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.
   
4. If you want to delete the instance record from the VMware Solutions console, complete the following steps:
   1. Click **Actions** again and click **Delete from the console**.
   2. In the **Delete instance** window, click **Delete**.

## Related links
{: #vc_deletinginstance-related}

* [Ordering vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Viewing vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Expanding and contracting capacity for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
