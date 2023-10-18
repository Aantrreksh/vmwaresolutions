---

copyright:

  years:  2016, 2023

lastupdated: "2023-09-19"

keywords: vCenter Server order instance, order vCenter Server, order vCenter Server instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Procedure to order vCenter Server instances
{: #vc_orderinginstance-procedure}

<!-- The {: #step-1} tag and the ordered list that has only 1s are intentional. Do not delete. This coding is necessary for proper indentation when the procedure is translated. -->

1. In the VMware Solutions console, click the **VMware vCenter Server** card in the **Platforms** section. {: #step-1}
1. Enter the instance name and select a resource group.
1. To specify the instance configuration name, click **Browse configurations** and choose a configuration in the **VMware instance configuration manager**.
   * If you do not see any configurations in the list and you want to create one, you must first save the instance settings as a new configuration without placing an order.
   * If you want to update a saved configuration or create a new configuration based on a saved one, select the configuration from the side panel, make your changes, and then save.
1. Select the instance type:
   * Click **Primary instance** to deploy a single instance in the environment or to deploy the first instance in a multisite topology.
   * Click **Secondary instance** to connect the instance with an existing (primary) instance in the environment for high availability. Select the primary instance that you want the secondary instance to be connected with, then enter the vCenter Server Administrator password for the primary instance.
1. Use the IBM-provided licenses for VMware components, which are included with purchase. For NSX, specify the license edition.

   Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide** and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.
   {: important}

1. Specify the settings for the consolidated cluster:
   1. Specify the cluster name.
   1. Specify the data center location. Click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") and select the geography, data center, and pod to host the instance.
   1. Specify the CPU model: either **Cascade Lake** or **SAP-certified Cascade Lake** and choose one of the available configurations. For **Cascade Lake**, also select the RAM size.
   1. Specify [the number of bare metal servers](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-consold-cluster#vc_orderinginstance-bare-metal-number).
   1. If you want to use NFS storage, select the corresponding option.
      * To add and configure file shares individually, toggle the **Configure shares individually** switch on. Then, click **Add shared storage** and select the **Size (GB)** and **Performance** for each file share. You must select at least one file share.
      * To add and configure the same settings to all file shares, specify the **Number of shares**, **Size (GB)**, and **Performance**.
   1. If you want to use vSAN™ storage, select the corresponding option.
      * Specify the disk type and size for the vSAN capacity disks, the number of vSAN capacity disks, the disk size for vSAN cache disks, and the number of vSAN cache disks.
      * By default, the **Enable vSAN deduplication and compression** checkbox is selected. If you do not want to enable vSAN deduplication and compression, clear the checkbox.
      * Specify the vSAN license edition.
   1. Specify the networking type.
   1. Select the uplink speed. The 25 Gb option is available only for specific pods and data center locations. 
   1. Select the VLAN settings:
      * If you want to order new public and private VLANs, click **Order new VLANs**.
      * If you want to reuse the existing public and private VLANs when they are available, click **Select existing VLANs** and specify the VLANs and the subnets. Optionally, click **Portable subnets settings**. Then, select the portable subnet for each purpose and click **Save**.
1. If you want to deploy a separate workload cluster, toggle the **Deploy separate workload cluster** switch on and specify [the workload cluster configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters#vc_orderinginstance-addl-clusters-wkld).

   If the consolidated or management cluster and the workload clusters are in the same location, you cannot use existing VLANs. Instead, the workload clusters reuse the VLANs from the management cluster.
   {: note}

1. If you want to deploy a gateway cluster with Juniper vSRX included, toggle the **Deploy gateway cluster** switch on and specify [the gateway cluster configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters#vc_orderinginstance-addl-clusters-gate).
1. Specify the **Network interface** settings:
   1. Enter the **Hostname prefix** and the root **Domain name** for the instance that you are creating. For a secondary instance, the domain name is automatically completed.
   1. Specify the **DNS configuration**.
   1. If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on.
1. Under **Add-on services**, review the available services. If you want to deploy an add-on service, toggle its switch on and review the service settings. If configuration is required, click **Edit**, then complete the edits and click **Save**. For more information about specific settings for a service, see the corresponding topic for ordering the service.
1. On the **Summary** pane, review the instance settings and the estimated price.
   * To save the settings as a new configuration template without placing an order, click **Save configuration**, enter a name for the configuration, and click **Continue**.
   * To save the updates to a saved configuration, click **Save configuration**, select **Modify current configuration**, and click **Continue**.
   * To save the updates to a new saved configuration, click **Save configuration**, select **Create new configuration**, enter a new name for the configuration, and click **Continue**.
1. To place the order, ensure that the account to be charged is correct, review and accept the terms, and then click **Create**.

## Results if you saved a configuration
{: #vc_orderinginstance-results-config}

You get a console notification that the configuration is saved successfully, and then you can find the template in the **Instance configurations** list. Next, you can manage the configuration template by viewing or deleting it in the **Instance configurations** list.

## Results if you placed an order
{: #vc_orderinginstance-results-order}

1. The deployment of the instance starts automatically and you receive confirmation that the order is being processed. You can check the deployment status, including any issues that might require your attention, by viewing the **Deployment history** tab of the instance details.
2. If you experience vSAN Health alerts and warnings, see [How do I manage vSAN Health alerts and warnings?](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_vsan_alerts)
3. When the instance is successfully deployed, the components that are described in [Technical specifications for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview#vc_vcenterserveroverview-specs) are installed on your VMware virtual platform. If you ordered add-on services, the deployment of the services starts after your order is completed.
4. When the instance is ready to use, its status changes to **Available**, and then you receive a notification by email.
5. When you order a secondary instance, the VMware vSphere Web Client for the primary instance (linked to the secondary one) might be restarted after your secondary instance order is completed.

Next, you can view and manage the vCenter Server instance that you ordered.

You must manage the {{site.data.keyword.vmwaresolutions_short}} components that are created in your {{site.data.keyword.cloud_notm}} account only from the VMware Solutions console, not the {{site.data.keyword.slportal}}, or any other means outside of the console.
If you change these components outside of the VMware Solutions console, the changes are not synchronized with the console.
{: important}

{{site.data.content.caution-component-management}}

   Exceptions to these activities include managing the shared storage file shares from the {{site.data.keyword.slportal}}. Such activities include ordering, deleting (which might impact data stores if mounted), authorizing, and mounting shared storage file shares.

## Related links
{: #vc_orderinginstance-procedure-related}

* [Adding clusters to vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingclusters)
* [Expanding and contracting capacity for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
