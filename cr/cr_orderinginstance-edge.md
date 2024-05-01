---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-03"

keywords: cyber recovery, cyber recovery edge cluster, gateway cluster cyber recovery, cyber recovery order instance, order cyber recovery, cyber recovery instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Gateway cluster
{: #cr-orderinginstance-edge}

 An edge gateway is required. You can bring your own gateway appliance or choose from one of the following options:

 * Gateway cluster with Juniper® vSRX
 * Gateway cluster with FortiGate® Virtual Appliance
 * FortiGate Security Appliance

 The gateway cluster is deployed in the same data center as the consolidated cluster.

The gateway cluster is available for all firewall appliances except for **FortiGate Security Appliance**.

The data center of the consolidated cluster must be available for gateway cluster deployment. Gateway cluster deployment is not supported for **Dallas 09**.
{: note}

## Cluster name
{: #cr-orderinginstance-edge-cluster-name}

The gateway cluster name is preset to **_instance name_-edge**.

{{site.data.content.orderinginstance-cluster-name-list}}

## Compute capacity
{: #cr-orderinginstance-edge-compute-capacity}

For compute capacity, you get two cluster hosts and two 3.8 TB SSD storage.

## CPU model
{: #cr-orderinginstance-edge-cpu-model}

You can choose between the following CPU models:
* Dual Intel Xeon® Silver 4210 processor (Cascade Lake) with 20 cores, 2.20 GHz, and 10 Gb of uplink speed.
* Dual Intel Xeon Gold 5218 processor (Cascade Lake) with 32 cores, 2.30 GHz, and 25 Gb of uplink speed.

## RAM
{: #cr-orderinginstance-edge-ram}

You can select different values of RAM in the range 64 GB - 1.5 TB.

## Networking type
{: #cr-orderinginstance-edge-network-type}

Select either **Public and private network** or **Private network only** for the gateway cluster.

## Related links
{: #cr-orderinginstance-edge-related-links}

* [Network interface](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-network-interface)
* [Procedure to order {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-order-procedure)
