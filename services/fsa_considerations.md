---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-12"

keywords: FortiGate security, FortiGate Security Appliance, tech specs FortiGate

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# FortiGate Security Appliance
{: #fsa_considerations}

Automated deployment of the FortiGate Security Appliance service is no longer supported. For a similar service, consider the [FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations), which is deployed automatically.
{: deprecated}

The FortiGate Security Appliance service deploys a pair of FortiGate Security Appliance (FSA) 300 series devices in a highly available mode. This deployment provides the following services to protect all the servers and virtual machines on the public VLAN of your instances:
* Firewall
* Routing
* NAT
* VPN
{: shortdesc}

You can manage this service by using the FortiOS Web Client or the command-line interface through SSH.

## Technical specifications for FortiGate Security Appliance
{: #fsa_considerations-specs}

The following components are ordered and included in the FortiGate Security Appliance service:

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

## Considerations when you install FortiGate Security Appliance
{: #fsa_considerations-install}

Review the following considerations before you install the FortiGate Security Appliance service:
* Ensure that the {{site.data.keyword.cloud_notm}} account that you're using has the **Hardware Firewall** permission. This permission is required to edit or view firewall logs and settings for the FortiGate Security Appliance service of your instance.
* If you want to add the FortiGate Security Appliance service to a deployed instance, ensure that no other firewall from {{site.data.keyword.cloud_notm}} infrastructure is already in place on the public VLAN of the instance.
* Installing the FortiGate Security Appliance service adds a new public VLAN.
* During the service deployment, your instance might not be able to access the internet temporarily.
* After the FortiGate Security Appliance service is installed successfully, you can manage and configure firewall rules for the FSA from the FortiGate console. Ensure the FSA firewall rules are defined to allow outbound HTTPS (TCP port 443) communications that are started by management components such as the Zerto Virtual Manager to communicate with the external management database on {{site.data.keyword.cloud_notm}} over the internet. The outbound HTTPS (TCP port 443) communications originate from the public IP address of the management services VMware NSX Edge Services Gateway (ESG) in your instance.
* You must manage the FortiGate Security Appliance configuration carefully to allow only necessary communications and deny all other communications.
* If you order extra clusters, the public VLANs for these newly added clusters do not have the HA-pair of Security Appliances.

### Notes for installation considerations
{: #fsa_considerations-install-notes}

Review the following notes about installation:
* Before the service is installed in your environment, a check is made against the available capacity of the default cluster in the environment to ensure that the service components can fit.
* If the capacity check fails, the service is not installed and the service status is set to **Capacity Validation Failed** on the console. In addition, a console message with more details is displayed and you are notified by email.
* To install the service, you must increase the capacity in your default cluster. You can either add more hosts or free up RAM, CPU, or disk space, and then add the service again in the console. After that, delete the existing service in the **Capacity Validation Failed** state by clicking the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to it.

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
