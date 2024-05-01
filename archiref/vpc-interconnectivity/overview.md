---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Interconnectivity overview
{: #interconnectivity-overview}

Interconnectivity consists of multiple services and offerings that enable customers to connect from their remote network locations to {{site.data.keyword.cloud}} deployments and between workloads and services that run in {{site.data.keyword.cloud_notm}}.

It can be divided into the following categories:
- Interconnecting with on-premises networks
- Interconnecting VPCs and {{site.data.keyword.cloud_notm}} services

The following diagram shows an overview of the interconnectivity solutions.

![Interconnectivity solutions with VMware on VPC](../../images/vpc-vcf-diagrams-xcon-vmw-arch.svg "Interconnectivity solutions with VMware on VPC"){: caption="Figure 1. Interconnectivity solutions with VMware® on VPC" caption-side="bottom"}

## Interconnecting VMware workloads with on-premises networks
{: #interconnectivity-onprem}

Interconnecting VMware workloads on VPC with on-premises networks provides the capability to know how to interconnect workloads with on-premises network.

The solution consists of the following key offerings:

- {{site.data.keyword.dl_full_notm}} offerings provide low-latency, high-throughput connections between {{site.data.keyword.vpc_short}} networks directly to a service provider-managed WAN, or a client-managed cloud backbone, or through a supported service provider.
- {{site.data.keyword.cloud_notm}} {{site.data.keyword.vpn_vpc_short}} can securely connect your virtual private cloud to another private network. This service offers two types of VPNs, such as Site-to-site gateways that connect your on-premises network to the {{site.data.keyword.vpc_short}} network and Client-to-site servers that allows clients to connect to VPN servers on the internet.

See the following sections for more detailed overview for these offerings for on-premises connectivity, and architectural considerations when used with VMware workloads on VPC.

## Interconnecting VMware workloads with VPCs and {{site.data.keyword.cloud_notm}} services
{: #interconnectivity-incloud}

Interconnecting workloads with VPCs and {{site.data.keyword.cloud_notm}} services provides the capability to know how to interconnect VMware workloads that are running on a VPC with other workloads on other VPCs and {{site.data.keyword.cloud_notm}} services.

The solution consists of the following key offerings:

- {{site.data.keyword.tg_full_notm}} provisions and defines connections between resources on the {{site.data.keyword.cloud_notm}} network, providing private interconnectivity between {{site.data.keyword.cloud_notm}} data centers worldwide. You can connect {{site.data.keyword.vpc_short}}, {{site.data.keyword.cloud_notm}} classic infrastructure, and networks advertised over GRE tunnels on {{site.data.keyword.cloud_notm}} classic infrastructure. You can also attach {{site.data.keyword.dl_full_notm}} to your {{site.data.keyword.tg_full_notm}}.
- With {{site.data.keyword.vpe_full}}, you can connect to supported {{site.data.keyword.cloud_notm}} services from your VPC network. To connect, you must use the IP addresses that you choose and that are allocated from a subnet within your VPC. You can use VPEs with your VMware workloads that run on VPC.

When you use the previous services, the data remains within the private {{site.data.keyword.cloud_notm}} backbone and is optimized for performance.

## Related links
{: #interconnectivity-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
