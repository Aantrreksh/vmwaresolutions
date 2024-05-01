---

copyright:

  years: 2023, 2024

lastupdated: "2024-04-04"

keywords: delete vmware cloud foundation instance, vmware cloud foundation instance, delete instance, delete vmware cloud edition instance

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deleting {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-deleting}

When you delete a {{site.data.keyword.vcf-vpc}} instance, the following components are released:
1. {{site.data.keyword.vcf-vpc-short}} licenses
2. {{site.data.keyword.vcf-vpc-short}} products
3. All {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) assets
4. All {{site.data.keyword.cloud_notm}} services that were deployed

   You can review the next account invoice to confirm that you are no longer being billed for this instance. From the {{site.data.keyword.cloud_notm}} console, click **Manage > Billing and usage**, then click **Invoices**.
   {: tip}

## Before you delete {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-deleting-before}

Only the resources that were created from the VMware Solutions console can be deleted. If you added ESXi servers to the {{site.data.keyword.vcf-vpc-short}} instance manually, the resources for those servers must be deleted manually as well.

## Procedure to delete {{site.data.keyword.vcf-vpc-short}} instances from the Resources page
{: #vpc-vcf-deleting-proc1}

1. In the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-vpc-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-vpc}}** table, find the instance to delete.
3. Click the recycle bin icon next to the **Status** column.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, all {{site.data.keyword.vpc_short}} resources and {{site.data.keyword.cloud_notm}} service instances that are associated with this instance are deleted, and the instance is removed from the table.

   If you receive a deletion error after you clicked **Delete instance**, click **Delete instance** again.
   {: note}

## Procedure to delete {{site.data.keyword.vcf-vpc-short}} instances from the instance details page
{: #vpc-vcf-deleting-proc2}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-vpc-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-vpc}}** table, click the instance to delete.
3. Click **Actions** next to **Go to SDDC console** and click **Delete instance**.

   The instance status is changed to **Deleting**. When the instance is deleted successfully, all {{site.data.keyword.vpc_short}} resources and {{site.data.keyword.cloud_notm}} service instances that are associated with this instance are deleted, and the instance is removed from the table.

   If you receive a deletion error after you clicked **Delete instance**, click **Delete instance** again.
   {: note}

## Related links
{: #vpc-vcf-deleting-links}

* [{{site.data.keyword.vcf-vpc-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw)
* [Ordering {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ordering)
* [Viewing {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-viewing)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
