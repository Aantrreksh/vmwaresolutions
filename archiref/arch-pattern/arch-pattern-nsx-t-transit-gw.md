---

copyright:

  years:  2022, 2024

lastupdated: "2024-01-30"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for using Transit Gateway with a vCenter Server with NSX-T instance
{: #arch-pattern-nsx-t-transit-gw}

This architecture pattern presents hybrid cloud connectivity by using [{{site.data.keyword.tg_full}}](/docs/transit-gateway?topic=transit-gateway-about). This solution is applicable for NSX-T based vCenter Server instance, which is provisioned in {{site.data.keyword.cloud_notm}} classic infrastructure. This pattern requires a [gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-about) or [gateway cluster](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters#vc_orderinginstance-addl-clusters-gate) with Juniper vSRX or other third-party device, which supports GRE. In this solution, GRE tunnel is established between this device and Transit GW Router in a specific Zone. NSX-T T0 advertises routes through vSRX (or other device) to Transit Gateway.

## Deploying Transit Gateway with vCenter Server and NSX-T
{: #arch-pattern-nsx-t-transit-gw-overview}

The following diagram presents an overview for an architecture pattern for deploying Transit Gateway with vCenter Server and NSX-T.

![Transit Gateway with vCenter Server and NSX-T](../../images/arch-pattern-vcs-nsx-t-transit-gw.svg "Transit Gateway with vCenter Server and NSX-T."){: caption="Figure 1. Transit Gateway with vCenter Server and NSX-T" caption-side="bottom"}

The following list summarizes the architecture pattern deployment:

1. vCenter Server instance is deployed at {{site.data.keyword.cloud_notm}} Classic Infrastructure. Two {{site.data.keyword.cloud_notm}} private VLANs and one {{site.data.keyword.cloud_notm}} Public VLAN (optional) is deployed. Each of them hosts multiple subnets. You can see the details through {{site.data.keyword.vmwaresolutions_short}} portal.
2. NSX-T T0 is deployed with two interfaces - private and public (optional). If you opt for a public, this interface is attached to your Public VLAN and has direct internet access. Your T0 private interface is attached to the Private VLAN and it is using {{site.data.keyword.cloud_notm}} Portable Private IP.
3. vSRX (or other device) running on the gateway cluster or gateway appliance is deployed to your Classic Infrastructure. Configure your vCenter Server instance private primary VLAN to be routed through the vSRX or Gateway Appliance. Also, establish routing between your NSX-T T0 and vSRX, such as BGP.
4. Order an {{site.data.keyword.tg_full_notm}} at your {{site.data.keyword.cloud_notm}} data center or zone location and [add your classic network as a connection](/docs/transit-gateway?topic=transit-gateway-adding-connections).
5. [Create a GRE connection on your transit gateway](/docs/transit-gateway?topic=transit-gateway-gre-connection&interface=ui) by using your classic network as the transport for your GRE tunnel. For the remote gateway IP, select your vSRX or gateway appliance private IP. For the Local gateway IP, you can select an IP address to be advertised through your Classic Network to the vSRX or Gateway Appliance. Ensure that your vSRX or Gateway Appliance has a route to this IP. For Local or Remote tunnel IP, you can select the IP addresses for the GRE tunnel IP addresses.
6. Your vSRX or Edge Gateway Appliance and Transit Gateway must exchange routes through BGP. TGW can choose a BGP ASN for your NSX-T networks, or you can enter your own ASN when you create the GRE connection in TGW. You must configure your T0 to advertise your preferred NSX-T overlay networks to the Transit Gateway. Ensure that you do not advertise routes that collide with your Classic Private Subnets. Also, ensure that you advertise the networks learned from your NSX-T T0 to the Transit Gateway.
7. [You can add other connections](/docs/transit-gateway?topic=transit-gateway-adding-connections) (VPC or other Classic) to the Transit Gateway. Your VPC IP address allocation design must not overlap with the attached Classic network nor with the NSX-T overlay networks.
8. You can [add {{site.data.keyword.dl_short}} connections to the transit gateway](/docs/transit-gateway?topic=transit-gateway-adding-connections) for on-premises Connectivity. Transit Gateway advertises the attached routes of VPC, classic network, and GRE tunnel to the attached {{site.data.keyword.dl_short}}.

## Considerations
{: #arch-pattern-nsx-t-transit-gw-considerations}

When you design or deploy this architecture pattern, you must consider the following steps:

* {{site.data.keyword.dl_short}} can be attached as a connection to the Transit Gateway.
* Transit gateway GRE tunnels support traffic flows:
   * From GRE to VPC and from VPC to GRE, and
   * From GRE to {{site.data.keyword.dl_short}} and from {{site.data.keyword.dl_short}} to GRE.
* Plan your AS numbering before you order the GRE tunnels to Transit Gateway.
* To speed up recovery in failure situations, you can tune BGP `keepalive` and `hold-time` values at your end of the GRE tunnel. These values are the main mechanisms that the Transit Gateway's BGP uses to ensure that its BGP neighbors are still alive through the GRE tunnel. [Transit gateway router](/docs/transit-gateway) provides its default `keepalive` and `hold-time` values for the BGP session inside the [GRE tunnel](/docs/transit-gateway?topic=transit-gateway-gre-connection&interface=ui), but you can provide smaller timer values on your side of the GRE tunnel.

When a BGP connection is established with the local routing device, a peer sends an open message that contains a `hold-time` value. If the router does not receive successive BGP messages, such as `keepalive` or `update` within the period that is specified in `hold-time` the BGP connection is closed. The BGP `hold-time` is three times the interval at which `keepalive` messages are sent, and `hold-time` is the maximum number of seconds allowed to elapse between successive `keepalive` messages that BGP receives from a peer. BGP on the local routing device uses the smaller of either the local `hold-time` value or the peer’s `hold-time` value as `hold-time` for the BGP connection between the two peers.

Bidirectional Forwarding Detection (BFD) is not supported by Transit gateway's GRE tunnels.
{: note}

In vSRX, the default `hold-time` is 90 seconds, which means that the default frequency for `keepalive` messages is 30 seconds. For more information, see [precision-timers](https://www.juniper.net/documentation/us/en/software/junos/cli-reference/topics/ref/statement/precision-timers-edit-protocols-bgp.html){: external} and [hold-time (Protocols BGP)](https://www.juniper.net/documentation/us/en/software/junos/cli-reference/topics/ref/statement/hold-time-edit-protocols-bgp.html){: external}.
{: note}

## Related links
{: #arch-pattern-nsx-t-transit-gw-links}

* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Getting started with {{site.data.keyword.cloud_notm}} Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-getting-started)
* [Getting started with {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [GRE Configuration Example](https://supportportal.juniper.net/s/article/Junos-GRE-Configuration-Example?language=en_US){: external}
