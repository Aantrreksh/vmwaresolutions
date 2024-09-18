---

copyright:

  years:  2016, 2024

lastupdated: "2024-09-18"

keywords: planning vcf classic, data center, vcf automated data centers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Planning for {{site.data.keyword.vcf-auto-short}}
{: #vc_planning}

Plan your instance based on the {{site.data.keyword.cloud}} data center location, your workload capacity requirements, and add-on services requirements. Review the following requirements before you order your {{site.data.keyword.vcf-auto}} instance.

* New deployments of instances with VMware vSphere® 6.5 or 6.7 are not supported.
* New deployments of multizone instances are not supported.
* New deployments of {{site.data.keyword.vcf-auto-short}} with NSX-V instances are not supported.

## Account requirements
{: #vc_planning-account-req}

The account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## Licensing considerations
{: #vc_planning-licensing}

{{site.data.content.vmware-licensing}}

## {{site.data.keyword.cloud_notm}} data center availability
{: #vc_planning-dc-availability}

The {{site.data.keyword.vcf-auto-short}} deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements. The following {{site.data.keyword.cloud_notm}} data centers are available for {{site.data.keyword.vcf-auto-short}} deployment.

| Data center | Pod | Server options for NSX-T[^nsx-t-7] | Server options for NSX-V[^nsx-v] |
|:----------- |:--- |:---------------------------------- |:-------------------------------- |
| CHE01 | 01 | Skylake, Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-che01] |
| OSA21 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| OSA22 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| OSA23 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| SNG01 | 02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SYD01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SYD04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SYD05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOK02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOK04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOK05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Automated instances - Asia Pacific" caption-side="bottom"}
{: tab-title="Asia Pacific"}
{: tab-group="Data centers for Automated instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-ap}

| Data center | Pod | Server options for NSX-T[^nsx-t-7-02] | Server options for NSX-V[^nsx-v-02] |
|:----------- |:--- |:------------------------------------- |:----------------------------------- |
| AMS03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| FRA02 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| FRA04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| FRA05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake |
| LON04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| MAD02 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| MAD04 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| MAD05 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| MIL01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-mil01] |
| PAR01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-par01] |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Automated instances - Europe" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for Automated instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Data center | Pod | Server options for NSX-T[^nsx-t-7-03] | Server options for NSX-V[^nsx-v-03] |
|:----------- |:--- |:------------------------------------- |:----------------------------------- |
| MON01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake[^sap-mon01] |
| TOR01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOR04 | 01 | Cascade Lake | Cascade Lake |
| TOR05 | 01 | Cascade Lake | Cascade Lake |
| WDC04 | 01-05 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| WDC06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| WDC07 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Automated instances - NA East" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for Automated instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}

| Data center | Pod | Server options for NSX-T[^nsx-t-7-04] | Server options for NSX-V[^nsx-v-04] |
|:----------- |:--- |:------------------------------------- |:----------------------------------- |
| DAL09 | 01-06 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| DAL10 | 01-04 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| DAL12 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| DAL13 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Automated instances - NA South" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for Automated instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Data center | Pod | Server options for NSX-T[^nsx-t-7-05] | Server options for NSX-V[^nsx-v-05] |
|:----------- |:--- |:------------------------------------- |:----------------------------------- |
| SJC03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake |
| SJC04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Automated instances - NA West" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for Automated instances"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Data center | Pod | Server options for NSX-T[^nsx-t-7-06] | Server options for NSX-V[^nsx-v-06] |
|:----------- |:--- |:------------------------------------- |:----------------------------------- |
| SAO01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SAO04 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
| SAO05 | 01 | Cascade Lake, SAP-certified Cascade Lake | Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for Automated instances - South America" caption-side="bottom"}
{: tab-title="South America"}
{: tab-group="Data centers for Automated instances"}
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

## Services for Automated instances
{: #vc_planning-addon-services}

You can order services for your instance based on your needs, for example, disaster recovery. For more information, see [Ordering services for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

Add-on services support varies between instance types and versions.

If you want to migrate your F5 BIG-IP or Veeam services from VMware NSX-V to VMware NSX-T, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: note}

## Capacity considerations
{: #vc_planning-capacity-considerations}

For more information about capacity considerations, see [Scaling capacity](/docs/vmwaresolutions?topic=vmwaresolutions-solution_scaling).

## Related links
{: #vc_planning-related}

* [{{site.data.keyword.vcf-auto-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [Ordering Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Expanding and contracting capacity for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Ordering services for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
