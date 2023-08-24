---

copyright:

  years:  2016, 2023

lastupdated: "2023-08-02"

keywords: vmware vSphere order instance, order vSphere, order vmware vSphere instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Bare metal server
{: #vs_orderinginstances-bare-metal}

When you size the capacity of your servers, consider your current requirements, and include extra capacity to accommodate anticipated growth. For more information about sizing properly, see [Exporting VMware inventory](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-inventory-export).

## Data center location
{: #vs_orderinginstances-bare-metal-dc-location}

Select the {{site.data.keyword.cloud}} data center settings. For more information, see [Region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

### Geography
{: #vs_orderinginstances-bare-metal-geo}

Select the region where the instance is to be hosted.

### Data center
{: #vs_orderinginstance-bare-metal-dc}

Select the {{site.data.keyword.cloud_notm}} data center where the instance is to be hosted. If you select a VMware vSAN™ component, the location list is filtered by SSD availability.

### Pod
{: #vs_orderinginstance-bare-metal-pod}

Select the {{site.data.keyword.cloud_notm}} data center pod where you want to deploy your resources. Keep the default pod selection if you do not have reasons to prefer a different pod.

## CPU model and RAM
{: #vs_orderinginstances-bare-metal-cpumodel-ram}

You can choose between **Cascade Lake** and **SAP-certified Cascade Lake** servers[^1u].

[^1u]: For clusters with NFS storage, where locations with appropriate 1U servers are available, 1U servers (up to 4 drives of storage) are ordered silently rather than 2U servers. For gateway clusters and clusters with vSAN storage, 2U servers are ordered.

### Cascade Lake
{: #vs_orderinginstances-bare-metal-cascade}

{{site.data.content.cascade-para-intro}}

| CPU model     | Cores     | GHz     | Storage type | RAM options |
|:------------- |:----------|:--------|:------------ |:----------- |
| Dual Intel Xeon Silver 4210 | 20 | 2.2 | Up to 12 drives | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 | 32 | 2.3 | Up to 12 drives | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 | 40 | 2.5 | Up to 12 drives | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6250 | 16 | 3.9 | Up to 12 drives | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 | 48 | 2.4 | Up to 12 drives | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 | 80 | 2.5 | Up to 24 drives | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 | 96 | 2.4 | Up to 24 drives | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 1. Options for Cascade Lake bare metal servers" caption-side="bottom"}

### SAP-certified Cascade Lake
{: #vs_orderinginstances-bare-metal-sap}

The **SAP-certified Cascade Lake** servers are not available if you selected VMware vSAN previously.
{: note}

{{site.data.content.sap-para-intro}}

{{site.data.content.simpletabtable-sap-netweaver}}

{{site.data.content.simpletabtable-sap-hana}}

## Number of bare metal servers
{: #vs_orderinginstances-bare-metal-number}

The number of VMware ESXi™ servers that you want add to the vSphere instance. You can order 1-59 servers. All servers have the same configuration.

## Related links
{: #vs_orderinginstances-bare-metal-related}

* [Storage](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-storage-settings)
* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
