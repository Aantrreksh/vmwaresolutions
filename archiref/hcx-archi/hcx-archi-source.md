---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware HCX source-side architecture
{: #hcx-archi-source}

Review the source architecture for the VMware® HCX™ components that are typically deployed in the customer data center. The tasks that can be accomplished and the features that support and enhance migration and network extension are also presented.

* HCX owns the source and destination encryption and decryption processes. It ensures consistent security and providing admission for hybrid workflows such as virtual machine (VM) migration and network extension.
* HCX creates an optimized, software-defined WAN to increase stretched network performance, enabling performance that approaches LAN speed.
* HCX also enables bidirectional workload migration to {{site.data.keyword.cloud}} Networking services.
* HCX integrates with vSphere vCenter and is managed from the vSphere Web Client.

## Understanding HCX
{: #hcx-archi-source-understand-hcx}

HCX supports a many-to-many relationship between on-premises vCenters and {{site.data.keyword.cloud_notm}}. VMware vCenter® in Linked Mode is supported.

During the installation, the HCX Manager virtual appliance is imported and configured as a plug-in for the on-premises vCenter. This plug-in is then used to configure the software-defined WAN service deployment. The automated configuration provisions each hybrid service appliance as a VM in the on-premises vCenter, and deploys a corresponding VM in {{site.data.keyword.cloud_notm}}.

A successful deployment requires the following items:
* Sufficient resources for the virtual appliances.
* The network must allow the appliances to communicate with both local and remote virtual appliances, and other VMs.

## Deployment overview
{: #hcx-archi-source-deployment-ovw}

The HCX Manager VM is installed first, and it manages the installation of any other service VM appliances on premises and in the cloud.

The following steps are basic installation tasks:
1. Obtain HCX Connector virtual appliance OVA file.
2. From the vSphere Web Client, install the HCX Manager virtual appliance in the on-premises vCenter that connects to {{site.data.keyword.cloud_notm}}.
3. From the vSphere Web Client, register an {{site.data.keyword.cloud_notm}} endpoint with the HCX plug-in. Registration establishes the one-to-one relationship between the on-premises HCX and the HCX instance on {{site.data.keyword.cloud_notm}}.
4. Install and configure the service's virtual appliances.
5. For each appliance installed on premises, the installer provisions a corresponding service virtual appliance in the target {{site.data.keyword.cloud_notm}}.
6. After the installation, HCX Manager controls both local and remote service virtual appliances. In the {{site.data.keyword.cloud_notm}}, HCX manages the provisioned Software-Defined WAN components as a service.

### Deployment component performance considerations
{: #hcx-archi-source-perf-consid}

Architecture planning includes the VMs to be migrated, the networks that are used for VM traffic, and the networks to be extended.

The following settings are the maximum and minimum values for the deployment components:
* vCenter. The HCX Manager appliance must be installed on the vCenter that requires hybrid services. You can have one HCX deployment per vCenter only. This restriction applies to linked mode. The HCX management appliance is only installed in the primary vCenter. HCX supports up to five registered vCenters in linked mode.
* Cloud registrations. The maximum number of cloud endpoints is ten. To find the number of endpoints, Hybrid Cloud Services tracks vCenter connections to the cloud.

### HCX virtual appliances
{: #hcx-archi-source-hcxva}

The installation package is an OVA file that contains the Hybrid Cloud Services plug-in. This Hybrid Cloud Services management appliance is installed and configured and then used to configure the service appliance VMs:
* HCX Cloud and HCX Connector
* HCX-IX Interconnect Appliance (HCX-IX)
* HCX WAN Optimization Appliance (HCX-WO)
* HCX Network Extension Virtual Appliance (HCX-NE)

### HCX Connector
{: #hcx-archi-source-hcxm}

The HCX Connector plug-in is deployed on-premises only. It manages the service virtual appliances for the SD-WAN. The HCX Connector virtual appliance is an extension to the source vCenter and is deployed as a VM. This appliance’s file structure contains all the hybrid service virtual appliances. The HCX Connector oversees the deployment and configuration of the HCX-IX, the HCX-NE, and HCX-WO virtual appliances both on-premises and in the cloud.

The virtual appliance can be installed with either thin provisioning or thick provisioning for the hard disk drive. By default, hard disk drives for the service virtual appliances are thinly provisioned.

After the service, virtual appliance configuration, and deployment are done, log in to this VM to use the Hybrid Cloud Services management portal.

### HCX-IX Interconnect Appliance
{: #hcx-archi-source-hcg}

The HCX-IX Interconnect Appliance establishes and maintains a secure channel between vSphere and the {{site.data.keyword.cloud_notm}}.

HCX uses strong encryption to bootstrap a site-to-site connection to {{site.data.keyword.cloud_notm}}. The secure channel between vSphere and {{site.data.keyword.cloud_notm}} achieves multitenancy for vSphere protocols that are not tenant aware, and to prevent networking "middle mile" security problems.

The HCX-IX Interconnect Appliance also incorporates vSphere replication technology to perform bidirectional migration.

### HCX WAN Optimization Appliance
{: #hcx-archi-source-wan-opt}

HCX also provides software-defined WAN Optimization. The HCX WAN Optimization appliance is a highly recommended component that performs WAN conditioning to reduce effects of latency. It also incorporates Forward Error Correction to negate packet loss scenarios, and deduplication of redundant traffic patterns. Altogether, these reduce bandwidth use and ensure the best use of available network capacity to expedite data transfer to and from {{site.data.keyword.cloud_notm}}.

VM migration relies on the combination of HCX-IX Interconnect Appliance and HCX WAN Optimization appliance to achieve unparalleled mobility between vSphere on-premises and {{site.data.keyword.cloud_notm}}.

### HCX Network Extension Virtual Appliance
{: #hcx-archi-source-layer-2-conc}

The Network Extension Service is provided by the HCX Network Extension Virtual Appliance. It extends a Layer 2 network from the on-premises vSphere data center to {{site.data.keyword.cloud_notm}} and enables seamless migration between the data center and the cloud. The HCX Network Extension Virtual Appliance is required to stretch the on-premises network to {{site.data.keyword.cloud_notm}}.

The HCX Network Extension Virtual Appliance has two interfaces:
* Internal trunk interface - Handles VM traffic on-premises for the extended networks by using a translational bridge mapping to a corresponding stretched network in {{site.data.keyword.cloud_notm}}.
* Uplink interface - HCX uses this interface to send encapsulated overlay traffic to and from {{site.data.keyword.cloud_notm}}. Application data travels through this interface.

### IP address requirements
{: #hcx-archi-source-ip-req}

To deploy the HCX, the proper number of IP addresses must be available both on-premises and in the target {{site.data.keyword.cloud_notm}}.

* vMotion address
   Maintaining a separate network for vMotion is a common practice in the on-premises data center. The Cloud Gateway must have access to the vMotion network. If it does not, an extra IP address is needed to communicate with the vMotion network.

* On-premises
   * One IP address for the HCX Connector appliance.
   * One for each HCX-IX Interconnect Appliance, add one for a separate vMotion network (if applicable).
   * One for each HCX Network Extension Virtual Appliance.

* {{site.data.keyword.cloud_notm}}
   * Two IP addresses per HCX Connector appliance connected to {{site.data.keyword.cloud_notm}}. The addresses can be used to connect to the internet or one or more {{site.data.keyword.cloud_notm}} Direct-Link connections.
   * Add one for a separate vMotion network connection (if applicable).

### Proximity routing
{: #hcx-archi-source-prox-routing-feat}

Proximity routing is a networking feature that can be enabled when the HCX-IX is configured. Proximity routing is only available with NSX-V target.

After 21 June 2022, provisioning new {{site.data.keyword.vcf-auto}} instances with NSX–V is no longer supported. However, you can add hosts and clusters to your existing NSX–V deployments. IBM strongly recommends that clients immediately assess their NSX–V networks and plan a much earlier migration to NSX–T.
{: note}

Proximity routing ensures forwarding between VMs that are connected to stretched and routed networks, both on-premises and in the cloud, is symmetrical. This feature requires Dynamic Routing to be configured between the customer premises and the cloud.

When users extend their networks to the cloud, Layer 2 connectivity is stretched onto {{site.data.keyword.cloud_notm}}. However, without route optimization, Layer 3 communication requests must return to the on-premises network origin to be routed. This return trip is called `tromboning` or `hairpinning`.

Tromboning is inefficient because packets must travel back and forth between the network origin and the Cloud, even when both the source and destination VMs are in the Cloud. In addition to inefficiency, if the forwarding path includes stateful firewalls, or other inline equipment that must see both sides of the connection, communication might fail. VM communication (without route optimization) failure occurs when the egress path that exits the cloud can be either the stretched Layer 2 network or through the NSX Edge Gateway. The on-premises network does not know about the stretched network "shortcut." This problem is called asymmetric routing. The solution is to enable proximity routing so the on-premises network can learn the routes from {{site.data.keyword.cloud_notm}}.

To prevent tromboning, HCX uses intelligent route management to choose routes appropriate to the VM state. The Cloud Gateway maintains an inventory of VMs in the cloud and it understands the VM states, which can be one of the following values:
* Transferred to the cloud with vMotion (zero-downtime migration).
* Migrated to the cloud by using host-based replication (low-downtime migration).
* Created in the cloud (on a stretched network).

For more information about HCX on-premises deployments, see the [VMware HCX documentation](https://docs.vmware.com/en/VMware-HCX/index.html){: external}.
