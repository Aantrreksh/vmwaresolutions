---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-16"

keywords: Caveonix RiskForesight, Caveonix configuration, order Caveonix

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering Caveonix RiskForesight
{: #caveonix_ordering}

You can include the Caveonix RiskForesight™ service with a new {{site.data.keyword.vcf-auto}} instance or add the service to your existing instance.

* For {{site.data.keyword.vcf-auto-short}} instances, Caveonix RiskForesight generates a license for the number of VMs (virtual machines) that you select.
* For {{site.data.keyword.rw}} and Security and Compliance Readiness Bundle instances, Caveonix RiskForesight offers per host licensing. You are charged for every host in the instance, which includes management, workload, and gateway clusters.

## Ordering Caveonix RiskForesight for a new instance
{: #caveonix_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. Caveonix RiskForesight is in the **Recommended services** category and is already selected.
2. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_ordering#caveonix_ordering-config), then click **Save**.

## Ordering Caveonix RiskForesight for an existing instance
{: #caveonix_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **Caveonix RiskForesight** service in the **Security and Compliance** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_ordering#caveonix_ordering-config), then click **Save**.

## Caveonix RiskForesight configuration
{: #caveonix_ordering-config}

When you order the Caveonix RiskForesight service, provide the following settings.

The configuration options do not apply to {{site.data.keyword.rw}} and Security and Compliance Readiness Bundle instances.
{: note}

### License name
{: #caveonix_ordering-config-license-name}

Specify a name for this license. The name must be unique across all Caveonix service instances and all instances in the {{site.data.keyword.cloud}} account.

### License notes
{: #caveonix_ordering-config-license-notes}

Enter the notes for the service instance. You can edit the notes later on the license details page.

### Number of VMs to license
{: #caveonix_ordering-config-vms}

Specify the number of VMs to license, in increments of 10. At least 10 VMs are required for license management.

After you order Caveonix RiskForesight, if you want more VMs licensed than you specified initially, complete the following steps:

1. Replace your Caveonix RiskForesight license by ordering a larger license.
2. Copy the license to your Caveonix RiskForesight console.
3. Delete the previous license from the {{site.data.keyword.vmwaresolutions_short}} console.

For more information, see:
* [Procedure to order Caveonix RiskForesight licenses](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_license_ordering#caveonix_license_ordering-procedure)
* [Procedure to delete Caveonix RiskForesight licenses](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_license_managing#caveonix_license_managing_procedure-delete)

## Related links
{: #caveonix_ordering-related}

* [Caveonix RiskForesight overview](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
* [Managing Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-managingcaveonix)
* [Ordering services for {{site.data.keyword.vcf-auto-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
