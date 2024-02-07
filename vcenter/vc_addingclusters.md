---

copyright:

  years:  2021, 2024

lastupdated: "2024-01-30"

keywords: vCenter Server add clusters, add cluster, vCenter Server cluster

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding clusters to vCenter Server instances
{: #vc_addingclusters}

You can add clusters to VMware vCenter Server® instances to expand the compute and storage capacity. Within a cluster, you can manage VMware ESXi™ servers for better resource allocation and high availability.

Adding clusters to vCenter Server instances with VMware vSphere® 6.5 or 6.7 is not supported.
{: deprecated}

## Before you add clusters to vCenter Server instances
{: #vc_addingclusters-before}

{{site.data.content.para-vcenteraddclusters}}

* New clusters are provisioned with mirrored M.2 boot drives.
* The number of clusters, hosts, and virtual machines (VMs) determines the maximum number of clusters that you can add. You must remain within the VMware® sizing guidelines and limits for your deployment. For more information, see [VMware configuration maximums](https://configmax.esp.vmware.com/home){: external}.
* You can add a cluster while another cluster is being created or deleted.

## Cluster type
{: #vc_addingclusters-cluster-type}

Select the cluster type: **Workload cluster** or **Gateway cluster**.

## System settings for workload clusters
{: #vc_addingclusters-sys-settings-workload}

When you add a workload cluster to a vCenter Server instance, you must specify the following settings.

### Cluster name
{: #vc_addingclusters-cluster-name}

The cluster name is set to **vcs-_xx_** by default, where _xx_ represents two randomly generated alphabetic characters.

{{site.data.content.cluster-name-requirements-list}}

### Licensing settings
{: #vc_addingclusters-licensing-settings}

Review the following information and specify the licensing setting for the VMware vSphere component in the cluster:
* For Business Partner users, the vSphere license (Enterprise Plus edition) is included and purchased on your behalf.
* For users who are not Business Partners, use the IBM-provided VMware licenses for this component, which are included with purchase.
* The **Use existing license** option is available only if you are using a BYOL vSphere license for your instance. When the option is enabled, you can select the existing license only if the instance has enough capacity for the additional hosts.

   Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide** or **Use existing license** and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.
   {: important}

### Bare metal server settings
{: #vc_addingclusters-bare-metal-settings}

The CPU models differ depending on the version that your instance was initially deployed in. You can choose between **Cascade Lake** and **SAP-certified Cascade Lake** servers[^1u].

[^1u]: For clusters with NFS storage, where locations with appropriate 1U servers are available, 1U servers (up to 4 drives of storage) are ordered silently rather than 2U servers. For gateway clusters and clusters with vSAN storage, 2U servers are ordered.

#### Data center location
{: #vc_addingclusters-dc-location}

The {{site.data.keyword.cloud}} data center location of the cluster is set to the {{site.data.keyword.cloud_notm}} data center of the vCenter Server instance by default. You can deploy the cluster to a different {{site.data.keyword.cloud_notm}} data center than the deployed instance if you ensure that the network latency between the two {{site.data.keyword.cloud_notm}} data centers is less than 150 ms.

If you deploy the cluster to a different {{site.data.keyword.cloud_notm}} data center or {{site.data.keyword.cloud_notm}} infrastructure pod, three extra VLANs are ordered for use with the ordered {{site.data.keyword.cloud_notm}} bare metal servers.

#### Cascade Lake
{: #vc_addingclusters-cascade}

{{site.data.content.cascade-para-intro}}

{{site.data.content.simpletabtable-cascade}}

#### SAP-certified Cascade Lake
{: #vc_addingclusters-sap}

{{site.data.content.sap-para-intro}}

{{site.data.content.simpletabtable-sap-netweaver}}

{{site.data.content.simpletabtable-sap-hana}}

#### Number of bare metal servers
{: #vc_addingclusters-bare-metal-number}

{{site.data.content.exception-number-of-baremetal-servers}}

### Storage settings
{: #vc_addingclusters-storage-settings}

Storage settings are based on your selection of {{site.data.keyword.cloud_notm}} bare metal server configuration and the storage type.

You can add NFS storage shares to an existing vSAN or NFS cluster. For more information, see [Adding NFS storage to vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs).
{: note}

#### NFS storage
{: #vc_addingclusters-nfs-storage}

When you select **NFS storage**, you can add file-level shared storage for your instance where all shares use the same settings or you can specify different configuration settings for each file share. The number of file shares must be in the range of 1 to 100.

Specify the following NFS options.
* **Configure shares individually** - Toggle this switch on to specify different configuration settings for each file share.
* **Number of shares** - If you want to use the same configuration setting for each file share, specify the number of file shares for the NFS shared storage that you want to add.
* **Size (GB)** - Select the capacity that meets your shared storage needs.
* **Performance** - Select the IOPS (input/output operations per second) per GB based on your workload requirements.
* **Add shared storage** - Select to add individual file shares with different configuration settings.

The following table indicates the performance level details.

| Option | Details |
|:------ |:------- |
| 0.25 IOPS/GB | This option is designed for workloads that are not used often. Example applications include vaulted data, hosting large databases with legacy data, or virtual disk images of virtual memory system as backup. |
| 2 IOPS/GB | This option is designed for most general-purpose workloads. Example applications include hosting small databases, backing up web applications, or VM disk images for a hypervisor. |
| 4 IOPS/GB | This option is designed for higher-intensity workloads that have a high percentage of active data at a time. Example applications include transactional databases. |
| 10 IOPS/GB | This option is designed for the most demanding workload types, such as analytics. Example applications include high-transaction databases and other performance-sensitive databases. This performance level is limited to a maximum capacity of 4 TB per file share. |
{: caption="Table 3. NFS performance level options" caption-side="bottom"}

#### vSAN storage
{: #vc_addingclusters-vsan-storage}

Specify the following vSAN options.

##### Size for vSAN capacity disks
{: #vc_addingclusters-vsan-capacity-size}

Select an option for the capacity disks that you need.

##### Number of vSAN capacity disks
{: #vc_addingclusters-vsan-capacity-number}

Specify the number of capacity disks that you want to add.

If you want to add more capacity disks, select the **High performance with Intel Optane** checkbox. This option provides two extra capacity disk bays, which are useful for workloads that require less latency and higher IOPS throughput.

The **High performance with Intel Optane** option is available only for vSphere 6 instances.
{: note}

##### Size for vSAN cache disks
{: #vc_addingclusters-vsan-cache-size}

Review the **Size for vSAN cache disks** value. The value depends on whether you checked the **High performance with Intel Optane** box.

##### Number of vSAN cache disks
{: #vc_addingclusters-vsan-cache-number}

Review **Number of vSAN cache disks**. The value depends on whether you checked the **High performance with Intel Optane** box.

##### Enable vSAN deduplication and compression
{: #vc_addingclusters-vsan-storage-enable-comp}

vSAN storage depends on the number of servers and your total disk capacity, and the use of deduplication and compression.

The amount of storage reduction from deduplication and compression depends on many factors, including the type of data stored and the number of duplicate blocks. Larger disk groups tend to provide a higher deduplication ratio. For more information, see [Using deduplication and compression](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vsan.doc/GUID-3D2D80CC-444E-454E-9B8B-25C3F620EFED.html){: external}.
{: note}

##### vSAN license
{: #vc_addingclusters-vsan-storage-lic}

Use the IBM-provided VMware license for the vSAN component, which is included with purchase.

Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide** or **Use existing license** and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.
{: important}

The **Use existing license** option is available only if you are using a BYOL vSAN license for your instance. When the option is enabled, you can select the existing license only if the instance has enough capacity for the additional hosts.

If your initial cluster was a vSAN cluster, any additional vSAN clusters use the same vSAN license and have the same configuration as the initial one. This behavior is also true if any cluster (initial or additional) in the instance has vSAN chosen to be deployed on it. The first time you're prompted for the vSAN license and the edition. The next time that you select vSAN for a new cluster, the license that was chosen initially is reused.

### Network interface settings
{: #vc_addingclusters-network-interface-settings}

When you add a cluster for a vCenter Server instance, you must specify the following network interface settings.

#### Hostname prefix
{: #vc_addingclusters-host-name}

You can use the default hostname prefix or specify a new one. When you specify a new hostname prefix, the hostname prefix must meet the following requirements:
- Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
- The hostname prefix must start with a lowercase alphabetic character.
- The hostname prefix must end with a lowercase alphabetic or numeric character.
- The maximum length of the hostname prefix is 10 characters.

#### Configure hostnames individually
{: #vc_addingclusters-network-diagram}

You can customize the hostnames prefix individually by toggling the switch on. 

The hostnames prefix must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* No consecutive hyphens are allowed.
* The hostname prefix must start with a lowercase alphabetic character.
* The hostname prefix must end with a lowercase alphabetic or numeric character.
* The maximum length of the hostname prefix is 13 characters.

#### Networking type
{: #vc_addingclusters-network}

Network interface card (NIC) enablement settings are based on your selection of either **Public and private network** or **Private network only**.

#### Uplink speed
{: #vc_addingclusters-uplink}

The **Uplink speed** option is not available to gateway clusters.
{: note}

{{site.data.content.uplink-speed-options-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

#### VLANs
{: #vc_addingclusters-vlans}

Network settings are based on your selection of either **Order new VLANs** or **Select existing VLANs**.

One public VLAN and two private VLANs are required for your instance order. The two private VLANs are trunked into each {{site.data.keyword.cloud_notm}} bare metal server.

##### Order new VLANs
{: #vc_addingclusters-new-vlans}

Select to order one new public VLAN and two new private VLANs.

##### Select existing VLANs
{: #vc_addingclusters-existing-vlans}

Depending on the {{site.data.keyword.cloud_notm}} data center that you selected, existing public and private VLANs might be available.

When you select to reuse existing public and private VLANs, specify the VLANs and subnets:
* **Public VLAN** is for public network access. If you select the **Allocate a new one** option for this field, a new public VLAN is allocated automatically. This field is only available on the **Public and private network** tab.
* **Public primary subnet** is assigned to physical hosts for public network access. If you select the **Auto assigned** option for this field, a new public primary subnet is selected automatically, and a new one is created if necessary. This field is only available on the **Public and private network** tab.
* **Private VLAN** is for connectivity among the data centers and services within the {{site.data.keyword.cloud_notm}}. If you select the **Allocate a new one** option for this field, a new private VLAN is allocated automatically.
* **Private primary subnet** is assigned to physical hosts for management traffic. If you select the **Auto assigned** option for this field, a new private primary subnet is selected automatically, and a new one is created if necessary.
* **Secondary private VLAN** is for VMware features such as vSAN. You can select an existing secondary private VLAN or select to allocate a new one.

Ensure that the firewall configuration on the selected VLANs does not block the management data traffic. Also, ensure that all the VLANs that you select are in the same pod. ESXi servers cannot be provisioned on mixed-pod VLANs.
{: important}

Optionally, use **Advanced settings** to configure portable subnets for VLANs.

Use the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** tabs to specify the **Portable subnet** for each applicable purpose. If you select the **Allocate a new one** option for this field, a new portable subnet is allocated automatically.
**Notes**
* Complete the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings before you can configure portable subnets.
* The number of portable subnets is displayed on the **Advanced settings** option after you save the portable subnet settings. Click **Portable subnets settings** to edit the settings.
* The saved portable subnet settings are cleared if you change the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings.

{{site.data.keyword.vmwaresolutions_short}} takes control of the entire subnet and you can't use any IP addresses in the subnet.
{: important}

## System settings for gateway clusters
{: #vc_addingclusters-sys-settings-edge}

When you add a gateway cluster to a vCenter Server instance, you must specify the following settings.

### Data center location
{: #vc_orderinginstance-dc-edge}

Select the {{site.data.keyword.cloud}} data center settings. For more information, see [Region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

#### Geography
{: #vc_orderinginstance-dc-region-edge}

Select the region where your consolidated cluster or instance is hosted.

#### Data center
{: #vc_orderinginstance-dc-location-edge}

Select the {{site.data.keyword.cloud_notm}} data center where the consolidated cluster is hosted.

#### Pod
{: #vc_orderinginstance-dc-pod-edge}

Select the {{site.data.keyword.cloud_notm}} data center pod where you want to deploy your resources. Keep the default pod selection if you do not have reasons to prefer a different pod.

### Cluster name
{: #vc_addingclusters-cluster-name-edge}

By default, the cluster names are set to **_instance name_-edge**.

You can also specify a new name for your clusters. The names must meet the requirements that are listed in [Cluster name](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-consold-cluster#vc_orderinginstance-consold-cluster-name).

### CPU model
{: #vc_addingclusters-edge-cluster-cpu}

You can choose between the following CPU models:
* Dual Intel Xeon® Silver 4210 processor (Cascade Lake) with 20 cores, 2.20 GHz, and 10 Gb of uplink speed.
* Dual Intel Xeon Gold 5218 processor (Cascade Lake) with 32 cores, 2.30 GHz, and 25 Gb of uplink speed.

### RAM
{: #vc_addingclusters-edge-cluster-ram}

You can select different values of RAM in the range 64 GB - 1.5 TB.

### Number of bare metal servers
{: #vc_addingclusters-edge-cluster-bare-metal}

The number of servers is set to two and cannot be changed. Both servers have the same configuration.

### Hostname prefix
{: #vc_addingclusters-edge-host-name-prefix}

The hostname prefix applies to all clusters in the instance. It must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* The hostname prefix must start with a lowercase alphabetic character.
* The hostname prefix must end with a lowercase alphabetic or numeric character.
* The maximum length of the hostname prefix is 10 characters.

### Configure hostnames individually
{: #vc_addingclusters-edge-network-diagram}

You can customize the hostnames prefix individually by toggling the switch on. 

The hostnames prefix must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* No consecutive hyphens are allowed.
* The hostname prefix must start with a lowercase alphabetic character.
* The hostname prefix must end with a lowercase alphabetic or numeric character.
* The maximum length of the hostname prefix is 13 characters.

### Networking type
{: #vc_addingclusters-edge-cluster-private-nics}

Select either **Public and private network** or **Private network only** for the gateway cluster.

## Summary
{: #vc_addingclusters-order-summary}

Based on your selected configuration for the cluster, the estimated price is instantly generated and displayed in the **Summary** pane. Click **Pricing details** to generate a PDF document with the price summary for the VMware Solutions resources.

You can also add the provisioned resources to the {{site.data.keyword.cloud_notm}} estimate tool, by clicking **Add to estimate**. The estimate tool is useful if you want to get an approximate price of the selected VMware Solutions resources together with other {{site.data.keyword.cloud_notm}} resources that you might consider purchasing.

## Procedure to add clusters to vCenter Server instances
{: #vc_addingclusters-procedure}

1. From the VMware Solutions console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance that you want to add clusters to.

   Ensure that the instance status is **Available**. Otherwise, you cannot add clusters to the instance.
   {: important}

3. Click the **Infrastructure** tab and click **Create** on the upper right of the **Clusters** table.
4. On the **Create cluster** page, select the cluster type.
5. For workload clusters, enter the cluster name and complete the following configuration.
   1. Complete the licensing settings.
      * For Business Partner users, the vSphere license (Enterprise Plus edition) is included and purchased on your behalf.
      * For users who are not Business Partners, select **Include with purchase** for the new vSphere license to be purchased on your behalf. 
      * Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide** or **Use existing license** and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.
      * The **Use existing license** option is available only if you are using a BYOL vSphere or vSAN license for your instance. When the option is enabled, you can select the existing license only if the instance has enough capacity for the additional hosts.

   2. Complete the bare metal server configuration. 
      * If you want to host the cluster in a different {{site.data.keyword.cloud_notm}} data center than the one that the instance is hosted in, toggle the **Select a different location** switch on and choose the {{site.data.keyword.cloud_notm}} data center to host the cluster.
      * For **Cascade Lake**, select the **CPU model**, **RAM size**, and the **Number of bare metal servers**.
      * For **SAP-certified Cascade Lake**, select one of the preset configurations.

   3. Complete the storage configuration.
      * If you select **NFS storage** and want to add and configure the same settings to all file shares, specify the **Number of shares**, **Size (GB)**, and **Performance**.
      * If you select **NFS storage** and want to add and configure file shares individually, toggle the **Configure shares individually** switch on, then click **Add shared storage** and select the **Size (GB)** and **Performance** for each individual file share. Select at least one file share. 
      * If you select **vSAN storage**, specify the following values:
         * Size for the vSAN capacity disks
         * Number of vSAN capacity disks
         * Size for vSAN cache disks
         * Number of vSAN cache disks
         * vSAN license edition

      If you want more storage, check the **High performance with Intel Optane** box.

      By default, the **Enable vSAN deduplication and compression** box is selected. If you do not want to enable vSAN deduplication and compression, clear the checkbox.

6. For gateway clusters, complete the following configuration.
   1. For data center location, click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") and select the geography, data center, and pod to host the cluster.
   2. Specify the cluster name.
   3. Select the CPU model, RAM size, and the number of bare metal servers.
   4. For network interface settings, enter the hostname prefix. 
   5. If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on. 
   6. Select the **Networking type**, either **Public and private network** or **Private network only**.

8. On the **Summary** pane, verify the cluster configuration before you add the cluster.
   1. Review the settings for the cluster.
   2. Review the estimated price of the cluster. Click **Pricing details** to generate a PDF summary. To save or print your order summary, click the **Print** or the **Download** icon ![Download icon](../../icons/download.svg "Download") on the upper right of the PDF window.
   3. Click the link or links of the terms that apply to your order, and confirm that you agree with these terms before you add the cluster.
   4. Click **Create**.

## Results after you add clusters to vCenter Server instances
{: #vc_addingclusters-results}

1. The deployment of the cluster starts automatically and the status of the cluster is changed to **Initializing**. You can check the status of the deployment by viewing the deployment history on the instance details page.
2. When the cluster is ready to use, its status changes to **Available**. The newly added cluster is enabled with vSphere High Availability (HA) and vSphere Distributed Resource Scheduler (DRS).

You cannot change the cluster name. Changing the cluster name might cause the add or delete ESXi servers operations in the cluster to fail.
{: important}

## Related links
{: #vc_addingclusters-related}

* [Viewing vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Expanding and contracting capacity for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
