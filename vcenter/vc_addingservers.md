---

copyright:

  years:  2021, 2024

lastupdated: "2024-09-04"

keywords: automated instance add host, add server automated instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding ESXi servers to Automated instances
{: #vc_addingservers}

You can expand the capacity of your {{site.data.keyword.vcf-auto}} instance according to your business needs by adding VMware ESXi™ servers.

## Before you add ESXi servers to Automated instances
{: #vc_addingservers-prereq}

{{site.data.content.para-vcenteraddESXiservers}}

### For all Automated instances
{: #vc_addingservers-prereq-all}

Review the following information applicable to all Automated instances:

* You can add up to 51 ESXi servers to the consolidated cluster and up to 59 ESXi servers to the workload cluster. You cannot add or delete ESXi servers for the gateway cluster.
* For clusters that belong to vCenter Server 7 instances, you can add only ESXi servers with vSphere 7.0u3.
* For NFS clusters that belong to vCenter Server 8 instances and were provisioned initially with vSphere 7, you can add ESXi servers either with vSphere 7.0u3 or vSphere 8.0u2.
* For clusters that belong to vCenter Server 8 instances and were provisioned initially with vSphere 8, you can add only ESXi servers with vSphere 8.0u2.
* For clusters that were provisioned initially with vSphere 8 ESXi servers, those servers use vSphere Distributed Switch (vDS) 8. You cannot add ESXi servers with vSphere 7 to a vSphere 8 cluster and its vDS.
* For ESXi servers with vSAN storage, you can add only vSphere 7 either with vCenter Server 7 or 8.
* For existing instances with VMware vSphere® 6.5 or 6.7, you cannot add ESXi servers. To add ESXi servers, upgrade your vSphere® software to 7.0. For more information, see [Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).

{{site.data.content.attnnote-addhost-byol}}

### For Automated instances with vSAN storage
{: #vc_addingservers-prereq-vsan}

Review the following additional information applicable to Automated instances with vSAN™ storage:

* Automated instances with vSAN storage must have at least 4 ESXi servers.
* If your initial cluster has vSAN storage, SED SSD disks are not available. Non-SED SSD disks are ordered.
* If you are adding ESXi servers to clusters provisioned after 24 August 2023, the servers are provisioned with mirrored M.2 boot drives.
* If you are adding ESXi servers to clusters provisioned before 24 August 2023, the servers are provisioned with mirrored M.2 boot drives only if you select a new bare metal server configuration.

### For Automated instances with NFS storage
{: #vc_addingservers-prereq-nfs}

Review the following additional information applicable to Automated instances with NFS storage:

* Automated instances with NFS storage must have at least 3 ESXi servers.
* If you are adding ESXi servers to clusters provisioned after 18 October 2023, the servers are provisioned with mirrored M.2 boot drives.
* If you are adding ESXi servers to clusters provisioned before 18 October 2023, the servers are provisioned with mirrored M.2 boot drives only if you select a new bare metal server configuration.

## Procedure to add ESXi servers to Automated instances
{: #vc_addingservers-procedure}
{: help}
{: support}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the instance for which you want to expand capacity.
3. Click the **Infrastructure** tab.
4. In the **Clusters** table, click the cluster to which you want to add ESXi servers.
5. In the **ESXi servers** section, click **Add**.
6. On the **Add ESXi server** side panel, enter the number of bare metal servers that you want to add. You can toggle the **Maintenance mode** switch on to add servers during maintenance mode.

   When you provision new ESXi servers, virtual machines (VMs) are immediately migrated to the new servers if you do not toggle the **Maintenance mode** switch on. You do not receive a confirmation message before the migration begins.
   {: important}

7. Complete the bare metal server configuration.
   1. Enter the number of bare metal servers.
      * For the consolidated cluster, you can order 1-51 servers in total, taking into account the existing number of hosts in the cluster.
      * For the workload cluster, you can order 1-59 servers in total, taking into account the existing number of hosts in the cluster.
   2. From the list, you can select a bare metal server configuration that is being used by the existing ESXi servers in the cluster. Then, click **Next**. This option is not available for existing ESXi servers with **Broadwell CPU** or if the storage type of the cluster is **Local disks**.
   3. You can also choose a new bare metal server configuration by selecting the option from the list and clicking **Next**. Select the **CPU model**, the **vSphere version** (vSphere 8 clusters only), the amount of **RAM**, and **vSAN** if you have vSAN storage type.

   

8. Click **Next** and complete the network settings.
    * You can continue to use the previously selected primary subnets.
    * You can specify different primary subnets. Then, use the lists to select the **Public primary subnet** and **Private primary subnet**.
    * If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on.
9. In the **Details** section, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Results after you add ESXi servers to Automated instances
{: #vc_addingservers-results}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to add ESXi servers is being processed. On the console, the status of the cluster that is associated with the ESXi servers is changed to **Modifying**.
3. If you do not see the new ESXi servers added to the list in the cluster, check your email or console notifications for more details.

If you are adding ESXi servers during maintenance mode, VMs are not migrated to the new servers until you remove maintenance mode.
{: important}

## Related links
{: #vc_addingservers-related}

* [Deleting Automated instances in a multisite configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletinginstance_multi)
* [Requirements for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Viewing Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Managing virtual servers](/docs/virtual-servers?topic=virtual-servers-managing-virtual-servers)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
