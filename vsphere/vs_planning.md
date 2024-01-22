---

copyright:

  years:  2016, 2024

lastupdated: "2024-01-22"

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

## {{site.data.keyword.cloud_notm}} data center availability
{: #vs_planning-dc-availability}

The vSphere deployment has strict requirements on the physical infrastructure. Therefore, you can deploy instances only in {{site.data.keyword.cloud_notm}} data centers that meet the requirements. The following {{site.data.keyword.cloud_notm}} data centers are available for vSphere deployment.

Cascade Lake bare metal servers are available in [multizone region](#x9774820){: term}
{{site.data.keyword.cloud_notm}} data centers. For more information, see [Multizone region (MZR) overview](/docs/loadbalancer-service?topic=loadbalancer-service-multi-zone-region-mzr-overview).

If you select a vSAN component, the location list is filtered by SSD (Solid-State Disk) availability.
{: note}

| Data center | Pod | Server options[^vsphere-7] |
|:----------- |:--- |:-------------------------- |
| CHE01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| OSA21 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| OSA22 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| OSA23 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| SNG01 | 02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SYD01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SYD04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SYD05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOK02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOK04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOK05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances - Asia-Pacific" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-ap}

| Data center | Pod | Server options[^vsphere-7-02] |
|:----------- |:--- |:----------------------------- |
| AMS03 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| FRA02 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| FRA04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| FRA05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON02 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON04 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON05 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| LON06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| MAD02 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| MAD04 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| MAD05 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| MIL01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| PAR01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances - Europe" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-eur}

| Data center | Pod | Server options[^vsphere-7-03] |
|:----------- |:--- |:----------------------------- |
| MON01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOR01 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| TOR04 | 01 | Cascade Lake |
| TOR05 | 01 | Cascade Lake |
| WDC04 | 01-05 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| WDC06 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| WDC07 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances - NA East" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-naeast}

| Data center | Pod | Server options[^vsphere-7-04] |
|:----------- |:--- |:----------------------------- |
| DAL09 | 01-06 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| DAL10 | 01-04 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| DAL12 | 01-02 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| DAL13 | 01-03 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances - NA South" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nasouth}

| Data center | Pod | Server options[^vsphere-7-05] |
|:----------- |:--- |:----------------------------- |
| SJC03 | 01-02 | Skylake, Cascade Lake |
| SJC04 | 01 | Skylake, Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances - NA West" caption-side="bottom"}
{: tab-title="NA West"}
{: tab-group="Data centers for VMware vSphere"}
{: class="simple-tab-table"}
{: #simpletabtable-cr-nawest}

| Data center | Pod | Server options[^vsphere-7-06] |
|:----------- |:--- |:----------------------------- |
| SAO01 | 01 | Skylake, Cascade Lake, SAP-certified Cascade Lake |
| SAO04 | 01 | Cascade Lake, SAP-certified Cascade Lake |
| SAO05 | 01 | Cascade Lake, SAP-certified Cascade Lake |
{: caption="Table 1. Available {{site.data.keyword.cloud_notm}} data centers for VMware vSphere instances - South America" caption-side="bottom"}
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
