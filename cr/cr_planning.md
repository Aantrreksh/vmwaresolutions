---

copyright:

  years:  2022, 2023

lastupdated: "2023-06-12"

keywords: planning cyber recovery, cyber recovery, cyber recovery instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Planning for Cyber Recovery
{: #cr_planning}

Review the following requirements before you order your Cyber Recovery instance. Plan your instance based on the {{site.data.keyword.cloud}} data center location, your capacity requirements, and services requirements.

## Account requirements
{: #cr_planning-account-req}

The account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## IBM Cloud data center availability
{: #cr_planning-dc-availability}

The Cyber Recovery deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements.

### Data centers available
{: #cr_planning-data-centers}

The following {{site.data.keyword.cloud_notm}} data centers are available for Cyber Recovery.

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific |CHE01 | 01 |
| Asia-Pacific | HKG02 | 02 |
| Asia-Pacific | OSA21 | 01 |
| Asia-Pacific | OSA22 | 01 |
| Asia-Pacific | OSA23 | 01 |
| Asia-Pacific | SEO01 | 01 |
| Asia-Pacific | SNG01| 02 |
| Asia-Pacific | SYD01 | 01-02 |
| Asia-Pacific | SYD04 | 01 |
| Asia-Pacific | SYD05 | 01 |
| Asia-Pacific | TOK02 | 01-02 |
| Asia-Pacific | TOK04 | 01 |
| Asia-Pacific | TOK05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-ap}

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
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA East | MON01 | 01-02 |
| NA East | TOR01 | 01-02 |
| NA East | TOR04 | 01 |
| NA East | TOR05 | 01 |
| NA East | WDC04 | 01-05 |
| NA East | WDC06 | 01 |
| NA East | WDC 07 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA South | DAL09 | 01-06 |
| NA South | DAL10 | 01-04 |
| NA South | DAL12 | 01-02 |
| NA South | DAL13 | 01-03 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA West | SJC03 | 01-02 |
| NA West | SJC04 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| South America | SAO01 | 01 |
| South America | SAO04 | 01 |
| South America | SAO05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery" caption-side="bottom"}
{: tab-title="South America"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-sa}

## Services for Cyber Recovery
{: #cr_planning-addon-services}

The following services and components are required for Cyber Recovery instances.

* [Veeam Backup and Replication 12](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) is required and also included. For Veeam, a Linux hardened repository is selected for you.
* An edge gateway is required. You can bring your own gateway appliance or choose from the following options:
   * Gateway cluster with Juniper® vSRX
   * Gateway cluster with FortiGate® Virtual Appliance
   * FortiGate Security Appliance

The [Caveonix RiskForesight™](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations) service is recommended.

The following services are optional for Cyber Recovery.

* [Entrust CloudControl™](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-cc_considerations)
* [F5® BIG-IP®](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)
* [HCX™](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations)
* [Red Hat® OpenShift® for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview)
* [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)
* [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr)

## Related links
{: #cr_planning-related-links}

* [Cyber Recovery overview](/docs/vmwaresolutions?topic=vmwaresolutions-cr_overview)
* [Requirements for Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
