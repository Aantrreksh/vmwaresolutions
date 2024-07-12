---

copyright:

  years:  2022, 2024

lastupdated: "2024-07-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for multisite NSX topologies
{: #arch-pattern-overlays-multi-site}

{{site.data.keyword.vcf-auto}} instances offer a standard NSX topology with a single NSX edge cluster, which includes a single Tier-0 (T0) and Tier-1 (T1) Gateways. You have several options to build and customize multisite overlay topologies. You can manually provision new NSX edge clusters and deploy new Tier-0 (T0) and Tier-1 (T1) Gateways after initial deployment by following VMware NSX™ documentation.

The following information provides a few examples on how these topologies can be customized for your needs.

The automated deployment provides a single NSX workload edge cluster with two edge transport nodes. Multisite topologies require more NSX edge transport nodes and clusters. You can manually deploy these after deployment by using {{site.data.keyword.cloud_notm}} private IP addresses for edge management and TEPs.
{: note}

## Multisite single-tenant
{: #arch-pattern-overlays-multi-site-multi-site-st}

Multisite single-tenant is a common use case and network deployment pattern. This topology provides seamless site recovery by using dynamic routing protocols, such as BGP. The vCenter Server automation does not deploy multisite topology automatically. However, you can customize the default single-site topology after initial vCenter Server deployment. When you have the compute capacity in the required data center, you can manually deploy the required additional edge nodes. Then, create a new edge cluster for the Tier-0 and Tier-1 Gateways through NSX. This overlay topology is highly scalable and it is possible to automate, for example, by using Ansible and Terraform.

The following diagram shows an example of a multisite single-tenant network topology. It consists of a two-layer Tier-0 design with three edge clusters. Two edge clusters in the two data centers or zones in a multizone region, and one edge cluster deployed across the multizone region with edge nodes in each participating zone or data center.

![Multisite single-tenant example topology](../../images/arch-pattern-2-zone.svg "Multisite single-tenant example topology for NSX deployment"){: caption="Figure 1. Multisite single-tenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys a single site solution, which can be manually expanded to support the target multisite topology. The deployment includes a single vCenter and three NSX Managers that are deployed in the cluster on the initial {{site.data.keyword.cloud_notm}} data center location. You must expand the compute capacity to have resources available in the other {{site.data.keyword.cloud_notm}} data center or zone in the specific {{site.data.keyword.cloud_notm}} multizone region.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 Gateways. You do not need the default Tier-1 Gateway, and it can be removed.
3. In the initial {{site.data.keyword.cloud_notm}} data center, the access to the private network is provided through private uplinks. They are attached to a portable subnet in a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, the access to the public network is provided through public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have IP addresses specific to this data center and they cannot move between the data centers.
4. You must manually deploy two additional edge cluster transport nodes. Also, you must create a new edge cluster for your Tier-0 and Tier-1 Gateways in the second {{site.data.keyword.cloud_notm}} data center hosts.
5. In the second {{site.data.keyword.cloud_notm}} data center, the access to the private network is provided through private uplinks. They are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, the access to the public network is provided through public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have IP addresses specific to this data center and they cannot move between the data centers.
6. You must manually deploy two or more edge cluster transport nodes in the regional edge cluster, at least one in each zone or data center for high availability. Then, create a new edge cluster by using these edge transport nodes, and create your regional Tier-0 in this cluster. You can select which data center (or edge node) is your preferred Tier-0 path in the regional cluster.
7. Create an overlay transit and uplinks in Tier-0 Gateways into the transit segment. Establish dynamic routing between the Tier-0 Gateways and BGP. This is the preferred routing protocol.
8. Then, create your Tier-1 Gateways in the regional edge cluster. You can select which data center (or edge node) is your preferred Tier-1 path in the regional cluster.
9. You can attach your segments into this level of Tier-1 Gateways. Also, you can create multiple segments and advertise them through Tier-1 Gateway to north bound Tier-0 Gateways.

This network topology example does not consider the management and control plane (vCenter and NSX Managers). The control plane of high availability is discussed in another availability pattern.
{: note}

The main reason that you need two layers is for physical north-south connectivity in the data centers and each data center having their own private and public VLANs and IP addresses for the uplinks. These IP addresses cannot move between the data centers. Therefore, you must consider the routing and network address translation if you use public connectivity in this topology.
{: important}

## Multisite multitenant
{: #arch-pattern-overlays-multi-site-multi-site-mt}

Multisite multitenant is a use case and network deployment pattern where tenants require a solution with conflicting IP spaces and complete route table isolation. This topology provides seamless site recovery by using dynamic routing protocols, such as BGP. The vCenter Server automation does not deploy multisite topology automatically. However, you can customize the default single-site topology after initial vCenter Server deployment. When you have the compute capacity in the required data center, you can manually deploy the required additional edge nodes. Then, create a new edge cluster for the Tier-0 and Tier-1 Gateways through NSX. This overlay topology is highly scalable and it is possible to automate, for example, by using Ansible and Terraform.

The following diagram shows an example of a multisite – multitenant topology. It consists of a two-layer Tier-0 design with three edge clusters. The routing table separation is done at Tier-1 and optionally, also at the regional Tier-0 level. Two edge clusters in the two data centers or zones in a multizone region, and one edge cluster deployed across the multizone region with edge nodes in each participating zone or data center.

![Multisite multitenant example topology](../../images/arch-pattern-2-zone-mt.svg "Multisite multitenant example topology for NSX deployment"){: caption="Figure 2. Multisite multitenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys a single site solution, which can be manually expanded to support the target multisite topology. The deployment includes a single vCenter and three NSX Managers that are deployed in the cluster on the initial {{site.data.keyword.cloud_notm}} data center location. You must expand the compute capacity to have resources available in the other {{site.data.keyword.cloud_notm}} data center or zone in the specific {{site.data.keyword.cloud_notm}} multizone region.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 Gateways. You do not need the default Tier-1 Gateway, and it can be removed.
3. In the initial {{site.data.keyword.cloud_notm}} data center, the access to the private network is provided through private uplinks. They are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, the access to the public network is provided through public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have IP addresses specific to this data center and they cannot move between the data centers.
4. You must manually deploy two additional edge cluster transport nodes and create a new edge cluster for your Tier-0 and Tier-1 Gateways in the second {{site.data.keyword.cloud_notm}} data center hosts.
5. In the second {{site.data.keyword.cloud_notm}} data center, the access to the private network is provided through private uplinks. They are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, the access to the public network is provided through public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have IP addresses specific to this data center and they cannot move between the data centers.
6. You must manually deploy two or more edge cluster transport nodes in the regional edge cluster, at least one in each zone or data center for high availability. Then, create a new edge cluster by using these edge transport nodes, and create your regional Tier-0 in this cluster. You can select which data center (or edge node) is your preferred Tier-0 path in the regional cluster. You can separate routing tables at this level by using VRF lite capability in the Tier-0 Gateway. For more information, see VMware documentation.
7. Manually create an overlay transit segment and create uplinks in Tier-0 Gateways into the transit segment. Establish dynamic routing between the Tier-0 Gateways and BGP is the preferred routing protocol. If you use VRF lite capability in the Tier-0 Gateway, you might use multiple transit segments depending on your design.
8. Then, create your Tier-1 Gateways in the regional edge cluster. You can select which data center (or edge node) is your preferred Tier-1 path in the regional cluster. You can separate routing tables at this level and decide which routes as advertised to the north bound Tier-0. As in the other multitenant patterns, you can use NAT as well.
9. You can attach your segments into this level of Tier-1 Gateways. You can create multiple segments and advertise them through Tier-1 Gateway to north-bound Tier-0 Gateways.

This network topology example does not consider the management and control plane (vCenter and NSX Managers). The control plane of high availability is discussed in another availability pattern.
{: note}

Tier-0 Gateways support VRF lite, which can be used if needed to support more complex topologies for isolating routing tables also at Tier-0 level. For more information about capabilities and limitations, see the [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}.
{: note}

The main reason that you need two layers is for physical north-south connectivity in the data centers and each data center having their own private and public VLANs and IP addresses for the uplinks. These IP addresses cannot move between the data centers. Therefore, you must consider the routing and network address translation if you use public connectivity in this topology.
{: important}

## Considerations for selecting an overlay network topology
{: #arch-pattern-overlays-multi-site-considerations}

VMware NSX™ provides many ways to build the network topologies, and the default network topology is useful for many use cases. You can typically start with this, and expand it as your needs grow. After the initial deployment is done, {{site.data.keyword.cloud_notm}} automation does use the workload overlay topology and you can change the example topology based on your needs. When changing the configuration, the default uplinks provide the basic routed connectivity to {{site.data.keyword.cloud_notm}} private and public networks. If you change the IP addresses or routing, your overlay workloads might lose connectivity.

{{site.data.keyword.cloud_notm}} offers a flexible way to build the NSX topology to your needs. When designing your own overlay network solution, it is important to know that you might deploy new NSX edge nodes and new NSX edge clusters manually. Also, consider using Ansible and Terraform to meet your goals. You can do this by following VMware documentation and design guidelines after the initial deployment.

Most of the content in the VMware NSX design guides and documentation can be applied in {{site.data.keyword.cloud_notm}}. Consider, for example, the number of required VLANs and the use of stretched VLAN in the underlay between data centers in multizone region. Also, {{site.data.keyword.cloud_notm}} private network must not be considered as Top of the Rack (ToR) switch. Backend Customer Router (BCR) does not provide dynamic routing support (BGP) by default.
{: note}

## Related links
{: #arch-pattern-overlays-multi-site-links}

* [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}
* [NSX Reference Design Guide](https://nsx.techzone.vmware.com/resource/nsx-reference-design-guide){: external}
* [NSX Multi-Location design guide (Federation + Multisite)](https://community.broadcom.com/viewdocument/nsx-t-multi-location-design-guide?CommunityKey=b76535ef-c5a2-474d-8270-3e83685f020e&tab=librarydocuments){: external}
