---

copyright:

  years:  2023, 2024

lastupdated: "2024-04-09"

keywords: FAQ, license, BYOL

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# FAQ about licensing
{: #faq_licensing}

Find answers to frequently asked questions about licensing.

## How are my service license charges being calculated?
{: #faq_licensing-service-charges}
{: faq}

* For Caveonix RiskForesight™ installed on {{site.data.keyword.rw}} or Security and Compliance Readiness Bundle, each server requires a service license.
* For Entrust CloudControl™ and Entrust DataControl®, service licenses are charged per two CPUs. Dual servers require a single license each. Quad servers require two licenses each.
* For VMware HCX™ and VMware Aria® Operations™, service licenses are included as part of the {{site.data.keyword.vcf-classic-short}} license bundle.
* All other services have static service license charges that do not change based on the number of servers in the instance.

## Why is there a discrepancy in the supported number of VMs for VMware Aria Operations licenses?
{: #faq_licensing-vrops}
{: faq}

You might see a discrepancy in the supported number of VMs between what is displayed on the VMware Aria Operations Manager console and the per CPU metering in {{site.data.keyword.cloud_notm}}. This issue happens if you did not select the **Product evaluation (no key required)** option when you first accessed the VMware Aria Operations Manager console after service installation. For more information, see [Accessing the VMware Aria Operations Manager console](/docs/vmwaresolutions?topic=vmwaresolutions-managing_vrops#managing_vrops-access-vrops-console).

This discrepancy is a result of VMware Aria Operations keys that are created for {{site.data.keyword.cloud_notm}} subscription licensing per virtual machine (VM) capacity. However, in {{site.data.keyword.cloud_notm}}, the VMware Aria Operations licenses are measured and billed per CPU, and not per VM.

The discrepancy does not indicate any service or licensing problem for VMware Aria Operations and VMware Aria Operations™ for Logs. The service is fully licensed for all VMs on each vCenter Server host and continues to work properly.

## Related links
{: #faq_licensing-related}

* [FAQ about BYOL for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-faq_byol)
* [Accessing the console](/docs/vmwaresolutions?topic=vmwaresolutions-loginmethod)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
