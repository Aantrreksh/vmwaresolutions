---

copyright:

  years:  2021, 2023

lastupdated: "2023-06-20"

keywords: vCenter Server add host, add server vCenter Server

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding ESXi servers to vCenter Server instances
{: #vc_addingservers}

You can expand the capacity of your VMware® vCenter Server® instance according to your business needs by adding VMware ESXi™ servers.

## Before you add ESXi servers to vCenter Server instances
{: #vc_addingservers-prereq}

* For existing instances with VMware vSphere® 6.5 or 6.7, you cannot add ESXi servers. To add ESXi servers, upgrade your vSphere® software to 7.0. For more information, see [Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).
* For existing instances with vSphere 7.0u2, you can add only ESXi servers with vSphere 7.0u3.
* For the gateway cluster, you cannot add or delete ESXi servers.
* {{site.data.content.para-vcenteraddESXiservers}}
* A vCenter Server instance with NFS storage must have at least three ESXi servers. Each of the nondefault clusters can be expanded to have up to 59 ESXi servers.
* A vCenter Server instance with vSAN™ storage must have at least four ESXi servers.
* If your initial cluster has vSAN storage, adding one or more ESXi servers after deployment can increase the cluster storage capacity.
* If your initial cluster has vSAN storage, SED SSD disks are no longer available. Non-SED SSD disks are ordered.
* You can add 1-20 ESXi servers at a time. For more information about the minimum of ESXi servers, see [Is a two-node vCenter Server instance highly available?](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions#is-a-two-node-vcenter-server-instance-highly-available)

Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Add a host to a BYOL cluster only if you are performing a migration or upgrade of an existing BYOL cluster.
{: important}

## Procedure to add ESXi servers to vCenter Server instances
{: #vc_addingservers-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance for which you want to expand capacity.
3. Click the **Infrastructure** tab.
4. In the **Clusters** table, click the cluster to which you want to add ESXi servers.
5. In the **ESXi servers** section, click **Add**.
6. On the **Add ESXi server** side panel, enter the number of bare metal servers that you want to add. You can keep the **Maintenance mode** checkbox selected to add servers during maintenance mode.

   When you provision new ESXi servers, virtual machines (VMs) are immediately migrated to the new servers if you do not select the **Maintenance mode** checkbox. You do not receive a confirmation message before the migration begins.
   {: important}

7. Complete the bare metal server configuration.
   1. Enter the number of bare metal servers.
      * For the consolidated cluster, you can order 1-51 servers in total, taking into account the existing number of hosts in the cluster.
      * For the workload cluster, you can order 1-59 servers in total, taking into account the existing number of hosts in the cluster.
   2. From the list, you can select a bare metal server configuration that is being used by the existing ESXi servers in the cluster. Then, click **Next**. This option is not available for existing ESXi servers with **Broadwell CPU** or if the storage type of the cluster is **Local disks**.
   3. You can also choose a new bare metal server configuration by selecting the option from the list and clicking **Next**. Select the **CPU model** and the amount of **RAM**.
8. Click **Next** and complete the networking settings.
    * You can continue to use the previously selected primary subnets.
    * You can specify different primary subnets. Then, use the lists to select the **Public primary subnet** and **Private primary subnet**.
    * If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on.
9. In the **Details** section, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Results after you add ESXi servers to vCenter Server instances
{: #vc_addingservers-results}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to add ESXi servers is being processed. On the console, the status of the cluster that is associated with the ESXi servers is changed to **Modifying**.
3. If you do not see the new ESXi servers added to the list in the cluster, check your email or console notifications for more details.

If you are adding ESXi servers during maintenance mode, VMs are not migrated to the new servers until you remove maintenance mode.   
{: important}

## Related links
{: #vc_addingservers-related}

* [Deleting vCenter Server instances in a multisite configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletinginstance_multi)
* [Requirements for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Viewing vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
