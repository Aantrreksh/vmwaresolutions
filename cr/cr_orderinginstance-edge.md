---

copyright:

  years:  2022, 2023

lastupdated: "2023-07-15"

keywords: cyber recovery, cyber recovery edge cluster, gateway cluster cyber recovery, cyber recovery order instance, order cyber recovery, cyber recovery instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Gateway cluster
{: #cr-orderinginstance-edge}

 An edge gateway is required. You can bring your own gateway appliance or choose from one of the following.

 * Gateway cluster with Juniper® vSRX
 * Gateway cluster with FortiGate® Virtual Appliance
 * FortiGate Security Appliance

 The gateway cluster is deployed in the same data center as the consolidated cluster.

The gateway cluster is available for all firewall appliances except for **FortiGate Security Appliance**.

The data center of the consolidated cluster must be available for gateway cluster deployment. Gateway cluster deployment is not supported for **Dallas 09**.
{: note}

## Cluster name
{: #cr-orderinginstance-edge-cluster-name}

By default, the gateway cluster name is set to **_instance name_-edge**.

{{site.data.content.orderinginstance-cluster-name-list}}

## Compute capacity
{: #cr-orderinginstance-edge-compute-capacity}

For compute capacity, you get two cluster hosts and two 3.8 TB SSD storage.

## CPU model
{: #cr-orderinginstance-edge-cpu-model}

For the CPU model, the default is a Cascade Lake Dual Intel Xeon
Silver 4210 with 20 cores, 2.20 GHz.

You can also select a Cascade Lake Dual Intel Xeon Gold
5218 with 32 cores, 2.30 GHz.

## RAM
{: #cr-orderinginstance-edge-ram}

You can select a RAM size from 64 GB, 96 GB, 128 GB, 192 GB, 384 GB,
768 GB, and 1.5 TB. The default is 768 GB.

## Uplink speed
{: #cr-orderinginstance-edge-uplink}

{{site.data.content.uplink-speed-options-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

## Networking type
{: #cr-orderinginstance-edge-network-type}

Select either **Public and private network** or **Private network only** for the gateway cluster.

## Related links
{: #cr-orderinginstance-edge-related-links}

* [Network interface](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-network-interface)
* [Procedure to order Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-order-procedure)
