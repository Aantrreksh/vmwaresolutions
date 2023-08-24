---

copyright:

  years:  2022, 2023

lastupdated: "2023-08-04"

keywords: Cyber Recovery delete instance, delete Cyber Recovery, remove Cyber Recovery

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting Cyber Recovery instances
{: #cr_deletinginstance}

To release the components that you ordered in a Cyber Recovery instance, delete the instance.

When you delete a Cyber Recovery instance, the following components are released sequentially:
1. All deployed services
2. The Support fee for VMware NSX-T™ instances or the Support and Services fee for NSX-V instances
3. VMware® product licenses
4. VMware ESXi™ servers
5. Subnets
6. VLANs

{{site.data.content.deletinginstance-delete-vlans}}

{{site.data.content.deletinginstance-delete-info}}

{{site.data.content.deletinginstance-important-note}}

The instance remains in **Deleting** status and the monthly ESXi servers are available for the remainder of the account monthly billing cycle. After the billing cycle ends, the status of the device changes from **ACTIVE** to **RECLAIM** until the reclaim process completes which can take days or weeks into the following month.

After the ESXi server reclaim process completes, the subnets and VLANs are deleted, and the instance deletion is completed.

You can review the next account invoice to confirm that you are no longer billed for this instance. From the {{site.data.keyword.cloud_notm}} console, click **Manage > Billing and usage** and click **Invoices**.

## Procedure to delete Cyber Recovery instances from the Resources page
{: #cr_deletinginstance-procedure1}

1. From the VMware Solutions console, click **Resources > Cyber Recovery** from the left navigation pane.
2. In the **Cyber Recovery** table, find the instance to delete.
3. Click the vertical overflow menu next to the **Status** column, and then click **Delete instance**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

4. If you want to delete the instance record from the VMware Solutions console, complete the following steps:
   1. Click the vertical overflow menu next to the **Status** column and click **Delete from the console**.
   2. In the **Delete instance** window, click **Delete**.

## Procedure to delete Cyber Recovery instances from the instance details page
{: #cr_deletinginstance-procedure2}

1. From the VMware Solutions console, click **Resources > Cyber Recovery** from the left navigation pane.
2. In the **Cyber Recovery** table, click the instance to delete.
3. Click **Actions** next to **vCenter console**, and then click **Delete instance**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, the instance components are released, and the instance status is changed to **Deleted**.

4. If you want to delete the instance record from the VMware Solutions console, complete the following steps:
   1. Click **Actions** again and click **Delete from the console**.
   2. In the **Delete instance** window, click **Delete**.

## Related links
{: #cr_deletinginstance-related}

* [Ordering Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
* [Viewing Cyber Recovery instances](/docs/vmwaresolutions?topic=vmwaresolutions-cr_viewinginstances)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
