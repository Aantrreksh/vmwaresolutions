---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-16"

keywords: classic delete instance, delete classic, delete multisite

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deleting Automated instances in a multisite configuration
{: #vc_deletinginstance_multi}

Be aware of the following considerations before you delete {{site.data.keyword.vcf-auto}} instances that are part of a multisite configuration.

{{site.data.content.deletinginstance-components-list}}

{{site.data.content.deletinginstance-delete-vlans}}

{{site.data.content.deletinginstance-delete-info}}

{{site.data.content.deletinginstance-important-note}}

## Procedure to delete Automated instances in a multisite configuration
{: #vc_deletinginstance_multi-procedure}
{: help}
{: support}

1. Delete all services from the secondary Automated instance.
2. Ensure that no NSX objects are expanded into the secondary instance that you want to delete.
3. Delete the secondary vCenter Server from the primary SSO (Single Sign-On) domain. For more information, see [Unregister vCenter Server from Single Sign-On](https://knowledge.broadcom.com/external/article?legacyId=2106736){: external}.
4. Demote the local domain controller VSI (Virtual Service Instance). For more information, see [Demoting domain controllers and domains](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/deploy/demoting-domain-controllers-and-domains--level-200-){: external}.
5. Delete the secondary Automated instance from the {{site.data.keyword.vmwaresolutions_short}} console.
6. Repeat steps 1 - 5 for all secondary Automated instances in your multisite configuration.
7. After deleting all secondary instances, you can also delete the primary instance from the {{site.data.keyword.vmwaresolutions_short}} console.

## Related links
{: #vc_deletinginstance_multi-related}

* [Deleting Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletinginstance)
* [Ordering services for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
