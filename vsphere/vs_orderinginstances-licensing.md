---

copyright:

  years:  2016, 2024

lastupdated: "2024-08-13"

keywords: flexible order instance, order vSphere, order flexible instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Licensing
{: #vs_orderinginstances-licensing-settings}

Select the VMware® components for your instance and specify the licensing option for them.

## VMware vSphere version
{: #vs_orderinginstances-vsphere-version}

Select the VMware vSphere® version for your instance. If you want to use vSphere 8, consider the following information:
* For new instances, you can use only VMware vCenter Server® 8.
* vSAN storage is not supported with vSphere 8.
* SAP-certified Cascade Lake servers are not supported with vSphere 8.
* BYOL users can also select a vSphere version for the instance.

## Licensing options
{: #vs_orderinginstances-licensing-options}

Select the VMware® components for your instance and specify the licensing option for them. You have the following options for licensing the selected VMware components:

* **Include license with purchase**: In this case, a new license for the VMware component is purchased on your behalf. A combined VMware license is generated to match the instance size of the order.

   When you purchase any license, except for VMware vSphere Enterprise Plus and VMware vCenter Server, and you order multiple VMware ESXi™ servers, an {{site.data.keyword.cloud_notm}} ticket is opened automatically to combine license keys. You are responsible to follow up with the ticket to ensure that you use only the license keys that the VMware Solutions Support team generates.

* **Bring your own license (BYOL)**: If you are a BYOL user, provide your own license key for vSphere Enterprise Plus edition. Toggle the **BYOL** switch to **Enabled** and enter your license key.

   {{site.data.content.attnnote-byol}}

## Related links
{: #vs_orderinginstances-licensing-related}

* [Bare metal server](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-bare-metal)
* [Procedure to order Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [VMware NSX documentation](https://docs.vmware.com/en/VMware-NSX/index.html){: external}
