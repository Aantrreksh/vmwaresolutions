---

copyright:

  years:  2023

lastupdated: "2023-06-16"

keywords: vmware vsphere add license, add license vmware vsphere, vmware vsphere delete license, delete license vmware vsphere, vmware vsphere view license, view license vmware vsphere

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Managing licenses for VMware vSphere instances
{: #vs_manage_licenses}

You can add or delete licenses for various VMware components in your VMware vSphere® instance. For more information about these components, see [Licensing](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-licensing-settings).

## Before you manage licenses for VMware vSphere instances
{: #vs_manage_licenses-prereq}

* For existing instances with VMware vSphere® 6, you cannot add or delete licenses. To add licenses, upgrade your vSphere software to version 7. For more information, see [Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).
* The VMware vSAN license is part of your instance by default and it cannot be deleted.
* If you want to combine license keys, open an IBM Support ticket by following the steps in [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support). 

## Procedure to add licenses to VMware vSphere instances
{: #vs_manage_licenses-add-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > vSphere** from the left navigation pane.
2. In the **vSphere** table, click the instance for which you want to add licenses.
3. Click the **Licensing** tab. From here, you can view the licenses in your instance. Click **Add licenses**.
5. On the **Add licenses** side panel, select the licenses that you want to add from the list of available components. The number of licenses that is displayed in the **Quantity** column is determined by the number of hosts in your instance.
6. In the **Summary** section, review the estimated pricing and ensure that the account to be charged is correct. Click **Add**.

## Procedure to delete licenses from VMware vSphere instances
{: #vs_manage_licenses-delete-procedure}
{: help}
{: support}

1. From the VMware Solutions console, click **Resources > vSphere** from the left navigation pane.
2. In the **vSphere** table, click the instance from which you want to delete licenses.
3. Click the **Licensing** tab. From here, you can view the licenses in your instance. Select the license to be deleted and click **Delete**.
4. On the **Delete licenses** window, click **Delete**.

## Results after you manage licenses for VMware vSphere instances
{: #vs_manage_licenses-results}

* You are notified by email that your request is being processed. On the console, the status of the instance is changed to **Modifying**.
* If you do not see the licenses being added or deleted from the instance, check your email or console notifications for more details.

## Related links
{: #vs_manage_licenses-links}

* [Viewing VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_viewinginstances)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
