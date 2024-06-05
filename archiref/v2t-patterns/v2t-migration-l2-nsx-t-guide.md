---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-04"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Setting up NSX-T L2 bridge for the migration from NSX-V to NSX-T
{: #v2t-l2-nsx-t-guide}

This use case is based on the [Lift and Shift Migration of Specific Parts of NSX Data Center for vSphere](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-3D173C9C-6BB9-48C3-B543-CF6B19DF4EF1.html){: external} scenario.

The NSX-T Edge node extends the NSX-V logical switch to the NSX-T overlay segment. The Edge Services Gateways (ESG) in the NSX-V environment serve as the default gateway for all north-south traffic from the workload VMs on the logical switch (virtual wire) until it is disconnected from the Distributed Logical Router (DLR), and the NSX-T overlay segment is connected to the Tier-0 (T0) or Tier-1 (T1) gateway. This process switches the default gateway to the NSX-T T0 or T1 gateway, depending on the chosen NSX-T topology. For more information, see [Extending Layer 2 networks with NSX-T Edge bridge](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-5B9390FB-7E52-4669-AF63-3C3490841432.html){: external}.

After all the workloads are migrated from NSX-V to NSX-T, the L2 bridge can be removed or reused for the next logical switch to be migrated.

## Setting up NSX-T L2 bridge in NSX-V environment
{: #v2t-l2-nsx-t-guide-setup}

![Setting up NSX-T L2 bridge in NSX-V environment](../../images/v2t-nsx-t-l2-bridge-1.svg "Set up NSX-T L2 bridge in NSX-V environment by installing an NSX-T edge node in the NSX-V environment"){: caption="Figure 1. Setting up NSX-T L2 bridge in NSX-V environment" caption-side="bottom"}

1. Register the vCenter appliance of the vCenter server with NSX-V environment as a compute manager in the NSX-T Manager. For more information, see [Add a Compute Manager](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/installation/GUID-D225CAFC-04D4-44A7-9A09-7C365AAFCA0E.html){: external}.
2. On the {{site.data.keyword.vcf-auto-short}} with NSX-V instance, complete the following steps:
   * Order a private portable subnet on the Private VLAN for use by the NSX-T Edge node VMs.
   * Create a distributed port group on the private vDS for use by the management and the overlay transport zone.
3. Using NSX-T Manager, the NSX-T Edge VMs are deployed onto hosts in the {{site.data.keyword.vcf-auto-short}} with NSX-V environment and configured:
   * Configure an IP Pool that contains IP addresses from the private portable subnet that were ordered previously. For example, TEP-NSX-V-IP-POOL.
   * The Edge Node VM requires two host switches:
     * `nsxHostSwitch overlay` - is associated with an overlay transport zone that is shared with the NSX-T ESXi transport nodes and uses the IP pool that was previously configured.
     * `nsxHostSwitch vlan` - is associated with a VLAN transport zone and is used to enable bridging the virtual wire that is connected to this interface to an NSX-T segment.
   * The Edge node VM must be part of an Edge cluster. An Edge cluster can consist of a single Edge node VM. If HA is required, deploy two Edge node VMs with the same configuration and add to the cluster.
4. Create NSX-T segments with connectivity turned off while the north-south traffic is being routed through the ESGs in the NSX-V environment. For more information, see [Create the NSX-T Data Center Topology](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-48287E4C-7C0F-4146-94D4-6D295623E7EB.html){: external}. Using NSX-T Manager, create an Edge Bridge Profile associated with the NSX-T Edges nodes. The profile defines the Edge cluster that is used for bridging, the primary node, the (optionally) backup node, and failover policy. Configure the bridging on the required NSX-T segment.
5. The NSX-V logical switch is now bridged to the associated NSX-T logical segment. You can test by deploying a VM on the {{site.data.keyword.vcf-auto-short}} with NSX-T environment on the bridged segment with an IP address from the subnet that is used on the NSX-V logical switch.

## Network switchover between NSX-V and NSX-T environments
{: #v2t-l2-nsx-t-guide-switchover}

The network switchover enables all north-south network traffic to and from the migrated VMs to traverse the NSX-T T1 and T0 routers. If issues occur with the north-south connectivity, the gateway can be moved back to the NSX-V environment.

![Network switchover](../../images/v2t-nsx-t-l2-bridge-2.svg "Network switchover requires connectivity change from NSX-V to NSX-T and enabling routing though NSX-T environment."){: caption="Figure 2. Network switchover" caption-side="bottom"}

1. Ensure that the NSX-T configuration for external connectivity such as load-balancing, NAT, BGP, and VPN tunnels are in place.
2. The NSX-V logical switch is disconnected from the DLR.
3. The NSX-T overlay segment is connected to the T1 router.
4. North-south traffic traverses now through the Workload T0.

## Migrating virtual machines
{: #v2t-l2-nsx-t-guide-migrate}

After the network switchover is complete, the workloads can be migrated. The migration can be achieved by using the Advanced Cross {{site.data.keyword.vcf-auto-short}} vMotion capability that is available with vSphere 7 Update 1c by using the UI or PowerCLI. Advanced Cross {{site.data.keyword.vcf-auto-short}} vMotion enables the migration of VMs between {{site.data.keyword.vcf-auto-short}} instances, without the requirement for Enhanced Linked Mode or Hybrid Linked Mode and hence it is now possible to migrate VMs between vCenter appliances that are in different Single Sign-On domains. Advanced Cross vCenter Server vMotion can be used for single VMs or bulk migrations. The source vCenter needs to be version 6.5 or greater.

The vMotion involves a network backing change that might be disruptive. For more information, see [vMotion between VDS/VSS and NSX-T virtual switch](https://kb.vmware.com/s/article/56991){: external}.

If you experience any issue during migration, see [Migrating a virtual machine between two different vDS versions](https://kb.vmware.com/s/article/79446){: external}.

![Migrating network connectivity with NSX-T L2 bridge solution](../../images/v2t-nsx-t-l2-bridge-3.svg "Migrating network connectivity with NSX-T L2 bridge solution."){: caption="Figure 3. Migrating network connectivity with NSX-T L2 bridge solution" caption-side="bottom"}

1. Before migrating VMs, ensure that you migrated the distributed firewall configuration to allow the required traffic flow to and from the VMs. If you are considering the Migration Coordinator, see [Migrating distributed firewall configuration](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-CFFE8C28-2D32-4AC5-98C2-9F1AEE525190.html){: external}.
2. To migrate the VMs hosted on the NSX-V logical switch that is stretched to the NSX-T environment, log in to the vCenter appliance on the {{site.data.keyword.vcf-auto-short}} with NSX-T environment and initiate the import VMs workflow. This process asks for credentials on the vCenter appliance on the {{site.data.keyword.vcf-auto-short}} with NSX-T environment and vMotion one or more VMs. For more information, see [Introducing the Advanced Cross vCenter Server vMotion capability](https://core.vmware.com/resource/introducing-advanced-cross-vcenter-server-vmotion-capability#section1){: external}.
3. When all the VMs are migrated, the L2 bridge can be disconnected.

## Considerations for using NSX-T L2 bridge in migration
{: #v2t-l2-nsx-t-guide-considerations}

A recommended practice is to use one NSX-T edge node to extend one NSX-V logical switch. This Edge node must be a virtual appliance because the NSX-T edge must be deployed on a {{site.data.keyword.cloud_notm}} Bare Metal Server that is prepared for NSX-V. Each NSX-T edge node has two N-VDS switches: the first one is connected to the physical network to provide a TEP uplink and the second one is connected to the NSX-V logical switch. The NSX-V logical switches do not support VLAN tagging, so only one logical switch can be connected to the edge node's interface. For this reason, one edge cluster (two edge nodes) is required for each NSX-V logical switch that requires L2 extension.

The default MAC address of the NSX-T virtual-distributed router needs to be changed so that it does not conflict with the one used by the NSX-V Distributed Logical Router (DLR). The virtual-distributed routers in all the transport nodes of an NSX-T environment use the default global MAC address, which is required even if the NSX-V DLR interface is disabled for that logical switch. For more information, see [Change the MAC Address of NSX-T Virtual Distributed Router](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-538774C2-DE66-4F24-B9B7-537CA2FA87E9.html){: external}.

The overlay segments in NSX-T must have the same virtual network identifier (VNI) as the Logical Switches in NSX-V. You must use the NSX-T APIs to create the overlay segments. You cannot create overlay segments with the same VNI in the NSX Manager UI.

The NSX-T Edge node VM can be deployed on any ESXi host as it has its own TEP. The ESXi host can be NSX-V prepared.

VMs running on NSX-V prepared hosts never see the VXLAN encapsulation. The ESXi host's NSX-V VTEP de-encapsulates VXLAN before it sends data to the VM. The NSX-T Edge node VM running on an NSX-V prepared host sees frames without encapsulation on the NSX-V logical switch (virtual wire) and can send these frames to the NSX-T segment.

The NSX-V logical switch (virtual wire) to be bridged requires MAC Learning or promiscuous mode and Forged Transmit to be enabled as the Edge Node VM must be able to send and receive traffic with different MAC address than its own. See [Configure the Logical Switch to Connect to the Edge Bridge](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-206CF244-3171-4146-9C60-43A797B15043.html){: external}.

VMware® uses the same MAC address for the NSX-V DLR and the NSX-T distributed router and an API call to NSX-T Manager is required to change the MAC address of the NSX-T distributed router to avoid overlap with the NSX-V DLR when bridging. For more information, see [Change the MAC address of NSX-T Virtual Distributed Router](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/migration/GUID-538774C2-DE66-4F24-B9B7-537CA2FA87E9.html){: external}.

The management NIC on the NSX-T Edge node VM must be able to reach the NSX-T Managers. The tunnel NIC (TEP) must have connectivity to the other NSX-T transport nodes, while the third NIC is connected directly to the NSX-V logical switch (virtual wire) to be bridged.

## Related links
{: #v2t-l2-nsx-t-guide-links}

* [Overview of Edge Bridging in NSX-T](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/migration/GUID-12FE83E9-2FA9-40F7-A3FF-BC21E13F6720.html){: external}
* [Extending Layer 2 Networks with NSX-T Edge Bridge](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/migration/GUID-5B9390FB-7E52-4669-AF63-3C3490841432.html){: external}
* [Ordering services for {{site.data.keyword.vcf-auto-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
