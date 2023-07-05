---

copyright:

  years:  2020, 2023

lastupdated: "2023-06-14"

keywords: vmware regulated workloads, vmware regulated workloads order instance, order vmware regulated workloads, vmware regulated workloads instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Witness cluster (Multizone VMware instance only)
{: #vrw-orderinginstance-witness-cluster}

New deployments of VMware Regulated Workloads multizone instances are no longer supported. You can still add or delete clusters, add or delete ESXi servers or NFS storage, and add or remove services for existing multizone instances.
{: deprecated}

## Cluster name
{: #vrw-orderinginstance-witness-cluster-name}

The witness cluster name is set to **mcv-_xx_-witness** by default, where _xx_ represents two randomly generated alphabetic characters. You can also specify a new witness cluster name, which must meet the following requirements.

## Witness cluster name requirements
{: #vrw-orderinginstance-witness-cluster-req}

* Only lowercase alphabetic, numeric, and dash (-) characters are allowed.
* The witness cluster name must start with a lowercase alphabetic character.
* The witness cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the witness cluster name is 10 characters.
* The witness cluster name must be unique within the regulated workload instance.

## CPU model and RAM
{: #vrw-orderinginstance-witness-cluster-compute}

You can choose the following CPU models and a supported RAM size:

| CPU model | Cores     | GHz     | RAM |
|:--------- |:----------|:--------|:--- |
| Dual Intel® Xeon® Silver 4210 (Cascade Lake) | 20 | 2.2 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 (Cascade Lake) | 32 | 2.3 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 (Cascade Lake) | 40 | 2.5 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6250 (Cascade Lake) | 16 | 3.9 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 (Cascade Lake) | 48 | 2.4 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 (Cascade Lake) | 80 | 2.5 | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 (Cascade Lake) | 96 | 2.4 | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 1. Options for Cascade Lake bare metal servers" caption-side="bottom"}

## Number of bare metal servers
{: #vrw-orderinginstance-witness-cluster-bare-metal}

You can order 3 - 30 servers. All servers have the same configuration.

## vSAN configuration
{: #vrw-orderinginstance-witness-cluster-vsan}

Specify the following settings for vSAN™ configuration.

### Size for vSAN capacity disks
{: #vrw-orderinginstance-witness-cluster-vsan-disktype}

Select an option for the capacity disks that you need.

### Number of vSAN capacity disks
{: #vrw-orderinginstance-witness-cluster-vsan-diskcount}

Specify the number of capacity disks that you want to add.

## Estimated resources available per cluster
{: #vrw-orderinginstance-witness-cluster-est}

Review the estimated resources available per cluster.

## Networking
{: #vrw-orderinginstance-witness-cluster-net}

Specify the networking type and uplink speed.

### Networking type
{: #vrw-orderinginstance-witness-cluster-net-type}

The networking type is set to **Private network only**.

### Uplink speed
{: #vrw-orderinginstance-witness-uplink}

{{site.data.content.uplink-speed-options-cascadelake-list}}

{{site.data.content.simpletable-uplink-speed-locations-other-ap}}

{{site.data.content.simpletable-uplink-speed-locations-other-eur}}

{{site.data.content.simpletable-uplink-speed-locations-other-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-other-nasouth}}

## Related links
{: #vrw-orderinginstance-whitness-related}

* [Management cluster (multizone VMware instance only)](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-mgmt-cluster)
* [Procedure to order VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-procedure)
* [VMware Regulated Workloads reference architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview)
