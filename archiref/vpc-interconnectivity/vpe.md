---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloud_notm}} VPE overview
{: #interconnectivity-vpe}

With {{site.data.keyword.cloud}} {{site.data.keyword.vpe_full}}, you can connect to supported {{site.data.keyword.cloud_notm}} services from your VPC network. You can use IP addresses that you choose, which are allocated from a subnet within your VPC.

VPE is an evolution of the private connectivity to {{site.data.keyword.cloud_notm}} services. VPEs are virtual IP interfaces that are bound to an endpoint gateway created on a per service, or service instance, basis (depending on the service operation model). The endpoint gateway is a virtualized function that scales horizontally. Also, it is redundant and highly available, and spans all availability zones of your VPC. Endpoint gateways enable communications from virtual server instances within your VPC and {{site.data.keyword.cloud_notm}} service on the private backbone. VPE for VPC gives you the experience of controlling all the private addressing within your cloud.

For more information about supported {{site.data.keyword.cloud_notm}} services, see [VPE supported services](/docs/vpc?topic=vpc-vpe-supported-services).

For more information about {{site.data.keyword.cloud_notm}} VPEs, see [Virtual Private Endpoint Gateways in VPC](/docs/vpc?topic=vpc-about-vpe).


## Considerations with roll-your-own VMware solution in VPC
{: #interconnectivity-vpe-ryo-considerations}

VPEs are located in your network address space within the VPC where your VMware® workloads are hosted. When you access {{site.data.keyword.cloud_notm}} services from VMware workloads, you can use VPE for VPCs as the endpoint for the service. Your VMware Workloads can either be attached to the VPC subnet, or to NSX-T™ overlay segments. VPE uses {{site.data.keyword.cloud_notm}} private backbone network to access the specific service, and data remains within the private {{site.data.keyword.cloud_notm}} backbone.

The following diagram presents an overview when using VPEs with VMware workloads on VPC subnets.

![VPEs with VMware Workloads on VPC subnets](../../images/vpc-ryo-diagrams-vpe-sub-arch.svg "VPEs with VMware Workloads on VPC subnets"){: caption="Figure 1. VPEs with VMware Workloads on VPC subnets" caption-side="bottom"}

The following diagram presents an overview when using VPEs with VMware NSX-T.

![VPEs with VMware Workloads with NSX-T](../../images/vpc-ryo-diagrams-vpe-nsx-t-arch.svg "VPEs with VMware Workloads with NSX-T"){: caption="Figure 2. VPEs with VMware Workloads with NSX-T" caption-side="bottom"}

VPE is integrated with {{site.data.keyword.dns_short}}. If your VMware workloads use {{site.data.keyword.dns_full_notm}}, they can resolve your VPE FQDNs to your private IP address instances that are provisioned under {{site.data.keyword.dns_full_notm}}. {{site.data.keyword.cloud_notm}} network can use resource records that are configured through {{site.data.keyword.dns_full_notm}} by querying {{site.data.keyword.dns_short}} resolvers.

Therefore, the first architectural decision you must make is how your VMware Workloads resolve DNS queries. {{site.data.keyword.dns_full_notm}} provide custom resolvers as a service that offers the ability to customize the hostname, which resolves rules for different hostnames. If your VMware workloads are attached to VPC subnet, you can use the DNS server IP addresses as defined in [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints).

The custom resolver feature offers fine-grained control of name resolution and forwarding of DNS Queries to and from on-premises DNS resolvers. You can create a custom resolver to run inside your VPC address space, and in a subnet you define. You can then use this custom resolver for your VMware Workloads on NSX-T overlays. For more information, see [Working with custom resolvers](/docs/dns-svcs?topic=dns-svcs-custom-resolver&interface=ui).

VPE for VPC IP addresses uses a multizone region, logical endpoint gateway to connect to a service endpoint on the {{site.data.keyword.cloud_notm}} private backbone. The endpoint gateway is designed to support the best practice of binding a single IP from each zone of the VPC.

You can create an endpoint gateway with zero IP addresses and bind IP addresses as each zone is brought online. When you create an endpoint gateway, a DNS zone and records are created. The VPE service automatically upgrades your virtual server instances to use the private DNS as the default DNS resolver. For more information about creating VPEs, see [Creating an endpoint gateway](/docs/vpc?topic=vpc-ordering-endpoint-gateway&interface=ui).

As more {{site.data.keyword.cloud_notm}} services are enabled for VPE for VPC, each service instance requires you to configure its endpoint gateway, but it uses the same topologies and best practices. For more information about provisioning and best practice guidelines, see the documentation that is provided by the individual service.

## Related links
{: #interconnectivity-vpe-ryo-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
