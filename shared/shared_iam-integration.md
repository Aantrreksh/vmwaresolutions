---

copyright:

  years:  2022, 2024

lastupdated: "2024-07-29"

keywords: manage shared resources, set IAM integration the VMware Cloud Director Management console, shared iam roles, iam roles

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Enabling and managing Identity and Access Management
{: #shared_set-iam}

{{site.data.content.shared-deprecated-note}}

You can optionally enable {{site.data.keyword.cloud}} Identity and Access Management (IAM) for your VMware Cloud Director Organization. For new organizations, IAM is enabled by default. For existing organizations, you can set or reset the IAM enablement from the virtual data center site details page.

## Before you begin
{: #shared_set-iam-prereq}

Review roles and assign resource access for {{site.data.keyword.vmwaresolutions_short}} Shared service instances. For more information, see [Managing IAM access for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-iam) and [Roles and permissions for VMware Cloud Director](/docs/vmwaresolutions?topic=vmwaresolutions-iam_vcd&interface=ui).

## Responsibilities when you use Identity and Access Management
{: #shared_set-iam-responsib}

Review the following considerations to understand your responsibilities and IBM responsibilities for managing IAM.

### IBM responsibilities
{: #shared_set-iam-responsib-ibm}

* Configure the IAM integration with the VMware Cloud Director console by using OpenID Connect (OIDC) for new site deployments.
* Populate the initial roles and permissions in VMware Cloud Director console that map to the IAM roles. For more information, see [Roles and permissions for VMware Cloud Director](/docs/vmwaresolutions?topic=vmwaresolutions-iam_vcd&interface=ui).

### Your responsibilities
{: #shared_set-iam-responsib-user}

* Maintain and manage the IAM integration with VMware Cloud Director as desired.
* Remove or disconnect the IAM integration with VMware Cloud Director if desired.
* Customize the populated roles and permissions in VMware Cloud Director as desired.
* Update the roles and permissions, including the IBM populated ones, as new permissions are provided in VMware Cloud Director.

## Procedure to enable IAM
{: #shared_set-iam-procedure}

Enable IAM for existing organizations or reset the IAM integration if necessary.

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > {{site.data.keyword.vm-shared}}** from the left navigation pane.
2. In the **{{site.data.keyword.vm-shared}}** table, click the site name to open the site properties page.
3. Click the **Summary** tab.
4. From the **Site details** pane, click **Set IAM integration**.

## Results after you enable IAM
{: #shared_set-iam-results}

The IAM integration status can have the following results.

| Status        | Description       |
|:------------- |:------------- |
| Integration pending | The IAM integration is in progress. |
| Integration incomplete | The integration is not successful. Open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support). |
| Integration enabled | The IAM integration was previously enabled for the organization. You can reset the integration, if needed. |
{: caption="Table 1. Status descriptions for IAM implementation" caption-side="bottom"}

### Resetting an IAM integration
{: #shared_set-iam-results-reset}

You must delete all OpenID Connect (OIDC) users and imported groups with the OIDC type, then the OIDC provider before you can reset the IAM integration. For more information, see [Deleting the OpenID Connect configuration in your VMware Cloud Director Organization](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-delete-oidc).

### Single sign-on availability
{: #shared_set-iam-results-sso}

After the IAM integration is enabled, you can use single sign-on to log in to the VMware Cloud Director console.
1. In the {{site.data.keyword.vmwaresolutions_short}} console, click **VMware Cloud Director console**.
2. From the log in panel, click **SIGN IN WITH SINGLE SIGN-ON** to log in to the console.

## Related links
{: #shared_set-iam-related}

* [{{site.data.keyword.vm-shared}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Viewing site and virtual data center details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-details)
* [Locating an IAM account administrator](/docs/vmwaresolutions?topic=vmwaresolutions-iam_verify_permissions)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [VMware Cloud Director](https://www.vmware.com/products/cloud-infrastructure/cloud-director){: external}
