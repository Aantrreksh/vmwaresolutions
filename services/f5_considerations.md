---

copyright:

  years:  2016, 2023

lastupdated: "2023-09-26"

keywords: F5 BIG-IP, F5 install, tech specs F5

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# F5 BIG-IP on {{site.data.keyword.cloud_notm}} overview
{: #f5_considerations}

F5 BIG-IP® on {{site.data.keyword.cloud}}(F5 BIG-IP Virtual Edition) provides:

* Intelligent L4-L7 load balancing and traffic management services at a local and global scale.
* Robust network and web application firewall protection.
* Secure and federated application access.

F5 BIG-IP on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from F5 Networks, not IBM.

You can install more than one instance of this service as needed.
{: shortdesc}

* For vCenter Server with NSX-T™ instances, F5 BIG-IP is supported for NSX-T 3.1 or later and for VMware vSphere® 7.0.
* For vCenter Server with NSX-V instances V4.7 and earlier, F5 BIG-IP is supported for vSphere 6.7.

{{site.data.content.para-promotion-services}}

The F5 BIG-IP version available for deployment is 17.1.
{: note}

## Technical specifications for F5 BIG-IP
{: #f5_considerations-specs}

For more information about resource requirements and capacity checking for some services, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

The following components are included with the F5 BIG-IP service:

### Virtual machines
{: #f5_considerations-specs-vms}

* Two virtual machines (VMs) with all options available.
* 2, 4, or 8 CPUs per VM depending on the licensing option.
* 4, 8, or 16 GB RAM per VM depending on the licensing option.

### Networking
{: #f5_considerations-specs-network}

* Private Virtual Extensible LAN (VXLAN) for High Availability (HA) synchronization.
* Access to Traffic Management Shell (TMSH) and Management Console through private management network.

### Licenses and fees
{: #f5_considerations-specs-license}

License fees for each VM are applied to each billing cycle, depending on the licensing option (Good, Better, or Best) and the selected bandwidth.

You cannot change the licensing level after service installation. To change the licensing level, you must delete the existing service and then use a different licensing option to reinstall the service.
{: important}

## Considerations when you install F5 BIG-IP
{: #f5_considerations-install}

Before you install the F5 BIG-IP service, review the following considerations.

Based on the license model and bandwidth that you select, two BIG-IP VE VMs are deployed with the following configuration:

| Maximum Bandwidth | License Model - Good | License Model - Better | License Model - Best |
|:------------------|:--------------------|:----------------------|:--------------------|
| 25 Mbps           | 2 CPUs, 4 GB RAM    | 4 CPUs, 8 GB RAM      | 8 CPUs, 16 GB RAM   |
| 200 Mbps          | 2 CPUs, 4 GB RAM    | 4 CPUs, 8 GB RAM      | 8 CPUs, 16 GB RAM   |
| 1 Gbps            | 2 CPUs, 4 GB RAM    | 4 CPUs, 8 GB RAM      | 8 CPUs, 16 GB RAM   |
| 3 Gbps            | 8 CPUs, 16 GB RAM   | 8 CPUs, 16 GB RAM     | 8 CPUs, 16 GB RAM   |
| 5 Gbps            | 8 CPUs, 16 GB RAM   | 8 CPUs, 16 GB RAM     | 8 CPUs, 16 GB RAM   |
| 10 Gbps           | 8 CPUs, 16 GB RAM   | 8 CPUs, 16 GB RAM     | 8 CPUs, 16 GB RAM   |
{: caption="Table 1. CPU and RAM deployments for different bandwidth and license model selections" caption-side="bottom"}
{: #f5_considerations-install-table}

### Additional considerations
{: #f5_considerations-additional}

* F5 BIG–IP limits the appliance throughput based on your chosen maximum bandwidth. Because network performance is affected by many factors, not all configurations and topologies might be able to achieve your chosen maximum bandwidth.
* The pair of BIG-IP VE VMs suitable for HA configuration is deployed only into the default cluster.

   In addition, 100% of CPU and RAM for the two BIG-IP VE VMs are also reserved because these VMs are in the data plane of the network communications. It is critical that resources are still available for them.

   To calculate the CPU and RAM reservation for a single BIG-IP VE VM, use the following formula:

   `CPU reservation = CPU speed of ESXi server * number of CPUs` (from Table 1)

   `RAM reservation = RAM size` (from Table 1)

* {{site.data.keyword.vmwaresolutions_short}} does not preconfigure HA. For more information, see the AskF5 article [Creating an Active-Standby Configuration Using the Setup Utility](https://techdocs.f5.com/en-us/bigip-14-1-0/big-ip-device-service-clustering-administration-14-1-0/creating-an-active-standby-configuration-using-the-setup-utility.html){: external}.

### Planning considerations
{: #f5_considerations-planning}

You must meet the following requirements to avoid failures with F5 BIG-IP:
* At least two active ESXi™ servers are available for the two BIG-IP VE VMs to be deployed with the anti-affinity rule of keeping the VMs on separate servers.
* The two active ESXi servers have enough resources available so that one BIG-IP VE VM can be hosted on each ESXi server with 100% CPU and RAM reservation.
* VMware vSphere HA has enough resources to host two BIG-IP VMs with 100% CPU and RAM.

Due to these requirements, you must plan for the space that is needed for F5 BIG-IP. If needed, before you order F5 BIG-IP, add 1-2 ESXi servers to your instance, or reduce vSphere HA CPU reservation for failover, or both.

## F5 BIG-IP order example
{: #f5_considerations-example}

You can order a VMware® vCenter Server **Small** instance with two ESXi servers with the following configuration: 16 cores at 2.10 GHz each with 128 GB RAM. For F5 BIG-IP, you select the **Best** license model and a value of 5 Gbps for **Maximum Bandwidth**.

In this case, a single BIG-IP VM requires on each server:

* 2.1 GHz * 8 CPUs = 16.8 GHz of CPU
* 16 GB RAM

In total that is 33.6 GHz CPU and 32 GB RAM for two BIG-IP VMs.

Each ESXi server has a capacity of 16 cores * 2.1 GHz = 33.6 GHz. Therefore, the first two requirements are met if both servers are active and there is at least 16.8 GHz of CPU and 16 GB RAM available on each server.

However, by default, vSphere HA reserves 50% of CPU and RAM for failover on vCenter Server instances that were initially deployed with two ESXi servers. For this example, the following configuration is available:

`50% of 2 * 16 cores * 2.1 GHz = 33.6 GHz available`

Other workloads are also present on the ESXi servers, for example, VMware vCenter Server, VMware NSX® Controller™, and VMware NSX Edge™. Because these resources are used, the third requirement cannot be satisfied because 33.6 GHz of CPU and 32 GB RAM are needed for the two BIG-IP VMs.

In this case, the F5 BIG-IP installation might fail, unless at least one ESXi server is added to the environment and vSphere HA failover reservations are updated to ensure that enough resources are available for two BIG-IP VE VMs. If more resources are needed to run the F5 BIG-IP service, you can add more ESXi servers before you install F5 BIG-IP.

## Related links
{: #f5_considerations-related}

* [Ordering F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_ordering)
* [Managing F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-managing_f5)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [F5 website](https://www.f5.com/){: external}
