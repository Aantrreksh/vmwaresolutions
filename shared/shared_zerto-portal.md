---

copyright:

  years:  2021, 2024

lastupdated: "2024-02-29"

keywords: zerto, zerto self-service portal, zerto portal access procedure

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Accessing the Zerto Self-Service Portal
{: #shared_zerto-portal}

{{site.data.content.shared-deprecated-note}}

The Zerto service is available and ready to use in all virtual data centers. Use Zerto as a service to replicate your VMs between your {{site.data.keyword.cloud}} data centers to {{site.data.keyword.cloud_notm}}. The Zerto service is enabled by default.

You can access the Zerto portal on the virtual data center details page when the status of the virtual data center is **Available**. For more information, see [Procedure to view the virtual data center summary](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary#shared_viewing-vdc-summary-procedure) or [Procedure to view virtual data center details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-details#shared_viewing-vdc-details-procedure).

Service charges are incurred only if you choose to use the services.
{: note}

## Before you begin
{: #shared_zerto-portal-prereq}

- Review the following limitations for Zerto:
   - The current version of Zerto is 9.7u1 and is only compatible with the N-1 and N+1 level of Zerto on your on-premises site.
   - Currently, Zerto does not support the replication of stand-alone VMs but only vApps with VMs inside them. IBM is working with Zerto to resolve this limitation.
- You must reset the zOrg administrator password before you can log in to the Zerto portal.

## Procedure to access the Zerto Self-Service Portal from the virtual data center
{: #shared_zerto-portal-procedure}

1. Under **Recommended services** on the virtual data center details page, click **Reset ZORG password**.
2. In the **Reset ZORG password** window, click **Reset password**.
3. Click **Zerto portal** and login to the self-service portal.

After you reset your password on a virtual data center, you have access to the Zerto portal from all virtual data centers in your account. You can now manage VMs across all of your virtual data centers.
{: note}

For more information about using the Zerto Self-Service Portal to create Virtual Protection Groups, see [Zerto technical documentation](https://help.zerto.com/category/WmWare_9.7){: external}.

## Licenses and fees for Zerto
{: #shared_zerto-portal-fees}

Zerto usage incurs charges on demand. For more information, see [VMware Shared pricing](/docs/vmwaresolutions?topic=vmwaresolutions-shared_pricing).

## Related links
{: #shared_zerto-portal-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [Ordering a Zerto Cloud Connector](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-order)
* [Viewing Zerto Cloud Connector details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-view)
* [Deleting Zerto Cloud Connector](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-delete)
* [Zerto for VMware vSphere](https://www.zerto.com/solutions/workloads-and-applications/vmware-vsphere/){: external}
* [Zerto Support and Services](https://www.zerto.com/support-and-services/){: external}
