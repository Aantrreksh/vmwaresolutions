---

copyright:

  years:  2021, 2024

lastupdated: "2024-04-23"

keywords: order Security and Compliance Readiness Bundle, order scb instances, order vcs scb
subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Consolidated and workload cluster
{: #scb-orderinginstance-consoli}

New deployments of Security and Compliance Readiness Bundle instances are no longer supported. You can still add or delete clusters, add or delete VMware ESXi™ servers or NFS storage, and add or remove services for existing instances. You can also view and delete your Security and Compliance Readiness Bundle instances.
{: deprecated}

Specify the following settings for the consolidated cluster.

You can select to include a separate workload cluster in the same way as you order the consolidated cluster.

## Cluster name
{: #scb-orderinginstance-consoli-cluster}

By default, the consolidated cluster name is set to **vcs-_xx_-management**. You can also specify a new cluster name, which must meet the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* The cluster name must start with a lowercase alphabetic character.
* The cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the cluster name is 10 characters.
* The cluster name must be unique within the regulated workload instance.

## CPU model
{: #scb-orderinginstance-consoli-cpu}

You can choose the following CPU models:
* Dual Intel® Xeon® Silver 4210 processor, 20 cores, 2.2 GHz
* Dual Intel Xeon Gold 5218 processor, 32 cores, 2.3 GHz
* Dual Intel Xeon Gold 6248 processor, 40 cores, 2.5 GHz
* Dual Intel Xeon Platinum 8260 processor, 48 cores, 2.4 GHz
* Quad Intel Xeon Gold 6248 processor, 80 cores, 2.5 GHz
* Quad Intel Xeon Platinum 8260 processor, 96 cores, 2.4 GHz

## RAM
{: #scb-orderinginstance-consoli-ram}

You can choose the RAM size from 128 GB, 192 GB, 384 GB, 768 GB, and 1.5 TB.

## Number of bare metal servers
{: #scb-orderinginstance-consoli-bare-metal-number}

For the consolidated cluster:

{{site.data.content.number-of-baremetal-servers-consol}}

For the workload cluster:

{{site.data.content.number-of-baremetal-servers-wkld}}

## Storage
{: #scb-orderinginstance-consoli-storage}

Storage settings are based on your selection of the storage type.

For deployed instances, you can add NFS storage shares to an existing NFS or vSAN cluster. For more information, see [Adding NFS storage to Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs).

### NFS storage
{: #scb-orderinginstance-consoli-nfs}

When you select NFS storage, you can add file-level shared storage for your instance where all shares use the same settings or you can specify different configuration settings for each file share. The number of file shares must be in the range 1 - 100.

Specify the following NFS options:
* **Configure shares individually** - Toggle this switch on to specify different configuration settings for each file share.
* **Number of shares** - When you use the same configuration setting for each file share, specify the number of file shares for the NFS shared storage that you want to add.
* **Size (GB)** - Select the capacity that meets your shared storage needs.
* **Performance** - Select the IOPS (input/output operations per second) per GB based on your workload requirements.
* **Add shared storage** - Select to add individual file shares that use different configuration settings.

Choose performance level options according to your needs.

| Option        | Details       |
|:------------- |:------------- |
| 0.25 IOPS/GB | This option is designed for workloads that are not used often. Example applications include vaulted data, hosting large databases with legacy data, or virtual disk images of virtual memory system as backup. |
| 2 IOPS/GB | This option is designed for most general-purpose workloads. Example applications include hosting small databases, backing up web applications, or virtual machine disk images for a hypervisor. |
| 4 IOPS/GB | This option is designed for higher-intensity workloads that have a high percentage of active data at a time. Example applications include transactional databases. |
| 10 IOPS/GB | This option is designed for the most demanding workload types, such as analytics. Example applications include high-transaction databases and other performance-sensitive databases. This performance level is limited to a maximum capacity of 4 TB per file share. |
{: caption="Table 1. NFS performance level options" caption-side="bottom"}

### vSAN storage
{: #scb-orderinginstance-consoli-vsan}

If you select vSAN storage, specify the following settings.

#### Size for vSAN capacity disks
{: #scb-orderinginstance-consoli-vsan-typesize-capdisks}

Select an option for the capacity disks that you need.

#### Number of vSAN capacity disks
{: #scb-orderinginstance-consoli-vsan-number-capdisks}

Specify the number of capacity disks that you want to add.

#### Size for vSAN cache disks
{: #scb-orderinginstance-consoli-vsan-cachedisks}

Review the **Size for vSAN cache disks** value.

#### Number of vSAN cache disks
{: #scb-orderinginstance-consoli-vsan-number-cachedisks}

Review **Number of vSAN cache disks**.

#### Enable vSAN deduplication and compression
{: #scb-orderinginstance-consoli-vsan-enable-comp}

vSAN storage depends on the number of servers and your total disk capacity, and the use of deduplication and compression.

The amount of storage reduction from deduplication and compression depends on many factors, including the type of data stored and the number of duplicate blocks. Larger disk groups tend to provide a higher deduplication ratio. For more information, see [Using deduplication and compression](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vsan.doc/GUID-3D2D80CC-444E-454E-9B8B-25C3F620EFED.html){: external}.
{: note}

#### vSAN license (BYOL only)
{: #scb-orderinginstance-vsan-storage-license}

{{site.data.content.attnnote-byol}}

If you are a BYOL user, provide your own vSAN license key. Toggle the **BYOL** switch to **Enabled** and enter your license key.

If your initial cluster is a vSAN cluster, any additional vSAN clusters use the same vSAN license and have the same configuration as the initial one. This statement is also true for any initial or extra clusters in the instance for which you select vSAN. The first time, you must provide the vSAN license and the edition. The next time that you select vSAN for a new cluster, the license you initially chose will be reused.

## Networking type
{: #scb-orderinginstance-consoli-private-nics}

Select **Public and private network** or **Private network only** for the consolidated cluster.

## Uplink speed
{: #scb-orderinginstance-consoli-uplink}

{{site.data.content.uplink-speed-options-list}}

{{site.data.content.simpletable-uplink-speed-locations-ap}}

{{site.data.content.simpletable-uplink-speed-locations-eur}}

{{site.data.content.simpletable-uplink-speed-locations-naeast}}

{{site.data.content.simpletable-uplink-speed-locations-nasouth}}

## VLANs
{: #scb-orderinginstance-consoli-vlans}

Network settings are based on your selection of **Order new VLANs** or **Select existing VLANs**.

One public VLAN and two private VLANs are required for your instance order. The two private VLANs are trunked into each {{site.data.keyword.cloud_notm}} bare metal server.

### Order new VLANs
{: #scb-orderinginstance-consoli-new-vlans}

Select to order one new public VLAN and two new private VLANs.

### Select existing VLANs
{: #scb-orderinginstance-consoli-existing-vlans}

Depending on the {{site.data.keyword.cloud_notm}} data center that you selected, existing public and private VLANs might be available.

When you select to reuse existing public and private VLANs, specify the VLANs and subnets:
* **Public VLAN** is for public network access. If you select the **Allocate a new one** option for this field, a new public VLAN is allocated automatically. This field is only available on the **Public and private network** tab.
* **Public primary subnet** is assigned to physical hosts for public network access. If you select the **Auto assigned** option for this field, a new public primary subnet is selected automatically and a new one is created if necessary. This field is only available on the **Public and private network** tab.
* **Private VLAN** is for connectivity among the data centers and services within the {{site.data.keyword.cloud_notm}}. If you select the **Allocate a new one** option for this field, a new private VLAN is allocated automatically.
* **Private primary subnet** is assigned to physical hosts for management traffic. If you select the **Auto assigned** option for this field, a new private primary subnet is selected automatically and a new one is created if necessary.
* **Secondary private VLAN** is for VMware features such as vSAN. You can select an existing secondary private VLAN or select to allocate a new one.

Ensure that the firewall configuration on the selected VLANs does not block the management data traffic. Also, ensure that all the VLANs that you select are in the same pod. ESXi servers cannot be provisioned on mixed-pod VLANs.
{: important}  

Optionally, use **Advanced settings** to configure portable subnets for VLANs.

Use the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** tabs to specify the **Portable subnet** for each applicable purpose. If you select the **Allocate a new one** option for this field, a new portable subnet is allocated automatically.

#### Notes
{: #scb-orderinginstance-consoli-existing-vlans-notes}

* You must complete the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings before you can configure portable subnets.
* The number of portable subnets is displayed under **Advanced settings** after you save the portable subnet settings. Click **Portable subnets settings** to edit the settings.
* The saved portable subnet settings are cleared if you change the **Public VLAN**, **Private VLAN**, or **Secondary private VLAN** settings.

{{site.data.keyword.vmwaresolutions_short}} takes control of the entire subnet and you can't use any IP addresses in the subnet.
{: important}
