---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-17"

keywords: IAM user, user role, user permission, IAM access for vmwaresolutions, permissions for vmwaresolutions, identity and access management for vmwaresolutions, roles for vmwaresolutions, actions for vmwaresolutions, assigning access for vmwaresolutions

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing IAM access for VMware Solutions
{: #iam}

Access to {{site.data.keyword.vmwaresolutions_full}} service instances for the users in your account is controlled by {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.vmwaresolutions_short}} services in your account must be assigned an access policy with an IAM user role defined.

The access policy determines the actions that the user can take within the context of the service or the instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.cloud_notm}} service as operations that can be applied to the service. The actions are then mapped to IAM user roles.

Policies enable access to be granted at different levels. Some of the options include the following accesses:

* Access across all service instances in your account
* Access to an individual service instance in your account
* Access to a specific resource within an instance
* Access to all IAM-enabled services in your account

After you define the scope of the access policy, you assign a role.

Review the following information, which outlines the actions that each role allows within the {{site.data.keyword.vmwaresolutions_short}} service.

## Platform management roles and permissions for VMware Solutions
{: #iam-roles}

Platform management roles enable users to complete tasks on service resources at the platform level. For example, assign user access to the service, create or delete service IDs, create instances, and bind instances to applications.

To use a smaller set of permissions, use the following roles:

* Reader in place of Viewer or Operator
* Writer in place of Editor
* Manager in place of Administrator

### Platform management roles for VMware Solutions
{: #iam-roles-solution}

The following table provides information about the actions that are mapped to platform management roles for VMware Solutions.

| Platform management role | Actions |
|:----------------- |:----------------- |
| Reader | Read-only actions to view service-specific resources. |
| Writer | Create and edit service-specific resources. |
| Manager | Privileged actions as defined by the service in addition to create and edit service-specific resources. |
| Viewer | Read-only actions to view the summary and details of instances. |
| Operator | Read-only actions. For example, list instances and view instance details. |
| Editor | Update a specific instance. For example, add or remove VMware ESXi™ servers, clusters, and services; upgrade an instance to a higher version. |
| Administrator | Full management access. For example, create new instances, delete instances, and grant platform access to other users.|
{: caption="Table 1. Platform management roles and allowed actions for VMware Solutions" caption-side="bottom"}
{: #iam-roles-table}

For VMware Solutions, the following actions exist:

| Action | Operation on service | Role |
|:------ |:-------------------- |:---- |
| `vmware-solutions.instances.create` | Create new instances | Administrator |
| `vmware-solutions.instances.delete` | Delete instances | Administrator |
| `vmware-solutions.instances.view` | List instances \n View the detail of an instance | Viewer, Operator, Editor, and Administrator |
| `vmware-solutions.instances.update` | Add or remove ESXi servers \n Add or remove clusters \n Add or remove services \n Upgrade an instance to a higher version | Editor and Administrator |
| `vmware-solutions.account.update` | Update account settings | Administrator |
{: caption="Table 2. Action descriptions and required roles" caption-side="bottom"}

## Assigning resource access
{: #iam-roles-user-access}

You can choose from the following options when you assign resource access.
* Assign all resources access to grant users access to all service resource created in all resource groups within the account.
* Specific resources access to grant users access to a specific resource group or VMware® instance.

### Procedure to grant user access
{: #iam-roles-user-access-all-procedure}

1. In the console, go to **Manage > Access (IAM)**.
2. Click **Users** from the left navigation pane.
3. From the row for the user that you want to assign access, select the **Actions** menu, and click **Assign access**.
4. Click **Access policies** and select **VMware Solutions** from the **Service** table. Then, click **Next**.
5. Select the resource to receive access and click **Next**.
   * Click **All resources** to grant access to all service resources.
   * Click **Specific resources** and select the attribute type, operator, and value.
6. Select any combination of roles and click **Review** to review all of your selections.
7. Optionally, click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") to update any of your selections.
8. Click **Add** and click **Assign**.

To grant user permission to create new instances for VMware Shared, you must also assign Resource Group access policies. For more information, see [Giving access to resources in resource groups](/docs/account?topic=account-rgs_manage_access) and [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering).
{: important}

## Managing access for users
{: #iam-users}

You can add new users to the {{site.data.keyword.cloud_notm}} account so that these users can share the services and resources that are provisioned for the account. For more information, see [Inviting users to access services and resources](/docs/vmwaresolutions?topic=vmwaresolutions-useraccount#useraccount-iamuserinv).

You can also manage the access for existing users, including modifying existing access, assigning new access, and reviewing assigned access. To manage access for users, you must be the account owner or you must have the **Administrator** platform management role. For more information, see [Managing access to resources](/docs/account?topic=account-assign-access-resources).

## Assigning access to VMware Solutions in the console
{: #iam-assign-access-console}
{: ui}

You can assign access in the console in one of the following ways:

* Access policies per user. You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For more information about the steps to assign IAM access, see [Assigning access to resources in the console](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).
* Access groups. Access groups are used to streamline access management by assigning access to a group once. After that, you can add or remove users as needed from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).

## Assigning access to VMware Solutions by using the API
{: #iam-assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api) or the [Create a policy API docs](/apidocs/iam-policy-management#create-policy). Role cloud resource names (CRN) in the following table are used to assign access with the API.

| Role name | Role description | Role CRN |
|-----------|----------------- |--------- |
| Viewer | As a viewer, you can view service instances, but you can't modify them. | `crn:v1:bluemix:public:iam::::role:Viewer` |
| Administrator | As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. | `crn:v1:bluemix:public:iam::::role:Administrator` |
| Operator | As an operator, you can perform platform actions that are required to configure and operate service instances, such as viewing a service's dashboard. | `crn:v1:bluemix:public:iam::::role:Operator` |
| Editor | As an editor, you can perform all platform actions except for managing the account and assigning access policies. | `crn:v1:bluemix:public:iam::::role:Editor` |
{: caption="Table 3. Role ID values and description for API use" caption-side="bottom"}
{: #iam-rolescrn-table}

The following example is for assigning the `<Viewer>` role for `<vmware-solutions>`:

Use `<programmatic_service_name>` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}

```curl
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json'
-d '{
  "type": "access",
  "description": "Viewer role for vmware solutions service instance",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "IBMid-123453user"
        }
      ]
    }'
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:iam::::role:Viewer"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceName",
          "value": "vmware-solutions"
        }
      ]
    }
  ]
}
```
{: curl}
{: codeblock}

## Related links
{: #iam-related}

* [Assigning access to resources by using access groups](/docs/account?topic=account-access-getstarted)
* [Inviting users to an account](/docs/account?topic=account-iamuserinv)
* [How IBM Cloud IAM works](/docs/account?topic=account-iamoverview)
* [Locating an IAM account administrator](/docs/vmwaresolutions?topic=vmwaresolutions-iam_verify_permissions)
* [Roles and permissions for VMware Cloud Director](/docs/vmwaresolutions?topic=vmwaresolutions-iam_vcd&interface=ui)
