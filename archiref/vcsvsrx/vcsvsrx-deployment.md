---

copyright:

  years:  2019, 2023

lastupdated: "2023-09-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# vSRX deployment
{: #vcsvsrx-deployment}

Deploy the VMware vCenter Server® instance before the vSRX edge gateway appliance order is placed.

## Ordering Juniper gateway devices
{: #vcsvsrx-deployment-order-gateway}

The following procedure assumes that you are deploying the IaaS KVM-based Juniper® vSRX HA cluster. If you want to build your own gateway by using VMware ESXi™, then order the No-OS gateway option instead. For more information, see [Ordering a Bring Your Own Gateway Appliance](/docs/gateway-appliance?topic=gateway-appliance-order-byoa).

Open the [{{site.data.keyword.cloud_notm}} infrastructure customer portal](https://control.softlayer.com), then select **Infrastructure > Network > Gateway Appliances > Create Gateway**.
* Gateway vendor - Juniper
* Gateway Appliance
   * Hostname - Provide hostname for node 1 in the gateway cluster. For example, `gateway01`. Select a hostname consistent with the existing vCenter Server naming convention since the vSRX nodes are manually added to the vCenter Server AD/DNS server for hostname resolution.
   * Domain - Enter the applicable domain name for the gateway cluster. For example, `myvcsdomain.local`, where `myvcsdomain.local` is the domain that is assigned to the previously deployed vCenter Server instance.
   * Select High availability.
      * HA hostname - Provide hostname for node 2 in the gateway cluster. For example, `gateway02`. Select a hostname consistent with the existing vCenter Server naming convention since the vSRX nodes are manually added to the vCenter Server AD/DNS server for hostname resolution.
      * HA Domain - Verify that this value is the same domain name that is provided for node1. For example, `myvcsdomain.local`
* Location
   * Select geography, for example, `NA South`
   * Select dataCenter, for example, `Dallas 10`
* POD
   * Select POD where existing vCenter Server instance is deployed to. For example, `dal10.pod01`
   * Ensure that you order the vSRX in the same POD as your vCenter Server instance. VLANs don't span PODs so you must deploy to the correct POD.
   * Determining `SoftLayer_Network_Pod`

   The setting `SoftLayer_Network_Pod` refers to a portion of a data center that share a Backend Customer Router (BCR) and usually a front-end counterpart that is known as a Frontend Customer Router (FCR). A Pod primarily denotes a logical location within the network and the physical aspects that support networks, in contrast to representing a specific physical location.

   A pod is identified by a name, which is unique. A Pod name follows the format `dddnn.podii`, where `ddd` is a data center code, `nn` is the data center number, and `pod` is a literal string. The value `ii` is a two-digit number, zero-padded to the left, which corresponds to a Backend Customer Router (BCR) of the data center. For example,

      `dal09.pod01` is Dallas 9, Pod 1 (that is, bcr01)
      `sjc01.pod04` is San Jose 1, Pod 4 (that is, bcr04)
      `ams01.pod01` is Amsterdam 1, Pod 1 (that is, bcr01)

* Select Dual Processor hardware option - Intel Xeon 5120, 28 core
* RAM - 192 GB
* Add-ons
   * Accept default values.
* Storage Disks
   * Type - RAID 1
   * Number of disks - 2
   * Disk Media - SATA (preselected)
   * Disk Size - 4 TB.
* Network interface
   * Uplink Port Speeds - 10 Gbps Public and Private Network Uplinks.
   * Ensure that you enable both public and private NICs (four ports total).
   * Add-ons - accept default values. Optionally select IPv6 address.

Review order and click **Create**. Provisioning takes three to four hours.

## Post deployment
{: #vcsvsrx-deployment-post}

If you deployed the IaaS KVM-based Juniper vSRX HA Cluster, you can continue with configuration of the vSRX cluster as described in [{{site.data.keyword.cloud_notm}} performing vSRX basics](/docs/vsrx?topic=vsrx-performing-ibm-cloud-juniper-vsrx-basics).

If you opted to deploy the No-OS gateway offering, then follow the guidance in [Installing an operating system on the gateway](/docs/gateway-appliance?topic=gateway-appliance-order-byoa#installing-an-operating-system-on-the-gateway) to prepare the hosts for your appliance.

## Related links
{: #vcsvsrx-deployment-related}

* [Getting started with {{site.data.keyword.cloud_notm}} Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started)
* [Juniper Networks vSRX deployment guide for VMware](https://www.juniper.net/documentation/en_US/vsrx/information-products/pathway-pages/security-vsrx-vmware-guide-pwp.html){: external}
* [Juniper Networks requirements for vSRX on VMware](https://www.juniper.net/documentation/en_US/vsrx/topics/reference/general/security-vsrx-vmware-system-requirement.html){: external}
* [Juniper Networks vSRX installation with vSphere Web Client](https://www.juniper.net/documentation/en_US/vsrx/topics/task/installation/security-vsrx-vsphere-client-installing.html){: external}
* [Juniper Networks configuring a vSRX Chassis Cluster in Junos OS](https://www.juniper.net/documentation/en_US/vsrx/topics/task/multi-task/security-vsrx-chassis-cluster-configuring.html){: external}
* [Configure ECMP on VMware NSX](https://letsv4real.com/2016/09/23/configure-ecmp-on-vmware-nsx/){: external}
