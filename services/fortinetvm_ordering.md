---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-28"

keywords: FortiGate VA, FortiGate configuration, order FortiGate

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering FortiGate Virtual Appliance
{: #fortinetvm_ordering}

You can include the FortiGate® Virtual Appliance service with a new VMware vCenter Server® instance or add the service to your existing instance.

You can deploy the service on a single-zone (new or existing) or multizone (existing only) instance. For multizone instances, three FortiGate Virtual Appliances are installed, one for each of the three gateway clusters.

## Ordering FortiGate Virtual Appliance for a new instance
{: #fortinetvm_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. FortiGate Virtual Appliance is in the **Security and compliance** category. 
2. Open the category, locate FortiGate Virtual Appliance, and toggle its switch on.
3. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_ordering#fortinetvm_ordering-config), then click **Save**.

You cannot install Juniper® vSRX and FortiGate Virtual Appliance on the same gateway cluster.
{: restriction}

## Ordering FortiGate Virtual Appliance for an existing instance
{: #fortinetvm_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **FortiGate Virtual Appliance** service in the **Security and Compliance** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_ordering#fortinetvm_ordering-config), then click **Save**.

## Ordering FortiGate Virtual Appliance for private instances
{: #fortinetvm_ordering-private}

When you order FortiGate Virtual Appliance for instances that are not configured with public interfaces, you must provide a proxy server to complete the installation. The HTTP proxy server must be configured and available through Virtual Routing and Forwarding (VRF) before the FortiGate Virtual Appliance installation can start.

To ensure continued operation, FortiGate Virtual Appliance must have persistent access to the FortiGate license server through the internet. The virtual appliance can access any of the following hostnames:

* `update.fortiguard.net`
* `service.fortiguard.net`
* `support.fortinet.com`
* `guard.fortinet.com`

## FortiGate Virtual Appliance service configuration
{: #fortinetvm_ordering-config}

When you order the service, provide the following settings.

### Name
{: #fortinetvm_ordering-config-name}

Enter the service name.

### FortiGuard network connection
{: #fortinetvm_ordering-config-network-connect}

Select **Public network** or **Private network** for FortiGuard. If the target cluster is configured with private-only network interfaces or the deployment is for a multizone instance, only the **Private network** option is available. This selection determines how FortiGuard contacts the Fortinet license server to activate the license and to download security fixes, and it doesn't impact the workload data plane.

If you select **Private network**, specify the following settings:
* **Proxy IP address** - The IPv4 address of the proxy server.
* **Proxy port number** - The port number of the proxy server, usually 8080 or 3128.
* **Proxy user name** - If you require proxy authentication, enter the username of the proxy server.
* **Proxy password** - If you require proxy authentication, enter the password of the proxy server.

### Deployment size
{: #fortinetvm_ordering-config-size}

{{site.data.keyword.cloud}} provides the following deployment size options. For deployment on a multizone instance, only FortiGate-VM16 and FortiGate-VM32 are available.
* FortiGate-VM02 (2 vCPUs)
* FortiGate-VM04 (4 vCPUs)
* FortiGate-VM08 (8 vCPUs)
* FortiGate-VM16 (16 vCPUs)
* FortiGate-VM32 (32 vCPUs)
   The FortiGate-VM32 deployment size requires Cascade Lake 5218 or higher.

### Monthly subscription license model
{: #fortinetvm_ordering-config-license}

The monthly subscription license model for FortiGate Virtual Appliance offers the following options:
* **Standard FW** - This bundle includes the following.
   * Stateful packet inspection
   * VLAN protection and advanced logging
   * Ingress and egress FW rules
   * SSL/IPsec VPN termination
   * Continuous support
* **Standard FW + UTM** - This bundle includes all standard firewall services in addition to the Advanced Malware Protection (AMP) service.
   * Advanced malware protection
   * NGFW IPS and web filtering
   * Antispam
   * Application control
* **Standard FW + Enterprise** This bundle includes all standard firewall and UTM services in addition to the following services:
    * CASB (Cloud Access Security Broker) - This service provides visibility, compliance, data security, and threat protection for cloud-based services.
    * Industrial security - This service provides signatures for common ICS/SCADA protocols.
    * Security rating - This service provides audit capabilities to identify critical vulnerabilities and configuration weaknesses and implement best practice recommendations.

You can't change the monthly subscription license model after service installation. To change the monthly subscription license model, you must delete the existing service and reinstall the service by selecting a different license option.
{: important}

## Related links
{: #fortinetvm_ordering-related}

* [FortiGate Virtual Appliance overview](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations)
* [Managing FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-managingfortinetvm)
* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Fortinet website](https://www.fortinet.com/){: external}
* [Fortinet Document Library](https://docs.fortinet.com/product/fortigate/6.2){: external}
