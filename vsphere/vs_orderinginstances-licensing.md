---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-14"

keywords: vmware vSphere order instance, order vSphere, order vmware vSphere instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Licensing
{: #vs_orderinginstances-licensing-settings}

Select the VMware® components to be ordered with your cluster and specify the licensing option for the components.

## Component bundles for IBM Business Partner users
{: #vs_orderinginstances-component-bundles-for-bp-users}

If you are an IBM® Business Partner user, you can select a component license bundle when you order a new VMware vSphere® instance. The following bundles are available:

| Bundle | Components |
|:------ |:---------- |
| Standard with Management | vSphere Enterprise Plus, VMware vCenter Server® Standard, VMware Aria Operations™ for Logs, VMware Aria® Operations™ Enterprise |
| Advanced | vSphere Enterprise Plus, vCenter Server Standard, VMware Aria Operations for Logs, VMware Cloud Director, NSX® Base |
| Advanced with Networking | vSphere Enterprise Plus, vCenter Server Standard, VMware Aria Operations for Logs, NSX Advanced |
| Advanced with Networking and Management | vSphere Enterprise Plus, vCenter Server Standard, VMware Aria Operations for Logs, VMware Aria Operations Enterprise, VMware Cloud Director, NSX Enterprise |
{: caption="Table 1. IBM Business Partner component bundles for vSphere instances" caption-side="bottom"}

You can also include the following VMware® components in your order:
* VMware vSAN™
* VMware Site Recovery Manager
* VMware Aria® Automation™ Enterprise

For IBM Business Partner users, bring your own license (BYOL) is not available.
{: note}

## Individual components for non-Business Partner users
{: #vs_orderinginstances-individual-components-for-non-bp-users}

If you're a non-Business Partner, you can select the following components for your vSphere instance:
* VMware vSphere Enterprise Plus 7.0u3
* VMware vCenter Server
* VMware NSX - Data Center SP Base, Data Center SP Professional, Data Center SP Advanced, or Data Center SP Enterprise Plus
* VMware vSAN
* VMware Site Recovery Manager
* VMware Aria Automation Enterprise
* VMware Aria Operation Enterprise
* VMware Aria Operations for Logs

Small differences exist between NSX-T Data Center and Data Center SP editions. For more information, see [Product offerings for VMware NSX-T Data Center 3.2.x](https://kb.vmware.com/s/article/86095){: external}.

## Licensing options
{: #vs_orderinginstances-licensing-options}

Using individual license keys together with the combined license keys does not meet the payment requirements for the licenses you need.
{: important}

You have the following options for licensing the selected VMware components:
* **Include license with purchase**: In this case, a new license for the VMware component is purchased on your behalf. A combined VMware license is generated to match the cluster size of the order.

   When you purchase any license, except for vSphere Enterprise Plus and vCenter Server, and you order multiple VMware ESXi™ servers, an {{site.data.keyword.cloud_notm}} ticket is opened automatically to combine license keys. You are responsible to follow up with the ticket to ensure that you use only the license keys that the VMware Solutions Support team generates.

* **I will provide the license**: Bring your own license (BYOL) is no longer allowed for VMware components except if you are migrating or upgrading an existing BYOL cluster. If you are upgrading your cluster, do not enter your BYOL licenses when you create your order for the first time, but do it later when the vSphere instance is created.

## Related links
{: #vs_orderinginstances-licensing-related}

* [Bare metal server](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-bare-metal-settings)
* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
