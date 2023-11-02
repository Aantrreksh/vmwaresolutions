---

copyright:

  years: 2023

lastupdated: "2023-10-12"

keywords: delete host, host remove, vmware cloud foundation, vmware cloud edition

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deleting ESXi servers from VMware Cloud Foundation instances
{: #vpc-vcf-host-deleting}

You can contract the capacity of your VMware Cloud Foundation™ instance according to your business needs by deleting VMware ESXi™ servers.

## Before you delete ESXi servers from VMware Cloud Foundation instances
{: #vpc-vcf-host-deleting-notes}

* Ensure that the current user has access to the {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) resources for the VMware Cloud Foundation instance from which you want to delete ESXi servers.
* Ensure that the number of remaining hosts after deletion still meets the minimum host requirements for each of the VMware Cloud Foundation clusters.
* You can delete only ESXi servers that are ordered or added through the VMware Solutions console.
* When the ESXi servers are deleted from the VMware Cloud Foundation instance, all its {{site.data.keyword.vpc_short}} resources (bare metal servers and the network interfaces of the servers) are also deleted from {{site.data.keyword.cloud}}.
* You can delete ESXi servers through automation only for the management and workload clusters in a VMware Cloud Foundation instance.

## Procedure to delete ESXi servers from VMware Cloud Foundation instances
{: #vpc-vcf-host-deleting-proc1}

1. From the VMware Solutions console, click **Resources > Cloud Foundation** from the left navigation pane.
2. In the **VMware Cloud Foundation** table, hover over the instance from which you want to delete ESXi servers.
3. Click **Edit hosts** on the row next to status.
4. In the **Hosts** section, select the servers that you want to delete and click **Remove hosts**.
5. In the **Remove hosts** window, type the hostname to confirm, then click **Delete**.

## Procedure to delete ESXi servers from the instance details page
{: #vpc-vcf-host-deleting-proc2}

1. From the VMware Solutions console, click **Resources > Cloud Foundation** from the left navigation pane.
2. In the **VMware Cloud Foundation** table, click the instance from which you want to delete ESXi servers.
3. Click the **Infrastructure** tab.
4. In the **Domains** table, click the domain from which you want to delete ESXi servers.
5. In the **Hosts** section, select the servers that you want to delete and click **Remove hosts**.
6. In the **Remove hosts** window, type the hostname to confirm, then click **Delete**.

## Results after you delete ESXi servers from VMware Cloud Foundation instances
{: #vpc-vcf-host-deleting-result}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email after you delete hosts from the VMware Cloud Foundation instance. If the operation is successful, the hosts are deleted from the **Hosts** table.

## Related links
{: #vpc-vcf-host-deleting-links}

* [VMware Cloud Foundation overview](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw)
* [Ordering VMware Cloud Foundation instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ordering)
* [Viewing VMware Cloud Foundation instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-viewing)
* [Deleting VMware Cloud Foundation instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-deleting)
