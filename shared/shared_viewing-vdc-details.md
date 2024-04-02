---

copyright:

  years:  2021, 2024

lastupdated: "2024-04-02"

keywords: manage shared resources, view shared virtual data centers details

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Viewing site and virtual data center details
{: #shared_viewing-vdc-details}

{{site.data.content.shared-deprecated-note}}

You can view property details for VMware Shared sites and virtual data centers. You can also review recommended services that are enabled or available for virtual data centers.

## Procedure to view site details
{: #shared_viewing-site-details-procedure}

1. From the VMware Solutions console, click **Resources > VMware Shared** from the left navigation pane.
2. In the **VMware Shared** table, click the site.
3. Ensure that you are on the **Summary** tab to view the property details of a site.

| Property | Description |
|:-------- |:----------- |
| Region | The {{site.data.keyword.cloud_notm}} data center region where your organization is created and the organization password is maintained. |
| ID | The ID of the virtual data center. |
| Instances | The current number of virtual data center instances provisioned for the site. |
| Red Hat activation key | The activation key that you use to register the Red Hat virtual machine (VM). |
| Access controls | Options for IAM integration and setting the administrator password for the organization. |
{: caption="Table 1. Virtual data center site details" caption-side="bottom"}

## Procedure to view virtual data center details
{: #shared_viewing-vdc-details-procedure}

1. Click the **Virtual data centers** tab to view the summary of each virtual data center.
2. Click the virtual data center name to view the properties.

| Property | Description |
|:-------- |:----------- |
| Name | The name of the virtual data center. |
| Type | The virtual data center type. |
| Deployment topology | A single-zone or multizone virtual data center. |
| Region | The {{site.data.keyword.cloud_notm}} data center region where your organization is created and the organization password is maintained. |
| Location | The {{site.data.keyword.cloud_notm}} data center where the virtual data center is hosted. |
| ID | The ID of the virtual data center. |
| Creation time | The date and time when the virtual data center was created, which is also when billing starts. |
| Red Hat activation key | The activation key that you use to register the Red Hat virtual machine (VM). |
{: caption="Table 2. Virtual data center property details" caption-side="bottom"}

### Opening a support ticket for additional IP addresses or subnet
{: #shared_viewing-vdc-details-support}

To request five additional public IP addresses or an entire subnet for your virtual data center, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

Include the following details in your support ticket:
* Virtual data center region and location
* Organization ID
* Virtual data center name
* Number of additional IP addresses required
* Specify whether you plan to use the additional IP addresses by using Network Address Translate through the virtual data center Edge Services Gateway or by directly assigning the IP address to a VM.

### Viewing virtual data center resource reservation details
{: #shared_viewing-vdc-details-resource}

Under **Resource reservation**, view the total reserved virtual CPU (vCPU) and RAM for the virtual data center.

| Resource | Description |
|:-------- |:----------- |
| vCPU limit | The limit or reserved amount of vCPU that can be used at any time by the virtual data center.  |
| RAM limit | The limit or reserved amount of memory that can be used at any time by the virtual data center.  |
{: caption="Table 3. Virtual data center resource reservation details" caption-side="bottom"}

## Viewing virtual data center recommended services details
{: #shared_viewing-vdc-details-services}

Click the **Services** tab to view the virtual data center recommended services details.

For more information about recommended services details, see [Managing Veeam for VMware Shared virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_veeam) and [Managing Zerto for VMware Shared virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-portal).

## Related links
{: #shared_viewing-vdc-details-related}

* [Creating a private network endpoint](/docs/vmwaresolutions?topic=vmwaresolutions-shared_creating-endpoints)
* [Resizing your virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_resize)
* [Deleting VMware Shared virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_deletinginstance)
* [Accessing the VMware Cloud Director Management console](/docs/vmwaresolutions?topic=vmwaresolutions-shared_accessing-vcd-console)
* [VMware Cloud Director](https://www.vmware.com/products/cloud-director.html){: external}
