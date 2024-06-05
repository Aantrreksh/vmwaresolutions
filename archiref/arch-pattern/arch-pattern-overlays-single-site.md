---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-03"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for single site NSX topologies
{: #arch-pattern-overlays-single-site}

{{site.data.keyword.vcf-auto}} instances offer a standard VMware NSX™ topology with a single NSX edge cluster, which includes Tier-0 (T0) and Tier-1 (T1) Gateways. You have several options to build and customize the overlay topology. You can provision new NSX edge clusters and deploy new Tier-0 (T0) and Tier-1 (T1) Gateways.

This pattern provides a few examples on how these topologies can be customized for your needs.

## Single-site single-tenant
{: #arch-pattern-overlays-single-site-single-site-st}

Single-site single-tenant is the most common use case and network deployment pattern. The vCenter Server automation deploys an example topology by following this model, which includes single Tier-0 and Tier-1 Gateways and a few NSX overlay segments as a starting point. This topology is highly scalable and easy to automate.

The following diagram shows an example of a customer deployment that uses the standard topology, when the segments are attached to the Tier-1 Gateway. You can add more segments to the existing Tier-1 Gateway or more Tier-1 Gateways on the same NSX edge clusters, if needed.

![Single-site single-tenant example topology with Tier-1 Gateway](../../images/arch-pattern-1-zone-t1.svg "Single-site single-tenant example topology using both Tier-0 and Tier-1 Gateways"){: caption="Figure 1. Single-site single-tenant example topology with Tier-1 Gateway" caption-side="bottom"}

1. The vCenter Server automation deploys an example single-site topology, which follows the principles that are presented in this model. The deployment includes a single vCenter and three NSX managers that are deployed in the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 Gateways.
3. The Tier-0 Gateway provides north-south routing capabilities and the access to {{site.data.keyword.cloud_notm}} private network is provided through its uplinks.
4. The access to private network is provided through private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. The automation provisions the IP addresses to the uplinks from the {{site.data.keyword.cloud_notm}} managed 10/8 address space.
5. If you provision your instance with public interfaces, the access to public network is provided through public uplinks. These uplinks are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks, and the public IP addresses to the uplinks are provisioned by the automation.
6. A single Tier-1 Gateway is provisioned by the automation for the workloads. You can use this topology or customize it by provisioning new Tier-1 Gateways.
7. You can expand the default topology by adding new segments to the existing Tier-1 Gateway (or to the new Tier-1 Gateways provisioned by you). The route advertisements between T1 and T0 gateways are fully customizable by you and are done by NSX. No routing protocol is required or used between T1 and T0 advertisements.

The following diagram shows an example of a customer deployment that uses the standard topology, when the segments are attached directly to the Tier-0 Gateway. You can add more segments to the Tier-0 Gateway or and delete the Tier-1 Gateway that is deployed by the automation, if needed.

![Single-site single-tenant example topology](../../images/arch-pattern-1-zone-t0.svg "Single-site single-tenant example topology for NSX deployment"){: caption="Figure 2. Single-site single-tenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys an example topology by following this model. The deployment includes a single vCenter and three NSX Managers that are deployed in the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 Gateways.
3. The Tier-0 Gateway provides north-south routing capabilities and the access to {{site.data.keyword.cloud_notm}} private network is provided through its uplinks.
4. The access to private network is provided through private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. The automation provisions the IP addresses to the uplinks from the {{site.data.keyword.cloud_notm}} managed 10/8 address space.
5. If you provision your instance with public interfaces, the access to public network is provided through public uplinks, which are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks, and the public IP addresses to the uplinks are provisioned by the automation.
6. You can expand the default topology by adding new segments to the existing Tier-0 Gateway. You can delete the Tier-1 gateway that is deployed by the automation, if not needed in your topology.

## Single-site – multitenant
{: #arch-pattern-overlays-single-site-single-site-mt}

Single-site – multitenant pattern provides a simple highly scalable pattern if you need multiple tenants (for example, different business units), which require route table isolation or have conflicting IP address spaces. This deployment pattern uses the base topology that is provided by {{site.data.keyword.cloud_notm}} vCenter Server automation, which includes single Tier-0 and Tier-1 Gateways and a few NSX overlay segments as a starting point. If you have multiple tenants, you can divide them by using multiple Tier-1 Gateways and by controlling routing advertisements, and use network address translation (NAT). 

The following diagram shows an example of a multitenant deployment by using the standard topology. Also, it shows how to expand it for a simple multitenant pattern. You can manually deploy multiple Tier-1 Gateways through NSX and add each tenant segment to their own Tier-1 Gateway.

![Single-site multitenant example topology](../../images/arch-pattern-1-zone-t1-mt.svg "Single-site  multitenant example topology for NSX deployment"){: caption="Figure 3. Single-site multitenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys an example single-site topology, which follows the principles that are presented in this model. The deployment includes a single vCenter and three NSX Managers that are deployed in the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 Gateways.
3. The Tier-0 Gateway provides north-south routing capabilities and the access to {{site.data.keyword.cloud_notm}} private network is provided through its uplinks.
4. The access to private network is provided through private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. The automation provisions the IP addresses to the uplinks from the {{site.data.keyword.cloud_notm}} managed 10/8 address space.
5. If you provision your instance with public interfaces, the access to public network is provided through public uplinks, which are attached to a portable subnet in a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks, and the public IP addresses to the uplinks are provisioned by the automation.
6. A single Tier-1 Gateway is provisioned for the workloads by the automation. You can use this topology and expand it by adding new Tier-1 Gateways. 
7. You can add new tenant segments to the existing Tier-1 Gateway (or to the other Tier-1 Gateways provisioned by you). The route advertisements between T1 and T0 Gateways are fully customizable by you and is done by NSX. No routing protocol is required or used between T1 and T0 advertisements. You can control which routes are advertised to the Tier-0. You can also use NAT, for example, each Tier-1 Gateway can have one or more IP public addresses for inbound or outbound public traffic to be used for NAT.

You can manually deploy edge nodes on the initial cluster for scalability, if needed. You can also manually deploy new edge clusters to host new Tier-1 Gateways. 
{: note}

Tier-0 Gateways support VRF lite, which can be used if needed to support more complex topologies for isolating routing tables also at Tier-0 level. Refer to VMware documentation for more details on capabilities and limitations.
{: note}

## Considerations for selecting an overlay network topology
{: #arch-pattern-overlays-single-site-considerations}

VMware NSX™ provides many ways to build the network topologies, and the default network topology is useful for many use cases. You can typically start with this, and expand it as your needs grow. Once the initial deployment is done, {{site.data.keyword.cloud_notm}} automation does not use the workload overlay topology and you can change the example topology based on your needs. When changing the configuration, note that the default uplinks provide the basic routed connectivity to {{site.data.keyword.cloud_notm}} private and public networks. If you change the IP addresses or routing, your overlay workloads might lose connectivity.

{{site.data.keyword.cloud_notm}} offers a flexible way to build the NSX topology to your needs. When designing your own overlay network solution, it is important to know that you might deploy new NSX edge nodes and new NSX edge clusters manually. Also, consider to use Ansible and Terraform to meet your goals. You can do this by following VMware documentation and design guidelines after the initial deployment.

Most of the content in the VMware NSX design guides and documentation can be applied in {{site.data.keyword.cloud_notm}}. Consider, for example, the number of required VLANs and the use of stretched VLAN in the underlay between data centers in multizone region. Also, {{site.data.keyword.cloud_notm}} private network must not be considered as Top of the Rack (ToR) switch. Backend Customer Router (BCR) does not provide dynamic routing support (BGP) by default.
{: note}

## Related links
{: #arch-pattern-overlays-single-site-links}

* [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}
* [NSX Reference Design Guide](https://nsx.techzone.vmware.com/resource/nsx-reference-design-guide){: external}
