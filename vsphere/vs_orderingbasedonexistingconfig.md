---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-23"

keywords: flexible order instances, flexible configuration, vmware order vSphere instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering Flexible instances based on existing configurations
{: #vs_orderingbasedonexistingconfig}

You can order a {{site.data.keyword.vcf-flex}} instance based on a configuration template that you saved. Use this procedure to define a new instance based on an existing instance configuration.

## Requirements for Flexible instances
{: #vs_orderingbasedonexistingconfig-req}

Ensure that you complete the following tasks:
* If you are ordering a {{site.data.keyword.vcf-flex-short}} instance for the first time, complete the tasks in the **Before you begin** section on the ordering page. For more information, see [Setting up your environment for your first order](/docs/vmwaresolutions?topic=vmwaresolutions-completing_checklist).
* Review the requirements and considerations in [Planning for Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_planning).
* Create a configuration template to be reused.

## Procedure to order Flexible instances based on existing configurations
{: #vs_orderingbasedonexistingconfig-procedure}

1. In the VMware Solutions console, click the **VMware Cloud Foundation (VCF) for Classic** card in the **Create a resource** section.
2. On the **Create** tab, click the **Flexible** card in the **Resource type** section.
2. Click **Browse configurations** to open the instance configuration manager and choose a configuration template from the list.
3. Enter a new instance name.
4. Review the instance settings that are automatically completed and update the settings according to your needs. For more information about the settings, see [Ordering new Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req).

   {{site.data.content.attnnote-byol}}

5. In the **Summary** pane, verify the ordered configuration and the estimated price.
   * To save the configuration as a template without placing an order, click **Save configuration**.
   * To place the order, make sure that the account to be charged is correct, review and accept the terms, and then click **Create**.

   Only the {{site.data.keyword.cloud_notm}} bare metal servers are installed. You're responsible for installing and configuring various components after instance deployment, such as VMware® vCenter Server, VMware NSX®, and VMware vSAN™ - Enterprise or Enterprise Plus editions.
   {: note}

## Results after you order Flexible instances based on existing configurations
{: #vs_orderingbasedonexistingconfig-results}

If you saved the instance configuration as a template, you get a console notification that the configuration was saved. You can then find the template in the **Browse configurations** list.

If you placed an order, the deployment of the instance starts automatically. You receive an email confirmation that the order is being processed. When the instance is ready to use, you're also notified by email.

## Related links
{: #vs_orderingbasedonexistingconfig-related}

* [Ordering Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req)
* [Adding ESXi servers to Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_addingservers)
