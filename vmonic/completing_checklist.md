---

copyright:

  years:  2020, 2024

lastupdated: "2024-04-29"

keywords: ordering prerequisites, before you order, pre-order checklist, before first order

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Setting up your environment for your first order
{: #completing_checklist}

The setup information applies only to the {{site.data.keyword.vcf-classic}} offerings: Automated, Flexible, {{site.data.keyword.cr}}, and {{site.data.keyword.rw}}.
{: note}

When you order an instance for the first time, you might be prompted to follow a set of instructions to ensure that your environment is ready for your order.

## Procedure to set up your environment for your first order
{: #completing_checklist-procedure}
{: help}
{: support}

Follow the instructions in the **Before you begin** section on the instance order page. The instructions vary depending on the instance type and whether your account meets the requirements.

The following table lists the possible instructions and additional information for you to complete the tasks.

| If you are asked to... | See... |
| ---------------------- | ------ |
| ...upgrade your account | [Upgrading to a Pay-As-You-Go account](/docs/account?topic=account-upgrading-account#upgrade-paygo) |
| ...create an API key | [Creating a classic infrastructure API key](/docs/account?topic=account-classic_keys#create-classic-infrastructure-key).\n Additional steps:\n 1. In the {{site.data.keyword.vmwaresolutions_full}} console, retrieve your API key and username.\n 2. Click **Settings** from the left navigation pane and click **Retrieve credentials**.\n 3. Review the username and API key that are automatically entered and click **Save credentials**. |
| ...locate an account administrator because admin access is required | [Locating an IAM account administrator](/docs/vmwaresolutions?topic=vmwaresolutions-iam_verify_permissions) |
| ...convert to a VRF account | [Converting to virtual routing and forwarding](/docs/direct-link?topic=direct-link-what-happens-during-the-account-conversion-process) |
| ...enable service endpoints | [Enabling service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).\n You can then connect to certain services over the {{site.data.keyword.cloud}} private network rather than the public network. |
| ...verify account permissions | [Permissions for the {{site.data.keyword.cloud_notm}} infrastructure account](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts#signing_required_accounts-infra-permissions) |
{: caption="Table 1. Information for completing before you begin tasks" caption-side="bottom"}

## Results
{: #completing_checklist-results}

* The {{site.data.keyword.cloud_notm}} infrastructure credentials are stored in the VMware Solutions console after the first order. Future orders use the stored credentials by default.
* After you complete the instructions, they are no longer displayed next time that you are on the ordering page. You can update the credentials on the **Settings** page later on.
* If the API key for your {{site.data.keyword.cloud_notm}} infrastructure account changes, you must update it on the **Settings** page in the VMware Solutions console.

## Related links
{: #completing_checklist-related}

* [Managing user accounts and settings](/docs/vmwaresolutions?topic=vmwaresolutions-useraccount)
* [General FAQ about VCF for Classic](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Ordering Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
