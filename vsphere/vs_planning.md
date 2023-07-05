---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-20"

keywords: planning vmware vSphere, data center, vSphere data centers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Planning for VMware vSphere
{: #vs_planning}

Review the following requirements before you order a VMware vSphere® instance. Plan your VMware vSphere based on the {{site.data.keyword.cloud}} data center location and your workload capacity requirements.

You are responsible for setting up the environment, installing, and configuring various VMware® components after the VMware ESXi™ servers are deployed. The following examples are VMware components: VMware vCenter Server®, VMware NSX®, and VMware vSAN™.
{: note}

## Account requirements
{: #vs_planning-account-req}

The account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## IBM Cloud data center availability
{: #vs_planning-dc-availability}

The vSphere deployment has strict requirements on the physical infrastructure. Therefore, you can deploy clusters only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements. The following {{site.data.keyword.cloud_notm}} data centers are available for vSphere deployment.

Cascade Lake bare metal servers are available in [multizone region](#x9774820){: term}
{{site.data.keyword.cloud_notm}} data centers. For more information, see [Multizone region (MZR) overview](/docs/loadbalancer-service?topic=loadbalancer-service-multi-zone-region-mzr-overview).

If you select a vSAN component, the location list is filtered by SSD (Solid-State Disk) availability.
{: note}

| Geography | Data center | Pod | Server options[^vsphere-7] |
|:--------- |:----------- |:--- |:-------------------------- |
| Asia-Pacific | CHE01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | OSA21 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | OSA22 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | OSA23 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SNG01 | 02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SYD01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SYD04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | SYD05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | TOK02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | TOK04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Asia-Pacific | TOK05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-ap}

| Geography | Data center | Pod | Server options[^vsphere-7-02] |
|:--------- |:----------- |:--- |:-------------------------- |
| Europe | AMS03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | FRA02 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | FRA04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | FRA05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | LON06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | MIL01  | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| Europe | PAR01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Geography | Data center | Pod | Server options[^vsphere-7-03] |
|:--------- |:----------- |:--- |:-------------------------- |
| NA East | MON01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA East | TOR01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA East | TOR04 | 01 | Cascade Lake |
| NA East | TOR05 | 01 | Cascade Lake |
| NA East | WDC04 | 01-05 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA East | WDC06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA East | WDC07 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}

| Geography | Data center | Pod | Server options[^vsphere-7-04] |
|:--------- |:----------- |:--- |:-------------------------- |
| NA South | DAL09 | 01-06 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA South | DAL10 | 01-04 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA South | DAL12 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA South | DAL13 |  01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Geography | Data center | Pod | Server options[^vsphere-7-05] |
|:--------- |:----------- |:--- |:-------------------------- |
| NA West | SJC03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| NA West | SJC04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Geography | Data center | Pod | Server options[^vsphere-7-06] |
|:--------- |:----------- |:--- |:-------------------------- |
| South America | SAO01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| South America | SAO04 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| South America | SAO05 | 01 | Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances" caption-side="bottom"}
{: tab-title="South America"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-sa}

[^vsphere-7]: Skylake is supported for existing vSphere 6 instances only

[^vsphere-7-02]: Skylake is supported for existing vSphere 6 instances only

[^vsphere-7-03]: Skylake is supported for existing vSphere 6 instances only

[^vsphere-7-04]: Skylake is supported for existing vSphere 6 instances only

[^vsphere-7-05]: Skylake is supported for existing vSphere 6 instances only

[^vsphere-7-06]: Skylake is supported for existing vSphere 6 instances only


## Related links
{: #vs_planning-related}

* [Ordering VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req)
* [Adding ESXi servers to VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_addingservers)

