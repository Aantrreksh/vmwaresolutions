---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-01"

keywords: vCenter Server Hybridity delete instance, delete vCenter Server Hybridity, delete multisite

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deleting vCenter Server with Hybridity Bundle instances in a multisite configuration
{: #vc_hybrid_deletinginstance_multi}

Before you plan to delete VMware vCenter Server® with Hybridity Bundle instances that are part of a multisite configuration, be aware of the following considerations.

When you delete a vCenter Server with Hybridity Bundle instance, the following components are released sequentially:
1. All deployed services
2. Support and Services fee
3. VMware® product licenses
4. VMware ESXi™ servers
5. Subnets
6. VLANs

Any VLANs to which you added your own resources, such as gateways or Veeam® servers are not deleted. In addition, any existing VLANs that you own, outside of {{site.data.keyword.vmwaresolutions_full}}, are not deleted.
{: note}

{{site.data.content.deletinginstance-delete-info}}

You are billed until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle for the deleted instance.
{: important}

## Procedure to delete vCenter Server with Hybridity Bundle instances in a multisite configuration
{: #vc_hybrid_deletinginstance_multi-procedure}

1. Delete all services from the secondary vCenter Server with Hybridity Bundle instance.
2. Ensure that you do not have any NSX objects that are expanded into the secondary instance that you want to delete.
3. Delete the secondary vCenter Server from the primary SSO (Single Sign-On) domain. For more information, see [Unregister vCenter Server from Single Sign-On](https://kb.vmware.com/s/article/2106736){: external}.
4. Demote the local domain controller Virtual Service Instance (VSI). For more information, see [Demoting domain controllers and domains](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/demoting-domain-controllers-and-domains--level-200-){: external}.
5. Delete the secondary vCenter Server with Hybridity Bundle instance from the {{site.data.keyword.vmwaresolutions_short}} console.
6. Repeat steps 1 - 5 for all secondary vCenter Server with Hybridity Bundle instances in your multisite configuration.
7. After you delete all secondary instances, you can also delete the primary instance from the {{site.data.keyword.vmwaresolutions_short}} console.
