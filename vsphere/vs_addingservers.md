---

copyright:

  years:  2023

lastupdated: "2023-08-15"

keywords: vmware vSphere add host, add server vmware vSphere

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding ESXi servers to VMware vSphere instances
{: #vs_addingservers}

You can expand the capacity of your VMware vSphere® instance according to your business needs by adding VMware ESXi™ servers.

## Before you add ESXi servers to VMware vSphere instances
{: #vs_addingservers-prereq}

* For existing instances with VMware vSphere® 6.5 or 6.7, you cannot add ESXi servers. To add ESXi servers, upgrade your vSphere® software to 7.0. For more information, see [Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphere_70_upgrade).
* For existing instances with vSphere 7.0u2, you can add only ESXi servers with vSphere 7.0u3.
* You can add up to 59 ESXi servers to a VMware vSphere instance.

For VMware vSphere instances with vSAN:
* If you are adding ESXi servers to instances provisioned after 23 August 2023, the servers are provisioned with mirrored M.2 drives.
* If you are adding ESXi servers to instances provisioned before 23 August 2023, the servers are provisioned with mirrored M.2 drives only if you select a new bare metal server configuration.

## Procedure to add ESXi servers to VMware vSphere instances
{: #vs_addingservers-procedure}
{: help}
{: support}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > VMware vSphere** from the left navigation pane.
2. In the **VMware vSphere** table, click the instance for which you want to expand capacity.
3. Click the **Infrastructure** tab.
4. In the **ESXi servers** section, click **Add**.
5. On the **Add ESXi server** side panel, enter the number of bare metal servers that you want to add.
6. From the list, select a bare metal server configuration and click **Next**.
7. Complete the networking settings:
    * You can use the previously selected primary subnets.
    * You can specify different primary subnets. Then, use the list to select the **Private primary subnet**.
    * If you want to customize the hostnames prefix individually, toggle the **Configure hostnames individually** switch on and enter the hostname prefix.
8. In the **Details** section, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Results after you add ESXi servers to VMware vSphere instances
{: #vs_addingservers-results}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to add ESXi servers is being processed. On the console, the status of the instance is changed to **Modifying**.
3. If you do not see the new ESXi servers added to the instance, check your email or console notifications for more details.

## Related links
{: #vs_addingservers-related}

* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [Viewing VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_viewinginstances)
* [Requirements for VMware vSphere](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
