---

copyright:

  years:  2019, 2023

lastupdated: "2023-06-30"

keywords: IAM user, user role, user permission, IAM account administrator

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Locating an IAM account administrator
{: #iam_verify_permissions}

Use {{site.data.keyword.cloud}} Identity and Access Management (IAM) to define users for platform services and to control user access to resources across {{site.data.keyword.cloud_notm}}. For more information about user roles (Viewer, Editor, Operator, and Administrator), see the [Platform management roles and permissions table](/docs/vmwaresolutions?topic=vmwaresolutions-iam#iam-roles-table).

You must have an IAM account administrator role to complete various tasks. For example, setting account credentials and granting platform access to users.

If you do not have an administrator role and you want to complete a task that requires the administrator role, you can locate someone with that role. The person that you located can then assign access. For more information about what an account administrator can do, see [IAM access](/docs/account?topic=account-userroles#userroles).

## Locating an account owner with the administrator role
{: #iam_verify_permissions-locate-admin}

To identify an account owner who has the administrator role, complete the following steps:

1. Log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com).
2. On the upper right of the window, select the {{site.data.keyword.cloud_notm}} account that you want to use.
3. Click **Manage** > **Access (IAM)**.
4. From the left navigation pane, click **Users**.
5. Scroll down through the list until you find a name with an **owner** tag next to the user's name, which indicates that the user is an account administrator.
6. Write down the name of this user.

If the owner that you identified is not available or has left the company, find one or more other users with the administrator role. Consider who might be assigned the role, for example, a manager, team lead, or someone who works directly with {{site.data.keyword.cloud_notm}} customers.

To locate a user with an administrator role, click the name link and review the information on the **Access** tab. Look for the following values:
* Service - VMware Solutions
* Resources - All
* Role - Administrator

## Assigning access
{: #iam_verify_permissions-assign-access}

After you find the account owner or another user with an administrator role, that person must perform the following steps to assign access:

1. Log in to [{{site.data.keyword.cloud_notm}}](https://cloud.ibm.com) as the {{site.data.keyword.cloud_notm}} account owner.
1. On the upper right of the window, select the {{site.data.keyword.cloud_notm}} account that you want to use.
1. At the right side of the banner, click **Manage** > **Access (IAM)**.
1. From the left navigation pane, click **Users**.
1. In the row for the user that you want to assign access, click the vertical overflow menu next to the **Status** column, and then click **Assign access**.
1. Select **Access groups** to add the user to one or more existing access groups. You can assign the user only to those access groups that you have access to manage.
   1. Select one or more group names.
   1. Click **Add > Assign**.
1. Select **Access policy** to assign individual access policies to the user.
   1. Select **VMware Solutions** from the list of services, and then click **Next**.
   1. Select **Specific resources** for the access scope. Select the attribute type as **VMware Instance**, the operator as **string equals**, and the value as **All instances**. Then, click **Next**.
   1. From the **Platform access** list, select **Administrator**. Then, click **Next**.
   1. Optionally, choose the time when you want the policy to grant access. Then, click **Review**.
   1. Click **Add > Assign**.

## Related links
{: #iam_verify_permissions-related}

* [How IBM Cloud IAM works](/docs/account?topic=account-iamoverview)
* [Managing access to resources](/docs/account?topic=account-assign-access-resources)
