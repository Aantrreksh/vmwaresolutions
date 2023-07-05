---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-30"

keywords: set credentials, update credentials, set notifications, IAM user, invite user

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Managing user accounts and settings
{: #useraccount}

Use the following procedures to invite users to update user account credentials, and to specify whether you want to receive email and console notifications for various events.

## Inviting users to access services and resources
{: #useraccount-iamuserinv}

{{site.data.keyword.vmwaresolutions_full}} is integrated with {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) for collaboration among multiple users. After you sign up for an {{site.data.keyword.cloud_notm}} account and log in to the {{site.data.keyword.vmwaresolutions_short}} console, you can add users to the {{site.data.keyword.cloud_notm}} account. These added users can share the services and resources that are provisioned for the account.

For more information, see the following topics.
* [Inviting users to an account](/docs/account?topic=account-iamuserinv)
* [Managing IAM access for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-iam)

## Setting notifications
{: #useraccount-set-notif}

You can also specify whether you want to receive email and console notifications for various events.

### Procedure to set notifications
{: #useraccount-set-notif-procedure}

1. In the {{site.data.keyword.vmwaresolutions_short}} console, click **Settings** from the left navigation pane.
2. If you want to be notified by email when events occur, click **Enable email notifications**.
3. If you want to be notified in the console when events occur, click **Enable console notifications**.

### Results after you set notifications
{: #useraccount-set-notif-results}

If email or console notifications are enabled for certain instance events, you're notified by email or console messages when these events occur.

## Updating user account credentials
{: #useraccount-set-cred}

The requirement to update user account credentials applies only to the following offerings: VMware vSphere, VMware vCenter Server, VMware Regulated Workloads, and Cyber Recovery.
{: note}

{{site.data.keyword.vmwaresolutions_short}} communicates with the {{site.data.keyword.cloud_notm}} infrastructure through {{site.data.keyword.slapi_short}} calls. To access the {{site.data.keyword.slapi_short}} securely, you must link the credentials of your {{site.data.keyword.cloud_notm}} infrastructure account to your {{site.data.keyword.cloud_notm}} account. After your first order, you can update the user account credentials on the **Settings** page.

### Before you begin
{: #useraccount-set-cred-prereqs}

* You can link only one {{site.data.keyword.cloud_notm}} infrastructure account to one {{site.data.keyword.cloud_notm}} user account.
* The {{site.data.keyword.cloud_notm}} infrastructure account that you're using must meet certain requirements. For more information, see [The {{site.data.keyword.cloud_notm}} infrastructure account](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts#signing_required_accounts-infra).
* If the API key for your {{site.data.keyword.cloud_notm}} infrastructure account changes, you must update the key on the **Settings** page in the {{site.data.keyword.vmwaresolutions_short}} console.

   It is your responsibility to ensure that the API key that is saved on the **Settings** page is correct and up-to-date. Otherwise, operations that require API key validation might fail.
   {: important}

### Procedure to update user account credentials
{: #useraccount-set-cred-procedure}
{: help}
{: support}

1. In the {{site.data.keyword.vmwaresolutions_short}} console, click **Settings** from the left navigation pane.
2. If you have both an {{site.data.keyword.cloud_notm}} infrastructure account and an {{site.data.keyword.cloud_notm}} account that are linked, click **Retrieve credentials** to complete the credentials automatically, and then skip to **Step 4**.
3. In the following situations, review the information the **IBM Cloud infrastructure credentials** area for the steps that you need to take:
   * If you have both an {{site.data.keyword.cloud_notm}} infrastructure account and an {{site.data.keyword.cloud_notm}} account that are not linked, you must link them. Follow the instructions in [Upgrading your account](/docs/account?topic=account-upgrading-account), then click **Retrieve credentials** to complete the credentials automatically.
   * If you do not have an {{site.data.keyword.cloud_notm}} infrastructure account, and you do not have a billable {{site.data.keyword.cloud_notm}} account, first [upgrade your account](/docs/account?topic=account-upgrading-account), and then [create a classic infrastructure API key](/docs/account?topic=account-classic_keys#create-classic-infrastructure-key).
4. Click **Save credentials**. If you receive a message that administrator access is required, you can locate an account administrator by using the steps in [Locating an IAM account administrator](/docs/vmwaresolutions?topic=vmwaresolutions-iam_verify_permissions).

### Results after you update user account credentials
{: #useraccount-set-cred-results}

After the {{site.data.keyword.cloud_notm}} account and the {{site.data.keyword.cloud_notm}} infrastructure account are linked, the console automatically retrieves the {{site.data.keyword.cloud_notm}} infrastructure account credentials to communicate with your VMware® environment on {{site.data.keyword.cloud_notm}}.

The stored {{site.data.keyword.cloud_notm}} infrastructure account credentials are used in future operations that require interaction with the {{site.data.keyword.cloud_notm}} infrastructure.

## Related links
{: #useraccount-related}

* [Setting up your environment for your first order](/docs/vmwaresolutions?topic=vmwaresolutions-completing_checklist)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Ordering vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Managing system notifications](/docs/vmwaresolutions?topic=vmwaresolutions-notifications)
* [How IBM Cloud IAM works](/docs/account?topic=account-iamoverview)
