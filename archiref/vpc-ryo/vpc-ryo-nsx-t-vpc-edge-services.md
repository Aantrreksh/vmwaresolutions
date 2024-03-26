---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Network services provided by Tier-0 and Tier-1 logical routers
{: #vpc-ryo-nsx-t-vpc-edge-services}

NSX-T™ Data Center supports network services such as IPsec Virtual Private Network (IPsec VPN), Network Address Translation (NAT) and Firewalls as shown in the following diagram.

![Network Services provided by Tier-0 and Tier-1 Logical Routers](../../images/vpc-ryo-diagrams-nsx-t-edge-services.svg "Network Services provided by Tier-0 and Tier-1 Logical Routers"){: caption="Figure 1. Network Services provided by Tier-0 and Tier-1 Logical Routers" caption-side="bottom"}

The topic provides a brief introduction to these capabilities and how they can be used in {{site.data.keyword.vpc_full}}.

## VPN services
{: #vpc-ryo-nsx-t-vpc-edge-services-vpn}

IPsec Virtual Private Network (IPsec VPN) and Layer 2 VPN (L2 VPN) run on an NSX Edge node. IPsec VPN offers site-to-site connectivity between an NSX Edge node and remote sites. With L2 VPN, you can extend your data center by enabling virtual machines (VMs) to keep their network connectivity across geographical boundaries while using the same IP address.

When configuring NSX-T VPN service in {{site.data.keyword.vpc_short}}, you can use the public `/32` floating IP addresses as the VPN Endpoints both Tier-0 and Tier-1 Logical Routers. You can have multiple VPN endpoints, if needed. When VPN service is configured on Tier-1 Logical Router, ensure that the floating IP is correctly advertised between Tier-0 and Tier-1 Logical Routers.

For more information about VPN service, see [VMware Documentation](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-A8B113EC-3D53-41A5-919E-78F1A3705F58.html){: external}.

## Network Address Translation
{: #vpc-ryo-nsx-t-vpc-edge-services-nat}

Network Address Translation (NAT) is supported on Tier-0 and Tier-1 Logical Routers.

The following types of NAT are supported.

* **Source NAT (SNAT)** translates a source IP address of outbound packets so that packets are shown as originating from a different network.
* **Destination NAT (DNAT)** translates the destination IP address of inbound packets so that packets are delivered to a target address into another network.

You can also disable SNAT or DNAT for an IP address or a range of addresses. If an address has multiple NAT rules, the rule with the highest priority is applied.

When configuring NSX-T NAT in {{site.data.keyword.vpc_short}}, you can use the public `/32` floating IP addresses as the public NAT IP addresses in both Tier-0 and Tier-1 Logical Routers. You can have multiple NAT IPs, if needed. When NAT is configured on Tier-1 Logical Router, ensure that the floating IP is correctly advertised between Tier-0 and Tier-1 Logical Routers.

For more information about NAT in NSX-T, see [VMware Documentation](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-7AD2C384-4303-4D6C-A44A-DEF45AA18A92.html){: external}.

## Firewall
{: #vpc-ryo-nsx-t-vpc-edge-services-fw}

You can configure East-West and North-South firewall policies in your NSX-T platform.

Gateway firewall represents rules that are applied to the perimeter firewall for North-South traffic connected to {{site.data.keyword.vpc_short}}. Gateway firewall can be applied to both Tier-0 and Tier-1 Logical Routers.

Distributed firewall monitors all the East-West traffic on your VMs. Grouping of objects simplifies rule management. Groups include different objects that are added both statically and dynamically, and can be used as the source and destination of a firewall rule. They can be configured to contain a combination of virtual machines, IP sets, MAC sets, segment ports, segments, AD user groups, and other groups. Dynamic inclusion of groups can be based on tag, machine name, OS name, or computer name.

For more information about Firewalls in NSX-T, see [VMware Documentation](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-F206A4B8-0F33-482D-8727-E71FE253BBCD.html){: external}.

## Related links
{: #vpc-ryo-nsx-t-vpc-edge-services-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
