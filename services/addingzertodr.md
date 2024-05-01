---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-12"

keywords: Zerto, Zerto components, tech specs Zerto

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Zerto on {{site.data.keyword.cloud_notm}} overview
{: #addingzertodr}

Zerto on {{site.data.keyword.cloud}} integrates replication and disaster recovery capabilities into the deployment offerings to protect and recover data in your VMware® virtual environment on {{site.data.keyword.cloud}}. Zerto on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from Zerto, not IBM.

Zerto is supported on {{site.data.keyword.vcf-auto}} instances that meet the following requirements:

* VMware NSX-T™ 3.1 or later
* VMware vSphere® 7.0
{: shortdesc}

{{site.data.content.para-promotion-services}}

The Zerto version available for deployment is 9.7u4.
{: note}

## Before you begin
{: #addingzertodr-req}

Ensure that your {{site.data.keyword.cloud_notm}} account is a billable account, and that it is linked to the {{site.data.keyword.cloud_notm}} infrastructure account where your instance is deployed. For more information, see [Billing for Zerto replication](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering#zerto_ordering-billing).

## Technical specifications for Zerto
{: #addingzertodr-specs}

For more information about resource requirements and capacity checking for some services, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

The following components are ordered and included in the Zerto service.

Zerto Virtual Replication Appliance (VRA) components are deployed only into the default cluster.
{: note}

### Virtual Service Instances
{: #addingzertodr-specs-vsi}

* One Virtual Service Instance (VSI) - Zerto Virtual Manager
* 2 x 2.0 GHz cores
* 4 GB RAM
* Windows® Server 2019 Standard Edition (64-bit)

### Storage
{: #addingzertodr-specs-storage}

100 GB (SAN) disk

### Zerto Networking
{: #addingzertodr-specs-network}

* VSI
   * One primary private IP address
   * 1 Gbps private network uplink
* Virtual replication appliances (VRAs) - One private portable subnet for VRA deployment

The Zerto service is not configured with an {{site.data.keyword.cloud_notm}} infrastructure portable IP address or with a NAT connection to the public network, even if you have public interfaces in your instance. This implementation helps to avoid the possibility of asymmetric routing when it uses a network gateway appliance.

When you deploy Zerto, you must configure your own proxy or NAT connection to the public network. If you do not complete the configuration, Zerto blocks management activities in 15 days.

For more information, see [Considerations for ordering Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering#zerto_ordering-private-only).

### Licenses and fees
{: #addingzertodr-specs-licenses}

Zerto Replication version 9.7u4 license.

## Related links
{: #addingzertodr-related}

* [Ordering Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering)
* [Managing Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-managingzertodr)
* [Ordering Zerto stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering_licenses)
* [Managing Zerto stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_managing_licenses)
* [Zerto product documentation](https://www.zerto.com/myzerto/technical-documentation/){: external}
