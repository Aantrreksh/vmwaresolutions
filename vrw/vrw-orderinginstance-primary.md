---

copyright:

  years:  2020, 2024

lastupdated: "2024-01-23"

keywords: vmware regulated workloads, vmware regulated workloads order instance, order vmware regulated workloads, vmware regulated workloads instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Primary cluster
{: #vrw-orderinginstance-consldt-cluster}

## Cluster name
{: #vrw-orderinginstance-consldt-cluster-name}

By default, the primary cluster name is set to **vrw-_xx_-management**.

{{site.data.content.orderinginstance-cluster-name-list}}

## Cluster type
{: #vrw-orderinginstance-consldt-capacity}

You can start with a smaller footprint by deploying a consolidated management and workload cluster, or you can deploy a management cluster and a separate cluster for workloads.

* **Management-optimized cluster** supports separate management and workload clusters.

   If you don't want workloads to run on the primary cluster, select this option. With this option, you get a 2-CPU Intel® Cascade Lake processor with 20 cores, 2.2 GHz, and 192 GB RAM per bare metal server. You must include a separate cluster for workloads. Under **Additional cluster for workloads**, complete the settings to customize the bare metal hardware based on your workload capacity requirements.

* **Customizable consolidated cluster** supports a range of CPU and RAM options to optimize capacity for both management and workload clusters.

   You can choose a Cascade Lake CPU model and a RAM size according to your needs. This option brings down the entry price point by enabling workloads to run alongside VMware® management components in the same cluster. You can start with only 6 hosts instead of 10. This option is helpful for proof of concepts (POCs) or if you want to start small and grow over time.

## Number of bare metal servers
{: #vrw-orderinginstance-consldt-bare-metal}

You can order 4-51 servers. All servers have the same configuration.

## vSAN configuration
{: #vrw-orderinginstance-consldt-vsan}

* For the **Small** capacity, you get two vSAN™ capacity disks 1.9 TB SSD.
* For the **Customizable** capacity, you can choose the type and number of capacity disks according to your needs.
* Use the IBM-provided VMware license for vSAN by selecting **Include with purchase**. Select **I will provide** only if you are upgrading an existing BYOL cluster.

## Estimated resources available per cluster
{: #vrw-orderinginstance-consldt-est}

Review the estimated resources available per cluster.

## Networking
{: #vrw-orderinginstance-consldt-net}

Specify the networking type and uplink speed.

### Networking type
{: #vrw-orderinginstance-consldt-net-type}

The networking type is set to **Private network only** by default.

### Uplink speed
{: #vrw-orderinginstance-consldt-uplink}

{{site.data.content.uplink-speed-options-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

## Related links
{: #vrw-orderinginstance-primary-related}

* [Procedure to order VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-procedure)
* [VMware Regulated Workloads reference architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview)
