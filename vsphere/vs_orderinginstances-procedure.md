---

copyright:

  years:  2016, 2024

lastupdated: "2024-08-12"

keywords: flexible order instances, order flexible, order vmaware vSphere instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Procedure to order Flexible instances
{: #vs_orderinginstances-procedure}



1. In the VMware Solutions console, click the **VMware Cloud Foundation (VCF) for Classic** card in the **Create a resource** section. {: #step-1}
1. On the **Create** tab, click the **Flexible** card in the **Resource type** section.
1. To specify the instance configuration name, click **Browse configurations** and choose a configuration in the **VMware instance configuration manager**.
   * If you do not see any configurations in the list and you want to create one, you must first save the instance settings as a new configuration without placing an order.
   * If you want to update a saved configuration or create a new configuration based on a saved one, select the configuration from the side panel, make your changes, and then save.
1. Enter the instance name and select a resource group.
1. Select the VMware vSphere® version for your instance.
1. Select the VMware® components for licensing:

   {{site.data.content.attnnote-byol}}

   If you do select that you are providing your own license, an {{site.data.keyword.cloud_notm}} ticket is opened automatically. This ticket requests the default vSphere licenses on your ordered bare metal servers to be replaced with your provided licenses.

   You are responsible to track the ticket so that you replace the vSphere license on the newly ordered VMware ESXi® servers. This way the {{site.data.keyword.cloud_notm}} infrastructure grants the cancellation of the initially provided {{site.data.keyword.cloud_notm}} infrastructure vSphere license charge. To replace your ESXi vSphere license, see [Configure license settings for an ESXi host](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vcenterhost.doc/GUID-1B128360-0060-40F2-A6F0-43CD2534B034.html?hWord=N4IghgNiBcIMIHsB2AzAlgcwK4CcCmABBGgMZ5IDOhVALjWkhhQSgjgWEgQKIDKAGmgIALBBRogAvkA){: external}.
   {: important}

1. Complete the bare metal server settings:
   1. For data center location, click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") and select the geography, data center, and pod where the instance is to be hosted.
   1. Select the CPU model:
      * For **Cascade Lake** servers, select the CPU model and the RAM size.
      * For **SAP-certified Cascade Lake** servers (vSphere 7 only), choose one of the preset configurations.
   1. Specify the number of bare metal servers.
1. If you selected the **VMware vSAN** component, complete the vSAN™ storage configuration.
   * If you want more storage, select the **High performance with Intel Optane** checkbox.
   * Specify the disk types for the capacity and cache disks, and the number of disks.
   * By default, the **Enable vSAN deduplication and compression** checkbox is selected. If you do not want to enable vSAN deduplication and compression, clear the checkbox.
1. Complete the network interface settings:
   1. Enter the hostname prefix and domain name.
   1. Select the network setting of either **Public and private network** or **Private network only**.
   1. Select the uplink speed. The 25 Gb option is available only for specific pods and data center locations.
   1. Select the network interface that you want to use.
      * If you want to order new public and private VLANs, click **Order new VLANs**.
      * If you want to reuse the existing public and private VLANs when they are available, click **Select existing VLANs** and specify the VLANs and optionally the subnets.
   1. If you are ordering public VLANs, specify whether to apply the FortiGate Physical Appliance 300 Series HA Pair to secure your cloud environment.
1. On the **Summary** pane, review the instance settings and the estimated price.
   * To save the settings as a new configuration template without placing an order, click **Save configuration**, enter a name for the configuration, and click **Continue**.
   * To save the updates to a saved configuration, click **Save configuration**, select **Modify current configuration**, and click **Continue**.
   * To save the updates to a new saved configuration, click **Save configuration**, select **Create new configuration**, enter a new name for the configuration, and click **Continue**.
1. To place the order, make sure that the account to be charged is correct, review and accept the terms, and then click **Create**.

   Only the {{site.data.keyword.cloud_notm}} bare metal servers are installed. You are responsible for installing and configuring various components after instance deployment, such as VMware vCenter Server, VMware NSX®, and VMware vSAN - Enterprise or Enterprise Plus editions.
   {: note}

## Results after you order Flexible instances
{: #vs_orderinginstances-results}

If you saved the instance configuration as a template, you get a console notification that the configuration is saved successfully, and then you can find the template in the **Instance configurations** list.

If you placed an order, the deployment starts automatically, and you receive an email confirmation that the order is being processed. When the instance is ready to use, you are notified by email.

## Related links
{: #vs_orderinginstances-procedure-related}

* [Ordering Flexible instances based on existing configurations](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderingbasedonexistingconfig)
* [Adding ESXi servers to Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_addingservers)
