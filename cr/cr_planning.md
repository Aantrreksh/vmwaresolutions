---

copyright:

  years:  2022, 2023

lastupdated: "2023-07-31"

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

## {{site.data.keyword.cloud_notm}} data center availability
{: #cr_planning-dc-availability}

The Cyber Recovery deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements.

### Data centers available
{: #cr_planning-data-centers}

The following {{site.data.keyword.cloud_notm}} data centers are available for Cyber Recovery.

| Data center | Pod |
|:----------- |:--- |
| CHE01 | 01 |
| OSA21 | 01 |
| OSA22 | 01 |
| OSA23 | 01 |
| SNG01 | 02 |
| SYD01 | 01-02 |
| SYD04 | 01 |
| SYD05 | 01 |
| TOK02 | 01-02 |
| TOK04 | 01 |
| TOK05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery - Asia-Pacific" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-ap}

| Data center | Pod |
|:----------- |:--- |
| AMS03 | 01-02 |
| FRA02 | 01-03 |
| FRA04 | 01 |
| FRA05 | 01 |
| LON02 | 01-02 |
| LON04 | 01 |
| LON05 | 01 |
| LON06 | 01 |
| MIL01 | 01 |
| PAR01 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery - Europe" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Data center | Pod |
|:----------- |:--- |
| MON01 | 01-02 |
| TOR01 | 01-02 |
| TOR04 | 01 |
| TOR05 | 01 |
| WDC04 | 01-05 |
| WDC06 | 01 |
| WDC07 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery - NA East" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}

| Data center | Pod |
|:----------- |:--- |
| DAL09 | 01-06 |
| DAL10 | 01-04 |
| DAL12 | 01-02 |
| DAL13 | 01-03 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery - NA South" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Data center | Pod |
|:----------- |:--- |
| SJC03 | 01-02 |
| SJC04 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery - NA West" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for Cyber Recovery"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Data center | Pod |
|:----------- |:--- |
| SAO01 | 01 |
| SAO04 | 01 |
| SAO05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Cyber Recovery - South America" caption-side="bottom"}
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

* [F5® BIG-IP®](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)
* [HCX™](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations)
* [Red Hat® OpenShift® for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview)
* [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)
* [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr)

## Related links
{: #cr_planning-related-links}

* [Cyber Recovery overview](/docs/vmwaresolutions?topic=vmwaresolutions-cr_overview)
* [Requirements for Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
