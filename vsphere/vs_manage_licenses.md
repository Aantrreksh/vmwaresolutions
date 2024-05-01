---

copyright:

  years:  2023, 2024

lastupdated: "2024-04-24"

keywords: flexible add license, add license flexible, flexible delete license, delete license flexible, flexible view license, view license flexible

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Managing licenses for Flexible instances
{: #vs_manage_licenses}

Managing licenses for Flexible instances is supported only for IBM-provided licenses. It does not apply to BYOL (Bring Your Own License).
{: important}

You can add licenses for various VMware components in your {{site.data.keyword.vcf-flex}} instance. For more information about these components, see [Licensing](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-licensing-settings).

## Before you manage licenses for Flexible instances
{: #vs_manage_licenses-prereq}

* For instances with VMware vSphere 6, you cannot add licenses. To add licenses, upgrade your vSphere software to version 7. For more information, see [Upgrading vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).
* The VMware vSAN license is part of your instance by default and it cannot be deleted.
* If you want to combine license keys, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

## Procedure to add licenses to Flexible instances
{: #vs_manage_licenses-add-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the Flexible instance for which you want to add licenses.
3. Click the **Licensing** tab. From here, you can view the licenses in your instance. Click **Add licenses**.
5. On the **Add licenses** side panel, select the licenses that you want to add from the list of available components. The number of licenses that is displayed in the **Quantity** column is determined by the number of hosts in your instance.
6. In the **Summary** section, review the estimated pricing and ensure that the account to be charged is correct. Click **Add**.

## Results after you add licenses for Flexible instances
{: #vs_manage_licenses-results}

* You are notified by email that your request is being processed. On the console, the status of the instance is changed to **Modifying**.
* If you do not see the licenses being added from the instance, check your email or console notifications for more details.

## Related links
{: #vs_manage_licenses-links}

* [Viewing Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_viewinginstances)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
