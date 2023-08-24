---

copyright:

  years:  2020, 2023

lastupdated: "2023-08-21"

keywords: planning VMware Solutions Shared, data center, VMware Solutions Shared data centers

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Requirements and planning for VMware Shared
{: #shared_planning}

Review the following requirements before you order your VMware Shared virtual data centers. Plan for your order by considering the {{site.data.keyword.cloud_notm}} data center location, your workload capacity requirements, and services requirements.

Price calculations are automatically generated when you access the VMware Shared instance order page. Default selections for on-demand virtual data centers include public and private networking, 2000 vCPU, and 40960 RAM. Default selections for reserved virtual data centers include public and private networking, and customizable vCPU and RAM limits.

## IBM Cloud account requirements
{: #shared_ordering-account-req}

To order VMware Shared, you must have a **Pay As You Go** or **Subscription** {{site.data.keyword.cloud_notm}} account. The cost of the resources that are ordered is billed to that {{site.data.keyword.cloud_notm}} account.

## Virtual data center name requirements
{: #shared_ordering-vdc-name-req}

The virtual data center name must meet the following requirements:

* Maximum length is 128 characters.
* Only alphanumeric, dash (-), and underscore (_) characters are allowed.
* The name must be unique from active virtual data centers within your account. You can create a virtual data center that has the same name as a previously deleted virtual data center.

## IBM Cloud data center availability
{: #shared_planning-dc-availability}

The VMware Shared deployment has strict requirements on the physical infrastructure. Therefore, you can deploy your virtual data centers only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements.

The following {{site.data.keyword.cloud_notm}} data centers are available for VMware Shared deployment.

| Site | Location | vSAN support | Multizone support |
|:---- |:-------- |:------------ |:----------------- |
| Frankfurt Director 01 | Frankfurt 02 | None | No |
| Frankfurt Director 01 | Frankfurt 04 | None | No |
| Frankfurt Director 01 | Frankfurt 05 | None | No |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for deployment - Europe" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for deployment"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Site | Location | vSAN support | Multizone support |
|:---- |:-------- |:------------ |:----------------- |
| Dallas Director 01 | Dallas 10 | vSAN | No |
| Dallas Director 01 | Dallas 12 | vSAN | No |
| Dallas Director 01 | Dallas 13 | vSAN | No |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for deployment - North America" caption-side="bottom"}
{: tab-title="North America"}
{: tab-group="Data centers for deployment"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-northamerica}

## Services for VMware Shared instances
{: #shared_planning-addon-services}

The following preinstalled services are available for your virtual data center based on your needs.
* [Managing Veeam for VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_veeam)
* [Managing Zerto for VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-portal)

Service charges are incurred only if you choose to use the service.
{: note}

## Configuration limits for VMware Cloud Director
{: #shared_ordering-cloud-dir-limits}

Review [VMware Cloud Director 10.4 Configuration Limits](https://configmax.esp.vmware.com/guest?vmwareproduct=%20VMware%20Cloud%20Director&release=VMware%20Cloud%20Director%2010.4&categories=35-0){: external} to ensure that you understand configuration limits in VMware Cloud Director.

### 10,000 vApps per Cloud Director organization
{: #shared_ordering-cloud-dir-limits-vapp}

One of the configuration limits in VMware Cloud Director is a maximum of 10,000 vApps per Cloud Director organization. In VMware Shared, it means you cannot have more than 10,000 vApps in a single account in a particular site location since each site location is the same Cloud Director instance. For more information about sites and VMware Cloud Director, see [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview).

If you need more than 10,000 vApps in a single account, consider the following design options.

* Increase the number of virtual machines in each vApp.
* Use a separate account in that region to host more vApps.

The number of VMware Shared instances (or virtual data centers) does not impact this limit.
{: note}

## Related links
{: #shared_planning-related}

* [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [Viewing and managing virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary)
* [Operating VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [VMware Cloud Director](https://www.vmware.com/ca/products/cloud-director.html){: external}
