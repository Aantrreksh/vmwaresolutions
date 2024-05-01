---

copyright:

  years:  2020, 2024

lastupdated: "2024-04-26"

keywords: manage shared resources, shared resources, shared resource tasks

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Resizing your virtual data centers
{: #shared_resize}

{{site.data.content.shared-deprecated-note}}

You can change the amount of resources that are assigned to a virtual data center when it is in the **Ready To Use** state.

## Procedure to resize virtual data centers
{: #shared_resize-procedure}

1. From the {{site.data.keyword.vmwaresolutions_full}} Shared virtual data center details page, click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") next to **Resource Reservation**.
2. Update the values of the virtual CPU (vCPU) limit or RAM limit properties.
3. Expand the **Total estimated cost** section to expand it. Verify the configuration and estimated price and click **Modify** to place the order.

Optionally, click **Reset changes** to return to the original resource values.
{: note}

The status of the virtual data center changes to **Modifying** while the update is being made. When the resources are ready to use, the status changes to **Available**.

The configuration change might fail if the vCPU and RAM resources are in use while they are reduced. The cause of the failure is that the virtual data center resources cannot be reduced to a level that is insufficient for the currently active resource usage.
{: note}

## Related links
{: #shared_resize-related}

* [{{site.data.keyword.vm-shared}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Viewing and managing virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary)
* [Deleting {{site.data.keyword.vm-shared}} virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_deletinginstance)
