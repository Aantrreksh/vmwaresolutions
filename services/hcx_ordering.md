---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-07"

keywords: VMware HCX deployment, HCX configuration, order HCX

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering VMware HCX
{: #hcx_ordering}

You can include the VMware HCX™ service with a new VMware vCenter Server® instance or add the service to your existing instance.

## Ordering HCX for a new instance
{: #hcx_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. HCX is in the **Data resiliency and migration** category.
2. Open the category, locate HCX, and toggle its switch on.
3. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering#hcx_ordering-config), then click **Save**.

## Ordering HCX for an existing instance
{: #hcx_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **HCX** service in the **Data resiliency and migration** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering#hcx_ordering-config), then click **Save**.

## HCX configuration
{: #hcx_ordering-config}

To install HCX, complete the following settings:

1. Select the **HCX Service Mesh target cluster**, either the management or the workload cluster.
2. Specify the **HCX network connection** by selecting one of the following options. If any of the management or service mesh target clusters are deployed with private network only, the only networking option that you can choose is private.
   * **Public network** - HCX creates an encrypted connection between sites over the public network. License registration and metering are completed over the public network.
   * **Private network** - HCX creates an encrypted connection between sites over the private network. License registration and metering are completed over a private network through HTTP proxy.  
3. If private network connection is selected, proxy information is displayed. Otherwise, a proxy option is not available.
   Complete the following fields:
   * **Proxy IP address** - The IPv4 address of the proxy server.
   * **Proxy port number** - The proxy server port. The port number is typically 8080 or 3128.
   * **Proxy user name** (Optional) - The username if proxy authentication is required.
   * **Proxy password** (Optional) - The password if proxy authentication is required.
   * **Reenter proxy password** (Optional) - Reenter the password for proxy authentication validation.
4. Specify the **Public endpoint certificate type**. If you select **CA Certificate**, configure the following settings:
   * **Certificate contents** - Enter the contents of the CA certificate.
   * **Private key** - Enter the private key of the CA certificate.
   * **Password** (Optional) - Enter the password for the private key, if it is encrypted.
   * **Reenter password** (Optional) - Enter the password for the private key again.
   * **Hostname** (Optional) - The hostname to be mapped to the common name (CN) of the CA certificate. HCX requires that the format of the CA certificate must be accepted by NSX Edge. For more information about NSX Edge certificate formats, see [Importing SSL Certificates](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.3/com.vmware.nsx.admin.doc/GUID-19D3A4FD-DF17-43A3-9343-25EE28273BC6.html){: external}.

## Deployment process for HCX
{: #hcx_ordering-deploy}

The deployment of HCX is automated. Whether you order a vCenter Server instance with the service included or you deploy the service later into your instance, the following steps are completed by the {{site.data.keyword.vmwaresolutions_short}} automation process:
1. Three subnets are ordered for HCX from the {{site.data.keyword.cloud_notm}} infrastructure:
   * One private portable subnet for HCX management.
   * One private portable subnet for HCX interconnects. This subnet is used when the **Private network** option is selected for **HCX connection type**.
   * One public portable subnet for HCX interconnects, if the **Public network** option is selected for **HCX connection type**. On NSX-V, this subnet is also used for activation and maintenance with VMware.

   The IP addresses in the subnets that are ordered for HCX are intended to be managed by the VMware Solutions automation. These IP addresses cannot be assigned to VMware resources (such as VMs and NSX Edges) that are created by you. If you need more IP addresses for your VMware artifacts, you must order your own subnets from {{site.data.keyword.cloud_notm}}.
   {: important}

2. If **Private Network** was selected for **HCX Network Connection**, a port group that is named **SDDC-DPortGroup-HCX-Private** is created on the private Distributed Virtual Switch (DVS).
3. An HCX activation key is ordered from VMware.
4. For vCenter Server with NSX-T instances, the firewall rules and network address translation (NAT) rules are configured to allow inbound and outbound HTTPS traffic to and from the HCX Manager.
5. For vCenter Server with NSX-V instances, a pair of NSX Edge Services Gateways (ESGs) for the HCX management traffic is deployed and configured:
   * Public and private uplink interfaces are configured by using the ordered subnets.
   * The ESGs are configured as a pair of extra large edge appliances with High Availability (HA) enabled.
   * The firewall rules and network address translation (NAT) rules are configured to allow inbound and outbound HTTPS traffic to and from the HCX Manager.
   * The load balancer rules and resource pools are configured. These rules and resource pools are used to forward HCX-related inbound traffic to the appropriate virtual appliances of HCX Manager and vCenter Server (with embedded Platform Services Controller).
   * An SSL certificate to encrypt the HCX-related inbound HTTPS traffic that is coming through the ESGs is applied.

   The HCX management edge is dedicated to the HCX management traffic between the on-premises HCX components and the cloud-side HCX components. Do not modify the HCX management edge or use it for HCX network extensions. Instead, create separate edges for network extensions. In addition, if you use a firewall or you disable the HCX management edge communications to the private IBM management components or the internet, the HCX functions might be impacted.
   {: important}

6. The HCX Manager is deployed, activated, and configured:
   * The HCX Manager is registered with vCenter Server.
   * The HCX Manager, vCenter Server (with embedded Platform Services Controller), and NSX Manager are configured.
   * The HCX Compute and Network profiles are created.
7. The hostname and IP address of the HCX Manager is registered with the DNS server of vCenter Server.

## Related links
{: #hcx_ordering-related}

* [HCX overview](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations#hcx_considerations)
* [Managing HCX](/docs/vmwaresolutions?topic=vmwaresolutions-managinghcx)
* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Glossary of HCX terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_glossary)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [Why does the installation fail for HCX with BYOL NSX Data Center Enterprise Plus?](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_hcx_install_fail)
* [VMware Hybrid Cloud Extension documentation](https://cloud.vmware.com/vmware-hcx/resources){: external}
