---

copyright:

  years:  2022, 2023

lastupdated: "2023-09-20"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture overview of roll-your-own VMware solution on VPC
{: #vpc-ryo-arch-overview}

An architecture overview of the roll-your-own VMware® solution in {{site.data.keyword.vpc_full}} is presented in the following diagram. The architecture uses the new {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}}. This fast provisioning {{site.data.keyword.cloud_notm}} bare metal server provides you compute capacity to host VMware clusters in the {{site.data.keyword.vpc_short}}. Through the integration with the VPC platform, you can take full advantage of the network, storage, and security capabilities provided by the VPC.

![Architecture overview of VMware on {{site.data.keyword.vpc_short}}](../../images/vpc-ryo-diagrams-aod-non-nsx-based.svg "The solution uses Virtual Private Cloud compute, network, and storage resources to be used for hosting VMware workloads."){: caption="Figure 1. Architecture overview of VMware on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

You can also use VMware software-defined networking for your workloads and NSX-T™. If you use NSX-T with your solution, then you need extra subnets, such as TEP traffic and NSX-T uplinks. NSX-T Tier-0 Logical Router uplinks are separated to private and public networks. You can use {{site.data.keyword.vpc_short}} provided public IP addresses on the NSX-T solution, which is routed without network address conversion that is done by {{site.data.keyword.vpc_short}}.

![Architecture overview of VMware with NSX-T on {{site.data.keyword.vpc_short}}](../../images/vpc-ryo-diagrams-aod-nsx-t-based.svg "The solution uses Virtual Private Cloud compute, network, storage resources, and VMware NSX-T for hosting VMware workloads."){: caption="Figure 2. Architecture overview of VMware with NSX-T on {{site.data.keyword.vpc_short}}" caption-side="bottom"}

These two architectures serve as the baseline designs for deploying VMware on {{site.data.keyword.vpc_short}}. The deployment architectures provide the foundation for the roll-your-own VMware solution in VPC.

You can alter and customize the architecture to meet your design goals within the limits of {{site.data.keyword.vpc_short}}, {{site.data.keyword.cloud_notm}} bare metal server for {{site.data.keyword.vpc_short}} and VMware capabilities.
{: note}

## Related links
{: #vpc-ryo-arch-overview-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on Bare Metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
