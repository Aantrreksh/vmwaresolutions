---

copyright:

  years:  2022, 2023

lastupdated: "2023-08-03"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Target NSX-T environment example topologies 
{: #v2t-example-overlays}

VMware vCenter Server® instances offer a standard VMware NSX-T™ topology with a single NSX-T edge cluster, which includes a single Tier-0 (T0) and Tier-1 (T1) gateways. You have several options to build and customize the overlay topology. Also, you can provision new NSX-T edge clusters and deploy new Tier-0 (T0) and Tier-1 (T1) gateways. 

The following examples show how these topologies can be customized for your needs.

The automated deployment provides you a single NSX-T workload edge cluster with two edge transport nodes. Some of the more advanced topologies might require additional NSX-T edge transport nodes and clusters. 
{: note}

## Single-site – single tenant
{: #v2t-example-overlays-single-site-st}

Single-site – single tenant is the most common use case and network deployment pattern. The vCenter Server® automation deploys an example topology by following this model, which includes single Tier-0 and Tier-1 gateways and a few NSX-T overlay segments as a starting point. This topology is highly scalable and can be automated.

These options are suitable for customers with workload that run on a single data center, single tenant, and do not have overlapping IP addresses inside their own workloads.

Overlapping IP addresses refers to overlay segments between customer environments that run on the vCenter Server instance.
{: note}

The following diagram shows an example of a customer deployment that uses the standard topology, when the segments are attached to the Tier-1 gateway. You can add more segments to the existing Tier-1 gateway or add more Tier-1 gateways on the same NSX-T edge clusters, if needed.

![Single-site – single tenant example topology with Tier-1 gateway](../../images/v2t-diagrams-1-zone-t1.svg "Single-site – single tenant example topology by using both Tier-0 and Tier-1 gateways."){: caption="Figure 1. Single-site – single tenant example topology with Tier-1 gateway" caption-side="bottom"}

1. The vCenter Server automation deploys an example single-site topology, which follows the principles that are presented in this model. The deployment includes a single vCenter and three NSX-T Managers that are deployed on the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 gateways.
3. The Tier-0 gateway provides north-south routing capabilities and access to {{site.data.keyword.cloud_notm}} private network is provided though its uplinks.
4. Access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. IP addresses for the uplinks are provisioned by automating the 10/8 address space that is managed by the {{site.data.keyword.cloud_notm}}.
5. If you provision your instance with public interfaces, access to public network is provided though public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks and public IP addresses to the uplinks are provisioned by the automation.
6. A single Tier-1 gateway is provisioned by the automation for the workloads. You can use this topology or customize it by provisioning new Tier-1 gateways. 
7. You can expand the default topology by adding new segments to the existing Tier-1 Gateway (or to the new Tier-1 gateways provisioned by you). The route advertisements between T1 and T0 gateways are customizable by you fully and done by NSX-T. No routing protocol is required or used between T1 and T0 advertisements.

The following diagram shows an example of a customer deployment by using the standard topology. Consider that the segments are attached directly to the Tier-0 gateway. You can add more segments to the Tier-0 gateway or delete the Tier-1 gateway that is deployed by the automation, if needed.

![Single-site – single tenant example topology](../../images/v2t-diagrams-1-zone-t0.svg "Single-site – single tenant example topology for NSX-T deployment."){: caption="Figure 2. Single-site – single tenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys an example single-site topology, which follows the principles that are presented in this model. The deployment includes a single vCenter and three NSX-T Managers that are deployed on the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 gateways.
3. The Tier-0 gateway provides north-south routing capabilities and access to {{site.data.keyword.cloud_notm}} private network is provided though its uplinks.  
4. Access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. IP addresses for the uplinks are provisioned by automating the 10/8 address space that is managed by the {{site.data.keyword.cloud_notm}}.
5. If you provision your instance with public interfaces, access to public network is provided though public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks and public IP addresses to the uplinks are provisioned by the automation.
6. You can expand the default topology by adding new segments to the existing Tier-0 Gateway. You can delete the Tier-1 gateway that is deployed by the automation, if not needed in your topology.


## Single-site - multitenant
{: #v2t-example-overlays-single-site-mt}

Single-site - multitenant pattern provides a simple highly scalable pattern if you need multiple tenants. For example, different business units that require route table isolation or have conflicting IP address spaces. This deployment pattern uses the base topology that is provided by {{site.data.keyword.cloud_notm}} vCenter Server automation. This includes single Tier-0 and Tier-1 gateways and a few NSX-T overlay segments as a starting point. If you have multiple tenants, you can divide them by using multiple Tier-1 gateways and by controlling routing advertisements and use network address translation (NAT). 

This option is suitable for customers with workloads that run on a multiple data center, single tenant, and have some overlapping IP addresses inside their own workloads.

Overlapping IP addresses refers to overlay segments between customer environments that run on the vCenter Server instance.
{: note}

The following diagram shows an example of a multitenant deployment by using the standard topology. Also, you can see how to expand that for a simple multitenant pattern. You can deploy multiple Tier-1 gateways manually through NSX-T and add each tenant segment to their own Tier-1 gateway.

![Single-site – multitenant example topology](../../images/v2t-diagrams-1-zone-t1-mt.svg "Single-site – multitenant example topology for NSX-T deployment."){: caption="Figure 3. Single-site – multitenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys an example single-site topology, which follows the principles that presented in this model. The deployment includes a single vCenter and three NSX-T Managers that are deployed on the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 gateways.
3. The Tier-0 gateway provides north-south routing capabilities and access to {{site.data.keyword.cloud_notm}} private network is provided though its uplinks.  
4. Access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. IP addresses for the uplinks are provisioned by automating the 10/8 address space that is managed by the {{site.data.keyword.cloud_notm}}.
5. If you provision your instance with public interfaces, access to public network is provided though public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks and public IP addresses to the uplinks are provisioned by the automation.
6. A single Tier-1 gateway is provisioned by the automation for the workloads. You can use this topology and expand it by adding new Tier-1 gateways. 
7. You can add new tenant segments to the existing Tier-1 gateway (or to the other Tier-1 gateways provisioned by you). The route advertisements between T1 and T0 gateways is customizable by you fully and done by NSX-T. No routing protocol is required or used between T1 and T0 advertisements. You can control which routes are advertised to the Tier-0. You can also use NAT, for example each Tier-1 gateway can have one or more IP public addresses for inbound or outbound public traffic to be used for NAT.

You can deploy edge nodes on the initial cluster for scalability manually, if needed. You can also deploy new edge clusters to host new Tier-1 gateways manually. 
{: note}

Tier-0 gateways support VRF Lite, which can be used if needed to support more complex topologies for isolating routing tables at Tier-0 level as well. Refer to VMware® documentation for more details on capabilities and limitations.
{: note}

## Multisite – single tenant
{: #v2t-example-overlays-multi-site-st}

Multisite – single tenant is also a common use case and network deployment pattern. This topology provides seamless site recovery by using dynamic routing protocols, such as BGP. The vCenter Server automation does not deploy multisite topology automatically. However, you can customize the default single-site topology post initial vCenter Server deployment. When you have the compute capacity in the required data center, you can deploy the required extra edge nodes manually. Then, you can create a new edge cluster for the Tier-0 and Tier-1 gateways though NSX-T. This overlay topology is highly scalable and it is possible to automate, for example by using Ansible and Terraform.

This option is suitable for customers with workloads that run on a multiple data center, single tenant, and do not have overlapping IP addresses inside their own workloads.

Overlapping IP addresses refers to overlay segments between customer environments that run on the vCenter Server instance.
{: note}

The following diagram shows an example of a multisite – single tenant network topology. It consists of a two layer Tier-0 design with three edge clusters. For this, consider two edge clusters in the two data centers or zones in a multizone region. And also, one edge cluster deployed across the multizone region with edge nodes in each participating zone or data center. 

![Multisite – single tenant example topology](../../images/v2t-diagrams-2-zone.svg "Multisite – single tenant example topology for NSX-T deployment."){: caption="Figure 4. Multisite – single tenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys a single site solution, which can be manually expanded to support the target multisite topology. The deployment includes a single vCenter and three NSX-T Managers that are deployed on the cluster on the initial {{site.data.keyword.cloud_notm}} data center location. You must expand the compute capacity to have resources available in the other {{site.data.keyword.cloud_notm}} data center or zone in the specific {{site.data.keyword.cloud_notm}} multizone region.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 gateways. You do not need the default Tier-1 Gateway, and it can be removed.
3. In the initial {{site.data.keyword.cloud_notm}} data center, access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, access to public network is provided though public uplinks. They are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have specific IP addresses to this data center and they cannot move between the data centers.
4. You must deploy two additional edge cluster transport nodes manually. Also, you must create a new edge cluster for your Tier-0 and Tier-1 gateways in the second {{site.data.keyword.cloud_notm}} data center hosts.
5. In the second {{site.data.keyword.cloud_notm}} data center, access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, access to public network is provided though public uplinks, which are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have specific IP addresses to this data center and they cannot move between the data centers.
6. You must deploy two or more edge cluster transport nodes in the regional edge cluster manually. Consider at least one in each zone or data center for high availability. Then, create a new edge cluster by using these edge transport nodes, and create your regional Tier-0 in this cluster. You can select which data center (or edge node) is your preferred Tier-0 path in the regional cluster.
7. Create an overlay transit and create uplinks in Tier-0 gateways into the transit segment. Establish dynamic routing between the Tier-0 gateways. BGP is the preferred routing protocol.
8. Create your Tier-1 gateways in the regional edge cluster. You can select which data center (or edge node) is your preferred Tier-1 path in the regional cluster.
9. You can attach your segments into this level of Tier-1 gateways. You can create multiple segments and advertise them through Tier-1 gateway to north bound Tier-0 gateways.

This network topology example doesn't consider the management and control plane (vCenter and NSX Managers). The control plane high availability is discussed in another availability pattern. 
{: note}

The main reason that you need two layers is for physical north-south connectivity in the data centers. Each data center must have their own private and public VLANs and IP addresses for the uplinks. These IP addresses cannot move between the data centers. Therefore, it requires your attention for routing and network address translation if you use public connectivity in this topology.
{: important}

## Multisite – multitenant
{: #v2t-example-overlays-multi-site-mt}

Multisite – single tenant is also a use case and network deployment pattern where tenants require a solution with conflicting IP spaces and complete route table isolation. This topology provides seamless site recovery by using dynamic routing protocols, such as BGP. The vCenter Server automation doesn't deploy multisite topology automatically. However, you can customize the default single-site topology post initial vCenter Server deployment. When you have the compute capacity in the required data center, you can deploy the required extra edge nodes manually. Then, you can create a new edge cluster for the Tier-0 and Tier-1 gateways through NSX-T. This overlay topology is highly scalable and it is possible to automate, for example by using Ansible and Terraform.

This option is suitable for customers with workloads that run on a multiple data center, single tenant, and have overlapping IP addresses inside their own workloads.

Overlapping IP addresses refers to overlay segments between customer environments that run on the vCenter Server instance.
{: note}

The following diagram shows an example of a multisite – multitenant topology. It consists of a two layer Tier-0 design with three edge clusters. The routing table separation is done at Tier-1 and optionally also at the regional Tier-0 level. For this, consider two edge clusters in the two data centers or zones in a multizone region. And also, one edge cluster deployed across the multizone region with edge nodes in each participating zone or data center.

![Multisite – multitenant example topology](../../images/v2t-diagrams-2-zone-mt.svg "Multisite – multitenant example topology for NSX-T deployment."){: caption="Figure 5. Multisite – multitenant example topology" caption-side="bottom"}

1. The vCenter Server automation deploys a single site solution, which can be manually expanded to support the target multisite topology. The deployment includes a single vCenter and three NSX-T Managers that are deployed on the cluster on the initial {{site.data.keyword.cloud_notm}} data center location. You must expand the compute capacity to have resources available in the other {{site.data.keyword.cloud_notm}} data center or zone in the specific {{site.data.keyword.cloud_notm}} multizone region.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 gateways. The default Tier-1 Gateway is not necessary, and it can be removed.
3. In the initial {{site.data.keyword.cloud_notm}} data center, access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, access to public network is provided though public uplinks, which are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have specific IP addresses to this data center and they cannot move between the data centers.
4. You must deploy two additional edge cluster transport nodes manually. Also, you must create a new edge cluster for your Tier-0 and Tier-1 gateways in the second {{site.data.keyword.cloud_notm}} data center hosts.
5. In the second {{site.data.keyword.cloud_notm}} data center, access to private network is provided though private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. If you provision your instance with public interfaces, access to public network is provided though public uplinks, which are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The uplinks have specific IP addresses to this data center and they cannot move between the data centers.
6. You must deploy two or more edge cluster transport nodes in the regional edge cluster manually. Consider at least one in each zone or data center for high availability. Then, create a new edge cluster by using these edge transport nodes, and create your regional Tier-0 in this cluster. You can select which data center (or edge node) is your preferred Tier-0 path in the regional cluster. You can separate routing tables at this level by using VRF lite capability in the Tier-0 Gateway. Refer to VMware documentation for more details.
7. Manually create an overlay transit segment and create uplinks in Tier-0 gateways into the transit segment. Establish dynamic routing between the Tier-0 gateways. BGP is the preferred routing protocol. If you use VRF lite capability in the Tier-0 Gateway, you can use multiple transit segments, depending on your design.
8. Then, create your Tier-1 gateways in the regional edge cluster. You can select which data center (or edge node) is your preferred Tier-1 path in the regional cluster. You can separate routing tables at this level and decide which routes as advertised to the north bound Tier-0. As in the other multitenant patterns, you can use NAT is this case as well.
9. You can attach your segments into this level of Tier-1 gateways. You can create multiple segments and advertise them through Tier-1 gateway to north bound Tier-0 gateways.

This network topology example doesn't consider the management and control plane (vCenter and NSX Managers). The control plane high availability is discussed in another availability pattern. 
{: note}

Tier-0 gateways support VRF lite, which can be used if needed to support more complex topologies for isolating routing tables also at Tier-0 level. Refer to VMware documentation for more details on capabilities and limitations. 
{: note}

The main reason that you need two layers is for physical north-south connectivity in the data centers. Each data center must have their own private and public VLANs and IP addresses for the uplinks. These IP addresses cannot move between the data centers. Therefore, it requires your attention for routing and network address translation if you use public connectivity in this topology.
{: important}

## Considerations for selecting an overlay network topology
{: #v2t-example-overlays-considerations}

VMware NSX-T provides many ways to build the network topologies, and the default network topology is useful for many use cases. You can typically start with this, and expand it as your needs grow. When the initial deployment is done, {{site.data.keyword.cloud_notm}} automation doesn't use the workload overlay topology and you can change the example topology based on your needs. When you change the configuration, the default uplinks provide you the basic-routed connectivity to {{site.data.keyword.cloud_notm}} private and public networks. If you change the IP addresses or routing, your overlay workloads might lose connectivity to them.  

{{site.data.keyword.cloud_notm}} offers a flexible way to build the NSX-T topology that you need. When you design your own overlay network solution, it is important to know that you might deploy new NSX-T edge nodes and new NSX-T edge clusters manually. Or using Ansible and Terraform to attend your needs. You can do this by following VMware documentation and design guidelines post the initial deployment.

Most of the content in the VMware NSX-T Design Guides and documentation can be applied on {{site.data.keyword.cloud_notm}}. Special attention is needed when you consider, for example, the number of required VLANs and the use of stretched VLAN in the underlay between data centers in multizone region. Also, {{site.data.keyword.cloud_notm}} private network must not be considered as Top of the Rack (ToR) switch. Backend Customer Router (BCR) doesn't provide dynamic routing support (BGP) by default.
{: note}

## Related links
{: #v2t-example-overlays-links}

* [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}
* [NSX-T reference design guide 3-0](https://nsx.techzone.vmware.com/resource/nsx-t-reference-design-guide-3-0){: external}
* [NSX-T multi-location design guide (federation + multisite)](https://communities.vmware.com/t5/VMware-NSX-Documents/NSX-T-Multi-Location-Design-Guide-Federation-Multisite/ta-p/2810327){: external}
