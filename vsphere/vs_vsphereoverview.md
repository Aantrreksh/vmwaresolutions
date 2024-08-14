---

copyright:

  years:  2016, 2024

lastupdated: "2024-08-12"

keywords: vcf flexible, vcf for classic flexible, tech specs flexible instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.vcf-flex-short}} overview
{: #vs_vsphereoverview}

{{site.data.keyword.vcf-flex}} is a streamlined and optimized ordering platform for VMware®. With this platform, you can build your own {{site.data.keyword.IBM}}-hosted VMware environment by customizing and ordering the VMware-compatible hardware based on your selected VMware components.
{: shortdesc}

The {{site.data.keyword.vmwaresolutions_full}} console filters the hardware automatically, based on the VMware components that you select. For example, when you create a new all-flash VMware vSAN™ cluster, only the hardware that is validated against the [VMware Compatibility Guide](https://www.vmware.com/resources/compatibility/search.php){: external} is presented.

{{site.data.keyword.vcf-flex}} does not automate the installation, configuration, and bring-up of the optional VMware components. The platform allows maximum of flexibility to design and build your hosted VMware environment while you incorporate VMware-compatible hardware.

Use this offering to create a new instance of VMware ESXi™ servers or scale out an existing instance of ESXi servers in an {{site.data.keyword.cloud_notm}} data center. Depending on the VMware components that you select, you can start with just one ESXi server and then scale the instance later as needed.

## Technical specifications for Flexible instances
{: #vs_vsphereoverview-specs}

Review the components for {{site.data.keyword.vcf-flex-short}} instances.

The availability and pricing of standardized hardware configurations might vary based on the {{site.data.keyword.cloud_notm}} data center that is selected for deployment.
{: note}

### VMware components
{: #vs_vsphereoverview-specs-vmware-components}

If you are a BYOL user, you must provide your own license keys for all VMware components.

   {{site.data.content.attnnote-byol}}

Select licenses for the following VMware components:
* VMware vSphere Enterprise Plus 7.0u3 or 8.0u2
* The following VMware components are optional:
   * VMware vCenter Server®
   * VMware NSX®
   * VMware vSAN
   * VMware Aria® Automation™
   * VMware Aria® Operations™
   * VMware Aria Operations™ for Logs

### Bare metal server
{: #vs_vsphereoverview-specs-bare-metal}

The options available depend on whether you selected the VMware vSAN component.
{: note}

You can order one or more {{site.data.keyword.cloud_notm}} bare metal servers with one of the following configurations:
* **Cascade Lake** - 4-CPU Intel® Cascade Lake generation servers (Quad Intel Xeon® 6200/8200 series) or 2-CPU Intel® Cascade Lake generation servers (Dual Intel Xeon® 4200/5200/6200/8200 series) with your selected RAM size.
* **SAP-certified Cascade Lake** - 2-CPU Intel Cascade Lake generation servers (Dual Intel Xeon 5200/6200/8200 series).

Additionally, the following disk and networking specifications apply:
* 10 Gbps and 25 Gbps dual public and private network uplinks
* One RAID disk controller

### Networking
{: #vs_vsphereoverview-specs-network}

* One VLAN (Virtual LAN) public VLAN and two private VLANs
* (Optional) An HA-pair of FortiGate® Physical Appliance devices

### Storage
{: #vs_vsphereoverview-specs-storage}

User-customized storage for vSAN configuration when the VMware vSAN component is selected:
* Storage disk options - 960 GB SSD, 1.9 TB SSD, 3.8 TB SSD, or 7.68 TB SSD.
* Disk quantity options - 2, 4, 6, 8, or 10. Additionally, two cache disks of 960 GB are also ordered per host.

   3.8 TB SSD (Solid-State Disk) drives are supported when they are made available in a data center.
   {: note}

## Technical specifications for expansion nodes for {{site.data.keyword.vcf-flex-short}} instances
{: #vs_vsphereoverview-expansion-node-specs}

Each {{site.data.keyword.vcf-flex-short}} instance expansion node deploys and incurs charges for the following components in your {{site.data.keyword.slportal}} account.

### Hardware for expansion nodes
{: #vs_vsphereoverview-expansion-node-specs-hardware}

One {{site.data.keyword.cloud_notm}} bare metal server with the hardware configuration presented in [Technical specifications for Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview#vs_vsphereoverview-specs).

### Networking for expansion nodes
{: #vs_vsphereoverview-expansion-node-specs-network}

One {{site.data.keyword.cloud_notm}} bare metal server with the networking configuration presented in [Technical specifications for Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview#vs_vsphereoverview-specs).

### VMware components for expansion nodes
{: #vs_vsphereoverview-expansion-node-specs-vmware-components}

* One {{site.data.keyword.cloud_notm}} bare metal server with VMware vSphere Enterprise Plus 7.0 or 6.7u3 for V4.7 and earlier.
* Optional VMware components presented in [Technical specifications for Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview#vs_vsphereoverview-specs).

You must manage the ESXi servers, optional VMware components, and extra hardware that is ordered and delivered to your {{site.data.keyword.cloud_notm}} account only from the {{site.data.keyword.slportal}}. After you create a new instance in the {{site.data.keyword.vmwaresolutions_short}} console, you can return to the console, and add capacity to the new instance. For more information, see [Adding ESXi servers to Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_addingservers).
{: important}

## Related links
{: #vs_vsphereoverview-related}

* [{{site.data.keyword.vcf-flex-short}} BOM](/docs/vmwaresolutions?topic=vmwaresolutions-vs_bom)
* [Planning for Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_planning)
* [Ordering Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req)
* [Adding ESXi servers to Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_addingservers)
