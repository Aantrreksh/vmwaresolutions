---

copyright:

  years:  2020, 2023

lastupdated: "2023-10-05"

keywords: Juniper vSRX, manage Juniper vSRX, Juniper vSRX console

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering Juniper vSRX
{: #juniper-ordering}

You can include the Juniper® vSRX service with a new VMware vCenter Server® instance or add the service to your existing instance.

You can install multiple instances of Juniper vSRX on the management cluster. On a single gateway cluster, you can install only one instance of Juniper vSRX.

You can install Juniper vSRX on 25 Gb uplink speed management and gateway clusters on VMware vSphere® 7 with NSX-T. On 25 Gb uplink speed clusters, only the Content Security Bundle license is available.

The license that is used depends on the target cluster you choose. 

* For vCenter Server instances with vSphere 7 and NSX-T, management and gateway clusters with 25 Gb uplink speed use the 25 Gb uplink speed version of the license selected. 
* For VMware Regulated Workloads (single-zone and multizone) and Security and Compliance Readiness Bundle instances, the same license selection process occurs for gateway clusters with 25 Gb uplink speeds.

You cannot install Juniper vSRX and FortiGate Virtual Appliance on the same gateway cluster.
{: restriction}

## Ordering Juniper vSRX for a new instance
{: #juniper-ordering-new-instance}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. Juniper vSRX is in the **Security and compliance** category. 
2. Open the category, locate Juniper vSRX, and toggle its switch on.
3. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-ordering#juniper-ordering-service-config), then click **Save**.

   The Juniper vSRX service is deployed on the management cluster unless you order a gateway cluster. For Juniper vSRX to function as a gateway for your instance, you must include the gateway cluster in your order.

## Ordering Juniper vSRX for an existing instance
{: #juniper-ordering-exist-instance}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **Juniper vSRX** service in the **Security and compliance** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-ordering#juniper-ordering-service-config), then click **Save**.

   When you add Juniper vSRX to an existing vCenter Server instance, you can select the cluster on which to install Juniper vSRX, either a management cluster or a gateway cluster. For Juniper vSRX to function as a gateway for your instance, you must deploy the service to a gateway cluster.

## Juniper vSRX service configuration
{: #juniper-ordering-service-config}

When you order the service, provide the following settings:

### Name
{: #juniper-ordering-service-config-name}

Specify the nickname for the installed instance in the **Enter a name for the HA deployment** field. Because multiple copies of Juniper vSRX can be in a single vCenter Server instance, this name is used to ensure that the names of all networking components are unique.

### License model
{: #juniper-ordering-service-config-license-model}

Review the features of the two licenses and select either **Standard Edition** or **Content Security Bundle**.

You can't change the license model after service installation. To change the license model, you must delete the existing service and reinstall the service by selecting a different license option.
{: important}

After the service is ordered, the vSRX nodes are automatically ordered with the selected license models.

### Juniper vSRX deployment on a gateway cluster
{: #juniper-ordering-service-config-edge-deployment}

If you deploy Juniper vSRX on a gateway cluster, after deployment, you must configure Juniper vSRX for your environment. Complete the following steps:

1. Configure the redundant Ethernet `reth2` interface with the default gateway IP addresses of each subnet in your private trunk VLAN. The IP addresses are assigned to the logical interface, which is in the format of `reth2.VLANid`.
2. Configure the redundant Ethernet `reth3` interface with the default gateway IP addresses of each subnet in your public trunk VLAN, if you have one. The IP addresses are assigned to the logical interface, which is in the format of `reth3.VLANid`.
3. In the {{site.data.keyword.cloud}} classic infrastructure view, look at the gateway appliance ordered for the gateway cluster. From there, assign the VLANs that you want to the gateway appliance and put them in `route-through` mode.

## Related links
{: #juniper-ordering-related-links}

* [Juniper vSRX overview](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview)
* [Managing Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-managing)
* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [General FAQ about VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [Juniper vSRX Virtual Firewall](https://www.juniper.net/us/en/products-services/security/srx-series/vsrx/){: external}
* [Juniper vSRX Documentation](https://www.juniper.net/documentation/product/en_US/vsrx){: external}
