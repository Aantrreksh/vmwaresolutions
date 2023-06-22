---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-22"

keywords: vCenter Server order instance, order vCenter Server, order vCenter Server instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Consolidated and Workload cluster
{: #vc_orderinginstance-consoldworkldcluster-settings}

VMware vCenter Server® instances are deployed with a consolidated cluster for VMware vSphere® 7 in which all the VMware® management components and user workloads run.

Optionally, you can order a separate workload cluster and a gateway cluster. To deploy a workload cluster, toggle the **Deploy separate workload cluster** switch on.

## Cluster name
{: #vc_orderinginstance-consoldworkldcluster-cluster-name}

By default, the cluster name set to the **_instance name_-consolidated** value for the consolidated cluster, and the workload cluster name is set to the **_instance name_-workload** value.

{{site.data.content.cluster-name-requirements-list}}

## Bare metal server settings
{: #vc_orderinginstance-bare-metal-settings}

Bare metal settings are based on your data center selection and bare metal server configuration. When you size the capacity of your servers, consider your current requirements, and include extra capacity to accommodate anticipated growth. For more information about sizing, see [Exporting VMware inventory](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-inventory-export).

### Data center location
{: #vc_orderinginstance-dc-location}

Select the {{site.data.keyword.cloud}} data center settings. For more information, see [Region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

#### Geography
{: #vc_orderinginstance-dc-region}

Select the region where your cluster or instance is hosted.

#### Data center
{: #vc_orderinginstance-dc-datacenterloc}

Select the {{site.data.keyword.cloud_notm}} data center where the cluster is hosted.

#### Pod
{: #vc_orderinginstance-dc-pod}

Select the {{site.data.keyword.cloud_notm}} data center pod where you want to deploy your resources. Keep the default pod selection if you do not have reasons to prefer a different pod.

### CPU model and RAM
{: #vc_orderinginstance-cpumodels}

#### Skylake
{: #vc_orderinginstance-skylake}

{{site.data.content.skylake-para-intro}}

{{site.data.content.skylake-note}}

{{site.data.content.simpletabtable-skylake-nsxt}}

{{site.data.content.vcenter-nsxv-note-skylake}}

{{site.data.content.simpletabtable-skylake-nsxv}}

#### Cascade Lake
{: #vc_orderinginstance-cascade}

{{site.data.content.cascade-para-intro}}

{{site.data.content.simpletabtable-cascade-nsxt}}

{{site.data.content.vcenter-nsxv-note-cascadelake}}

{{site.data.content.simpletabtable-cascade-nsxv}}

#### SAP-certified
{: #vc_orderinginstance-sap}

{{site.data.content.sap-para-intro}}

{{site.data.content.simpletabtable-sap-netweaver}}

{{site.data.content.simpletabtable-sap-hana}}

### Number of bare metal servers
{: #vc_orderinginstance-bare-metal-number}

* All servers that you order have the same configuration.
* If you are planning to use vSAN™ storage, you can order 4 - 20 servers.
* A minimum limit of three servers applies for VMware NSX-T™ clusters.
* For production workloads, a minimum of three servers is recommended.

## Storage settings
{: #vc_orderinginstance-storage-settings}

Storage settings are based on your selection of bare metal server configuration and the storage type.

For deployed instances, you can add NFS storage shares to an existing NFS or vSAN™ cluster. For more information, see [Adding NFS storage to vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs).

### NFS storage
{: #vc_orderinginstance-nfs-storage}

When you select **NFS storage**, you can add file-level shared storage for your instance where all shares use the same settings or you can specify different configuration settings for each file share. The number of file shares must be in the range 1 - 100.

Specify the following NFS options:
* **Configure shares individually** - Toggle this switch on to specify different configuration settings for each file share.
* **Number of shares** - When you use the same configuration setting for each file share, specify the number of file shares for the NFS shared storage that you want to add.
* **Size (GB)** - Select the capacity that meets your shared storage needs.
* **Performance** - Select the IOPS (input/output operations per second) per GB based on your workload requirements.
* **Add shared storage** - Select to add individual file shares that use different configuration settings.

Choose performance level options according to your needs.

| Option       | Details       |
|:------------ |:------------- |
| 0.25 IOPS/GB | This option is designed for workloads that are not used often. For example, vaulted data, hosting large databases with legacy data, or virtual disk images of virtual memory system as backup. |
| 2 IOPS/GB | This option is designed for most general-purpose workloads. For example, hosting small databases, backing up web applications, or virtual machine disk images for a hypervisor. |
| 4 IOPS/GB | This option is designed for higher-intensity workloads that have a high percentage of active data at a time. For example, transactional databases. |
| 10 IOPS/GB | This option is designed for the most demanding workload types, such as analytics. For example, high-transaction databases and other performance-sensitive databases. This performance level is limited to a maximum capacity of 4 TB per file share. |
{: caption="Table 4. NFS performance level options" caption-side="bottom"}

### vSAN storage
{: #vc_orderinginstance-vsan-storage}

vSAN is available for the **Skylake** and **Cascade Lake** bare metal configurations only.

#### Size for vSAN capacity disks
{: #vc_orderinginstance-vsan-storage-typesize-capdisks}

Select an option for the capacity disks that you need.

#### Number of vSAN capacity disks
{: #vc_orderinginstance-vsan-storage-number-capdisks}

Specify the number of capacity disks that you want to add.

* For VMware vSphere® 7.0, order up to 10 disks for Dual CPU models and order up to 8 disks for Quad CPU models.
* For vSphere 6.3, order up to 12 disks with Intel® Optane for Dual CPU models and order up to 8 disks for Quad CPU models.

If you want to add more capacity disks, select the **High performance with Intel Optane** checkbox. This option provides two extra capacity disk bays, which are useful for workloads that require less latency and higher IOPS throughput.

The **High performance with Intel Optane** option is available only for vSphere 6 instances.

#### Size for vSAN cache disks
{: #vc_orderinginstance-vsan-storage-size-cachedisks}

Review the **Size for vSAN cache disks** value. The value depends on whether you selected the **High performance with Intel Optane** checkbox.

#### Number of vSAN cache disks
{: #vc_orderinginstance-vsan-storage-number-cachedisks}

Review **Number of vSAN cache disks**. The value depends on whether you selected the **High performance with Intel Optane** checkbox.

#### Enable vSAN deduplication and compression
{: #vc_orderinginstance-vsan-storage-enable-comp}

vSAN storage depends on the number of servers and your total disk capacity, and the use of deduplication and compression.

The amount of storage reduction from deduplication and compression depends on many factors, including the type of data stored and the number of duplicate blocks. Larger disk groups tend to provide a higher deduplication ratio. For more information, see [Using deduplication and compression](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vsan.doc/GUID-3D2D80CC-444E-454E-9B8B-25C3F620EFED.html){: external}.
{: note}

#### vSAN license
{: #vc_orderinginstance-vsan-storage-license}

Use the IBM-provided VMware license for the vSAN component, which is included with purchase.

Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide** and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.
{: important}

If your initial cluster is a vSAN cluster, any additional vSAN clusters use the same vSAN license and have the same configuration as the initial one. This statement is also true for any initial or extra clusters in the instance for which you select vSAN. The first time, you must provide the vSAN license (BYOL or purchased) and the edition. The next time that you select vSAN for a new cluster, the license you initially chose will be reused.

## Networking type
{: #vc_orderinginstance-public-private-network}

Select **Public and private network** or **Private network only**.

## Uplink speed
{: #vc_orderinginstance-uplink}

{{site.data.content.uplink-speed-options-list}}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific | TOK02 | 02 |
| Asia-Pacific | TOK04 | 01 |
| Asia-Pacific | TOK05 | 01 |
| Europe | FRA02 | 02 |
| Europe | FRA04 | 01 |
| Europe | FRA05 | 01 |
| Europe | LON04 | 01 |
| Europe | LON06 | 01 |
| Europe | MAD02 | 01 |
| Europe | MAD04 | 01 |
| Europe | MAD05 | 01 |
| Europe | PAR04 | 01 |
| Europe | PAR05 | 01 |
| Europe | PAR06 | 01 |
| NA East | TOR04 | 01 |
| NA East | WDC04 | 05 |
| NA East | WDC06 | 01 |
| NA East | WDC07 | 01 |
| NA South | DAL10 | 03 |
| NA South | DAL12 | 01 |
| NA South | DAL13 | 02 |
{: caption="Table 5. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: #simpletable-uplink-speed-locations}

## VLANs
{: #vc_orderinginstance-vlans}

Network settings are based on your selection of **Order new VLANs** or **Select existing VLANs**.

One public VLAN and two private VLANs are required for your instance order. The two private VLANs are trunked into each {{site.data.keyword.cloud_notm}} bare metal server.

### Order new VLANs
{: #vc_orderinginstance-new-vlans}

Select to order one new public VLAN and two new private VLANs.

### Select existing VLANs
{: #vc_orderinginstance-existing-vlans}

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

#### Notes
{: #vc_orderinginstance-existing-vlans-notes}

* You must complete the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings before you can configure portable subnets.
* The number of portable subnets is displayed under **Advanced settings** after you save the portable subnet settings. Click **Portable subnets settings** to edit the settings.
* The saved portable subnet settings are cleared if you change the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings.

{{site.data.keyword.vmwaresolutions_short}} takes control of the entire subnet and you can't use any IP addresses in the subnet.
{: important}

### Reuse VLANs from the consolidated cluster
{: #vc_orderinginstance-reuse-vlans}

For the workload cluster network settings, select the **Reuse VLANs from the consolidated cluster** option to reuse the public and private VLANs of the consolidated cluster. The workload cluster and the consolidated cluster are going to use the same set of public and private VLANs.

## Related links
{: #vc_orderinginstance-consoldworkldcluster-related}

* [Gateway cluster](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-edge-gateway-cluster)
* [Procedure to order vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure)
