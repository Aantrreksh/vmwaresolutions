---

copyright:

  years:  2024

lastupdated: "2024-04-20"

keywords: vmware cloud foundation, configure firewall, firewall config, vcf for vpc

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the NSX firewalls for {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-firewall}

Before you configure the VMware NSX firewalls, review the information in [NSX firewall add-ons](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-add-ons#vmware-add-ons-nsx-firewall).

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-vpc-short}}** from the left navigation pane.
2. In the instances table, click the instance to configure the firewalls for.
3. On the **Access Information** tab, under **Management domain**, use the NSX-T admin account for VMware NSX-T Data Center to log in to the VMware NSX-T console.
   * To configure the gateway firewall, see [Gateway Firewall](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-A52E1A6F-F27D-41D9-9493-E3A75EC35481.html){: external}.
   * To configure the distributed firewall, see [Distributed Firewall](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-6AB240DB-949C-4E95-A9A7-4AC6EF5E3036.html){: external}.

{{site.data.keyword.cloud}} Security Groups for VPC (Virtual Private Cloud) also provide network security and act as a virtual firewall for your Virtual Server Instances and Bare Metal Servers in the {{site.data.keyword.cloud_notm}} VPC environment by managing east-west and north-south network traffic.

Security Groups for VPC provides a convenient way to define and apply rules that establish filtering to a target of a resource, based on protocols, ports, and IP addresses. For more information, see [About security groups](/docs/vpc?topic=vpc-using-security-groups).

## Related links
{: #vpc-vcf-firewall-links}

* [NSX firewall add-ons](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-add-ons&interface=ui#vmware-add-ons-nsx-firewall)
