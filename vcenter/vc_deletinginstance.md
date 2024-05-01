---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-25"

keywords: delete automated instance, delete vcf classic, remove vcf automated

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting Automated instances
{: #vc_deletinginstance}

To release the components that you ordered in a {{site.data.keyword.vcf-auto}} instance, delete the instance.

{{site.data.content.deletinginstance-components-list}}

{{site.data.content.deletinginstance-delete-vlans}}

{{site.data.content.deletinginstance-delete-info}}

{{site.data.content.deletinginstance-important-note}}

The instance remains in **Deleting** status and the monthly ESXi servers are available for the remainder of the account monthly billing cycle. After the billing cycle ends, the status of the device changes from **ACTIVE** to **RECLAIM** until the reclaim process completes which can take days or weeks into the following month.

After the ESXi server reclaim process completes, the subnets and VLANs are deleted and the instance deletion is completed.

You can review the next account invoice to confirm that you are no longer billed for this instance. From the {{site.data.keyword.cloud_notm}} console, click **Manage > Billing and usage** and click **Invoices**.

## Procedure to delete Automated instances from the Resources page
{: #vc_deletinginstance-procedure1}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, find the instance to delete.
3. Click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to the **Status** column.
4. In the **Delete instance** window, enter the instance name to confirm, and click **Delete**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

## Procedure to delete Automated instances from the instance details page
{: #vc_deletinginstance-procedure2}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the instance to delete.
3. Click **Actions** next to **vCenter console** and click **Delete instance**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

## Related links
{: #vc_deletinginstance-related}

* [Ordering Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Viewing Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Expanding and contracting capacity for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
