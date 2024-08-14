---

copyright:

  years:  2016, 2024

lastupdated: "2024-08-13"

keywords: automated consolidated cluster, order consolidated cluster, order automated instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Consolidated cluster
{: #vc_orderinginstance-consold-cluster}

{{site.data.keyword.vcf-auto}} instances are deployed with a consolidated cluster for VMware vSphere® 7 in which all the VMware® management components and user workloads run.

Optionally, you can order a separate workload cluster or a gateway cluster, or both. For more information, see [Additional clusters (optional)](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters).

## Cluster name
{: #vc_orderinginstance-consold-cluster-name}

By default, the name of the consolidated cluster is set to **_instance name_-consolidated**.

{{site.data.content.cluster-name-requirements-list}}

## Data center location
{: #vc_orderinginstance-consold-cluster-dc-location}

Specify the {{site.data.keyword.cloud}} data center settings. For more information, see [Region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

### Geography
{: #vc_orderinginstance-consold-cluster-dc-region}

Select the region where your cluster is hosted.

### Data center
{: #vc_orderinginstance-consold-cluster-dc}

Select the {{site.data.keyword.cloud_notm}} data center where the cluster is hosted.

### Pod
{: #vc_orderinginstance-consold-cluster-dc-pod}

Select the {{site.data.keyword.cloud_notm}} data center pod where you want to deploy your resources. Keep the default pod selection unless you want a specific pod.

## CPU model
{: #vc_orderinginstance-cpumodel}

You can choose between **Cascade Lake** and **SAP-certified Cascade Lake** servers[^1u].

[^1u]: For clusters with NFS storage, where locations with appropriate 1U servers are available, 1U servers (up to 4 drives of storage) are ordered silently rather than 2U servers. For gateway clusters and clusters with vSAN storage, 2U servers are ordered.

### Cascade Lake
{: #vc_orderinginstance-cascade}

{{site.data.content.cascade-para-intro}}

{{site.data.content.simpletabtable-cascade}}

### SAP-certified Cascade Lake
{: #vc_orderinginstance-sap}

{{site.data.content.sap-para-intro}}

{{site.data.content.simpletabtable-sap-netweaver}}

{{site.data.content.simpletabtable-sap-hana}}

vSphere 8 is not supported for SAP-certified Cascade Lake servers.
{: important}

## RAM
{: #vc_orderinginstance-consold-cluster-ram}

Various RAM sizes are available depending on the CPU model.

## Number of bare metal servers
{: #vc_orderinginstance-bare-metal-number}

{{site.data.content.number-of-baremetal-servers-consol}}

When you size the capacity of your bare metal servers, consider your current requirements and include extra capacity to accommodate anticipated growth. For more information about sizing, see [Exporting VMware inventory](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-inventory-export).
{: tip}

## Storage
{: #vc_orderinginstance-consold-cluster-storage}

Storage settings are based on your selection of bare metal server configuration and the storage type.

For deployed instances, you can add NFS storage shares to an existing NFS or vSAN™ cluster. For more information, see [Adding NFS storage to Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs).

### NFS storage
{: #vc_orderinginstance-nfs-storage}

When you select **NFS storage**, you can add file-level shared storage for your instance where all shares use the same settings or you can specify different configuration settings for each file share. The number of file shares must be in the range 1 - 100.

For new instances, NFS storage is available with both vSphere 7 and vSphere 8.
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
{: #vc_orderinginstance-vsan-storage}

Specify the following settings for vSAN storage.

For new instances, vSAN storage is not available with vSphere 8. To use vSAN storage, select vSphere 7.
{: important}

#### Size for vSAN capacity disks
{: #vc_orderinginstance-vsan-storage-typesize-capdisks}

Select an option for the capacity disks that you need.

#### Number of vSAN capacity disks
{: #vc_orderinginstance-vsan-storage-number-capdisks}

Specify the number of capacity disks that you want to add. You can order up to 10 disks for Dual CPU models and up to 8 disks for Quad CPU models.

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

#### vSAN license (BYOL only)
{: #vc_orderinginstance-vsan-storage-license}

{{site.data.content.attnnote-byol}}

If you are a BYOL user, provide your own vSAN license key. Toggle the **BYOL** switch to **Enabled** and enter your license key.

If your initial cluster is a vSAN cluster, any additional vSAN clusters use the same vSAN license and have the same configuration as the initial one. This statement is also true for any initial or extra clusters in the instance for which you select vSAN. The first time, you must provide the vSAN license and the edition. The next time that you select vSAN for a new cluster, the license you initially chose will be reused.

## Networking type
{: #vc_orderinginstance-public-private-network}

Select **Public and private network** or **Private network only**.

## Uplink speed
{: #vc_orderinginstance-uplink}

{{site.data.content.uplink-speed-options-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

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

#### Portable subnets notes
{: #vc_orderinginstance-existing-vlans-notes}

* Complete the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings before you can configure portable subnets.
* The number of portable subnets is displayed under **Advanced settings** after you save the portable subnet settings. Click **Portable subnets settings** to edit the settings.
* The saved portable subnet settings are cleared if you change the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings.

{{site.data.keyword.vmwaresolutions_short}} takes control of the entire subnet and you can't use any IP addresses in the subnet.
{: important}

## Related links
{: #vc_orderinginstance-consold-cluster-related}

* [Gateway cluster configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-addl-clusters#vc_orderinginstance-addl-clusters-gate)
* [Procedure to order Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure)
