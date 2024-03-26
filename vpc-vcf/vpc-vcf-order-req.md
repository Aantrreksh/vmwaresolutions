---

copyright:

  years:  2023, 2024

lastupdated: "2024-03-26"
  
keywords: vmware cloud foundation, IBM Cloud, vpc

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Requirements for VMware Cloud Foundation instances
{: #vpc-vcf-order-req}

With the bare metal server infrastructure provided in {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}), you can quickly deploy VMware Cloud Foundation™ on {{site.data.keyword.cloud_notm}}.

Ensure that you complete the following tasks:
* Review the [{{site.data.keyword.cloud_notm}} account requirements](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-plan#vpc-vcf-plan-acc).
* Review the [required permissions for managing {{site.data.keyword.cloud_notm}} resources](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-plan#vpc-vcf-plan-permission).

The installation of VMware Cloud Foundation on {{site.data.keyword.cloud_notm}} uses the Terraform IBM Provider to create the necessary infrastructure resources and services.

Do not modify any values that are set during resource deployment and VMware Cloud Foundation instance order from the Schematics workspace. After the instance is provisioned, do not add or remove hosts manually.
{: attention}

## Related links
{: #vpc-vcf-order-req-related}

* [The {{site.data.keyword.cloud_notm}} account](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts#signing_required_accounts-cloud)
* [Getting started with {{site.data.keyword.vpc_short}}](/docs/vpc?topic=vpc-getting-started)
* [VPC network design](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-vpc-deployment)
* [Architecture overview of roll-your-own VMware solution on VPC](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
