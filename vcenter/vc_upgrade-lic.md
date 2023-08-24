---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-28"

keywords: NSX license upgrade, upgrade license hybridity, hybridity license

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Upgrading licenses for vCenter Server with NSX-V instances
{: #vc_upgrade-lic}

You can upgrade your VMware NSX® license for V2.1 or later instances.

## Procedure to upgrade your NSX license
{: #vc_upgrade-lic-nsx}
{: help}
{: support}

This procedure applies to instances that are deployed in V2.1 or later. For instances that are deployed in V2.0 and earlier, you must upgrade the VMware NSX license manually.

You can upgrade the NSX license for your instance to a later edition. Reverting the license to an earlier edition is not supported.

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance to upgrade the NSX license for.
3. On the **Summary** page, verify that all instance details are displayed correctly. Then, click the **Infrastructure** tab to verify the details on the **Infrastructure** page.

   If the details are not displayed, a connectivity problem might occur with the IBM CloudDriver Virtual Server Instance (VSI), as a result of a firewall rule or a networking issue. Resolve the problem before you continue with the next step, otherwise the upgrade might fail.

4. Click the **Licensing** tab and click **Upgrade** in the **License upgrades** table. In the **Upgrade NSX license edition** window, select the edition that you want to upgrade to and click **Upgrade**.

   The license upgrade replaces all existing NSX licenses on the instance. Additional charges can be incurred from an overlap of old and new licenses if you upgrade in the middle of a billing cycle. To avoid additional charges, it is recommended to upgrade the license at the end of the billing cycle.
   {: note}

## Related links
{: #vc_upgrade-lic-related}

* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQs](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
