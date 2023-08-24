---

copyright:

  years:  2022, 2023

lastupdated: "2023-07-28"

keywords: Cyber Recovery add host, add server Cyber Recovery

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding ESXi servers to Cyber Recovery instances
{: #cr_addingservers}

You can expand the capacity of your Cyber Recovery instance according to your business needs by adding VMware ESXi™ servers.

## Before you add ESXi servers to Cyber Recovery instances
{: #cr_addingservers-prereq}

* For the gateway cluster, you cannot add or remove ESXi servers.
* Whenever possible, add ESXi servers by using the VMware Solutions console because changes that you make on the VMware vSphere® Web Client are not synchronized with the VMware Solutions console. Therefore, add ESXi servers to Cyber Recovery only for on-premises ESXi servers or ESXi servers that you don't manage in the VMware Solutions console.
* For the consolidated cluster, you can order 1-51 servers in total, taking into account the existing number of hosts in the cluster.
* For the workload cluster, you can order 1-59 servers in total, taking into account the existing number of hosts in the cluster.
* If your initial cluster has vSAN storage, adding one or more ESXi servers after deployment can increase the cluster storage capacity.
* If your initial cluster has vSAN storage, SED SSD disks are not available. Non-SED SSD disks are ordered.

## Procedure to add ESXi servers to Cyber Recovery instances
{: #cr_addingservers-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > Cyber Recovery** from the left navigation pane.
2. In the **Cyber Recovery** table, click the instance for which you want to expand capacity.
3. Click the **Infrastructure** tab.
4. In the **Clusters** table, click the cluster to which you want to add ESXi servers.
5. In the **ESXi servers** section, click **Add**.
6. On the **Add ESXi server** side panel, enter the number of bare metal servers that you want to add. You can keep the **Maintenance mode** checkbox selected to add servers during maintenance mode.

   When you provision new ESXi servers, virtual machines (VMs) are immediately migrated to the new servers if you do not select the **Maintenance mode** checkbox. You do not receive a confirmation message before the migration begins.
   {: important}

7. Complete the bare metal server configuration.
   * From the list, you can select a bare metal server configuration that is being used by the existing ESXi servers in the cluster. Then, click **Next**. This option is not available under the following conditions:
      * The bare metal configuration that is used by the existing ESXi servers in the cluster is **Broadwell**.
      * The storage type of the cluster is **Local disks**.
   * You can also choose a new bare metal server configuration by selecting the option from the list and clicking **Next**. Select the **CPU model** and the amount of **RAM**.
8. Click **Next** and complete the networking settings.
    * You can continue to use the previously selected primary subnets.
    * You can specify different primary subnets. Then, use the lists to select the **Public primary subnet** and **Private primary subnet**.
    * If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on.
9. In the **Details** section, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Results after you add ESXi servers to Cyber Recovery instances
{: #cr_addingservers-results}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to add ESXi servers is being processed. On the console, the status of the cluster that is associated with the ESXi servers is changed to **Modifying**.
3. If you do not see the new ESXi servers added to the list in the cluster, check your email or console notifications for more details.

If you are adding ESXi servers during maintenance mode, VMs are not migrated to the new servers until you remove maintenance mode.
{: important}

## Related links
{: #cr_addingservers-related}

* [Ordering Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
* [Viewing Cyber Recovery instances](/docs/vmwaresolutions?topic=vmwaresolutions-cr_viewinginstances)
* [Requirements for Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_orderinginstance_reqs)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
