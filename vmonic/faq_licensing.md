---

copyright:

  years:  2023

lastupdated: "2023-06-13"

keywords: FAQ, license, BYOL

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# FAQ about licensing
{: #faq_licensing}

Find answers to frequently asked questions about licensing.

## What happens if the license key you provided is not correct?
{: #faq_licensing-incorrect-license}
{: faq}

All license keys that you provide are validated to ensure that the following conditions are met:
* They are correct for the corresponding VMware components.
* They meet the minimum edition and CPU requirements of the VMware components.

If the validation of any license key fails, you get a notification and you cannot proceed with the instance order.

## Can you provide a license key with more than 8 CPUs?
{: #faq_licensing-license-key}
{: faq}

Yes. For each VMware component, one license per CPU is required. Currently, all VMware vCenter Server® servers have two CPUs. Therefore, two licenses are required for each server. It is recommended that you provide a license key that can support the base instance and any expansion nodes that you want to add to the instance in the future.

## How are my service license charges being calculated?
{: #faq_licensing-service-charges}
{: faq}

* For Caveonix RiskForesight™ on VMware Regulated Workloads or Security and Compliance Readiness Bundle, each server requires a service license.
* For VMware HCX™, service licenses are charged per two CPUs. Dual servers require a single license each. Quad servers require two licenses each. For servers with more than 16 cores per CPU, an increase in the license charge occurs.
* For Entrust CloudControl™ and Entrust DataControl®, service licenses are charged per two CPUs. Dual servers require a single license each. Quad servers require two licenses each.
* For VMware Aria® Operations™, license charges depend on the CPU type. Dual servers have different charges than Quad servers. For servers with more than 16 cores per CPU, an increase in the license charge occurs.
* All other services have static service license charges that do not change based on the number of servers in the instance.

## Why is there a discrepancy in the supported number of VMs for VMware Aria Operations licenses?
{: #faq_licensing-vrops}
{: faq}

You might see a discrepancy in the supported number of VMs between what is displayed on the VMware Aria Operations Manager console and the per CPU metering in {{site.data.keyword.cloud_notm}}. This issue happens if you did not select the **Product evaluation (no key required)** option when you first accessed the VMware Aria Operations Manager console after service installation. For more information, see [Accessing the VMware Aria Operations Manager console](/docs/vmwaresolutions?topic=vmwaresolutions-managing_vrops#managing_vrops-access-vrops-console).

This discrepancy is a result of VMware Aria Operations keys that are created for {{site.data.keyword.cloud_notm}} subscription licensing per virtual machine (VM) capacity. However, in {{site.data.keyword.cloud_notm}}, the VMware Aria Operations licenses are measured and billed per CPU, and not per VM.

The discrepancy does not indicate any service or licensing problem for VMware Aria Operations and VMware Aria Operations™ for Logs. The service is fully licensed for all VMs on each vCenter Server host and continues to work properly.


## Related links
{: #faq_licensing-related}

* [Accessing the console](/docs/vmwaresolutions?topic=vmwaresolutions-loginmethod)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ about Bring Your Own License for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-faq_byol)
