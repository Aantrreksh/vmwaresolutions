---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-19"

keywords: planning vCenter Server, data center, vCenter Server data centers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Planning for vCenter Server instances
{: #vc_planning}

Plan your instance based on the {{site.data.keyword.cloud}} data center location, your workload capacity requirements, and add-on services requirements. Review the following requirements before you order your VMware vCenter Server® instance.

* New deployments of vCenter Server instances with VMware vSphere® 6.5 or 6.7 are not supported.
* New deployments of vCenter Server multizone instances are not supported.
* New deployments of vCenter Server with NSX-V instances are not supported.

## Account requirements
{: #vc_planning-account-req}

The account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## IBM Cloud data center availability
{: #vc_planning-dc-availability}

The vCenter Server deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements. The following {{site.data.keyword.cloud_notm}} data centers are available for vCenter Server deployment.

| Geography | Data center | Pod | Server options for NSX-T[^nsx-t-7] | Server options for NSX-V[^nsx-v] |
|:--------- |:----------- |:--- |:---------------------------------- |:-------------------------------- |
| Asia-Pacific | CHE01 | 01 | Skylake, Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-che01] |
| Asia-Pacific | OSA21 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | OSA22 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | OSA23 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SNG01| 02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SYD01 | 01-02 | Skylake, Cascade Lake, SAP-certified | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SYD04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SYD05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | TOK02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | TOK04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | TOK05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for vCenter Server instances" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for vCenter Server instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-ap}

| Geography | Data center | Pod | Server options for NSX-T[^nsx-t-7-02] | Server options for NSX-V[^nsx-v-02] |
|:----------|:------------|:----|:--------------------------------------|:------------------------------------|
| Europe | AMS03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | FRA02 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | FRA04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | FRA05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake |
| Europe | LON04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | MIL01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-mil01] |
| Europe | PAR01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-par01] |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for vCenter Server instances" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for vCenter Server instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Geography | Data center | Pod | Server options for NSX-T[^nsx-t-7-03] | Server options for NSX-V[^nsx-v-03] |
|:----------|:------------|:----|:--------------------------------------|:------------------------------------|
| NA East | MON01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-mon01] |
| NA East | TOR01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified |
| NA East | TOR04 | 01 | Cascade Lake | Cascade Lake |
| NA East | TOR05 | 01 | Cascade Lake | Cascade Lake |
| NA East | WDC04 | 01-05 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA East | WDC06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA East | WDC07 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for vCenter Server instances" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for vCenter Server instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}


| Geography | Data center | Pod | Server options for NSX-T[^nsx-t-7-04] | Server options for NSX-V[^nsx-v-04] |
|:----------|:------------|:----|:--------------------------------------|:------------------------------------|
| NA South | DAL09 | 01-06 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA South | DAL10 | 01-04 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA South | DAL12 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA South | DAL13 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for vCenter Server instances" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for vCenter Server instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Geography | Data center | Pod | Server options for NSX-T[^nsx-t-7-05] | Server options for NSX-V[^nsx-v-05] |
|:----------|:------------|:----|:--------------------------------------|:------------------------------------|
| NA West | SJC 03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake |
| NA West | SJC 04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for vCenter Server instances" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for vCenter Server instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Geography | Data center | Pod | Server options for NSX-T[^nsx-t-7-06] | Server options for NSX-V[^nsx-v-06] |
|:----------|:------------|:----|:--------------------------------------|:------------------------------------|
| South America | SAO 01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| South America | SAO 04 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| South America | SAO 05 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for vCenter Server instances" caption-side="bottom"}
{: tab-title="South America"}
{: tab-group="Data centers for vCenter Server instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-sa}

[^nsx-t-7]: Skylake is supported for existing vSphere 6 instances only

[^nsx-t-7-02]: Skylake is supported for existing vSphere 6 instances only

[^nsx-t-7-03]: Skylake is supported for existing vSphere 6 instances only

[^nsx-t-7-04]: Skylake is supported for existing vSphere 6 instances only

[^nsx-t-7-05]: Skylake is supported for existing vSphere 6 instances only

[^nsx-t-7-06]: Skylake is supported for existing vSphere 6 instances only

[^nsx-v]: Existing NSX-V instances only

[^nsx-v-02]: Existing NSX-V instances only

[^nsx-v-03]: Existing NSX-V instances only

[^nsx-v-04]: Existing NSX-V instances only

[^nsx-v-05]: Existing NSX-V instances only

[^nsx-v-06]: Existing NSX-V instances only

[^sap-che01]: Existing vSphere 6 clusters only

[^sap-mil01]: Existing vSphere 6 clusters only

[^sap-mon01]: Existing vSphere 6 clusters only

[^sap-par01]: Existing vSphere 6 clusters only

## Backup of management components
{: #vc_planning-backup-mgmt-components}

You are responsible for maintaining and ensuring the availability of all instance components. It is recommended that you plan for backup or high availability of all management components. For more information, see [Backing up components](/docs/vmwaresolutions?topic=vmwaresolutions-solution_backingup).

## Services for vCenter Server instances
{: #vc_planning-addon-services}

You can order services for your instance based on your needs, for example, disaster recovery. For more information, see [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

Add-on services support varies between vCenter Server with NSX-T™ and existing vCenter Server with NSX-V instances V4.7 and earlier.

If you want to migrate your F5 BIG-IP or Veeam services from VMware NSX-V to VMware NSX-T, open an IBM Support ticket by following the steps in [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: note}

## Capacity considerations
{: #vc_planning-capacity-considerations}

For more information about capacity considerations, see [Scaling capacity](/docs/vmwaresolutions?topic=vmwaresolutions-solution_scaling).

## Related links
{: #vc_planning-related}

* [vCenter Server overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [Ordering vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Expanding and contracting capacity for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
