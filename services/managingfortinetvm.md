---

copyright:

  years:  2016, 2024

lastupdated: "2024-01-31"

keywords: FortiGate console, FortiGate VA, login FortiGate console

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing FortiGate Virtual Appliance
{: #managingfortinetvm}

## Accessing the FortiGate console
{: #managingfortinetvm-access-console}

To manage the FortiGate® Virtual Appliance service, you must access the FortiGate console in one of the following ways:
* Log in to the FortiOS Web Client by using the credentials that you can find on the FortiGate Virtual Appliance service details page.
* Access the console through SSH connection by using the credentials that you can find on the FortiGate Virtual Appliance service details page.

For more information, see [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Considerations when you delete FortiGate Virtual Appliance
{: #fortinetvm_considerations-remove}

Review the following considerations before you delete the service:

* Before you delete the FortiGate Virtual Appliance service, ensure that the configuration of the existing FortiGate Virtual Appliances is deleted correctly. Specifically, network traffic must be routed around FortiGate Virtual Appliances instead of through FortiGate Virtual Appliances. Otherwise, the existing data traffic within your environment might be impacted.
* If you installed the FortiGate Virtual Appliance service before VMware Solutions v4.0, and you then delete that service, you must manually remove the DNS entries. For more information, see [Manually removing the DNS entries](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices#vc_deletingservices-DNS-entries).

## Related links
{: #managingfortinetvm-related}

* [FortiGate Virtual Appliance overview](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [fortinet.com website](https://www.fortinet.com/){: external}
* [Fortinet document library](https://docs.fortinet.com/product/fortigate/7.4){: external}
