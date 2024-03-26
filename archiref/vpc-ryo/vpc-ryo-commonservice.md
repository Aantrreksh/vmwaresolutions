---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Common Services design
{: #vpc-ryo-commonservice}

Common Services provide the services that are used by other services in the Cloud Management platform. The common services of the solution include identity and access services, domain name services, NTP services, and certificate authority services.

![Common services](../../images/vpc-ryo-diagrams-overview-commonservices.svg "Common services"){: caption="Figure 1. Common services" caption-side="bottom"}

## Identity and Access Services
{: #vpc-ryo-commonservice-identity-access}

### vCenter Single Sign-On
{: #vpc-ryo-commonservice-vcenter}

The VMware vCenter Server® includes a built-in identity provider, which is a service that manages identity sources and authenticates principals. Identity Source (Directory Service) stores and manages principals. Principals consist of a collection of attributes about a user or service account such as name, address, email, and group membership. The internal (local) LDAP repository in vCenter Server contains user identities, groups, and configuration data.

### Microsoft Active Directory
{: #vpc-ryo-commonservice-msad}

Starting with VMware vSphere® 7.0, you can configure vCenter Server for an external identity provider by using federated authentication. In such a configuration, you replace vCenter Server as the identity provider, and Active Directory™ Federation Services (AD FS) can be used as the external identity provider. In this configuration, AD FS interacts with the identity sources on behalf of vCenter Server.

In this design, customers can use their own Microsoft® Active Directory (MS AD) for Identity Management for the vCenter and NSX-T™ managers. Your vCenter Server must be configured for MS AD authentication.

You have several options for reference to your existing domain as an identity source:

* If you have connectivity to your domain controllers in or from {{site.data.keyword.vpc_full}}, you can reference them directly.
* You can deploy read-only replica controllers in {{site.data.keyword.vpc_short}}.
* You can add one-way trust from the domain controllers that are deployed in {{site.data.keyword.vpc_short}} to your domain controllers.

In {{site.data.keyword.vpc_short}}, you can deploy one or two Active Directory domain controllers by using VPC Virtual Servers Instances or by using VMs in your VMware cluster.

If you choose the option to deploy the MS AD servers on VMware, you are responsible to provide Microsoft licensing and activation.
{: note}

### vSphere Single Sign On (SSO) Domain
{: #vpc-ryo-commonservice-vsphere-sso}

The vSphere Single Sign On (SSO) domain is used as the initial authentication mechanism for a single instance or multiple linked instances. The SSO domain also serves to connect a VMware instance or multiple linked instances to the MS AD server.

The following considerations must be done for SSO configuration:

* By default, vCenter Server uses the `vsphere.local` domain as the identity source. However, you can change it during installation.
* Select your own SSO domain to be used. For example, `ibmcloud.local`.
* Make the previous selections before you deploy your hosts and vCenter Server.

## Domain Name Services
{: #vpc-ryo-commonservice-dns}

In this design, the Domain Name Services (DNS) use {{site.data.keyword.dns_full_notm}}. The {{site.data.keyword.dns_full_notm}} provides private DNS to VPC users and it can be used for workloads, management, and infrastructure components.

Private DNS zones are resolvable only on {{site.data.keyword.cloud_notm}}, and only from explicitly allowed networks in an account. For shared cloud service endpoints, use the following DNS server addresses `161.26.0.10` and `161.26.0.11`.

You can also use private DNS custom resolvers, which extend {{site.data.keyword.dns_full_notm}} capability by enabling resolution of the {{site.data.keyword.vpc_short}} hostnames from on-premises DNS resolvers. They also enable the resolution of on-premises hostnames from the {{site.data.keyword.cloud_notm}}. Custom resolvers are deployed in your VPC subnet, for example, they use IP addresses, which are routable in your VPC and outside the VPC with interconnectivity services. Forwarding rules can be configured to notify the service where to forward the DNS queries for resolution. After provisioning and configuring, through forwarding, the DHCP option for the resolver changes to the custom resolver IP addresses. For example, the {{site.data.keyword.cloud_notm}} bare metal server or Virtual Servers in VPC use these new IP addresses as the DNS servers. Otherwise, you can use these IP addresses for the VMware VMs.

For more information, see [{{site.data.keyword.dns_full_notm}}](/docs/dns-svcs?topic=dns-svcs-about-dns-services).

## NTP Services
{: #vpc-ryo-commonservice-ntp}

This design uses the {{site.data.keyword.cloud_notm}} infrastructure NTP servers. It is critical that all components within the design use the same NTP server for certificates and Active Directory authentication to function correctly.

The IBM NTP server is available for VPC instances to use for time synchronization. All deployed VPC components are configured to use these NTP servers, but you must configure vCenter or the NSX-T managers and edges to use the NTP server.

An NTP server is available from `time.adn.networklayer.com`, which resolves to `161.26.0.6`.

## Certificate authority services
{: #vpc-ryo-commonservice-cas}

By default, VMware vSphere uses TLS certificates that are signed by the VMware certificate authority (VMCA), which is located in the VMware Platform Services Controller (PSC) appliance. These certificates are not trusted by the user devices or browsers. It is a security best practice to replace user-facing certificates with certificates that are signed by a third-party or enterprise certificate authority (CA). Certificates for machine-to-machine communication can remain as VMCA–signed certificates. However, it is recommended that you follow best practices for your organization, which typically involve the use of an identified enterprise CA.

You can use Windows® AD servers within this design to create certificates that are signed by the local instance. However, you can also choose to configure CA services if needed. For these services, you must allow the required network flows for servers to check the validity of the certificates.

## Related links
{: #vpc-ryo-commonservice-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
