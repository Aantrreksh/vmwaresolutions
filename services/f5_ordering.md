---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-06"

keywords: F5 license activation, F5 configuration, order F5

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering F5 BIG-IP
{: #f5_ordering}

You can include the F5 BIG-IP® service with a new vCenter Server® instance or add the service to your existing instance.

## Ordering F5 BIG-IP for new instances
{: #f5_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. F5 BIG-IP is in the **Security and compliance** category. 
2. Open the category, locate F5 BIG-IP, and toggle its switch on.
3. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-f5_ordering#f5_ordering-config), then click **Save**.

## Ordering F5 BIG-IP for existing instances
{: #f5_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **F5 BIG-IP** service in the **Security and Compliance** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-f5_ordering#f5_ordering-config), then click **Save**.

## Ordering F5 BIG-IP for private instances
{: #f5_ordering-private}

When you order F5 BIG-IP for instances that are not configured with public interfaces, you must provide a proxy server to complete the installation. The HTTP proxy server must be configured and available by using Virtual Routing and Forwarding (VRF) before the F5 BIG-IP installation can begin.

The BigIP Virtual Edition (VE) endpoints must be able to activate their license before they can become operational. After the BigIP VE endpoints are installed, they no longer require the use of the proxy server.

The F5 BIG-IP service cannot be added without a working proxy server at the time of service installation.
{: important}

## F5 BIG-IP service configuration
{: #f5_ordering-config}

When you order the service, provide the following settings.

### Name
{: #f5_ordering-config-name}

Enter the service name.

### F5 license activation connection
{: #f5_ordering-config-license}

Select **Public network** or **Private network** for license activation. This selection determines how the F5 virtual servers contact the F5 license server, and it does not impact the workload data plane.

If the target cluster is configured with private-only network interfaces, only the **Private network** option is available. 

If you select **Private network**, specify the following settings:

* **Proxy IP address**: The IPv4 address of the proxy server.
* **Proxy port number**: The port number of the proxy server, usually 8080 or 3128.

Authenticated proxy is not supported.
{: note}

### Maximum bandwidth
{: #f5_ordering-config-bandwidth}

Specify the maximum throughput of the F5 BIG–IP appliance.

### License model
{: #f5_ordering-config-license-model}

The license model for F5 BIG-IP offers the following options:
* **Good** - This offer uses the BIG-IP Local Traffic Manager™ (LTM) VE, operating as a full-proxy architecture, which provides:
   * Intelligent local traffic management
   * Complete SSL traffic visibility
   * Analytics and health monitoring to ensure that application servers are always available to your users.
* **Better** - This offer is built on the benefits of the **Good** option, with the addition of BIG-IP DNS™, BIG-IP Advanced Firewall Manager™ (AFM), and BIG-IP Application Acceleration Manager™ (AAM) modules. It delivers global traffic management services, application performance optimization, and advanced network firewall and Distributed Denial of Service (DDoS) mitigation capabilities.
* **Best** - In addition to the **Good** and **Better** offers, BIG-IP Application Security Manager™ (ASM) provides:
   * Comprehensive application protection against L7 DDoS
   * Open Web Application Security Project (OWASP) top 10 threats
   * Common application vulnerabilities

BIG-IP Access Policy Manager™ (APM) offers users secure, simplified access to applications located anywhere within a multicloud environment, incorporating features such as SSO (Single Sign-On) and MFA (Multifactor Authentication).

You cannot change the license model after service installation. To change the license model, you must delete the existing service and reinstall the service by choosing a different license model.
{: important}

## Related links
{: #f5_ordering-related}

* [F5 BIG-IP overview](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)
* [Managing F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-managing_f5)
* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [F5 Deployment Guides](https://www.f5.com/services/resources/deployment-guides){: external}
