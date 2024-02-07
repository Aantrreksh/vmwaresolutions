---

copyright:

  years:  2023

lastupdated: "2023-12-14"
  
keywords: vmware cloud foundation, IBM Cloud, vpc

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Planning for VMware Cloud Foundation instances
{: #vpc-vcf-plan}

## {{site.data.keyword.cloud_notm}} account requirements
{: #vpc-vcf-plan-acc}

To order a VMware Cloud Foundation™ instance, you must have a **Pay As You Go** {{site.data.keyword.cloud}} account. The cost of the resources that are ordered are billed to that {{site.data.keyword.cloud}} account. For more information, see [Upgrading to a Pay-As-You-Go account](/docs/account?topic=account-upgrading-account#upgrade-paygo).

## Required permissions for managing {{site.data.keyword.cloud_notm}} resources
{: #vpc-vcf-plan-permission}

Access to {{site.data.keyword.cloud_notm}} resources for users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Every user that accesses infrastructure services resources in your account must be assigned one or more access policies that define their IAM roles. Each user must also have access to the resource group that contains the infrastructure resources. 

A resource group organizes account resources in customizable groupings so that you can quickly assign access to more than one resource at a time. Every resource that is managed by IAM belongs to a resource group within your account.
To manage users access and resource groups, your account must have permissions to [manage resource groups](/docs/account?topic=account-rgs&interface=ui) and to [manage accounts](/docs/account?topic=account-groups&interface=ui#prereq-create-groups).

Ensure that the following requirements are met:
* You have an Editor or Administrator role on a resource group in the account. For more information, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).
* You have permission to [create an {{site.data.keyword.bplong_notm}} workspace](/docs/schematics?topic=schematics-access#access-roles).
* Your account meets the [required IAM permissions](/docs/vpc?topic=vpc-resource-authorizations-required-for-api-and-cli-calls) to interact with {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) infrastructure objects.
* Your account meets the [required IAM permissions](/docs/vpc?topic=vpc-planning-for-bare-metal-servers&interface=ui) for Bare Metal Servers on {{site.data.keyword.vpc_short}}.
* Your account meets the [required IAM permissions](/docs/dns-svcs?topic=dns-svcs-iam) for {{site.data.keyword.cloud_notm}} DNS Services.
* (Optional) Your account meets the [required IAM permissions](/docs/log-analysis?topic=log-analysis-work_iam) for {{site.data.keyword.cloud_notm}} Log Analysis service.

## {{site.data.keyword.cloud_notm}} region and zone availability for VMware Cloud Foundation deployment
{: #vpc-vcf-plan-region}

The ESXi servers in VMware Cloud Foundation are built on Bare Metal Servers on {{site.data.keyword.vpc_short}}. Therefore, you can deploy instances only in {{site.data.keyword.cloud}} data centers that meet the requirements for {{site.data.keyword.vpc_short}} bare metal server profiles that are supported by VMware Cloud Foundation.

The following Bare Metal Server profiles are supported:
* `bx2d-metal-96×384`
* `mx2d-metal-96x768`

For more information about {{site.data.keyword.vpc_short}} bare metal servers by region, see [Profile availability by region](/docs/vpc?topic=vpc-bare-metal-servers-profile&interface=ui#bare-metal-profile-availability-by-region).

## {{site.data.keyword.cloud_notm}} quotas and service limits
{: #vpc-vcf-plan-limits}

When you plan your VMware Cloud Foundation deployment, you also need to consider [quotas and service limits](/docs/vpc?topic=vpc-quotas) for {{site.data.keyword.vpc_short}} and the resources available. For example, for bare metal server on {{site.data.keyword.vpc_short}}, the limitation is 25 per account by default. To increase a quota for a resource, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
