---

copyright:

  years:  2021, 2024

lastupdated: "2024-04-26"

keywords: VMware Solutions Shared view private network endpoint

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Viewing a private network endpoint for a virtual data center
{: #shared_viewing-endpoints}

{{site.data.content.shared-deprecated-note}}

You can view the details of a private network endpoint for a virtual data center.

## Procedure to view a private network endpoint for a virtual data center
{: #shared_viewing-endpoints-procedure}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > {{site.data.keyword.vm-shared}}** from the left navigation pane.
2. In the **{{site.data.keyword.vm-shared}}** table, expand the site and click a virtual data center name.
3. View the **Private network endpoint** details. Expand **Allow listed IPs and subnets** to view the list of IP addresses and subnets that you added when you ordered the private network endpoint.

| Item | Description |
|:---- |:----------- |
| Device type | The multitenant or dedicated device and size. |
| Service network IP | The IP address for the service network. |
| Private network IP | The IP address for the private network. |
| Service address | The IP address that your virtual data center is allocated for {{site.data.keyword.cloud_notm}} access. |
| Allow listed IPs and subnets | The list of all allow listed IP addresses and subnets for the virtual data center. |
{: caption="Table 1. Private network endpoint items" caption-side="bottom"}

The **Service address** is available only when you select the *Dedicated 1 Gbps uplinks* or *Dedicated 10 Gbps uplinks* **Device type** when you order the private network endpoint.
{: important}

The private network endpoint can have different statuses.

| Status        | Description   |
|:------------- |:------------- |
| Creating | The private network endpoint is being created. |
| Ready to use | The private network endpoint is operating. |
| Modifying | The allow listed IPs and subnets are being modified. |
| Deleting | The private network endpoint is being deleted. |
| Deleted | The private network endpoint is deleted. |
{: caption="Table 2. Status descriptions for a private network endpoint" caption-side="bottom"}

## Related links
{: #shared_viewing-endpoints-related}

* [Operating {{site.data.keyword.vm-shared}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [{{site.data.keyword.vm-shared}} pricing](/docs/vmwaresolutions?topic=vmwaresolutions-shared_pricing)
* [Creating a private network endpoint](/docs/vmwaresolutions?topic=vmwaresolutions-shared_creating-endpoints)
* [Modifying a private network endpoint for a virtual data center](/docs/vmwaresolutions?topic=vmwaresolutions-shared_modifying-endpoints)
* [Deleting a private network endpoint from a virtual data center](/docs/vmwaresolutions?topic=vmwaresolutions-shared_deleting-endpoints)
