---

copyright:

  years:  2023, 2024

lastupdated: "2024-04-19"

keywords: flexible delete instance, delete flexible instance, remove flexible instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting Flexible instances
{: #vs_deletinginstance}

When you delete a {{site.data.keyword.vcf-flex}} instance, the VMware® product licenses and the VMware ESXi™ servers are released.

Because of resource dependencies, the ESXi servers in your instance might not be released until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle. At the end of the billing cycle, which is typically 30 days, the instance deletion is completed.

{{site.data.content.deletinginstance-important-note}}

The instance remains in **Deleting** status and the monthly ESXi servers are available for the remainder of the account monthly billing cycle. After the billing cycle ends, the status of the device changes from **ACTIVE** to **RECLAIM** until the reclaim process completes which can take days or weeks into the following month.

After the ESXi server reclaim process completes, the instance deletion is completed.

You can review the next account invoice to confirm that you are no longer billed for the deleted instance. From the {{site.data.keyword.cloud_notm}} console, click **Manage > Billing and usage** and click **Invoices**.

## Procedure to delete Flexible instances from the Resources page
{: #vs_deletinginstance-procedure1}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, find the Flexible instance to delete.
3. Click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to the **Status** column.
4. In the **Delete instance** window, enter the instance name to confirm, and click **Delete**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

## Procedure to delete Flexible instances from the instance details page
{: #vs_deletinginstance-procedure2}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the Flexible instance to delete.
3. Click **Actions** at the upper right of the instance details page and click **Delete instance**.
4. In the **Deleting instance** window, click **Delete**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

## Related links
{: #vs_deletinginstance-related}

* [Procedure to order Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [Viewing Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_viewinginstances)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
