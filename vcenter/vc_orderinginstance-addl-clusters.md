---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-24"

keywords: additional cluster, optional cluster, workload cluster, separate cluster, gateway cluster

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Additional clusters (optional)
{: #vc_orderinginstance-addl-clusters}

Optionally, you can order a separate cluster for workloads by toggling the **Deploy separate workload cluster** switch on.

Also, you can order a dedicated cluster for the network edge and the firewall components that are required for the Juniper® vSRX service by toggling the **Deploy gateway cluster** switch on. The gateway cluster is deployed in the same data center as the consolidated cluster.

The data center of the consolidated cluster must be available for gateway cluster deployment. Gateway cluster deployment is not supported for **Dallas 09**.
{: important}

## Workload cluster configuration
{: #vc_orderinginstance-addl-clusters-wkld}

By default, the name of the separate workload cluster is set to the **_instance name_-workload**.

You can also specify a new cluster name that meets the requirements listed in [Cluster name](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-consold-cluster#vc_orderinginstance-consold-cluster-name).

The configuration options for the separate workload cluster are similar to the consolidated cluster, with the exception of the number of bare metal servers that you can order:

{{site.data.content.number-of-baremetal-servers-wkld}}



### Reuse VLANs from the consolidated cluster
{: #vc_orderinginstance-addl-clusters-wkld-reuse-vlans}

This setting is specific to the separate workload cluster. In the **VLANs** section of the workload cluster configuration, you can select the **Reuse VLANs from the consolidated cluster** option to reuse the public and private VLANs of the consolidated cluster.

## Gateway cluster configuration
{: #vc_orderinginstance-addl-clusters-gate}

By default, the name of the gateway cluster is set to the **_instance name_-edge**.

You can also specify a new cluster name that meets the requirements listed in [Cluster name](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-consold-cluster#vc_orderinginstance-consold-cluster-name).

### CPU model
{: #vc_orderinginstance-addl-clusters-gate-cpu}

You can choose between the following CPU models:
* Dual Intel Xeon® Silver 4210 processor (Cascade Lake) with 20 cores, 2.20 GHz, and 10 Gb of uplink speed.
* Dual Intel Xeon Gold 5218 processor (Cascade Lake) with 32 cores, 2.30 GHz, and 25 Gb of uplink speed.

### RAM
{: #vc_orderinginstance-addl-clusters-gate-ram}

You can select different values of RAM in the range 64 GB - 1.5 TB.

### Number of bare metal servers
{: #vc_orderinginstance-addl-clusters-gate-bm}

The number of servers is set to 2 and cannot be changed. Both servers have the same configuration.

### Networking type
{: #vc_orderinginstance-addl-clusters-gate-netw}

Select either **Public and private network** or **Private network only**.

## Related links
{: #vc_orderinginstance-addl-clusters-links}

* [Network interface](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-network-interface-settings)
* [Procedure to order Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure)
