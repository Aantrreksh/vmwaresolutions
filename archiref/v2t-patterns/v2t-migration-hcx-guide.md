---

copyright:

  years:  2022, 2024

lastupdated: "2024-10-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Setting up HCX for migration from NSX-V to NSX-T
{: #v2t-hcx-guide}

You can provision an optional HCX service in the new {{site.data.keyword.vcf-auto}} instance with NSX-T, which is running in parallel with the existing {{site.data.keyword.vcf-auto-short}} with NSX-V environment. HCX deployment is fully automated in the new {{site.data.keyword.vcf-auto-short}} with NSX-T environment. HCX has various migration services (Bulk and vMotion) to help you move the workload VMs, and it provides embedded L2 Network Extension Services for the NSX-V logical switches to the NSX-T segments.

## HCX site peering over private network
{: #v2t-hcx-guide-site-peering}

![HCX site peering over private network](../../images/v2t-hcx-site-peering.svg "HCX site peering happens over a private network"){: caption="HCX site peering over private network" caption-side="bottom"}

1. Order the HCX service on the new {{site.data.keyword.vcf-auto-short}} with NSX-T environment. For more information, see [Ordering VMware HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering). This use case assumes that you specify the HCX network connection type of Public, which allows license registration and metering to be completed over the public network.

   However, if your NSX-T consolidated or management cluster is deployed with private network only, the only networking option that you can choose is private. You then need to configure a proxy server to enable license registration and metering over the public network. For more information, see [Deployment process for HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering#hcx_ordering-deploy).
2. When the automated HCX service deployment is completed, the following components are deployed and configured in the {{site.data.keyword.vcf-auto-short}} with NSX-T environment.
   * An HCX Manager appliance with an IP address on the primary VLAN portable subnet for the management of the instance.
   * A portable HCX private subnet on the primary VLAN for use by the HCX fleet appliances.
   * 8 IP addresses on the existing portable subnet for vMotion traffic on the secondary VLAN are reserved for use by the HCX fleet appliances.
   * A portable HCX public subnet on the public VLAN. This HCX Uplink network is not used in this use case.
   * HCX Manager is integrated with the {{site.data.keyword.vcf-auto-short}} with NSX-T environment's vCenter and compute and network profiles configured.
3. Install HCX Manager manually in the existing {{site.data.keyword.vcf-auto-short}} with NSX-V environment. Use an OVA downloaded through the HCX Manager in the Center Server with NSX-T environment. Deploy it onto a manually ordered portable subnet on the primary VLAN. Order an HCX activation key from the VMware Solutions console and use it to register the HCX Manager.
4. Using the HCX Manager in the {{site.data.keyword.vcf-auto-short}} with NSX-V environment, establish a site pairing to the HCX Manager in the {{site.data.keyword.vcf-auto-short}} with NSX-T environment and instantiate an HCX service mesh.

## Configuring HCX service mesh for NSX-V to NSX-T migration
{: #v2t-hcx-guide-config-hcx}

![Configuring HCX service mesh for NSX-V to NSX-T migration](../../images/v2t-hcx-service-mesh-net.svg "Configuring HCX service mesh for NSX-V to NSX-T migration uses optimal connectivity for network bandwidth point of view though the secondary VLAN."){: caption="Configuring HCX service mesh for NSX-V to NSX-T migration" caption-side="bottom"}

1. In the {{site.data.keyword.vcf-auto-short}} with NSX-T environment, HCX uses the HCX Private subnet for management for interfaces of the HCX fleet appliances, and the vMotion subnet on the secondary VLAN.
2. In the {{site.data.keyword.vcf-auto-short}} with NSX-V environment, order a new portable subnet on the primary VLAN for use as the HCX private subnet.
3. Order a new portable subnet manually on the Secondary VLAN for use as the HCX private uplink subnet.
4. The network profiles in the {{site.data.keyword.vcf-auto-short}} with NSX-T environment are created initially by the VMware Solutions automation. No changes are required for the Management and vMotion profiles. A new profile for the HCX private uplink network profile is created in the {{site.data.keyword.vcf-auto-short}} with NSX-T environment. THe profile is created by using the subnet, IP range, and gateway from the manually provisioned HCX uplink portable subnet on the Secondary VLAN. This subnet is also used by the HCX private uplink network profile in the {{site.data.keyword.vcf-auto-short}} with NSX-V environment. Therefore, ensure that the IP ranges in each environment do not overlap with each other.
5. The network profiles in the {{site.data.keyword.vcf-auto-short}} with NSX-V environment must be created:
   * The management network profile is configured by using the subnet, IP range, and gateway from the manually provisioned HCX Management portable subnet on the primary VLAN.
   * The vMotion network profile uses the subnet, IP range, and gateway from the existing vMotion subnet on the secondary VLAN. Ensure that the IP range that you define is not used by the ESXi hosts.
   * The private uplink network profile is created by using the subnet, IP range, and gateway from the manually provisioned HCX uplink portable subnet on the secondary private VLAN. This subnet is also used by the HCX private uplink network profile in the {{site.data.keyword.vcf-auto-short}} with NSX-T environment. Therefore, ensure that the IP ranges in each environment do not overlap with each other.
6. On the {{site.data.keyword.vcf-auto-short}} with NSX-V HCX Manager, create a Site Pairing and then a Service Mesh. Complete performance testing to understand bandwidth and throughput between the environments so you can calculate migration durations. For more information, see [HCX Network Underlay Characterization and Performance Outcomes](https://community.broadcom.com/viewdocument/hcx-network-underlay-characterizati?CommunityKey=ab5e7256-62d1-4688-875f-f2fe64d0aa85&tab=librarydocuments){: external}.

## Deploying HCX fleet for migration
{: #v2t-hcx-guide-deploy-hcx-fleet}

![Deploying HCX fleet for migration](../../images/v2t-hcx-hcx-fleet.svg "Deploying HCX fleet for migration. You can deploy multiple appliances to scale the migration solution."){: caption="Deploying HCX fleet for migration" caption-side="bottom"}

1. When you create a Service Mesh through the {{site.data.keyword.vcf-auto-short}} with NSX-V HCX Manager, HCX creates the HCX responder fleet appliances in the {{site.data.keyword.vcf-auto-short}} with NSX-T environment. These appliances consist of an interconnect appliance, WAN optimizer, and network extension appliance. One or more of these appliances are deployed depending on the settings that are used during the service mesh creation workflow. For more information, see [HCX deployment considerations and best practices](https://hcx.design/wp-content/uploads/2019/07/hcx_dbp_wp.pdf){: external} and [HCX compute profiles](https://hcx.design/wp-content/uploads/2020/02/hcx-compute-profiles.pdf){: external}.
2. When you create a Service Mesh through the {{site.data.keyword.vcf-auto-short}} with NSX-V HCX Manager, HCX creates the HCX initiator fleet appliances in the {{site.data.keyword.vcf-auto-short}} with NSX-V environment. These appliances consist of an interconnect appliance, WAN optimizer, and network extension appliance. One or more of these appliances are deployed depending on the settings that are used during the service mesh creation workflow.
3. The HCX network Extension service workflow is initiated through the {{site.data.keyword.vcf-auto-short}} with NSX-V HCX Manager. This workflow uses L2 bridging to connect the required NSX-V logical switches to automatically created NSX-T segments.
4. The migration workflow is used to select the required VMs to be migrated by using the vMotion, bulk, or cold migration options. At this stage, the VMs are on the NSX-T environment but north-south traffic is through the NSX-V Edges.
5. Distributed firewall and dynamic routing configurations of the NSX-T environment needs to be completed to enable network switch-over from the NSX-V environment to the NSX-T environment.

## Network switchover with HCX
{: #v2t-hcx-guide-switchover}

![Network switchover with HCX](../../images/v2t-hcx-network.svg "Network switchover with HCX."){: caption="Network switchover with HCX." caption-side="bottom"}

1. The final stage of the cut-over is to initiate the unextend networks workflow with connect cloud network to cloud edge gateway after unextending option. This workflow removes the HCX L2 bridge between the NSX-V and NSX-T environments.
2. The workflow connects the NSX-T segment to the T1 router.
3. The workflow disconnects the logical switch from the NSX-V distributed logical router.
4. North-south traffic from the VMs hosted on this segment is now through the NSX-T T0 uplink networks that are hosted on the public or primary VLANs.
5. The network switchover is now complete.

## Considerations for migrating with HCX
{: #v2t-hcx-guide-considerations}

Each HCX-NE appliance can extend up to eight segments at a time, and you can create multiple HCX-NEs if needed. You can configure them when you create the service mesh.

## Related links
{: #v2t-hcx-guide-links}

* [Ordering VMware HCX in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering)
* [HCX for {{site.data.keyword.cloud_notm}} for VMware Solutions guide](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-planning-prep-install)
* [VMware HCX user guide](https://docs.vmware.com/en/VMware-HCX/4.3/VMware%20HCX%20Documentation%204.3.zip){: external}
