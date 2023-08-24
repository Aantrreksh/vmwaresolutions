---

copyright:

  years:  2022, 2023

lastupdated: "2023-07-17"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for using layer 2 (L2) bridging with NSX-T
{: #arch-pattern-bridging}

With layer 2 bridging, you can have a L2 connection to a VLAN-backed port group or a device that is outside of your NSX-T data center deployment. An L2 bridge is also useful in a migration scenario, in which you need to split a subnet across physical and virtual workloads. Or when you run a database cluster on {{site.data.keyword.cloud_notm}} bare metal servers.

You can use layer 2 bridging in {{site.data.keyword.cloud_notm}} by following the principles that are presented in this pattern. You can adapt the pattern based on your needs by following VMware® best practices and {{site.data.keyword.cloud_notm}} Classic network capabilities.

## Layer 2 bridging with NSX-T
{: #arch-pattern-bridging-overview}

The following diagram presents an overview for an architecture pattern for using layer 2 bridging with NSX-T edges in {{site.data.keyword.cloud_notm}} classic infrastructure.

![Layer 2 bridging with NSX-T](../../images/arch-pattern-l2-bridge.svg "Layer 2 bridging with NSX-T."){: caption="Figure 1. Layer 2 bridging with NSX-T" caption-side="bottom"}

The following list is a summary of the architecture pattern deployment:

1. An L2 bridge requires an Edge cluster and an Edge Bridge profile to be deployed. An Edge Bridge profile specifies which Edge cluster to use for bridging and which Edge transport node acts as the primary and backup bridge.
2. You need to have a new VLAN for the bridged devices. After the VLAN is provisioned, you can request to trunk the hosts. VLAN must be trunked to all hosts in your cluster through {{site.data.keyword.cloud_notm}} Classic portal (Classic Infrastructure > Network > Gateway appliances). Then, add the ESX hosts to a wanted NSX-T VLAN transport zone, for example `tz-bridge`.
3. On the edge cluster uplink distributed port group, enable Promiscuous mode and Forged transmits for bridging. Add these settings to the wanted NSX-T VLAN transport zone, for example `tz-bridge`.
4. When you configure an NSX-T overlay segment, you can specify an Edge bridge profile to enable layer 2 bridging. Use the VLAN ID of the additional bridged VLAN on your configuration.
5. Provision your servers (for example Bare Metal Servers) normally to the VLAN, and after the provisioning you can change the IP configuration to match your NSX-T overlay design. Logically, you can attach the server to the same subnet as configured on your NSX-T overlay segment.
6. After the change, your server's default gateway is Tier 1 (T1) gateway's IP address. You can then communicate with the VMs on your overlay segments and use NSX-T gateway firewalls.

To use the capability, you can either use the existing workload edge cluster, or deploy a new edge cluster for bridging. If you use the existing workload edge cluster, you must create the edge bridge profile by using that cluster and change the existing-distributed port group to allow Promiscuous mode and Forged transmits. This setup shares the capacity of the private uplinks from the edge nodes for both private routed and bridged traffic. Transport zones are defined in the edge host switch (N-VDS), for example add the new `tz-bridge` to `nvds-edge-private`.

![Layer 2 bridge setup with workload edge cluster](../../images/arch-pattern-l2-workload-edge.svg "Layer 2 bridge setup with workload edge cluster."){: caption="Figure 2. Layer 2 bridge setup with workload edge cluster" caption-side="bottom"}

Alternatively, you can deploy a new edge cluster for bridging. In this case, you must create new edge nodes and create a new edge cluster by using these nodes. When you configure the edge bridge profile, you can then use this edge cluster for bridging only. This alternative scales better, and provides a better dedicated bridging performance. Transport zones are defined in the edge host switch (N-VDS), for example add the new `tz-bridge` to `nvds-bridge`.

![Layer 2 bridge setup with a new bridge edge cluster](../../images/arch-pattern-l2-bridge-edge.svg "Layer 2 bridge setup with a new bridge edge cluster."){: caption="Figure 3. Layer 2 bridge setup with a new bridge edge cluster" caption-side="bottom"}

Make sure you have the bridged VLANs transport zone (for example `tz-bridge`) configured on all wanted transport nodes.
{: note}

## Considerations
{: #arch-pattern-bridging-considerations}

When you design or deploy this architecture pattern, consider the following steps: 

* Using the existing workload edge cluster is good for testing the layer 2 capability and for small deployments.
* If you have a larger deployment, deploying a dedicated edge cluster or several edge clusters offers better performance and generally scales better.
* If you use new edge nodes for bridging, they do not have to be in the same network or POD as the workload edge. Edge nodes are transport nodes and they communicate with the other NSX-T transport nodes (edges or hosts) through Geneve tunnels over layer 3 routed connections by using the {{site.data.keyword.cloud_notm}} classic network as a transport network.

## Related links
{: #aarch-pattern-bridging-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Getting started with {{site.data.keyword.cloud_notm}} Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started)
* [Installing NSX-T edge transport nodes](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/installation/GUID-5EF2998C-4867-4DA6-B1C6-8A6F8EBCC411.html){: external}
* [Administering NSX-T Layer 2 bridging](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-B4ABDE64-52BC-40F0-A560-670D3B7EAF7A.html){: external}
