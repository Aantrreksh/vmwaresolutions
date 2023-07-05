---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-30"

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

{{site.data.content.exception-number-of-baremetal-servers}}

### Reuse VLANs from the consolidated cluster
{: #vc_orderinginstance-addl-clusters-wkld-reuse-vlans}

This setting is specific to the separate workload cluster. In the **VLANs** section of the workload cluster configuration, you can select the **Reuse VLANs from the consolidated cluster** option to reuse the public and private VLANs of the consolidated cluster.

## Gateway cluster configuration
{: #vc_orderinginstance-addl-clusters-gate}

By default, the name of the gateway cluster is set to the **_instance name_-edge**.

You can also specify a new cluster name that meets the requirements listed in [Cluster name](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-consold-cluster#vc_orderinginstance-consold-cluster-name).

### CPU model
{: #vc_orderinginstance-addl-clusters-gate-cpu}

You can choose the following CPU models:
* Dual Intel® Xeon® Silver 4210 processor (Cascade Lake)
* Dual Intel Xeon Gold 5218 processor (Cascade Lake)

### RAM
{: #vc_orderinginstance-addl-clusters-gate-ram}

You can select different values between 64 GB and 1.5 TB.

### Number of bare metal servers
{: #vc_orderinginstance-addl-clusters-gate-bm}

The number of servers is set to 2 and cannot be changed. Both servers have the same configuration.

### Uplink speed
{: #vc_orderinginstance-addl-clusters-gate-uplink}

{{site.data.content.uplink-speed-options-cascadelake-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

### Networking type
{: #vc_orderinginstance-addl-clusters-gate-netw}

Select either **Public and private network** or **Private network only**.

## Related links
{: #vc_orderinginstance-addl-clusters-links}

* [Network interface](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-network-interface-settings)
* [Procedure to order vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure)
