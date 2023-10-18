---

copyright:

  years:  2020, 2023

lastupdated: "2023-10-06"

keywords: Veeam, Veeam license, manage Veeam license, Veeam Backup and Replication 12 

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Managing Veeam stand-alone licenses
{: #veeam_managing_licenses}

You can view, edit notes, or delete the Veeam® licenses that you ordered for stand-alone use.

## Procedure to view Veeam stand-alone licenses
{: #veeam_managing_licenses-procedure-view}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Licenses** from the left navigation pane.
2. Scroll down to the **Veeam licenses** table.
3. To view the details of a specific license, click the license.

The following information is displayed for the Veeam license:
* License name
* License notes
* Number of virtual machines (VMs) licensed
* Creation date
* Status - the status can be one of the following items.
   * Modifying - The license is being created.
   * Installed - The license is ready to use.
   * Removing - The license is being deleted.

   A license key is not displayed. When licenses are ordered, the system does not generate a key, but it applies a primary key.
   {: note}

## Procedure to edit notes for Veeam stand-alone licenses
{: #veeam_managing_licenses-procedure-edit}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Licenses** from the left navigation pane.
2. Scroll down to the **Veeam licenses** table.
3. Click the license that you want to edit the notes for.
4. On the license details page, edit the license notes, and then click **Confirm**.

## Known issues about license date display
{: #veeam_managing_licenses-considerations-date}

If you are using Mozilla® Firefox® as your browser, the license start and end dates might be displayed with no values on the Veeam console. To resolve the issue, view the license information in another browser, such as Google Chrome™.

If you are experiencing this problem and the only browser you can use is Firefox, contact [Veeam support](https://www.veeam.com/support.html){: external} for assistance.

## Procedure to delete Veeam stand-alone licenses
{: #veeam_managing_licenses-procedure-delete}

Review the [considerations for installing and deleting Veeam licenses](/docs/vmwaresolutions?topic=vmwaresolutions-managingveeam#managingveeam-install-delete-consid) before you delete a Veeam license.
{: important}

Deleting a Veeam license does not delete the Veeam service that is installed on a vCenter Server instance. To delete the service, you must do so in the VMware Solutions console.

For more information, see [Deleting services from vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices).

To delete a Veeam license:

1. From the VMware Solutions console, click **Licenses** from the left navigation pane.
2. Scroll down to the **Veeam licenses** table and select the license that you want to delete.
3. From the **Actions** menu, click **Delete instance**.
4. In the **Delete license** window, click **Delete**.
   The status of the license is changed to **Removing**. When the license deletion is completed, the license is no longer listed in the **Veeam licenses** table.

## Related links
{: #veeam_managing_licenses-related}

* [Veeam on {{site.data.keyword.cloud_notm}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [Ordering Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering)
* [Managing Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-managingveeam)
* [Ordering Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering_licenses)
* [Ordering and configuring {{site.data.keyword.cloud_notm}} Object Storage with Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-icos_ordering)
