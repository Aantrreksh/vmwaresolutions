---

copyright:

  years:  2021, 2024

lastupdated: "2024-03-19"

keywords: manage shared resources, view shared virtual data centers summary

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Viewing the virtual data center summary
{: #shared_viewing-vdc-summary}

{{site.data.content.shared-deprecated-note}}

You can view a summary of all the {{site.data.keyword.vmwaresolutions_full}} Shared virtual data centers that are provisioned for the user account.

Optionally, validate that you are in the correct account for your instance. From the console banner, click the **Avatar** icon ![Avatar icon](../../icons/i-avatar-icon.svg "Avatar"), and then click the **Account** field to select the user account where you want to view virtual data centers.
{: note}

## Procedure to view the virtual data center summary
{: #shared_viewing-vdc-summary-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > VMware Shared** from the left navigation pane.
2. In the **VMware Shared** table, view the list of data center sites and the virtual data centers that are provisioned for each site.

| Item | Description |
|:---- |:----------- |
| Site | The name of the site where the instance is hosted. |
| Region | The region where the instance is hosted. |
| Creation time | The date and time when the instance was created. |
| Instances | The number of virtual data center instances provisioned for the site. |
{: caption="Table 1. Data center site details" caption-side="bottom"}

Expand the instance site to view the summary of each virtual data center that is provisioned for the user account.

| Item | Description |
|:---- |:----------- |
| Name | The name of the virtual data center. |
| Type | The pricing plan for the virtual data center: On-demand or Reserved. |
| Location | The {{site.data.keyword.cloud_notm}} data center where the virtual data center is hosted. |
| Creation time | The date and time when the virtual data center was created. |
| Status | The status of the virtual data center. |
{: caption="Table 2. Virtual data center details by site" caption-side="bottom"}

The virtual data center can have different statuses.

| Status | Description |
|:------ |:----------- |
| Creating | The virtual data center is being created. |
| Available | The virtual data center is ready to use. |
| Modifying | The virtual data center is being modified. |
| Deleting | The virtual data center is being deleted. |
{: caption="Table 3. Status descriptions for virtual data centers" caption-side="bottom"}

## Related links
{: #shared_viewing-vdc-summary-related}

* [Resizing-virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_resize)
* [Operating VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [Deleting VMware Shared virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_deletinginstance)
* [Viewing-virtual data center details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-details)
* [Accessing the VMware Cloud Director Management console](/docs/vmwaresolutions?topic=vmwaresolutions-shared_accessing-vcd-console)
* [VMware Cloud Director](https://www.vmware.com/products/cloud-director.html){: external}
