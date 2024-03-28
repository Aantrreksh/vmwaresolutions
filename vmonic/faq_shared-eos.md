---

copyright:

  years:  2024

lastupdated: "2024-03-20"

keywords: FAQ vmware solutions shared, vmware shared, end of support vmware shared, vmware shared deprecated

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# FAQ about End of Support for VMware Shared
{: #faq-vmwaresolutions-shared-eos}

{{site.data.content.shared-deprecated-note}}

Find answers to frequently asked questions about the End of Support for VMware Shared deployments.

## What does the End of Support announcement mean?
{: #faq-shared-eos}
{: faq}

If you are an existing customer, support for {{site.data.keyword.cloud}} for VMware Shared deployments will continue until 15 January 2025. You can also add instances during this period, but it is recommended that you deply any new instances on the next-generation multitenant offering {{site.data.keyword.vmware-service_full}}. {{site.data.keyword.vmware-service_notm}} is based on the same underlying software VMware Cloud Director, which retains the same admin console. You also benefit from performance improvements, options of network edge tier, improved private networking through {{site.data.keyword.tg_full_notm}}, greater regional coverage, and minor rebalancing in pricing. All these benefits make {{site.data.keyword.vmware-service_short}} the ideal landing zone for your workloads.

If you are new to VMware Shared, and don't have any existing deployments, you are not able to provision new instances of VMware Shared. You can directly use the next-generation performance that is offered by {{site.data.keyword.vmware-service_short}}, with on-demand pricing (hourly) and discounted reserved usage (monthly). For more discounts for continued use, contact your {{site.data.keyword.IBM}} seller.

## Why is the support for {{site.data.keyword.cloud_notm}} for VMware Shared ending?
{: #faq-shared-eos-support}
{: faq}
{: support}

It is important to understand that {{site.data.keyword.cloud_notm}} for VMware Shared is based on VMware NSX-V, which will continue to be supported until the end of 2024. {{site.data.keyword.IBM_notm}}'s exclusive support extension contract with VMware® by Broadcom will end in January 2025, thus rendering {{site.data.keyword.cloud_notm}} for VMware Shared unsupported.

## What is the next step?
{: #faq-shared-eos-next}
{: faq}

It is recommended that you immediately assess your workloads on {{site.data.keyword.cloud_notm}} for VMware Shared, and plan the migration to {{site.data.keyword.vmware-service_short}} at the earliest. For more information about migration options, see [Migrating from VMware Shared to {{site.data.keyword.vmware-service_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_migration).

## Is the price changing? Will it cost more?
{: #faq-share-eos-price}
{: faq}

While the price remains largely the same between the two platforms, you can benefit from three key changes:
* The pricing for vCPU and RAM is rebalanced to enable more cost-effective scaling of RAM.
* On-demand Base Charge is not applicable in {{site.data.keyword.vmware-service_short}}, as it is replaced by the network edge tiers.
* Network edge tiers are added with four available options, such as Efficiency Edge, Medium Edge, Large Edge, and Extra-Large Edge. {{site.data.keyword.IBM_notm}} anticipates that most customers require an Efficiency Edge for their virtual data center, which keeps the price flat across the two platforms.

Customers with an average virtual machine (VM) of 4 vCPU, 12 GB of RAM cannot see any difference in their monthly bills after they migrate to {{site.data.keyword.vmware-service_short}}. However, customers that use a higher ratio of RAM can see a cost benefit while they move migrate {{site.data.keyword.vmware-service_short}}. Both scenarios assume that customers require an Efficiency Edge, rather than a larger tier.
{: important}

In addition to these changes, {{site.data.keyword.IBM_notm}} also aligns the Veeam Block Storage pricing to the vSAN storage rates to remain consistent with the underlying technology used. As a result, some VMware Shared customers (with heavy Veeam Block Storage usage) can see a net price increase, when they move to {{site.data.keyword.vmware-service_short}}.

All existing customers will receive an email with these changes.

## How different is {{site.data.keyword.vmware-service_short}} from VMware Shared?
{: #faq-shared-eos-vmwaas}
{: faq}

{{site.data.keyword.vmware-service_short}} offers several advantages over {{site.data.keyword.cloud_notm}} for VMware Shared:
* Better architecture design that is based on the most recent supported software-defined networking platform from VMware NSX-T™ Networking, with upgraded High Availability.
* Increased global reach with planned expansion through 2024 and 2025.
* Single-pane-of-glass management for customers that use both single and multitenant consumption, with a common bill across.
* Optimized compute pricing model to provide better cost economics for scaling of RAM.
* Optional high-performance network edges to support bandwidth-intensive workloads.
* Improved private networking experience by using {{site.data.keyword.tg_full_notm}}.

## Do I have options for self-service migration tools to migrate my VMs?
{: #faq-shared-eos-self-service-migration}
{: faq}

Yes. VMware Cloud Director Availability (VCDA) enables the VMs migration to {{site.data.keyword.vmware-service_short}}. You can find more details on how to onboard and migrate your VMs to {{site.data.keyword.vmware-service_short}} in a secure, simple, and cost-effective manner with the help of VCDA. For more information about migration paths, step-by-step guides, and managed migration services options, see [Migrating from VMware Shared to {{site.data.keyword.vmware-service_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_migration).

## I have complex workloads that require migration support. What migration paths can I explore?
{: #faq-shared-eos-workloads}
{: faq}

Some migrations require redesigning and reestablishing network connections, edge migrations, and extra support. {{site.data.keyword.IBM_notm}} offers a range of managed services through IBM Consulting, IBM Cloud Expert Labs, and migration partners, such as PrimaryIO. For more information about migration paths, step-by-step guides, and managed migration services options, see [Migrating from VMware Shared to {{site.data.keyword.vmware-service_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_migration).

## Do I have promotions or discounts to offset the cost of dual run?
{: #faq-shared-eos-promotions}
{: faq}

Yes. {{site.data.keyword.IBM_notm}} offers migration promotions and discounts for existing VMware Shared customers. Contact your IBM Customer Success Manager or IBM Sales Representative for details about approved promotions that you can take advantage of and start your upgrade or migration. You will also receive a personalized email with the promotion details in April 2024.

## Does {{site.data.keyword.vmware-service_short}} offer all the features and capabilities that are available in VMware Shared? If any parity gaps exist, when will they be addressed?
{: #faq-shared-eos-features}
{: faq}

{{site.data.keyword.vmware-service_short}} has nearly identical features and capabilities that are used in VMware Shared, in addition to a few new capabilities and performance improvements. 

The key capabilities that both platforms offer are:
* Private-only connectivity
* IBM Operated Management Plane with 99.99 availability SLA, based on VMware Cloud Director, with API connectivity
* On-demand (hourly), reserved (monthly), 1 and 3-year committed use
* NFS and vSAN storage options
* Self-managed backup to cloud through Veeam
* Migration tool
* High availability: single-zone

{{site.data.keyword.IBM_notm}} is actively working on some features to address in 2024, which include:
* Load balancer
* Self-managed disaster recovery that uses Veeam Cloud Connect
* High availability: multi-zone regional network HA
* High availability: stretched vSAN
* SOC2 and C5 report

If you rely on the roadmap features, contact your IBM Customer Success Manager or IBM Sales Representative to understand the custom upgrade paths and migration promotions that are available to you.

Self-managed disaster recovery that uses Zerto is not on the roadmap for 2024.
{: note}

## Related links
{: #faq_shared-eos-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [End of Support for VMware Shared deployments](/docs/vmwaresolutions?topic=vmwaresolutions-eos-vmware-shared)
