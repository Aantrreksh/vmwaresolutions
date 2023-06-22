---

copyright:

  years:  2022, 2023

lastupdated: "2023-06-22"

keywords: cyber recovery, cyber recovery consolidated cluster, cyber recovery consolidated settings, cyber recovery instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Consolidated and workload clusters
{: #cr_orderinginstance-consolidwkld}

Cyber Recovery instances are deployed with a consolidated cluster for VMware vSphere® 7, in which all the VMware® management components and user workloads run.

You can also order an extra workload cluster.

## Cluster name
{: #cr_orderinginstance-consolidwkld-cluster-name}

* For the consolidated cluster, the cluster name is preset to **_instance name_-consolidated**.
* For the workload cluster, the cluster name is preset to **_instance name_-workload**.

{{site.data.content.cluster-name-requirements-list}}

## Bare metal server settings
{: #cr_orderinginstance-consolidwkld-bare-metal-settings}

Bare metal settings are based on your data center selection and bare metal server configuration. When you size the capacity of your servers, consider your current requirements, and include extra capacity to accommodate anticipated growth. For more information about sizing, see [Exporting VMware inventory](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-inventory-export).

## Data center location
{: #cr_orderinginstance-consolidwkld-dc-location}

Select the {{site.data.keyword.cloud}} data center settings. For more information, see [Region and data center locations for resource deployment](/docs/overview?topic=overview-locations).

### Geography
{: #cr_orderinginstance-consolidwkld-dc-region}

Select the region where your cluster or instance is hosted.

### Data center
{: #cr_orderinginstance-consolidwkld-dc-datacenterloc}

Select the {{site.data.keyword.cloud_notm}} data center where the cluster is hosted.

### Pod
{: #cr_orderinginstance-consolidwkld-dc-pod}

Select the {{site.data.keyword.cloud_notm}} data center pod where you want to deploy your resources. Keep the default pod selection unless you have specific reasons to choose a different pod.

## CPU generation
{: #cr_orderinginstance-consolidwkld-cpu-generation}

Select either Cascade Lake or SAP-certified. Cascade Lake is the default.

## CPU model
{: #cr_orderinginstance-consolidwkld-cpumodel}

Select the CPU model. For Cascade Lake, the default is Dual Intel® Xeon® Platinum 8260 with 48 cores and 2.40 Ghz.

### Cascade Lake
{: #cr_orderinginstance-consolidwkld-cascade}

{{site.data.content.cascade-para-intro}}

| CPU model     | Cores     | GHz     | RAM sizes   |
|:------------- |:----------|:--------|:----------- |
| Dual Intel Xeon Silver 4210 processor | 20 | 2.2 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 processor | 32 | 2.3 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 processor | 40 | 2.5 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6250 processor | 16 | 3.9 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 processor | 48 | 2.4 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 processor | 80 | 2.5 | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 processor | 96 | 2.4 | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 1. Options for Cascade Lake bare metal servers - NSX-T instances" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NSX-T instances"}
{: tab-group="Cascade Lake Intel servers"}
{: #simpletabtable-cascade-nsxt}

### SAP-certified
{: #cr_orderinginstance-consolidwkld-sap}

{{site.data.content.sap-para-intro}}

| CPU model     | Cores     | GHz     | RAM sizes   |
|:------------- |:----------|:--------|:----------- |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.NW192) | 32 | 2.3 | 192 GB |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.NW384) | 32 | 2.3 | 384 GB |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.NW768) | 40 | 2.5 | 768 GB |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.NW768_v2) | 48 | 2.4 | 768 GB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.NW1500) | 56 | 2.7 | 1.5 TB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.NW3000) | 56 | 2.7 | 3 TB |
{: caption="Table 2. Options for SAP-certified bare metal servers - NetWeaver" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NetWeaver"}
{: tab-group="SAP-certified Intel servers"}
{: #simpletabtable-sap-netweaver}


| CPU model     | Cores     | GHz     | RAM sizes |
|:------------- |:----------|:--------|:--------- |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.H2.192) | 32 | 2.3 | 192 GB |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.H2.384) | 32 | 2.3 | 384 GB |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.H2.768) | 40 | 2.5 | 768 GB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H2.1500) | 56 | 2.7 | 1.5 TB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H2.3000) | 56 | 2.7 | 3 TB |
| Quad Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H4.3000) | 112 | 2.7 | 3 TB |
| Quad Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H4.6000) | 112 | 2.7 | 6 TB |
{: caption="Table 2. Options for SAP-certified bare metal servers - HANA" caption-side="bottom"}
{: tab-title="HANA"}
{: tab-group="SAP-certified Intel servers"}
{: class="simple-tab-table"}
{: #simpletabtable-sap-hana}

## Number of bare metal servers
{: #cr_orderinginstance-consolidwkld-bare-metal-number}

Select the number of bare metal servers. The default is three.

* All servers that you order have the same configuration.
* If you are planning to use vSAN™ storage, you can order 3 - 20 servers.
* A minimum limit of three servers applies for VMware NSX-T clusters.
* For production workloads, a minimum of three servers is recommended.

## Storage
{: #cr_orderinginstance-consolidwkld-storage-settings}

Storage settings are based on your selection of bare metal server configuration and the storage type.

For deployed instances, you can add NFS storage shares to an existing NFS or vSAN cluster. For more information, see [Adding NFS storage to vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingnfs).

### NFS storage
{: #cr_orderinginstance-consolidwkld-nfs-storage}

When you select **NFS storage**, you can decide on one of the following options:

* Add file-level shared storage for your instance, where all shares use the same settings
* Specify different configuration settings for each file share.

The number of file shares must be in the range 1 - 100.

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

vSAN is available for the **Cascade Lake** bare metal configuration only.

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

#### vSAN license
{: #cr_orderinginstance-consolidwkld-vsan-storage-license}

Use the IBM-provided VMware license for the vSAN component, which is included with purchase.

Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide** and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.
{: important}

If your initial cluster is a vSAN cluster, any additional vSAN clusters use the same vSAN license and have the same configuration as the initial one. This statement is also true for any initial or additional clusters in the instance for which you select vSAN. The first time, you're prompted for the vSAN license (BYOL or purchased) and the edition. The next time that you select vSAN for a new cluster, the license that is chosen initially is reused.

## Networking type
{: #cr_orderinginstance-consolidwkld-public-private-network}

Select **Public and private network** or **Private network only**.

## Uplink speed
{: #cr_orderinginstance-consolidwkld-uplink}

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
{: caption="Table 4. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: #simpletable-uplink-speed-locations}

## VLANs
{: #cr_orderinginstance-consolidwkld-vlans}

Network settings are based on your selection of **Order new VLANs** or **Select existing VLANs**. For your first purchase of Cyber Recovery, only the **Order new VLANs** selection is available.

One public VLAN and two private VLANs are required for your instance order. The two private VLANs are trunked into each {{site.data.keyword.cloud_notm}} bare metal server.

### Order new VLANs
{: #cr_orderinginstance-consolidwkld-new-vlans}

When you select to **Order new VLANs**, one new public VLAN and two new private VLANs are ordered.

### Select existing VLANs
{: #cr_orderinginstance-consolidwkld-existing-vlans}

For your first purchase of Cyber Recovery, only the **Order new VLANs** selection is available.
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
* [Procedure to order Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance-order-procedure)
