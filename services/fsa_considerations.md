---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-11"

keywords: FortiGate security, FortiGate Security Appliance, tech specs FortiGate

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# FortiGate Security Appliance
{: #fsa_considerations}

Automated deployment of the FortiGate Security Appliance service is no longer supported. For a similar service, consider the [FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations), which is deployed automatically.
{: deprecated}

FortiGate Security Appliance has a pair of FortiGate Security Appliance (FSA) 300 series devices in a highly available mode. This deployment provides the following services to protect all the servers and virtual machines on the public VLAN of your instances:
* Firewall
* Routing
* NAT
* VPN
{: shortdesc}

You can manage this service by using the FortiOS Web Client or the command-line interface through SSH.

## Technical specifications for FortiGate Security Appliance
{: #fsa_considerations-specs}

The following components are included in the FortiGate Security Appliance service:

### Hardware
{: #fsa_considerations-hardware}

The FortiGate 300 series Security Appliance.

### High availability
{: #fsa_considerations-ha}

Two appliances are deployed in active-passive configuration.

### Networking
{: #fsa_considerations-networking}

* Dual 1 GbE bonded on both upstream and downstream networks
* One new upstream {{site.data.keyword.cloud}} public VLAN
* One existing downstream {{site.data.keyword.cloud_notm}} public VLAN

## Managing FortiGate Security Appliance
{: #fsa_considerations-managingfsa}

After the FortiGate Security Appliance service is installed successfully, you can manage and configure firewall rules for the FSA from the FortiGate console.

Ensure the FSA firewall rules are defined to allow outbound HTTPS (TCP port 443) communications that are initiated by management components such as the Zerto Virtual Manager to communicate with the external management database on the {{site.data.keyword.cloud}} infrastructure over the internet. The outbound HTTPS (TCP port 443) communications originate from the public IP address of the management services VMware NSX Edge Services Gateway (ESG) in your instance.
{: important}

### Accessing the FortiGate 300 series console
{: #managingfsa-access-console}

To manage the FortiGate Security Appliance service, you must access the FortiGate® 300 series console in one of the following ways:
* Log in to the FortiOS Web Client by using the credentials that you can find on the FortiGate Security Appliance service details page.
* Access the console through SSH connection by using the credentials that you can find on the FortiGate Security Appliance service details page.

For more information, see [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Considerations when you delete FortiGate Security Appliance
{: #fsa_considerations-remove}

Review the following considerations before you delete the FortiGate Security Appliance service:
* Deleting the FortiGate Security Appliance service deletes the public VLAN that was added.
* During the service deletion, your instance might not be able to access the internet temporarily.
* All FortiGate rules to permit, inspect, block, and route NAT traffic are deleted together with the Fortinet service. If you have any NAT rules, you must reconfigure them.
