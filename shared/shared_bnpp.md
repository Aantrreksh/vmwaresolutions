---

copyright:

  years:  2020, 2023

lastupdated: "2023-05-22"

keywords: troubleshooting VMware Solutions Shared, data center, VMware Solutions Shared data centers, Business Partners

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Limitations and workarounds for Business Partner users
{: #shared_bnpp}

Review the following considerations and limitations that Business Partner users can experience.

## High availability in stretched locations
{: #shared_bnpp-ha}

For Business Partner users, VMware Shared virtual data centers support highly availability for in-cloud replication from one virtual data center to another. However, ordering a Zerto Cloud Connector (ZCC) to replicate on-premises virtual machines (VMs) to {{site.data.keyword.cloud_notm}} does not support high availability.

## Resetting passwords
{: #shared_bnpp-pw-reset}

Business Partner users cannot use one virtual data center to reset the VMware Cloud Director account password for the entire data center region.

For Business Partner users, all virtual data centers in the same data center number group have the same password. Groups with the same data center number can reset the VMware Cloud Director account password from any virtual data center in the number group.

For example, ``PAR04- windows`` and ``PAR04- linux`` are in a group with the same data center number. When you reset the VMware Cloud Director password in either, the password is reset for any virtual data center in ``PAR04``. The password is not reset for the ``PAR05`` or ``PAR06`` data center number groups.

## Modifying roles used for IAM integration
{: #shared_bnpp-iam}

Business Partner users cannot modify a role in VMware Cloud Director used for the IAM integration.

When the VMware Cloud Director version is updated, the new version can introduce new dependencies between rights. If the affected right is used by one of the roles created in VMware Cloud Director for the integration with IAM, you cannot modify that role in VMware Cloud Director.

An error similar to the following displays.
``Required implied right <right name 1> has not been selected for selected right <right name 2>``

This occurs because the roles were created before the update of VMware Cloud Director and the roles do not have the latest information about their rights. Complete one of the following options to resolve this limitation.

* Reset the OpenID Connect configuration. For more information, see [Deleting the OpenID Connect configuration in your VMware Cloud Director Organization](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-delete-oidc).
* Create a copy of the affected role and add the missing right. This option helps you to keep all possible changes made to one specific role used for OpenID Connect.

 1. Select the role and click **Clone**.
 2. Before cloning, select the **Modify selected rights** toggle button. The rights error displays.
 3. Find the right that you need to update, uncheck it, and check it again. The missing right is now added.
 4. Click **Save**.
 5. Make note of the name of the original role, then delete the role. If you assigned this role to users that were created manually, you must reassign the users to the cloned role before you can delete the original role.
 6. Rename the cloned role with the name of the original role.

## Related links
{: #shared_bnpp-related}

* [Operating VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [VMware Cloud Director](https://www.vmware.com/ca/products/cloud-director.html){: external}
