---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-04"

keywords: cyber recovery order procedure, order procedure cyber recovery, cyber recovery order instance, order cyber recovery, order cyber recovery instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Procedure to order {{site.data.keyword.cr}}
{: #cr_orderinginstance-order-procedure}



1. In the VMware Solutions console, click the **VMware Cloud Foundation (VCF) for Classic** card in the **Create a resource** section. {: #step-1}
1. On the **Create** tab, click the **{{site.data.keyword.cr}}** card in the **Resource type** section.
1. Select the VMware vCenter Server® and the VMware vSphere® version. Then, enter the instance name and select a resource group.
1. To specify the instance configuration name, click **Browse configurations** and choose a configuration in the **VMware instance configuration manager**.
   * If you do not see any configurations in the list and you want to create one, you must first save the instance settings as a new configuration without placing an order.
   * If you want to update a saved configuration or create a new configuration based on a saved one, select the configuration from the side panel, make your changes, and then save.
1. Select the instance type.
   * Click **Primary instance** to deploy a single instance in the environment or to deploy the first instance in a multisite topology.
   * Click **Secondary instance** to connect the instance with an existing (primary) instance in the environment for high availability. Select the primary instance that you want the secondary instance to be connected with, then enter the {{site.data.keyword.cr}} Administrator password for the primary instance.
1. If you are a BYOL user, provide your own license keys for all VMware components. Toggle the **BYOL** switch to **Enabled** and enter your license keys.

   {{site.data.content.attnnote-byol}}

1. In the **Consolidated cluster** section, accept or change the default name of the consolidated cluster. For more information, see [Cluster name](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-consolidwkld#cr_orderinginstance-consolidwkld-cluster-name).
   1. For the **Data center location**, select the **Geography**, **Data Center**, and **Pod** to host the clusters. For more information, see [Data center location](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-consolidwkld#cr_orderinginstance-consolidwkld-dc-location).
   1. For the **CPU model**, select either **Cascade Lake** or **SAP-certified Cascade Lake** and choose one of the available configurations. For **Cascade Lake**, also select the RAM size.
   1. Select the number of bare metal servers. You can order 4-51 bare metal servers.
   1. If you want to use **NFS storage**, select the corresponding option.
      * To add and configure file shares individually, toggle the **Configure shares individually** switch on. Select at least one file share. Then, click **Add shared storage** and select the **Size (GB)** and **Performance** for each file share.
      * To add and configure the same settings to all file shares, specify the **Number of shares** and then, select the **Size (GB)** and **Performance** for all the shares.
   1. If you want to use **vSAN storage**, select the corresponding option.
      1. Select the size for and number of **vSAN capacity disks**.
      1. Select the size for and number of **vSAN cache disks**.
      1. Select the box if you want to **Enable vSAN deduplication and compression**.
   1. Select the **Networking type**, either **Public and private network** or **Private network only**.
   1. Select the **Uplink speed**. The 25 Gb option is available only for specific pods and data center locations.
   1. Specify the VLAN settings:
      * To order new public and private VLANs, choose **Order new VLANs**. A new public VLAN and two private VLANs are provisioned.
      * To reuse existing public and private VLANs, if they are available, choose **Select existing VLANs**. Specify the VLANs and the subnets.
1. If you want to deploy a separate workload cluster, in the **Workload cluster** section, toggle the **Deploy separate workload cluster** switch on and specify the cluster settings:
   1. Accept or change the default name of the workload cluster.
   1. For the **Data center location**, select the **Geography**, **Data Center**, and **Pod** to host the clusters. For more information, see [Data center location](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-consolidwkld#cr_orderinginstance-consolidwkld-dc-location).
   1. For the **CPU model**, select either **Cascade Lake** or **SAP-certified Cascade Lake** and choose one of the available configurations. For **Cascade Lake**, also select the RAM size.
   1. Select the **number of bare metal servers**. You can order 4-59 bare metal servers.
   1. If you want to use **NFS storage**, select the corresponding option.
      * To add and configure file shares individually, toggle the **Configure shares individually** switch on. Select at least one file share. Then, click **Add shared storage** and select the **Size (GB)** and **Performance** for each file share.
      * To add and configure the same settings to all file shares, specify the **Number of shares** and select the **Size (GB)** and **Performance** for all the shares.
   1. If you want to use **vSAN storage**, select the corresponding option.
      1. Select the size for and number of **vSAN capacity disks**.
      1. Select the size for and number of **vSAN cache disks**.
      1. Select the box if you want to **Enable vSAN deduplication and compression**.
   1. Select the **Networking type**, either **Public and private network** or **Private network only**.
   1. Select the **Uplink speed**. The 25 Gb option is available only for specific pods and data center locations.
   1. Specify the VLAN settings:
      * To order new public and private VLANs, choose **Order new VLANs**. A new public VLAN and two private VLANs are provisioned.
      * To reuse existing public and private VLANs, if they are available, choose **Select existing VLANs**. Specify the VLANs and the subnets.
      * If the consolidated or management cluster and the workload clusters are in the same location, you cannot use existing VLANs. Instead, choose **Reuse VLANs from the consolidated cluster** so that the workload cluster and the consolidated cluster use the same VLANs.
1. Choose the firewall appliance for your instance and follow the steps, depending on your selection:
   * For **Gateway cluster with Juniper® vSRX**, **Gateway cluster with FortiGate® Virtual Appliance**, and **Bring your own gateway appliance**, specify the [gateway cluster name](/docs/vmwaresolutions?topic=vmwaresolutions-cr-orderinginstance-edge#cr-orderinginstance-edge-cluster-name), the CPU model, the RAM size, and the networking type.
   * For **Gateway cluster with Juniper vSRX** and **Gateway cluster with FortiGate Virtual Appliance**, you must also specify the corresponding service settings in a later step.
   * For **FortiGate Security Appliance**, you must order the **FortiGate Security Appliance 10 Gbps** service from the [{{site.data.keyword.cloud_notm}} catalog](/netsec/firewalls/multi-vlan/provision#about). Confirm that you ordered the service and continue with the following steps.
1. Specify the **Gateway cluster** settings:
   1. Accept or change the default name of the gateway cluster.
   1. Select the **CPU model** and the RAM size.
   1. Select the **Networking type**, either **Public and private network** or **Private network only**.
1. Specify the **Network interface** settings:
   1. Enter the **Hostname prefix** and the root **Domain name** for the instance that you are creating.
   1. If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on.
   1. Specify the **DNS configuration**.
1. Under **Add-on services**, review the available services:
    * The **Included services** category lists the services that are included in your order.
    * The **Recommended services** category lists the services that IBM recommends to fully use your resources.
    * If you want to deploy an add-on service, toggle its switch on and review the service settings. If configuration is required, click **Edit**, then complete the edits and click **Save**. For more information about specific settings for a service, see the corresponding topic for ordering the service.
1. On the **Summary** pane, review the instance settings and the estimated price.
   * To save the settings as a new configuration template without placing an order, click **Save configuration**, enter a name for the configuration, and click **Continue**.
   * To save the updates to a saved configuration, click **Save configuration**, select **Modify current configuration**, and click **Continue**.
   * To save the updates to a new saved configuration, click **Save configuration**, select **Create new configuration**, enter a new name for the configuration, and click **Continue**.
1. To place the order, ensure that the account to be charged is correct, review and accept the terms, and then click **Create**.

## Related links
{: #cr_orderinginstance-order-procedure-related-links}

* [Adding, viewing, and deleting clusters for {{site.data.keyword.cr}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-cr_addingviewingclusters)
* [Expanding and contracting capacity for {{site.data.keyword.cr}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-cr-addingremovingservers)
