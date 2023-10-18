---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-03"

keywords: VMware HCX standalone, HCX on-premises, delete HCX

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deleting on-premises HCX instances
{: #standalone_deletingserviceinstances}

Use this procedure to delete the VMware® HCX™ instances that you ordered for on-premises use.

## Considerations before you delete on-premises HCX instances
{: #standalone_considerations-delete}

Review the following considerations before you delete an HCX instance that was ordered for on-premises use:
1. In the VMware vSphere Web Client, go to the HCX user interface and check the following items:
    1. Ensure that no HCX migration or disaster recovery operation is running.
    2. Ensure that all the extended networks are removed.
    3. Ensure that all the interconnect components with paired cloud sites are removed.

   You must complete all the previous steps before you proceed to the next step. Otherwise, the activation key for the on-premises HCX instance is canceled. If the activation key is canceled, migrations can't be performed and errors might occur for HCX components.
   {: important}

2. In the {{site.data.keyword.vmwaresolutions_short}} console, delete the on-premises HCX instance that was ordered to obtain the activation key for the on-premises HCX Manager. Ensure that the deleted instance is no longer available in the console before you proceed to the next step.

3. In the VMware vSphere Web Client, delete the on-premises HCX Manager.

## Procedure to delete on-premises HCX instances
{: #standalone_deletingserviceinstances-procedure}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Licenses** from the left navigation pane.
2. Scroll down to the **On-premises HCX activation keys** table and find the instance to delete.
3. In the **Actions** column, click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete").
4. In the **Delete instance** window, click **OK**.
   The status of the instance is changed to **Removing**. When the instance deletion is completed, the instance is no longer available in the **On-premises HCX activation keys** table.

## Related links
{: #standalone_deletingserviceinstances-related}

* [Ordering on-premises HCX instances](/docs/vmwaresolutions?topic=vmwaresolutions-standalone_orderingserviceinstances)
* [Viewing on-premises HCX instances](/docs/vmwaresolutions?topic=vmwaresolutions-standalone_viewingserviceinstances)
* [Glossary of HCX terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_glossary)
* [VMware HCX documentation](https://docs.vmware.com/en/VMware-HCX/index.html){: external}
