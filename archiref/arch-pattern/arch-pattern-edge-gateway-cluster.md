---

copyright:

  years:  2022, 2024

lastupdated: "2024-07-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for using gateway cluster with NSX
{: #arch-pattern-edge-gateway-cluster}

When you deploy a {{site.data.keyword.vcf-auto}} instance in your {{site.data.keyword.cloud}} classic infrastructure, you might optionally deploy a gateway cluster.

The gateway cluster might host, for example, a Juniper® vSRX, Fortinet® FortiGate® or other third-party router or firewall. You can control which VLANs are associated with the router or firewall that is running on it through the [gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-about#firewall) configurations.

The gateway cluster must not be mixed with the NSX edge cluster, which consists of VMware NSX™ edge transport nodes. The gateway cluster provides compute capacity for hosting Juniper vSRX, Fortinet FortiGate, or other third-party routers or firewalls. The VLAN routing can be controlled by [gateway appliance configuration](/docs/gateway-appliance?topic=gateway-appliance-managing-vlans-and-gateway-appliances) though {{site.data.keyword.cloud_notm}} Classic portal.
{: important}

## Deploying a gateway cluster with NSX
{: #arch-pattern-edge-gateway-cluster-overview}

The following diagram presents an overview for an architecture pattern for deploying a gateway cluster with NSX.

![Gateway cluster with NSX](../../images/arch-pattern-nsx-t-edge-services-cluster.svg "Gateway cluster with NSX"){: caption="Figure 1. Gateway cluster with NSX" caption-side="bottom"}

The following list is a summary of the architecture pattern deployment:

1. You can optionally deploy a gateway cluster to host Juniper vSRX or your own routing or firewall device. This cluster is attached to both {{site.data.keyword.cloud_notm}} private and public networks through transit networks.
2. vSRX or the third-party device can route assigned VLANs through it. You can choose the VLANs to be routed through it from {{site.data.keyword.cloud_notm}} portal. You must configure the required VLAN interfaces and IP addresses to the devices, the firewall zones, the rules, and the policies.
3. If you route your management VLAN through the firewall, you can also secure your management workloads, such as vCenter and NSX managers. Ensure that you allow the traffic for your management.
4. Your workload T0 is attached to {{site.data.keyword.cloud_notm}} private network. If you route this VLAN through the firewall, add the required rules on both the firewall and T0.
5. Your workload T0 is attached to {{site.data.keyword.cloud_notm}} public network. If you route this VLAN through the firewall, add the required rules on both the firewall and T0.
6. Alter the automation-deployed routes if you need to customize the routing behavior, or establish dynamic routing between your T0 and the vSRX (or third-party device).

## Ordering new VLAN for gateway cluster with NSX
{: #arch-pattern-edge-gateway-cluster-vlan}

In some designs, extra VLANs might be preferred or needed, especially with a gateway cluster. In {{site.data.keyword.cloud_notm}}, you can provision extra VLANs for your classic NSX network deployment. While the new VLAN can be ordered through {{site.data.keyword.cloud_notm}}, the VMware vSphere® networking and NSX configuration must be done by you, manually or though scripting.

This architecture pattern shows an example for using a new VLAN for NSX T0 gateway's private uplinks. VLAN tagging design and configuration are important to get the VLAN IDs correctly through the vSphere distributed virtual switches, NSX edge transport nodes, and edge cluster up to the T0 gateways that are running on these components.

![Adding VLANs with gateway cluster](../../images/arch-pattern-nsx-t-edge-services-cluster-vlans.svg "Adding VLANs with gateway cluster."){: caption="Figure 2. Adding VLANs with gateway cluster" caption-side="bottom"}

1. In this example, you deployed an optional gateway cluster to host Juniper vSRX (or your own routing or firewall device). This cluster is attached to both {{site.data.keyword.cloud_notm}} private and public networks through untagged transit networks. These transit networks are used for static routes to route public and private traffic through the firewall that is hosted on the gateway cluster.
2. You can associate and route traffic through vSRX (or the third-party device) by assigning VLANs to the gateway cluster. You can choose the VLANs to be assigned and routed through it by using {{site.data.keyword.cloud_notm}} classic portal. You must manually configure the required VLAN interfaces and IP addresses to the vSRX or third-party devices, the related firewall zones, the rules, and the policies. Every interface that is associated and routed though VLAN is tagged with the specific VLAN ID in the gateway cluster's trunked-distributed port group. Therefore, VLAN tagged interfaces must also be used on the firewall appliance configuration.
3. In this example, a new VLAN is ordered in the private network, but you can follow the same process and logic for public side. Primary private and public VLANs are untagged (VLAN 0), while all other extra VLANs are tagged (for example VLAN 2222 or 3333 in the previous example). This tagging must be taken care of in the clusters' distributed port groups. In addition, you must manually request to trunk these VLANs to your ESXi hosts though the {{site.data.keyword.cloud_notm}} console (Classic Infrastructure > Network > Gateway appliances) so that NSX edge node VMs that are running on the specific vSphere cluster can access these VLANs. Also, if you add new hosts to the cluster, you must handle the trunking by yourself to avoid connectivity issues.
4. Your edge transport node virtual machines (VMs) use a private N-VDS host switch internally, and the edge nodes have their virtual network interfaces attached to vSphere distributed port groups, for example private VLAN uplinks. The edge transport nodes' private uplinks must be attached to a trunked-distributed port group, which allow the new VLAN ID to pass through. You can specify or limit the allowed VLANs on this trunked port group, if needed.
5. Workload T0 gateway's (hosted on the edge nodes) private uplinks are attached to the {{site.data.keyword.cloud_notm}} private network. The default private VLAN uplinks are attached to an untagged VLAN segment (VLAN 0). When you configure T0 gateway for the new uplink, you must create a new VLAN backed NSX segment for the uplink that matches its VLAN ID (for example VLAN 3333) and use that in the uplink configuration.
6. In addition to the private side, your edge transport nodes VMs also use a public N-VDS host switch, which has a nontrunk-distributed port group to an untagged VLAN (VLAN 0) providing access only to this untagged VLAN by default. This detail is important if you need new public VLANs.
7. Workload T0 gateway is attached to {{site.data.keyword.cloud_notm}} public network with its public uplink. Your primary public VLAN uplinks are attached to an untagged VLAN segment (VLAN 0), and a matching VLAN backed segment (for the default setup, VLAN 0 is used) is created for the public uplinks.

## Considerations
{: #arch-pattern-edge-gateway-cluster-considerations}

When you design or deploy this architecture pattern, consider the following steps:

* Refer to the specific third-party vendor hardware and software specifications for interoperability with VMware® ESXi™ and NSX™.
* You must provide licensing (BYOL) for the third-party router or firewall solution. Contact your vendor for details.

## Related links
{: #arch-pattern-edge-gateway-cluster-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Getting started with {{site.data.keyword.cloud_notm}} Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started)
* [Tier-0 Gateways](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-E9E62E02-C226-457D-B3A6-FE71E45628F7.html){: external}
