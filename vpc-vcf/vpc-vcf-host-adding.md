---

copyright:

  years: 2023, 2024

lastupdated: "2024-04-05"

keywords: add host, host adding, vmware cloud foundation, vmware cloud edition

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Adding ESXi servers to {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-host-adding}

You can increase or decrease the capacity of your deployment by adding or deleting hosts to and from a cluster.

## Before you add ESXi servers to {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-host-adding-before}

* You can add hosts only when the {{site.data.keyword.vcf-vpc}} instance is in **Available** status.
* You can add hosts only to one domain at a time.
* Ensure that the current user has access to the {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) resources of the {{site.data.keyword.vcf-vpc-short}} instance to which you want to add ESXi servers.
* In a {{site.data.keyword.vcf-vpc-short}} environment with a Consolidated architecture, the new VMware ESXi™ servers are added to the management cluster. In a {{site.data.keyword.vcf-vpc-short}} environment with a Standard architecture, the new VMware ESXi™ servers can be added to both the management and the workload cluster.
* The new ESXi servers are configured with the same profile as the other servers in the cluster. vSAN storage is offered.
* When you add ESXi servers to your infrastructure, they are provisioned with the same version that was initially configured during the setup process. 
* Adding ESXi servers through automation is provided only for management and workload clusters in a {{site.data.keyword.vcf-vpc-short}} instance.

## Procedure to add ESXi servers from the resources page
{: #vpc-vcf-host-adding-proc1}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-vpc-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-vpc}}** table, hover over the instance to add ESXi servers.
3. Click the **Edit hosts** link on the row next to status.
4. In the **Hosts** section, click **Add host**.
5. On the **Add host** side panel, enter the number of hosts that you want to add in the **Host quantity** field. Keep the default value for **Host name suffix** or enter the suffix for each newly added host. Ensure that the suffix is unique across the domain.
6. In the **Summary** section on the side panel, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Procedure to add ESXi servers from the instance details page
{: #vpc-vcf-host-adding-proc2}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-vpc-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-vpc}}** table, click the instance to add ESXi servers to.
3. Click the **Infrastructure** tab.
4. In the **Domains** table, click the domain to add ESXi servers to.
5. In the **Hosts** section, click **Add host**.
6. On the **Add host** side panel, enter the number of hosts that you want to add in the **Host quantity** field. Keep the default value for **Host name suffix** or enter the suffix for each newly added host. Ensure that the suffix is unique across the domain.
7. In the **Summary** section on the side panel, review the estimated pricing, ensure that the account to be charged is correct, and review and accept the terms. Then, click **Add**.

## Results after you add ESXi servers to {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-host-adding-result}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email after you add hosts to the {{site.data.keyword.vcf-vpc-short}} instance. If the operation is successful, you can view the newly added hosts on the **Hosts** table.

## Related links
{: #vpc-vcf-host-adding-links}

* [{{site.data.keyword.vcf-vpc-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw)
* [Ordering {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ordering)
* [Viewing {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-viewing)
* [Deleting {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-deleting)
