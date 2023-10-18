---

copyright:

  years:  2020, 2023

lastupdated: "2023-09-22"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Supported topologies
{: #vrw-nsxt-topologies}

## Single data center base topology
{: #vrw-nsxt-topologies-single}

This topology creates a single gateway cluster, with active-passive Tier-0 and Tier-1.

Active-passive on the Tier0 provides IPsec capability for access through the HA VIP address. Alternatively, Tier-0 can use Border Gateway Protocol (BGP) and peer with a vSRX firewall.

The following diagram shows an example of a customer deployment that uses the standard topology, when the segments are attached to the Tier-1 Gateway. You can add more segments to the existing Tier-1 Gateway or more Tier-1 Gateways on the same NSX-T edge clusters, if needed.

![Single-site single-tenant example topology with Tier-1 Gateway](../../images/arch-pattern-1-zone-t1.svg "Single-site single-tenant example topology that uses both Tier-0 and Tier-1 Gateways"){: caption="Figure 1. Single-site single-tenant example topology with Tier-1 Gateway" caption-side="bottom"}

1. The vCenter Server automation deploys an example single-site topology, which follows the principles that are presented in this model. The deployment includes a single vCenter and three NSX-T managers that are deployed in the cluster on the initial {{site.data.keyword.cloud_notm}} data center location.
2. The vCenter Server automation deploys two edge cluster transport nodes and a single edge cluster for your Tier-0 and Tier-1 Gateways.
3. The Tier-0 Gateway provides north-south routing capabilities and the access to {{site.data.keyword.cloud_notm}} private network is provided through its uplinks.
4. The access to private network is provided through private uplinks, which are attached to a portable subnet on a private primary VLAN on the {{site.data.keyword.cloud_notm}} private network. The routing to {{site.data.keyword.cloud_notm}} services uses these uplinks. The automation provisions the IP addresses to the uplinks from the {{site.data.keyword.cloud_notm}} managed 10/8 address space.
5. If you provision your instance with public interfaces, the access to public network is provided through public uplinks. These uplinks are attached to a portable subnet on a public VLAN on the {{site.data.keyword.cloud_notm}} public network. The routing to internet uses these uplinks, and the public IP addresses to the uplinks are provisioned by the automation.
6. A single Tier-1 Gateway is provisioned by the automation for the workloads. You can use this topology or customize it by provisioning new Tier-1 Gateways.
7. You can expand the default topology by adding new segments to the existing Tier-1 Gateway (or to the new Tier-1 Gateways provisioned by you). The route advertisements between T1 and T0 gateways are fully customizable by you and are done by NSX-T. No routing protocol is required or used between T1 and T0 advertisements.

The following diagram shows an example of a customer deployment that uses the standard topology, when the segments are attached directly to the Tier-0 Gateway. You can add more segments to the Tier-0 Gateway or and delete the Tier-1 Gateway that is deployed by the automation, if needed.

## Related links
{: #vrw-nsxt-topologies-related}

* [{{site.data.keyword.cloud_notm}} compliance programs](https://www.ibm.com/cloud/compliance)
