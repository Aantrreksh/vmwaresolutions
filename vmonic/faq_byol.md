---

copyright:

  years:  2016, 2023

lastupdated: "2023-05-25"

keywords: FAQ, license, BYOL

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# FAQ about Bring Your Own License for VMware
{: #faq_byol} 

## What is BYOL and is it supported for VMware perpetual licenses?
{: #faq_byol-def}
{: faq}
{: support}

BYOL was a feature available to vCenter Server and VMware vSphere® instances in version 2.0 and later. IBM Cloud previously allowed clients to bring their own licenses (BYOL) when moving their existing on-premises VMware workloads to IBM Cloud. BYOL is no longer allowed by VMware. You can no longer bring your own licenses for any new hosts. This applies to all VMware products that are available through IBM Cloud.

Existing BYOL servers will be able to perform upgrades and migrations to refresh software and hardware.

## Can you use the BYOL feature for some VMware components and purchase monthly licenses for others?
{: #faq_byol-mthly-license}
{: faq}

Yes. You can continue to use the BYOL feature for clusters that already have BYOL. You must purchase licenses from IBM for any new combination of the four VMware components. The {{site.data.keyword.vmwaresolutions_short}} console makes it straightforward for you to select the licensing option when you order your instance. Select **I will provide**, and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster. 

## For a specific VMware component, can you use BYOL for some licenses and buy the rest of licenses from IBM?
{: #faq_byol-purchase}
{: faq}

Yes. If you selected BYOL for a specific VMware component when you created a cluster, you have the following options:

* Continue to use an existing BYOL key.
* Purchase IBM-provided licensing for any new clusters.

Currently, only VMware vSphere Enterprise and VMware vSAN can be licensed per cluster.

You cannot mix and match BYOL and IBM-provided licensing for any VMware component within a cluster.
{: note}

## Can you use BYOL when you create a cluster?
{: #faq_byol-cluster}
{: faq}

No. BYOL is no longer supported except for migrations or upgrades of existing BYOL clusters. Select **I will provide**, and enter your own license key only if you are performing an upgrade or migration of an existing BYOL cluster.

## How do you manage BYOL licenses?
{: #faq_byol-mgmt}
{: faq}

You can manage your BYOL licenses by using the VMware vSphere Web Client. 

## Does IBM provide support if you select the BYOL licensing option?
{: #faq_byol-support}
{: faq}

IBM Support continues to be your point of contact for any instance configuration concern. However, if the reported concern is determined to be for a BYOL VMware component, you are directed to VMware Support.

## Related links
{: #faq_byol-related}

* [Accessing the console](/docs/vmwaresolutions?topic=vmwaresolutions-loginmethod)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ about licensing](/docs/vmwaresolutions?topic=vmwaresolutions-faq_licensing)
