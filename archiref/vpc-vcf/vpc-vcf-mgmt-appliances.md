---

copyright:

  years:  2022, 2023

lastupdated: "2023-08-25"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Networking for VMware Cloud Foundation appliances
{: #vpc-vcf-mgmt-appliances}

The topic provides an overview of networking deployment for VMware Cloud Foundation™ appliances in {{site.data.keyword.vpc_short}} and inside the NSX deployment of the VMware Cloud Foundation instance.

## VLAN interfaces for Cloud Builder, SDDC manager, and VMware vCenter Server on VPC subnet
{: #vpc-vcf-mgmt-appliances-vlan-nics}

The VMware® Cloud Builder appliance automates the deployment of the entire software-defined stack. VMware Cloud Builder is a virtual appliance that is used to deploy and configure the first cluster of the management domain and transfer inventory and control to SDDC manager. During the deployment process, the VMware Cloud Builder appliance validates network information that you provide in the deployment parameter workbook, such as DNS, network (VLANS, IP addresses, MTUs), and credentials. The VMware Cloud Builder appliance must have network access to all hosts on the management network.

VMware vSphere uses virtualization to transform individual data centers into aggregated computing infrastructures that include CPU, storage, and networking resources. VMware vCenter Server® manages these infrastructures as a unified operating environment and provides you with the tools to administer the data centers that participate in that environment.

SDDC manager automates the entire system lifecycle, that is, from configuration and provisioning to upgrades and patching, which includes host firmware and simplifies day-to-day management and operations.

The following table summarizes the required VLAN interfaces in {{site.data.keyword.vpc_short}} for these appliances.

| Interface name | Interface type | VLAN ID | Subnet | Allow float | VCF appliance | Distributed port group name |
| ---------------|----------------|---------|--------|-------------|---------------|---------------------------- |
| `vlan-nic-cloud-builder` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | Cloud Builder | `pg-mgmt` |
| `vlan-nic-vcenter` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | vCenter Server | `pg-mgmt` |
| `vlan-nic-sddc-manager` | `vlan` | 1611 | `vpc-mgmt-subnet` | `true` | SDDC Manager | `pg-mgmt` |
{: caption="Table 1. VLAN interfaces for VMware Cloud Foundation appliances" caption-side="bottom"}

## Overlay subnets for Aria Lifecycle
{: #vpc-vcf-mgmt-appliances-overlay}

Aria Suite Lifecycle (vRealize Suite Lifecycle Manager) is deployed at the NSX overlay. Two segments (`avn-local-network` and `avn-x-region-network`) are created in the management domain behind the management Tier-0 gateway on AVN segment. The automation configures and provisions the required routing so that the Aria Suite Lifecycle appliance can communicate with other VMware Cloud Foundation assets in VPC subnets and access Internet (egress only) to download the required deployment and update files for other Aria products from VMware public repositories. Internet access is provided through SNAT configured on the Tier-0 gateway. A VPC floating IP address is provisioned and configured in Tier-0 gateway for this purpose.  

## Related links
{: #vpc-vcf-mgmt-appliances-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} bare metal servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
* [VMware on bare metal VPC tutorial](/docs/solution-tutorials?topic=solution-tutorials-vpc-bm-vmware)
