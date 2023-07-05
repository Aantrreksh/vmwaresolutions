---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-20"

keywords: vmware vSphere order instance, order vSphere, order vmware vSphere instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Storage (vSAN only)
{: #vs_orderinginstances-storage-settings}

The **Storage** section of your VMware vSphere instance order is applicable only if you select the VMware vSAN component.

* For orders without VMware vSAN™, VMware ESXi™ servers are ordered with a 12-disk chassis, with two disks for the ESXi operating system (OS).
* For orders with vSAN, ESXi servers are ordered with a 12-disk chassis and two disks are ordered for caching. The ESXi OS is placed on a single M.2 solid-state drive that does not use a disk bay. These settings are configured by default and cannot be changed. You can order more capacity disks by selecting **Size for vSAN capacity disks** and **Number of vSAN capacity disks**.

Specify the following settings for the vSAN component:
* **Size for vSAN capacity disks** - Select an option for the capacity disks that you need.
* **Number of vSAN capacity disks** - Specify the number of capacity disks that you want to add.
* If you want to add more capacity disks, select the **High performance with Intel Optane** checkbox. This option provides two extra capacity disk bays, which are useful for workloads that require less latency and higher IOPS throughput.

   The **High performance with Intel Optane** option is available only for existing instances with VMware vSphere® 6, and for Skylake and dual-processor Cascade Lake CPU models.
   {: note}

* Review the **Size for vSAN cache disks** and **Number of vSAN cache disks** values.

## Enable vSAN deduplication and compression
{: #vs_orderinginstance-storage-enable-comp}

vSAN storage depends on the number of servers and your total disk capacity, and the use of deduplication and compression.

The amount of storage reduction from deduplication and compression depends on many factors, including the type of data stored and the number of duplicate blocks. Larger disk groups tend to provide a higher deduplication ratio. For more information, see [Using deduplication and compression](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vsan.doc/GUID-3D2D80CC-444E-454E-9B8B-25C3F620EFED.html){: external}.
{: note}

## Related links
{: #vs_orderinginstances-storage-related}

* [Network interface](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-network-interface-settings)
* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
