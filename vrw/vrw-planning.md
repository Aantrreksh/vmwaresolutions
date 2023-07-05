---

copyright:

  years:  2021, 2023

lastupdated: "2023-06-12"

keywords: planning vmware regulated workloads, data center vmware regulated workloads, vmware regulated workloads data centers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Planning for VMware Regulated Workloads
{: #vrw-planning}

Review the following requirements before you order your VMware® Regulated Workloads instance. Plan your instance based on the {{site.data.keyword.cloud}} data center location, your capacity requirements, and services requirements.

## Account requirements
{: #vrw-planning-account-req}

The account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## IBM Cloud data center availability
{: #vrw-planning-dc-availability}

The VMware Regulated Workloads deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements.

### Data centers available for single-zone deployment
{: #vrw-planning-dc-single-zone}

The following {{site.data.keyword.cloud_notm}} data centers are available for VMware Regulated Workloads single-zone deployment.

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific |CHE01 | 01 |
| Asia-Pacific | OSA21 | 01 |
| Asia-Pacific | OSA22 | 01 |
| Asia-Pacific | OSA23 | 01 |
| Asia-Pacific | SNG01| 02 |
| Asia-Pacific | SYD01 | 01-02 |
| Asia-Pacific | SYD04 | 01 |
| Asia-Pacific | SYD05 | 01 |
| Asia-Pacific | TOK02 | 01-02 |
| Asia-Pacific | TOK04 | 01 |
| Asia-Pacific | TOK05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware Regulated Workloads single-zone deployment" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for VMware Regulated Workloads"}
{: class="simple-tab-table"}
{: #simpletabtable-vrw-ap}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Europe | AMS03 | 01-02 |
| Europe | FRA02 | 01-03 |
| Europe | FRA04 | 01 |
| Europe | FRA05 | 01 |
| Europe | LON02 | 01-02 |
| Europe | LON04 | 01 |
| Europe | LON05 | 01 |
| Europe | LON06 | 01 |
| Europe | MIL01 | 01 |
| Europe | PAR01 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware Regulated Workloads single-zone deployment" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for VMware Regulated Workloads"}
{: class="simple-tab-table"}
{: #simpletabtable-vrw-eur}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA East | MON01 | 01-02 |
| NA East | TOR01 | 01-02 |
| NA East | TOR04 | 01 |
| NA East | TOR05 | 01 |
| NA East | WDC04 | 01-05 |
| NA East | WDC06 | 01 |
| NA East | WDC07 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware Regulated Workloads single-zone deployment" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for VMware Regulated Workloads"}
{: class="simple-tab-table"}
{: #simpletabtable-vrw-naeast}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA South | DAL09 | 01-06 |
| NA South | DAL10 | 01-04 |
| NA South | DAL12 | 01-02 |
| NA South | DAL13 | 01-03 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware Regulated Workloads single-zone deployment" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for VMware Regulated Workloads"}
{: class="simple-tab-table"}
{: #simpletabtable-vrw-nasouth}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA West | SJC03 | 01-02 |
| NA West | SJC04 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware Regulated Workloads single-zone deployment" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for VMware Regulated Workloads"}
{: class="simple-tab-table"}
{: #simpletabtable-vrw-nawest}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| South America | SAO01 | 01 |
| South America | SAO04 | 01 |
| South America | SAO05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware Regulated Workloads single-zone deployment" caption-side="bottom"}
{: tab-title="South America"}
{: tab-group="Data centers for VMware Regulated Workloads"}
{: class="simple-tab-table"}
{: #simpletabtable-vrw-sa}

## Services for VMware Regulated Workloads
{: #vrw-planning-addon-services}

The following services are required for VMware Regulated Workloads:
* [Hyper Protect Crypto Services](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services)
* [KMIP for VMware](https://cloud.ibm.com/infrastructure/vmware-solutions/console/servicestandalonenew/KMIPAdapter)
* [Direct Link Dedicated](https://cloud.ibm.com/interconnectivity/direct-link)

The following services are included with VMware Regulated Workloads:
* [Veeam Backup and Replication](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
* [Entrust CloudControl](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-cc_considerations)
* [Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview). This service is included when you choose **Gateway cluster with Juniper vSRX**.
* [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)

The following services are optional for VMware Regulated Workloads:
* [VMware HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations)
* [F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)

## Related links
{: #vrw-planning-related}

* [VMware Regulated Workloads overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-overview)
* [Ordering VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-req)
* [Viewing and deleting VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-view-delete-instance)
* [VMware Regulated Workloads reference architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview)
