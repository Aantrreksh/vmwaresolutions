---

copyright:

  years:  2024

lastupdated: "2024-04-02"

keywords: vmware solutions packaging, vmware solutions pricing, vmware solutions naming

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Packaging and pricing for VMware by Broadcom
{: #vmwaresol_packaging-pricing}

Broadcom announced several changes to the packaging and pricing of the VMware® portfolio, which will be effective on 1 May 2024. One key change is that cloud service providers, including {{site.data.keyword.cloud}}, will no longer be able to sell individual VMware software solutions. These solutions will be available only as part of VMware Cloud Foundation™. Broadcom also announced a new pricing structure for VMware Cloud Foundation.

In response, {{site.data.keyword.cloud_notm}} is changing its {{site.data.keyword.vmwaresolutions_short}} portfolio and pricing, which will be effective on 1 May 2024.

## Packaging and naming for offerings
{: #vmwaresol_packaging-naming}

Existing VMware Solutions offerings will no longer be available as separate components and will be replaced by VMware Cloud Foundation. VMware Solutions users will see these changes in the {{site.data.keyword.cloud_notm}} catalog and invoices. 

The following table shows the changes of the offering names across the portfolio:

| Current offering | Updated offering |
|:---------------- |:---------------- |
| VMware as a Service | VMware Cloud Foundation as a Service |
| VMware Cloud Foundation | VMware Cloud Foundation for VPC |
| VMware vCenter Server® | VMware Cloud Foundation for Classic - Automated |
| VMware vSphere® | VMware Cloud Foundation for Classic - Flexible |
| VMware Shared | VMware Shared (no change) \n This offering is reaching [End of Support](/docs/vmwaresolutions?topic=vmwaresolutions-eos-vmware-shared). |
| VMware ESXi™ on Bare Metal for Classic | VMware ESXi on Bare Metal for Classic (no name change) |
| VMware ESXi on Bare Metal for VPC | VMware ESXi on Bare Metal for VPC (no name change) \n This offering is reaching [End of Support](/docs/vpc?topic=vpc-release-notes&interface=ui#vpc-mar2824). |
{: caption="Table 1. Current and updated offering names" caption-side="bottom"}

## Pricing and discounts
{: #vmwaresol_packaging-pricing-options}

VMware Cloud Foundation (for Classic and for VPC Bare Metal Servers) is charged at a flexible, on-demand rate of $38 per core and per month with a minimum of 16 cores per CPU. 

Discounts are available for longer-term commitments as shown in the following table:

| Contract commitment | Discounts and price (per month, per core) |
|:--------------------|:----------------------------------------- |
| 1 year | 30% discount |
| 3 years | 38% discount |
| On-demand | $38.00 |
{: caption="Table 2. Pricing and discounts for contract commitments" caption-side="bottom"}

### Considerations about pricing changes
{: #vmwaresol_packaging-pricing-considerations}

* For existing VMware Cloud Foundation for VPC customers, this change represents a price reduction.
* On-demand pricing and 1-year contract commitments for VMware Cloud Foundation as a Service (formerly known as VMware as a Service) remain unchanged. A 50% discount applies for 3-year contract commitments.
* The VMware Solutions Support and Services fee of $350.00 per host for vCenter Server instances will be removed on 1 May 2024.

For the most up-to-date pricing information, you can create a cost estimate by clicking **Add to estimate** from either the provisioning or the plan page.
{: important}

## Impact to existing users
{: #vmwaresol_packaging-pricing-impact}

If you are using VMware vSphere, VMware vCenter Server, or VMware ESXi on Bare Metal for Classic, you are updated to VMware Cloud Foundation on 1 May 2024 and billed at its pricing.

Customers will be entitled to all of the following VMware software products that are included in the VMware Cloud Foundation bundle:

* vSphere Enterprise Plus
* vCenter Server Standard
* VMware vSAN Enterprise
* VMware NSX Enterprise
* VMware Aria Suite Enterprise
* VMware HCX Enterprise
* VMware Tanzu Kubernetes Grid
* VMware Data Services Manager

VMware by Broadcom extracted the edge and distributed firewalls from NSX into the VMware Cloud Foundation bundle and made it a separately priced add-on. Customers must purchase the number of cores that are required for their environment separately. The firewall add-on will be available in the {{site.data.keyword.cloud_notm}} catalog on 1 May 2024. At a later date, VMware by Broadcom will disable the firewall on NSX and require new license keys.

vSAN is included at a rate of 1 TiB per VMware Cloud Foundation core. If a customer environment exceeds 1 TiB of vSAN storage per VMware Cloud Foundation core, additional vSAN will be required. The vSAN overage add-on will also be available in the {{site.data.keyword.cloud_notm}} catalog on 1 May 2024.

If you need access to a software product that you are entitled to with VMware Cloud Foundation, contact your IBM Business Partner representative or IBM Support.
{: note}

## Related links
{: #vmwaresol_packaging-pricing-related}

* [Counting Cores for VMware Cloud Foundation and vSphere Foundation and TiBs for vSAN](https://kb.vmware.com/s/article/95927){: external}
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
