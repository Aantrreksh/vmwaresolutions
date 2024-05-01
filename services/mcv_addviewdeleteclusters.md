---

copyright:

  years:  2021, 2024

lastupdated: "2024-04-12"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding clusters to {{site.data.keyword.vcf-auto-short}} multizone instances
{: #mcv_addviewdeleteclusters}

New deployments of {{site.data.keyword.vcf-auto}} multizone instances are no longer supported. You can still add and delete clusters, add and remove ESXi servers, and add and delete storage for existing multizone instances.
{: deprecated}

You can add workload or gateway clusters to {{site.data.keyword.vcf-auto-short}} multizone instances. When no longer needed, delete the clusters from your instance.

## Procedure to add workload clusters to Automated multizone instances
{: #mcv_addviewdeleteclusters-workload-procedure}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources** > **{{site.data.keyword.vcf-auto-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-auto-short}}r** table, click the multizone instance that you want to add the workload cluster to.
3. Click the **Infrastructure** tab and click **Create** on the upper right of the **Workload clusters** table.
4. On the **Create cluster** page, enter the cluster name.
5. Select the **CPU model**, the amount of **RAM**, and the **Number of bare metal servers**.
6. Specify the vSAN storage settings. Specify the disk types for the capacity and cache disks and the number of disks. Optionally, select the **Enable vSAN deduplication and compression** checkbox. For more information, see [Enable vSAN deduplication and compression](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingclusters#vc_addingclusters-vsan-storage-enable-comp).
7. On the **Summary** pane, review the cluster settings and the estimated price.
      * To save the settings as a new configuration template without placing an order, click **Save configuration**, enter a name for the configuration, and click **Continue**.
      * To save the updates to a saved configuration, click **Save configuration**, select **Modify current configuration**, and click **Continue**.
      * To save the updates to a new saved configuration, click **Save configuration**, select **Create new configuration**, enter a new name for the configuration, and click **Continue**.
8. To place the order, ensure that the account to be charged is correct, review and accept the terms, and click **Create**.

## Procedure to add gateway clusters to Automated multizone instances
{: #mcv_addviewdeleteclusters-edge-procedure}

You can add gateway clusters to your {{site.data.keyword.vcf-auto-short}} multizone instance if you did not select to enable during your initial order. When you add gateway clusters, you must add each cluster one at a time.

You cannot add more than one cluster in the same data center pod.
{: restriction}

1. From the VMware Solutions console, click **Resources** > **{{site.data.keyword.vcf-auto-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-auto-short}}** table, click the multizone instance that you want to add the gateway cluster to.
3. Click the **Infrastructure** tab and click **Create** on the upper right of the **Gateway clusters** table.
4. On the **Create cluster** page, select the data center to host the cluster, then enter the cluster name.
5. Select the amount of **RAM** and the **Number of bare metal servers**.
6. On the **Summary** pane, verify the cluster configuration before you add the cluster.
   1. Review the settings for the cluster.
   2. Review the estimated price of the cluster. Click **Pricing details** to generate a PDF summary. To save or print your order summary, click the **Print** or the **Download** icon ![Download icon](../../icons/download.svg "Download") on the upper right of the PDF window.
   3. Click the link or links of the terms that apply to your order, and confirm that you agree with these terms before you add the cluster.
   4. Click **Create**.
