---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-30"

keywords: vCenter Server migrate instance, add account vCenter Server, migrate cloud account

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Migrating pre-V2.5 vCenter Server instances to IBM Cloud accounts
{: #vc_addinstancetousraccount}

VMware vCenter Server® instances that are deployed in V2.5 and later releases in your {{site.data.keyword.cloud}} account are automatically added to your account and are managed by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM).

For instances that were deployed in V2.4 and earlier releases, you can migrate them to specified {{site.data.keyword.cloud_notm}} accounts for IAM-enabled user management.

## Before you begin
{: #vc_addinstancetousraccount-prereq}

Ensure that the {{site.data.keyword.cloud_notm}} account that you want to migrate the instance to is not an IaaS-only account. An IaaS-only account is an {{site.data.keyword.cloud_notm}} infrastructure account that is not linked to an {{site.data.keyword.cloud_notm}} account.

For more information about how to link your Iaas-only account to your PaaS account, see [Linking your IaaS and PaaS accounts](https://www.ibm.com/cloud/blog/follow-steps-link-iaas-paas-accounts){: external}.

## Procedure to migrate pre-V2.5 vCenter Server instances to IBM Cloud accounts
{: #vc_addinstancetousraccount-procedure}

1. In the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. From the console banner, click the **Avatar** icon ![Avatar icon](../../icons/i-avatar-icon.svg "Avatar"), and then click the **Account** field to select the user account that you want to migrate the instance to.
3. In the **vCenter Server** table, find the pre-V2.5 instance.
4. Click the vertical overflow menu next to the **Status** column, and then click **Migrate instance to account**.
5. In the **Migrate instance to account** window, confirm the account to migrate the instance to, and then click **Migrate**.

## Results
{: #vc_addinstancetousraccount-results}

1. You get a console notification that your request to migrate the instance to the specified {{site.data.keyword.cloud_notm}} account is accepted.
2. When the instance migration is completed, the instance is displayed on the **Resources** page under the account to which it was migrated. The migrated instance is no longer displayed in the original account from which it was migrated.

## Related links
{: #vc_addinstancetousraccount-related}

* [Managing user access with IAM](/docs/vmwaresolutions?topic=vmwaresolutions-iam#iam)
* [Inviting users to access services and resources](/docs/vmwaresolutions?topic=vmwaresolutions-useraccount#useraccount-iamuserinv)
* [How IBM Cloud IAM works](/docs/account?topic=account-iamoverview)
