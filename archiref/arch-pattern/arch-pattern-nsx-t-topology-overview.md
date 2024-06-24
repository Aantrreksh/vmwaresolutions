---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-03"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture patterns for the vCenter Server deployment default connectivity options
{: #arch-pattern-nsx-t-topology-overview}

When you deploy a [{{site.data.keyword.vcf-auto-short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) instance in your {{site.data.keyword.cloud}} classic infrastructure, the deployment consists of a number of network constructs and VMware® management components.

This architecture pattern gives an overview for standard private and public connectivity options for a standard deployment. This pattern also includes an overview for the standard {{site.data.keyword.vcf-auto}}  components, basic cluster types, and customer topologies deployed as part of the {{site.data.keyword.cloud_notm}} automation. 

## VMware vCenter Server components overview
{: #arch-pattern-nsx-t-topology-overview-vcs-comp}

When you deploy a {{site.data.keyword.vcf-auto-short}} instance in your {{site.data.keyword.cloud_notm}} classic infrastructure, the deployment consists of the components that are presented in the following diagram.

![vCenter Server deployment overview](../../images/arch-pattern-vcs-nsx-t-whatu-get.svg "vCenter Server deployment overview"){: caption="Figure 1. vCenter Server deployment overview" caption-side="bottom"}

The following steps summarize a standard deployment.

1. Depending on the network preference selection, your instance is deployed with both public and private connectivity or private connectivity only.
2. Upon your selection, a {{site.data.keyword.vcf-auto-short}} instance can be deployed with various bare metal server hardware options. You can select an initial deployment to include one consolidated cluster or separate management and workload clusters. You can optionally deploy a gateway cluster to host Juniper® vSRX or your own routing or firewall device. The solution can be expanded after the initial deployment by adding more hosts to existing clusters, or by adding new clusters.
3. Your clusters can have multiple datastores. You can use VMware vSAN™ with local SSDs or {{site.data.keyword.filestorage_full_notm}} (NFS), where you can have one or more LUNs with different performance and size characteristics. You can expand the volumes as your needs grow.
4. The automation deploys a vCenter Server appliance on the management or consolidated cluster. Your vCenter Server has an IP address from the {{site.data.keyword.cloud_notm}} classic infrastructure provided `10/8` address space.
5. The automation deploys three VMware NSX™ managers and a cluster is formed which uses NSX virtual IP for High Availability. Your NSX managers have an IP address from the {{site.data.keyword.cloud_notm}} classic infrastructure provided `10/8` address space.
6. The automation deploys an Active Directory for authentication and name resolution. You can select between a single Windows virtual server instance in {{site.data.keyword.cloud_notm}} IaaS hypervisor or two highly available dedicated Windows Server VMs (with bring your own license) on the VMware management cluster.
7. The automation deploys four edge nodes in your deployment and forms two NSX edge clusters - Services edge cluster and Workload edge cluster.
8. The services edge cluster is used to host services Tier 0 Gateway, which provides network connectivity services for your management components.
9. Workload edge cluster hosts workload Tier 0 and Tier 1 Gateways for your workloads. A predefined example overlay network topology with one Tier 1 Gateway is provided by the automation. You can customize it for your own requirements by changing or deleting example segments or by adding new segments.

## VMware vCenter Server clusters
{: #arch-pattern-nsx-t-topology-overview-vcs-clusters}

The vCenter Server deployment might consist of several clusters. The following diagram provides an overview of the key cluster types.

![vCenter Server clusters](../../images/arch-pattern-vcs-nsx-t-edge-services-cluster.svg "vCenter Server clusters"){: caption="Figure 2. vCenter Server clusters" caption-side="bottom"}

This clustering can be summarized as follows: 

1. You can select an initial deployment to include one consolidated cluster or separate management and workload clusters.
2. You can optionally deploy a gateway cluster to host Juniper vSRX or your own routing or firewall device. 
3. You can expand the solution after initial deployment, by adding more hosts to existing clusters, by adding new clusters or by adding NFS storage to your instance.
4. Each cluster might have different bare metal server hardware options and different storage options.
5. The automation deploys four edge nodes in your deployment and forms two NSX edge clusters - Services edge cluster and Workload edge cluster.
6. The services edge cluster is used to host services Tier 0 Gateway, which provides network connectivity services for your management components.
7. Workload edge cluster hosts workload Tier 0 and Tier 1 Gateways for your workloads. A predefined example overlay network topology with one Tier 1 Gateway is provided by automation. You can customize it for your own needs by changing or deleting example segments or by adding new segments.

The gateway cluster must not be mixed with the NSX edge cluster, which consists of VMware NSX™ edge transport nodes. The gateway cluster provides compute capacity for hosting Juniper vSRX, Fortinet FortiGate, or other third-party routers or firewalls. The VLAN routing can be controlled by [gateway appliance configuration](/docs/gateway-appliance?topic=gateway-appliance-managing-vlans-and-gateway-appliances) though {{site.data.keyword.cloud_notm}} Classic portal.
{: important} 

## NSX topology
{: #arch-pattern-nsx-t-topology-overview-overlay}

When you deploy a {{site.data.keyword.vcf-auto-short}} instance in your {{site.data.keyword.cloud_notm}} Classic Infrastructure, you obtain the default network topology as presented in the following diagram.

![NSX default network topology](../../images/arch-pattern-nsx-t-topology.svg "NSX default network topology."){: caption="Figure 3. NSX default network topology" caption-side="bottom"}

The default topology can be summarized as follows: 

1. Depending on the network preference selection, your instance is deployed with both public and private connectivity or private connectivity only.
2. The automation deploys an NSX Tier 0 (T0) Gateway in the NSX workload edge cluster. The T0 gateway is attached to both {{site.data.keyword.cloud_notm}} private and public networks or {{site.data.keyword.cloud_notm}} private network only based on the selection. 
3. The automation deploys an example NSX overlay topology with a Tier 1 (T1) Gateway and a few example overlay segments attached both to the T1 and T0 Gateways. You might customize the topology based on your needs. 
4. There are default firewall rules (deny any) and example SNAT/DNAT rules in the T1 and T0 Gateway Firewalls for private or public connectivity. You must customize them to fit your needs.
5. The deployed T0 gateway has a default route `0.0.0.0/0` to the internet with FCR as a next-hop.
6. The deployed T0 gateway has routes to {{site.data.keyword.cloud_notm}} private network `10.0.0.0/8` and {{site.data.keyword.cloud_notm}} Services networks `166.8.0.0/14` and `161.26.0.0/16` with BCR as a next-hop.
7. {{site.data.keyword.cloud_notm}} Services can be reached through {{site.data.keyword.cloud_notm}} private network by using Cloud Services Endpoints when it uses {{site.data.keyword.cloud_notm}} private network addresses. You need SNAT to access these endpoints.

## Private connectivity
{: #arch-pattern-nsx-t-topology-overview-private}

When you deploy a {{site.data.keyword.vcf-auto-short}} instance in your {{site.data.keyword.cloud_notm}} classic infrastructure, you obtain the default private network topology as presented in the following diagram.

![Access to {{site.data.keyword.cloud_notm}} Private network](../../images/arch-pattern-nsx-t-private-access.svg "Access to {{site.data.keyword.cloud_notm}} Private network"){: caption="Figure 4. Access to {{site.data.keyword.cloud_notm}} Private network" caption-side="bottom"}

Private connectivity pattern is summarized as follows: 

1. The automation deploys an NSX Tier 0 (T0) Gateway in the NSX workload edge cluster. The T0 gateway provides connectivity to {{site.data.keyword.cloud_notm}} private network. 
2. The deployed T0 gateway has a route to {{site.data.keyword.cloud_notm}} private network `10.0.0.0/8` and {{site.data.keyword.cloud_notm}} Services networks `166.8.0.0/14` and `161.26.0.0/16` with BCR as a next-hop.
3. The automation deploys an example NSX overlay topology with a Tier 1 (T1) Gateway and a few example segments attached both to the T1 and T0 Gateways. You can customize the topology based on your needs.
4. {{site.data.keyword.cloud_notm}} Services can be reached through {{site.data.keyword.cloud_notm}} private network by using Cloud Services Endpoints when it uses {{site.data.keyword.cloud_notm}} private network addresses.
5. When you use BYOIP on NSX overlay networks, you must use SNAT at T0 or T1. If you use SNAT at T1, you can advertise the NAT IP addresses from T1 to T0, where proxy arp is used.
6. You can create DNAT rules on T0 Gateway to access your workloads from {{site.data.keyword.cloud_notm}} private networks.
7. You can use IP addresses from {{site.data.keyword.cloud_notm}} private portable subnet that is deployed for NSX Edge Uplinks for the NAT. Alternatively, you can order [{{site.data.keyword.cloud_notm}} Private static subnets](/docs/subnets?topic=subnets-getting-started) that are routed toward your T0's private HA VIP to be used for NAT-ing or on segments.

## Public connectivity
{: #arch-pattern-nsx-t-topology-overview-public}

When you deploy a {{site.data.keyword.vcf-auto-short}} instance in your {{site.data.keyword.cloud_notm}} classic infrastructure, you obtain the default public network topology as presented in the following diagram. 

![Access to {{site.data.keyword.cloud_notm}} Public network](../../images/arch-pattern-nsx-t-public.svg "Access to {{site.data.keyword.cloud_notm}} Public network"){: caption="Figure 5. Access to {{site.data.keyword.cloud_notm}} Public network" caption-side="bottom"}

Public connectivity pattern is summarized as follows: 

1. The automation deploys an NSX Tier 0 (T0) Gateway in the NSX workload edge cluster. The T0 gateway provides connectivity to {{site.data.keyword.cloud_notm}} public network. 
2. The deployed T0 gateway has a default route `0.0.0.0/0` to the internet with FCR as a next-hop.
3. The automation deploys an example NSX overlay topology with a Tier 1 (T1) Gateway and a few example segments attached both to the T1 and T0 Gateways. You can customize the topology based on your needs.
4. You can use IP addresses from {{site.data.keyword.cloud_notm}} private portable subnet that is deployed for NSX Edge Uplinks for NAT or for NSX network services (for example IPSec VPN).
5. The automation deploys example SNAT rules for outbound internet access. You can customize and delete these rules based on your needs. 
6. You can configure DNAT rules to access your workloads that are attached to NSX segments through internet.
7. You can order [{{site.data.keyword.cloud_notm}} Public static subnets](/docs/subnets?topic=subnets-getting-started) for your HA VIP to allocate public subnets directly to NSX segments. They are routed through the T0 public uplink HA VIP.

## Related links
{: #arch-pattern-nsx-t-topology-overview-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [VMware NSX design](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design)
