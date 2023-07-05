---

copyright:

  years:  2023

lastupdated: "2023-06-20"

keywords: vmware vSphere delete instance, delete vmware vSphere instance, remove vmware vSphere instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting VMware vSphere instances
{: #vs_deletinginstance}

When you delete a VMware vSphere® instance, the VMware® product licenses and the VMware ESXi™ servers are released.

Because of resource dependencies, the ESXi servers in your instance might not be released until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle. At the end of the billing cycle, which is typically 30 days, the instance deletion is completed.

{{site.data.content.deletinginstance-important-note}}

The instance remains in **Deleting** status and the monthly ESXi servers are available for the remainder of the account monthly billing cycle. After the billing cycle ends, the status of the device changes from **ACTIVE** to **RECLAIM** until the reclaim process completes which can take days or weeks into the following month.

After the ESXi server reclaim process completes, the instance deletion is completed.

You can review the next account invoice to confirm that you are no longer billed for the deleted instance. From the {{site.data.keyword.cloud_notm}} console, click **Manage > Billing and usage**, then click **Invoices**.

## Procedure to delete VMware vSphere instances from the Resources page
{: #vs_deletinginstance-procedure1}

1. From the VMware Solutions console, click **Resources > vSphere** from the left navigation pane.
2. In the **vSphere** table, find the instance to delete.
3. Click the vertical overflow menu next to the **Status** column and click **Delete**.
4. In the **Deleting instance** window, click **Delete**.
   The status of the instance is changed to **Deleting**. When the instance is deleted successfully, the components of the instance are released, and the status of the instance is changed to **Deleted**.
5. If you want to delete the instance record from the VMware Solutions console, complete the following steps:
   1. Click the vertical overflow menu next to the **Status** column again and click **Delete from the console**.
   2. In the **Deleting instance** window, click **Delete**.

## Procedure to delete VMware vSphere instances from the instance details page
{: #vs_deletinginstance-procedure2}

1. From the VMware Solutions console, click **Resources > vSphere** from the left navigation pane.
2. In the **vSphere** table, click the instance to delete.
3. Click the **Actions** at the upper right of the instance details page and click **Delete instance**.
4. In the **Deleting instance** window, click **Delete**.
   The status of the instance is changed to **Deleting**. When the instance is deleted successfully, the components of the instance are released, and the status of the instance is changed to **Deleted**.
5. If you want to delete the instance record from the VMware Solutions console, complete the following steps:
   1. Click **Actions** again and click **Delete from the console**.
   2. In the **Deleting instance** window, click **Delete**.

## Related links
{: #vs_deletinginstance-related}

* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [Viewing VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_viewinginstances)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
