---

copyright:

  years:  2023, 2024

lastupdated: "2024-08-05"

keywords: flexible instance add host, add server flexible instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding ESXi servers to Flexible instances
{: #vs_addingservers}

You can expand the capacity of your {{site.data.keyword.vcf-flex}} instance according to your business needs by adding VMware ESXi™ servers.

## Before you add ESXi servers to Flexible instances
{: #vs_addingservers-prereq}

### For all Flexible instances
{: #vs_addingservers-prereq-all}

Review the following information applicable to all Flexible instances:

* You can add up to 59 ESXi servers to a Flexible instance.
* For existing instances with VMware vSphere® 6.5 or 6.7, you cannot add ESXi servers. To add ESXi servers, upgrade your vSphere® software to 7.0. For more information, see [Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).

{{site.data.content.attnnote-addhost-byol}}

### For Flexible instances with vSAN storage
{: #vs_addingservers-prereq-vsan}

Review the following additional information applicable to Flexible instances with vSAN™ storage:

* If you are adding ESXi servers to instances provisioned after 24 August 2023, the servers are provisioned with mirrored M.2 boot drives.
* If you are adding ESXi servers to instances provisioned before 24 August 2023, the servers are provisioned with mirrored M.2 boot drives only if you select a new bare metal server configuration.

## Procedure to add ESXi servers to Flexible instances
{: #vs_addingservers-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the Flexible instance for which you want to expand capacity.
3. Click the **Infrastructure** tab.
4. In the **ESXi servers** section, click **Add**.
5. On the **Add ESXi server** side panel, enter the number of bare metal servers that you want to add.
6. Complete the bare metal server configuration.
   * From the list, you can select a bare metal server configuration that is being used by the existing ESXi servers in the cluster. Then, click **Next**. This option is not available under the following conditions:
     * The bare metal configuration that is used by the existing ESXi servers in the cluster is **Broadwell**.
     * The storage type of the cluster is **Local disks**.
   * You can also choose a new bare metal server configuration by selecting the option from the list and clicking **Next**. Select the **CPU model**, the amount of **RAM**, and **vSAN** if you have vSAN storage type.
7. Click **Next** and complete the network settings.
   * You can use the previously selected primary subnets.
   * You can specify different primary subnets. Then, use the list to select the **Private primary subnet**.
   * If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on and enter the hostname prefix.
8. In the **Details** section, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Results after you add ESXi servers to Flexible instances
{: #vs_addingservers-results}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to add ESXi servers is being processed. On the console, the status of the instance is changed to **Modifying**.
3. If you do not see the new ESXi servers added to the instance, check your email or console notifications for more details.

## Related links
{: #vs_addingservers-related}

* [Procedure to order Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [Viewing Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_viewinginstances)
* [Requirements for Flexible instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
