---

copyright:

  years:  2016, 2024

lastupdated: "2024-10-18"

keywords: FAQ, host, ESXi server

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# FAQ about ESXi servers
{: #faq_esxi}

Find answers to frequently asked questions about the VMware ESXi™ servers managed on the {{site.data.keyword.vmwaresolutions_full}} console.

## How many ESXi servers can I add to my instance?
{: #faq_esxi-instance}
{: faq}

Your {{site.data.keyword.vcf-auto}} instance allows you to expand the consolidated cluster to have up to 51 ESXi servers. Each of the workload clusters can be expanded to have up to 59 ESXi servers. Since you can add up to 10 clusters to an instance, each deployed instance can have a maximum of 51 + 9x59 = 582 ESXi servers across all clusters.

## How many ESXi servers can I add to a cluster?
{: #faq_esxi-cluster}
{: faq}

You can add a maximum of 51 ESXi servers to a consolidated cluster and a maximum of 59 ESXi servers to a workload or gateway cluster.

## Can I change the ESXi server names and IP addresses?
{: #faq_esxi-change-name-ip}
{: faq}

The ESXi server names and IP addresses cannot be changed because they are registered for Windows® DNS resolution. Changes might cause failures during deployment or failures of vCenter Server functions.

Don't use the **Rename Device** feature on the {{site.data.keyword.cloud_notm}} user interface to change ESXi server names. This function changes the FQDN of the ESXi server, but the configured vCenter Server and the Windows VSI host registrations are incorrect and might cause failures.
{: attention}

## Can I disable root access on my ESXi servers?
{: #faq_esxi-disable-root}
{: faq}

It is recommended to keep root access enabled on the ESXi servers, otherwise failures of the VMware Solutions functions might occur.

If necessary, you can disable root access when the ESXi servers have a status of **Available** on the VMware Solutions console.

You must re-enable root access for subsequent automation operations. For example, when you add or remove file shares, or when you install add-on services such as Zerto.

## Can I use OS reload on the ESXi servers in my Automated instance?
{: #faq_esxi-OS-reload}
{: faq}

The [OS reload feature](/docs/bare-metal?topic=bare-metal-reloading-the-os) cannot be used for ESXi servers that were provisioned through the VMware Solutions automation.

By using OS (operating system) reload, the ESXi servers are returned to a previous state before the servers were added to vCenter Server and to the Active Directory Domain by the automated configuration.

The OS reload deletes the automated configuration of vCenter Server and that configuration cannot be restored.

Only ESXi servers that are part of {{site.data.keyword.vcf-auto-short}} instances are affected by OS reloads. Hosts that are part of {{site.data.keyword.vcf-flex}} instances are not affected.

## How do I place a host in maintenance mode?
{: #faq_esxi-maint-mode}
{: faq}

To place a host from a VMware vSAN cluster in maintenance mode, complete the following steps:
1. Review the three options provided in the VMware vSphere Web Client: **Ensure accessibility**, **Full data migration**, and **No data migration**.
2. Select the **Ensure accessibility** option.
3. If failures occur, complete the process by using the **Full data migration** option. For more information, see [Place a member of vSAN cluster in maintenance mode](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.vsphere.virtualsan.doc/GUID-521EA4BC-E411-47D4-899A-5E0264469866.html){: external}.
4. If you experience problems, [contact IBM support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) for assistance.

## Can I add static routes on my ESXi servers to mount storage from other locations?
{: #faq_esxi-static-routes}
{: faq}

You can add static routes for storage but you must do it with extreme care. Otherwise, the existing shares might become unmounted.

Adding static routes for vMotion is not supported. Changes in vMotion subnet configuration cause failures of the VMware Solutions functions.
{: attention}

## Related links
{: #faq_esxi-related}

* [Expanding and contracting capacity for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Adding clusters to Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingclusters)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
