---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Fortinet FortiGate VM implementation and management
{: #fortigate-implementation}

## Planning
{: #fortigate-implementation-planning}

The FortiGate® virtual machine (VM) is available in several sizes and licensing options. The license sizes limit the number of virtual CPUs that you can operate. For example, FortiGate–VM08 entitles you to up to 8 virtual CPUs. The following license bundles are available.

* Standard FW
* Standard FW + Unified Threat Management
* Standard FW + Enterprise

For more information about the capabilities of each license tier and bundle, see [FortiGate–VM on VMware ESXi data sheet](https://www.fortinet.com/content/dam/fortinet/assets/data-sheets/FortiGate_VM_ESXi.pdf){: external}.

## Specifications
{: #fortigate-implementation-specs}

FortiGate VM appliances are deployed according to the following specifications.

| Component | Specification |
|:--------- |:------------- |
| vCPU      | Determined by the selected license tier |
| vRAM      | For 2–CPU deployments, the initial allocation is 4 GB; for 4–CPU deployments, it is 6 GB; for all other deployments, it is 12 GB |
| High availability | Two appliances deployed to ensure high availability |
| Disk usage | One 2 GB and one 30 GB disk |
| Disk backing | When deployed to a gateway cluster, local SSD storage; when deployed to any other cluster, by using vSAN or {{site.data.keyword.cloud}} Endurance, as applicable |
{: caption="Table 1. Appliance specifications" caption-side="bottom"}

{{site.data.keyword.cloud_notm}} automation limits you to choosing 16– and 32–CPU options when you deploy FortiGate into a gateway cluster.

## Network configuration
{: #fortigate-implementation-network}

The FortiGate virtual appliances are deployed with 10 network interfaces.

### Management interface
{: #fortigate-implementation-management-network}

The management interface is attached to the management VLAN and port group for the corresponding cluster, and a management IP address is assigned by {{site.data.keyword.cloud_notm}} automation for this interface. Do not reassign or reconfigure this management interface.

When deployed to a management cluster that has public interfaces, a firewall and source NAT rules are created on the services NSX Edge™ to allow the FortiGate devices to connect to the public network by using http and https only. It allows license management and it is not recommended to change these rules as it might lead to your license to be deactivated.

When deployed to a gateway cluster, or to a management cluster that has only private interfaces, you must instead provide the details for a proxy server that the FortiGate appliances can use to connect to the public network for licensing. The appliances might attempt to access any of the following hostnames:

* update.fortiguard.net
* service.fortiguard.net
* support.fortinet.com
* guard.fortinet.com

### HA interface
{: #fortigate-implementation-ha-network}

When deployed to a management cluster, the FortiGate appliances’ HA interfaces are connected to a dedicated logical switch.

When deployed to a gateway cluster, the FortiGate appliances’ HA interfaces are connected to the storage VLAN used by the gateway cluster.

### Firewall interfaces
{: #fortigate-implementation-firewall-network}

When deployed to a management cluster, the remaining firewall interfaces for the FortiGate appliances are attached to the management network yet with no IP addresses assigned. You must assign these interfaces to the networks you want to protect.

When deployed ot a gateway cluster, the FortiGate VM appliances are connected to the {{site.data.keyword.cloud_notm}} transit network and configured to peer with the {{site.data.keyword.cloud_notm}} customer routers. Define appropriate firewall rules before you configure your VLANs to be protected by the gateway cluster.

## VMware DRS and reservations
{: #fortigate-implementation-drs}

Because it provides time–sensitive networking services, FortiGate VM must be configured to ensure that it has adequate resources. The {{site.data.keyword.cloud_notm}} automation configures a reservation to ensure that the virtual appliances receive their full allotment of CPU and memory. To assure high availability, the {{site.data.keyword.cloud_notm}} automation also creates a DRS anti–affinity rule to restrict the two FortiGate VM virtual appliances from running on the same host.

## License requirements
{: #fortigate-implementation-license}

This architecture requires FortiGate VM licensing from Fortinet®. {{site.data.keyword.cloud_notm}} automation provisions the FortiGate VM license based on your chosen license tier and deployment size. Your {{site.data.keyword.cloud_notm}} monthly bill reflects your order and ongoing usage of FortiGate VM. The FortiGate virtual appliances require outbound connectivity to Fortinet licensing servers to activate and maintain their license.

## Caveats
{: #fortigate-implementation-caveats}

It is not possible to change the licensing tier or licensed throughput of your FortiGate VM deployment after it is deployed. To achieve this scenario, you must deploy a new instance of FortiGate VM, migrate your configuration to the new instance, and delete the original instance.

## Related links
{: #fortigate-implementation-related}

* [Solution overview](/docs/vmwaresolutions?topic=vmwaresolutions-fortigate-overview)
* [Solution design](/docs/vmwaresolutions?topic=vmwaresolutions-fortigate-design)
* [FortiGate–VM on VMware ESXi data sheet](https://www.fortinet.com/content/dam/fortinet/assets/data-sheets/FortiGate_VM_ESXi.pdf)
