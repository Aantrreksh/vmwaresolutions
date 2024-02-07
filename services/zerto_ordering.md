---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-06"

keywords: Zerto, Zerto replication billing, order Zerto

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering Zerto
{: #zerto_ordering}

You can include the Zerto service with a new VMware vCenter Server® instance or add the service to your existing instance.

Zerto v9.5u1 does not support VMware vSphere 6.5 and 6.7. However, you can still order stand-alone licenses for existing vSphere 6.x instances.
{: restriction}

## Billing for Zerto replication
{: #zerto_ordering-billing}

VMs (virtual machines) that are replicated by using Zerto are metered by Zerto and {{site.data.keyword.cloud}}. Your bill for this usage is charged through an {{site.data.keyword.cloud_notm}} billable account instead of an {{site.data.keyword.cloud_notm}} infrastructure account.

Before you order Zerto, ensure that your {{site.data.keyword.cloud_notm}} account is a billable account, and that it is linked to the same {{site.data.keyword.cloud_notm}} infrastructure account where your instance is deployed.

### Viewing Zerto charges
{: #zerto_ordering-view-charge}

To view your Zerto usage charges, follow these steps:

1. Go to the [{{site.data.keyword.cloud_notm}} Billing and Usage](https://cloud.ibm.com/billing/usage) page.
2. From the **Filter by group** list, select **VMware Solutions**.

## Ordering Zerto for a new instance
{: #zerto_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. Zerto is in the **Data resiliency and migration** category.
2. Open the category, locate Zerto, and toggle its switch on.
3. Click **Edit** to review and specify the configuration information, then click **Save**.

## Ordering Zerto for an existing instance
{: #zerto_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **Zerto** service in the **Data resiliency and migration** section and toggle its switch on.
4. Click **Edit** to review and specify the configuration information, then click **Save**.

If you add Zerto to a vCenter Server instance that has a VMware® ESXi™ server that is in maintenance mode, you must use the Zerto Virtual Manager (ZVM) console. Use the pre-populated Zerto Virtual Replication Appliance (VRA) IP address to manually deploy the VRA virtual machine (VM).
{: important}

## Considerations for ordering Zerto
{: #zerto_ordering-private-only}

When you deploy Zerto, you must configure your own proxy or NAT connection to the public network.

Within 15 days, you must configure the Call Home feature for Zerto. If you do not complete the configuration in this time frame, Zerto blocks certain management activities.

For more information about Zerto Call Home, see [How to configure Zerto Reporting for Enterprise environments (Call Home)](https://help.zerto.com/kb/000004824){: external}.

## Related links
{: #zerto_ordering-related}

* [Zerto overview](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr)
* [Managing Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-managingzertodr)
* [Ordering Zerto stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering_licenses)
* [Managing Zerto stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_managing_licenses)
* [Zerto product documentation](https://www.zerto.com/myzerto/technical-documentation/){: external}
