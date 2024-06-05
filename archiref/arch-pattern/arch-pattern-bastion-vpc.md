---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-03"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for a bastion VPC to manage {{site.data.keyword.vcf-auto}} instance in Classic
{: #arch-pattern-bastion-vpc}

This architecture pattern presents Client VPN based connectivity to a {{site.data.keyword.vcf-auto}} instance provisioned in {{site.data.keyword.cloud}} classic infrastructure. This solution uses a bastion VPC with [client-to-site VPNaaS](/docs/vpc?topic=vpc-vpn-client-to-site-overview&interface=ui) and a connecting [{{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-about), or alternatively using a VPC provisioned with [classic connectivity](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure). [{{site.data.keyword.dns_full_notm}}](/docs/dns-svcs?topic=dns-svcs-getting-started) are used in VPC with a custom resolver.

## Deploying a bastion VPC for managing vCenter Server deployment in Classic
{: #arch-pattern-bastion-vpc-overview}

The following diagram presents an overview for an architecture pattern for deploying bastion VPC to manage vCenter Server deployment in Classic.

![Architecture overview for a bastion VPC with VMware Solutions](../../images/arch-pattern-bastion-vpc.svg "The solution uses Virtual Private Cloud compute, network, storage resources, and VMware NSX for a Bastion host."){: caption="Figure 1. Architecture overview for a bastion VPC with VMware® Solutions" caption-side="bottom"}

This architecture pattern deployment is summarized as follows: 

1. [Create a VPC](/docs/vpc?topic=vpc-creating-vpc-resources-with-cli-and-api&interface=cli) for the Bastion hosts. [Choose a VPC prefix](/docs/vpc?topic=vpc-choosing-ip-ranges-for-your-vpc), which does not overlap with your Classic. For example, the default VPC prefix of the MZR and Zone typically works on this step. Provision a subnet with a size of your preference, for example, /27 or larger.
2. [Provision client-to-site VPNaaS](/docs/vpc?topic=vpc-vpn-client-to-site-overview) for OpenVPN based VPN connectivity. Configure your preferred authentication method for the clients. Use a prefix for your clients, which does not overlap with the rest. You might use SNAT when the VPN clients communicate with your connected resources. Advertise 10.0.0.0/8 to your client, or smaller prefix based on your preference.
3. Use [classic connectivity](/docs/vpc?topic=vpc-setting-up-access-to-classic-infrastructure), or provision a [{{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-about) and add your VPC and Classic as connections to it. This provides routed connectivity between your Bastion VPC, Classic, and connected VPN clients.
4. [Provision a DNS service](/docs/dns-svcs?topic=dns-svcs-getting-started) with a local domain of your choice. For example, `bastion.ibmcloud.local`.
5. [Provision a custom resolver](/docs/dns-svcs?topic=dns-svcs-custom-resolver) to your Bastion VPC subnet. Also, configure it as the [DNS server for your VPN clients](/docs/vpc?topic=vpc-vpn-create-server&interface=ui).
6. [Configure a DNS forwarder](/docs/dns-svcs?topic=dns-svcs-cr-fwd-rules-add&interface=ui) in your custom resolver to point to your {{site.data.keyword.vcf-auto}} instance AD root domain, for example, `vcs-zyx.ibmcloud.local`.
7. If you need, provision Windows® or Linux® Bastion hosts to your Bastion VPC subnet. You might access them through internet by using OpenVPN client.

If you use any IP address range out of the Class A block 10.0.0.0/8 as the VPC prefix, you must add a route to your Classic servers to access the VPC hosted servers. Classic servers have default setting for routes to {{site.data.keyword.cloud_notm}} private network (10.0.0.0/8) and {{site.data.keyword.cloud_notm}} Services networks (166.8.0.0/14 and 161.26.0.0/16) with BCR as a next-hop. If your VPC uses something else, ensure that your Classic assets are routed to it through the BCR.
{: note}

## Considerations
{: #arch-pattern-bastion-vpc-considerations}

When you design or deploy this architecture pattern, consider that you might alternatively use classic Virtual Server Instances for Jump or bastion hosts. Configure the server DNS to point toward vCenter Server Instance Active Directory™ or DNS server, or create entries in the hosts file.

## Related links
{: #arch-pattern-bastion-vpc-links}

* [Getting started with Virtual Private Cloud (VPC)](/docs/vpc?topic=vpc-getting-started)
* [VMware vSphere overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview)
* [Getting started with {{site.data.keyword.tg_full_notm}}](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [VPNs for VPC overview](/docs/vpc?topic=vpc-vpn-overview)
