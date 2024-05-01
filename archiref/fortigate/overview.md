---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-26"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Fortinet FortiGate VM overview
{: #fortigate-overview}

{{site.data.keyword.vmwaresolutions_full}} offers various solutions to meet your network security requirements. The base offering includes VMware NSX–T™ for integrated virtual networking and security. More network security features are available with the FortiGate® VM offering, which provides Fortinet®’s next–generation firewall (NGFW) capabilities in the form of a highly available pair of virtual FortiGate appliances. In addition to the architecture for FortiGate virtual machine (VM), {{site.data.keyword.cloud}} also offers a [FortiGate Security Appliance](/docs/fortigate-10g) offering, which provides a perimeter firewall, NAT, and VPN services in the form of a physical appliance.

The solution is considered to be an extra component and extension of the VMware vCenter Server® offering on {{site.data.keyword.cloud_notm}}. As a result, this document doesn’t cover the existing configuration of the foundation solutions on {{site.data.keyword.cloud_notm}}. For more information about the foundation solution architecture, see [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview).

## Topologies
{: #fortigate-overview-topologies}

You can deploy FortiGate VM according to several different strategies:

* FortiGate VM can be deployed as part of an ESXi™ gateway cluster that is directly integrated with the {{site.data.keyword.cloud_notm}} customer routers. It provides firewall and gateway functions for your private and public {{site.data.keyword.cloud_notm}} network VLANs.
* FortiGate VM can be deployed to your management and workload cluster. In this form, you can use FortiGate to provide firewall and gateway services between various networks. FortiGate VM provides controlled connectivity between:
   * Public and private networks
   * Private VLANs and NSX logical switches
   * Several VMware NSX® logical switches

Additionally, FortiGate VM offers direct integration with NSX–T including service chaining and dynamic import of security groups.

## Key benefits
{: #fortigate-overview-benefits}

Several licensing option bundles are available for FortiGate VM on {{site.data.keyword.cloud_notm}}.

* **Standard FW** - This bundle includes the following services.
   * Stateful packet inspection
   * VLAN protection and advanced logging
   * Ingress or egress FW rules
   * SSL or IPsec VPN termination
   * Continuous support
* **Standard FW + UTM** - This bundle includes all standard firewall services in addition to the Advanced Malware Protection (AMP) service.
   * Advanced malware protection
   * NGFW IPS and web filtering
   * Antispam
   * Application control
* **Standard FW + Enterprise** This bundle includes all standard firewall and UTM services in addition to the following services.
    * CASB (Cloud Access Security Broker) - This service provides visibility, compliance, data security, and threat protection for cloud-based services.
    * Industrial security - This service provides signatures for common ICS/SCADA protocols.
    * Security rating - This service provides audit capabilities to identify critical vulnerabilities and configuration weaknesses and implement best practice recommendations.

## Related links
{: #fortigate-overview-related}

* [Solution design](/docs/vmwaresolutions?topic=vmwaresolutions-fortigate-design)
* [Implementation and management](/docs/vmwaresolutions?topic=vmwaresolutions-fortigate-implementation)
