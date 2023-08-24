---

copyright:

  years:  2022, 2023

lastupdated: "2023-07-17"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture patterns for deploying a third-party router on a vCenter Server with NSX-T instance
{: #arch-pattern-3rd-party-router}

On [VMware vCenter Server®](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) instance in
{{site.data.keyword.cloud}} classic infrastructure, your workloads are deployed and run on VMware NSX-T™ overlay networks. As part of the deployment, the automation deploys an example NSX-T topology. You can use the provisioned examples as your base or build your own topologies on overlay. These overlay networks are not automatically advertised to {{site.data.keyword.cloud_notm}} classic infrastructure network.

vCenter Server instance is deployed at {{site.data.keyword.cloud_notm}} classic infrastructure. By default, two {{site.data.keyword.cloud_notm}} private VLANs and one {{site.data.keyword.cloud_notm}} public VLAN (optional) are deployed. In addition to the VLANs, NSX-T T0 Gateway is deployed on them with two interfaces, to private and to public (optional). If you opt for a public, the public uplink interface is attached to your public VLAN and has direct internet access. Your T0's private interface is attached to the private VLAN and it is using {{site.data.keyword.cloud_notm}} portable private IP.

The architecture patterns give an introduction to connectivity patterns to integrate a third-party router, firewall, or other network device. They run as a virtual appliance on VMware with the standard NSX-T based vCenter Server instance. 

## Deploying third-party router in gateway cluster
{: #arch-pattern-3rd-party-router-edge-gateway-cluster}

When you deploy a vCenter Server instance in your {{site.data.keyword.cloud_notm}} classic infrastructure, you might optionally deploy a gateway cluster. This cluster can host a third-party router or firewall. You are able to control which VLANs are routed through the router or firewall running on it.

The gateway cluster must not be mixed with NSX-T edge cluster, which consists of NSX-T edge transport nodes. The gateway cluster provides compute capacity for third-party router or firewalls, and VLAN routing can be controlled by the [gateway appliance configuration](/docs/gateway-appliance?topic=gateway-appliance-managing-vlans-and-gateway-appliances) in {{site.data.keyword.cloud_notm}} classic network.
{: important} 

![Deploying third-party router in third-party router or firewall in gateway cluster](../../images/arch-pattern-nsx-t-edge-services-cluster.svg "Deploying third-party router in third-party router or firewall in gateway cluster."){: caption="Figure 1. Deploying third-party router in third-party router or firewall in gateway cluster" caption-side="bottom"}

This architecture pattern deployment is summarized as follows: 

1. You can optionally deploy a gateway cluster to host your own routing or firewall device. This cluster is attached to both {{site.data.keyword.cloud_notm}} private and public networks through transit networks.
2. The third-party device can route assigned VLANs through it. You can choose the VLANs to be routed through it on {{site.data.keyword.cloud_notm}} portal. You must configure the required VLAN interfaces and IP addresses to the devices as well as firewall zones, rules, and policies.
3. If you route your management VLAN through the firewall, you can also secure your management workloads, such as vCenter and NSX-T managers. Ensure that you allow the traffic for your management.
4. Your workload T0 is attached to {{site.data.keyword.cloud_notm}} private network. If you route this VLAN through the firewall, add the required rules on both the firewall and T0.
5. Your workload T0 is attached to {{site.data.keyword.cloud_notm}} public network. If you route this VLAN through the firewall, add the required rules on both the firewall and T0.
6. Alter the automation deployed routes if you need to customize the routing behavior, or establish dynamic routing between your T0 and the third-party device.

## Deploying third-party router or firewall in converged or management clusters
{: #arch-pattern-3rd-party-router-fw-conv-mng-cluster}

When you deploy a vCenter Server instance in your {{site.data.keyword.cloud_notm}} classic infrastructure, you might optionally deploy a Juniper vSRX or host a third-party router or firewall on the converged or management clusters. You can integrate the firewall with your overlay topology in multiple ways, by using the VLAN or NSX-T overlay, if your firewall supports this.

In this pattern, you are not able to control which VLANs are routed through the router or firewall running on the firewall.
{: important}

![Deploying third-party router or firewall in converged or management clusters](../../images/arch-pattern-nsx-t-3rd-party.svg "Deploying third-party router or firewall in converged or management clusters."){: caption="Figure 2. Deploying third-party router or firewall in converged or management clusters" caption-side="bottom"}

This architecture pattern deployment is summarized as follows: 

1. Depending on the network preference selection, your vCenter Server instance is deployed with both public and private connectivity or private connectivity only.
2. You can optionally deploy a gateway cluster to host Juniper vSRX or your own routing or firewall device. In this case, you might put public and private VLANs behind the firewall.
3. You can deploy third-party network devices into vCenter Server clusters by bringing in your own license and following the hardware and software guidance as provided by the specific third-party vendor. Discuss the technical details with the vendor.
4. You can integrate the third-party network device or a router into using service insertion. With service insertion, you can apply third-party services to north-south traffic as well as east-west traffic that passes through a router. The services typically provide advanced security features, such as an intrusion detection system (IDS) or an intrusion prevention system (IPS).
5. When you use service insertion and after, deploy a service instance, you can configure the type of traffic that the router redirects to the service. Configuring traffic redirection is similar to configuring a firewall.
6. Alternatively, you can add the device into north-south traffic path and customize the NSX-T customer topology. Contact your third-party vendor to discuss the wanted network topology, for example, router mode versus transparent.

The following diagram presents the routing topology and routing for this pattern. 

![Network topology with third-party router or firewall in converged or management clusters](../../images/arch-pattern-nsx-t-3rd-party-topo.svg "Network topology with third-party router or firewall in converged or management clusters."){: caption="Figure 3. Network topology with third-party router or firewall in converged or management clusters" caption-side="bottom"}

This architecture pattern deployment is summarized as follows: 

1. You can deploy third-party network devices into vCenter Server clusters by bringing in your own license and following the hardware and software guidance as provided by the specific third-party vendor. Discuss the technical details with the vendor.
2. You can attach the private interface of the appliance into the {{site.data.keyword.cloud_notm}} private network by using the {{site.data.keyword.cloud_notm}} private VLAN. You can use {{site.data.keyword.cloud_notm}} private portable IP addresses for the appliance.
3. You can attach the public interface of the appliance into the {{site.data.keyword.cloud_notm}} public network. You can use {{site.data.keyword.cloud_notm}} public portable IP addresses for the appliance.
4. You can remove or disable the public uplinks on T0. If you do, remove the default route as well.
5. Create an NSX-T overlay segment for a transit network between the T0 and the third-party device. Add T0 uplink and an interface in the third-party device and establish static or dynamic routing between them.
6. Add the default, {{site.data.keyword.cloud_notm}} private network, and {{site.data.keyword.cloud_notm}} services networks into the device routing definitions based on your communications needs. 
7. If needed, you might reassign more IPs from the public portable subnet or order new public static subnets for your overlay. With public static subnets, order them with a next of a VIP of the third-party device to cater for failure situations.

## Considerations
{: #arch-pattern-3rd-party-router-considerations}

When you design or deploy this architecture pattern, consider the following steps: 

* Refer to the specific third-party vendor HW and SW specifications for interoperability with VMware ESXi™ and NSX-T.
* This approach supports BYOL only for the third-party solution licensing. Contact your vendor for licensing details. 

## Related links
{: #arch-pattern-3rd-party-router-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [About {{site.data.keyword.cloud_notm}} Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-about)
