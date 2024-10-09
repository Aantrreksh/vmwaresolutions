---

copyright:

  years:  2022, 2024

lastupdated: "2024-10-01"

keywords: cyber recovery, cyber recovery consolidated cluster, cyber recovery consolidated settings, cyber recovery instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Consolidated and workload cluster
{: #cr_orderinginstance-consolidwkld}

{{site.data.keyword.cr}} instances are deployed with a consolidated cluster for VMware vSphere®, in which all the VMware® management components and user workloads run.

You can also order an extra workload cluster.

## Cluster name
{: #cr_orderinginstance-consolidwkld-cluster-name}

* For the consolidated cluster, the cluster name is preset to **_instance name_-consolidated**.
* For the workload cluster, the cluster name is preset to **_instance name_-workload**.

{{site.data.content.cluster-name-requirements-list}}

## Data center location
{: #cr_orderinginstance-consolidwkld-dc-location}

Select the {{site.data.keyword.cloud}} data center settings. For more information, see [{{site.data.keyword.cloud_notm}} locations for resource deployment](/docs/overview?topic=overview-locations).

### Geography
{: #cr_orderinginstance-consolidwkld-dc-region}

Select the region where your cluster or instance is hosted.

### Data center
{: #cr_orderinginstance-consolidwkld-dc-datacenterloc}

Select the {{site.data.keyword.cloud_notm}} data center where the cluster is hosted.

### Pod
{: #cr_orderinginstance-consolidwkld-dc-pod}

Select the {{site.data.keyword.cloud_notm}} data center pod where you want to deploy your resources. Keep the default pod selection unless you have specific reasons to choose a different pod.

## CPU model
{: #cr_orderinginstance-consolidwkld-cpumodel}

Select **Cascade Lake** or **SAP-certified Cascade Lake**.



### Cascade Lake
{: #cr_orderinginstance-consolidwkld-cascade}

{{site.data.content.cascade-para-intro}}

{{site.data.content.simpletabtable-cascade}}

### SAP-certified Cascade Lake
{: #cr_orderinginstance-consolidwkld-sap}

{{site.data.content.sap-para-intro}}

{{site.data.content.simpletabtable-sap-netweaver}}

{{site.data.content.simpletabtable-sap-hana}}

vSphere 8 is not supported for SAP-certified Cascade Lake servers.
{: important}

## RAM
{: #cr_orderinginstance-consold-cluster-ram}

Various RAM sizes are available depending on the CPU model.

## Number of bare metal servers
{: #cr_orderinginstance-consolidwkld-bare-metal-number}

For the consolidated cluster:

{{site.data.content.number-of-baremetal-servers-consol}}

For the workload cluster:

{{site.data.content.number-of-baremetal-servers-wkld}}

When you size the capacity of your servers, consider your current requirements, and include extra capacity to accommodate anticipated growth. For more information, see [Exporting VMware inventory](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-inventory-export).

## Storage
{: #cr_orderinginstance-consolidwkld-storage-settings}

Storage settings are based on your selection of bare metal server configuration and the storage type.

For deployed instances, you can add NFS storage shares to an existing NFS or vSAN cluster. For more information, see [Adding NFS storage to Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs).

### NFS storage
{: #cr_orderinginstance-consolidwkld-nfs-storage}

When you select **NFS storage**, you can add file-level shared storage for your instance where all shares use the same settings or you can specify different configuration settings for each file share. The number of file shares must be in the range 1 - 100.

For new instances, NFS storage is available with vSphere 7 and 8 versions.
{: important}

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
{: caption="Table 3. NFS performance level options" caption-side="bottom"}

### vSAN storage
{: #cr_orderinginstance-consolidwkld-vsan-storage}



vSAN is available only for **Cascade Lake** bare metal servers.

For new instances, vSAN storage is not available with vSphere 8. To use vSAN storage, select vSphere 7.
{: important}



#### Size for vSAN capacity disks
{: #cr_orderinginstance-consolidwkld-vsan-storage-typesize-capdisks}

Select an option for the capacity disks that you need.

#### Number of vSAN capacity disks
{: #cr_orderinginstance-consolidwkld-vsan-storage-number-capdisks}

Specify the number of capacity disks that you want to add.

For VMware vSphere 7, order up to 10 disks for Dual CPU models and order up to eight disks for Quad CPU models.

#### Size for vSAN cache disks
{: #cr_orderinginstance-consolidwkld-vsan-storage-size-cachedisks}

Review the **Size for vSAN cache disks** value.

#### Number of vSAN cache disks
{: #cr_orderinginstance-consolidwkld-vsan-storage-number-cachedisks}

Review the **Number of vSAN cache disks** value.

#### Enable vSAN deduplication and compression
{: #cr_orderinginstance-conconsolidwkldsolidated-vsan-storage-enable-comp}

vSAN storage depends on the number of servers and your total disk capacity, and the use of deduplication and compression.

The amount of storage reduction from deduplication and compression depends on many factors, including the type of data stored and the number of duplicate blocks. Larger disk groups tend to provide a higher deduplication ratio. For more information, see [Using deduplication and compression](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vsan.doc/GUID-3D2D80CC-444E-454E-9B8B-25C3F620EFED.html){: external}.
{: note}



#### vSAN license (BYOL only)
{: #cr_orderinginstance-consolidwkld-vsan-storage-license}

{{site.data.content.attnnote-byol}}

If you are a BYOL user, provide your own vSAN license key. Toggle the **BYOL** switch to **Enabled** and enter your license key.

If your initial cluster is a vSAN cluster, any additional vSAN clusters use the same vSAN license and have the same configuration as the initial one. This statement is also true for any initial or extra clusters in the instance for which you select vSAN. The first time, you must provide the vSAN license and the edition. The next time that you select vSAN for a new cluster, the license you initially chose will be reused.

## Networking type
{: #cr_orderinginstance-consolidwkld-public-private-network}

Select **Public and private network** or **Private network only**.

## Uplink speed
{: #cr_orderinginstance-consolidwkld-uplink}

{{site.data.content.uplink-speed-options-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

## VLANs
{: #cr_orderinginstance-consolidwkld-vlans}

Network settings are based on your selection of **Order new VLANs** or **Select existing VLANs**. For your first purchase of {{site.data.keyword.cr}}, only the **Order new VLANs** selection is available.

One public VLAN and two private VLANs are required for your instance order. The two private VLANs are trunked into each {{site.data.keyword.cloud_notm}} bare metal server.

### Order new VLANs
{: #cr_orderinginstance-consolidwkld-new-vlans}

When you select to **Order new VLANs**, one new public VLAN and two new private VLANs are ordered.

### Select existing VLANs
{: #cr_orderinginstance-consolidwkld-existing-vlans}

For your first purchase of {{site.data.keyword.cr}}, only the **Order new VLANs** selection is available.
{: note}

Depending on the {{site.data.keyword.cloud_notm}} data center that you selected, existing public and private VLANs might be available.

When you select to reuse existing public and private VLANs, specify the VLANs and subnets:
* **Public VLAN** is for public network access. If you select the **Allocate a new one** option for this field, a new public VLAN is allocated automatically. This field is only available on the **Public and private network** tab.
* **Public primary subnet** is assigned to physical hosts for public network access. If you select the **Auto assigned** option for this field, a new public primary subnet is selected automatically, and a new one is created if necessary. This field is only available on the **Public and private network** tab.
* **Private VLAN** is for connectivity among the data centers and services within the {{site.data.keyword.cloud_notm}}. If you select the **Allocate a new one** option for this field, a new private VLAN is allocated automatically.
* **Private primary subnet** is assigned to physical hosts for management traffic. If you select the **Auto assigned** option for this field, a new private primary subnet is selected automatically, and a new one is created if necessary.
* **Secondary private VLAN** is for VMware features such as vSAN. You can select an existing secondary private VLAN or select to allocate a new one.

Ensure that the firewall configuration on the selected VLANs does not block the management data traffic. Also, ensure that all the VLANs that you select are in the same pod. VMware ESXi™ servers cannot be provisioned on mixed-pod VLANs.
{: important}

Optionally, use **Advanced settings** to configure portable subnets for VLANs.

Use the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** tabs to specify the **Portable subnet** for each applicable purpose. If you select the **Allocate a new one** option for this field, a new portable subnet is allocated automatically.

#### Notes
{: #cr_orderinginstance-consolidwkld-existing-vlans-notes}

* You must complete the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings before you can configure portable subnets.
* The number of portable subnets is displayed under **Advanced settings** after you save the portable subnet settings. Click **Portable subnets settings** to edit the settings.
* The saved portable subnet settings are cleared if you change the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings.

{{site.data.keyword.vmwaresolutions_short}} takes control of the entire subnet and you can't use any IP addresses in the subnet.
{: important}

## Related links
{: #cr_orderinginstance-consolidwkld-related-links}

* [Gateway cluster](/docs/vmwaresolutions?topic=vmwaresolutions-cr-orderinginstance-edge)
* [Procedure to order {{site.data.keyword.cr}}](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-order-procedure)
