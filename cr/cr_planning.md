---

copyright:

  years:  2022, 2024

lastupdated: "2024-09-11"

keywords: planning cyber recovery, cyber recovery, cyber recovery instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Planning for {{site.data.keyword.cr}}
{: #cr_planning}

Review the following requirements before you order your {{site.data.keyword.cr}} instance. Plan your instance based on the {{site.data.keyword.cloud}} data center location, your capacity requirements, and your service requirements.

## Account requirements
{: #cr_planning-account-req}

The account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## Licensing considerations
{: #cr_planning-licensing}

{{site.data.content.vmware-licensing}}

## {{site.data.keyword.cloud_notm}} data center availability
{: #cr_planning-dc-availability}

The {{site.data.keyword.cr}} deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements.

### Data centers available
{: #cr_planning-data-centers}

The following {{site.data.keyword.cloud_notm}} data centers are available for {{site.data.keyword.cr}}.

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
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for {{site.data.keyword.cr}} - Asia Pacific" caption-side="bottom"}
{: tab-title="Asia Pacific"}
{: tab-group="Data centers for {{site.data.keyword.cr}}"}
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
| MAD02 | 01 |
| MAD04 | 01 |
| MAD05 | 01 |
| MIL01 | 01 |
| PAR01 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for {{site.data.keyword.cr}} - Europe" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for {{site.data.keyword.cr}}"}
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
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for {{site.data.keyword.cr}} - NA East" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for {{site.data.keyword.cr}}"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}

| Data center | Pod |
|:----------- |:--- |
| DAL09 | 01-06 |
| DAL10 | 01-04 |
| DAL12 | 01-02 |
| DAL13 | 01-03 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for {{site.data.keyword.cr}} - NA South" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for {{site.data.keyword.cr}}"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Data center | Pod |
|:----------- |:--- |
| SJC03 | 01-02 |
| SJC04 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for {{site.data.keyword.cr}} - NA West" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for {{site.data.keyword.cr}}"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Data center | Pod |
|:----------- |:--- |
| SAO01 | 01 |
| SAO04 | 01 |
| SAO05 | 01 |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for {{site.data.keyword.cr}} - South America" caption-side="bottom"}
{: tab-title="South America"}
{: tab-group="Data centers for {{site.data.keyword.cr}}"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-sa}

## Services for {{site.data.keyword.cr}}
{: #cr_planning-addon-services}

The following services and components are available for {{site.data.keyword.cr}} instances.

* [Veeam Backup and Replication](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) (required) is included and a Linux hardened repository is selected for you.
* An edge gateway (required) provides the virtual air-gap and manages access to the isolated recovery environment. You can bring your own gateway appliance or choose from the following options:
   * Gateway cluster with Juniper® vSRX
   * Gateway cluster with FortiGate® Virtual Appliance
   * FortiGate Security Appliance

The [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations) service (optional) provides security and risk compliance.

## Related links
{: #cr_planning-related-links}

* [{{site.data.keyword.cr}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-cr_overview)
* [Requirements for {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
