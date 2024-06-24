---

copyright:

  years:  2021, 2024

lastupdated: "2024-05-16"

keywords: vcf classic remove NFS storage

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Removing NFS storage from Automated instances
{: #vc_removingnfs}

You can contract the capacity of your {{site.data.keyword.vcf-auto}} instance according to your business needs by removing Network File System (NFS) storage.

## Before you remove NFS storage from Automated instances
{: #vc_removingnfs-prereq}

* Removing NFS storage from instances with VMware vSphere® 6.5 is not supported.
* Do not remove NFS storage from the VMware vSphere Web Client. The changes that you make on the vSphere Web Client are not synchronized with the {{site.data.keyword.vmwaresolutions_full}} console.
* Before you remove the NFS storage, ensure that you removed all the VMs that reside on the storage.
* Ensure that the shares that you plan to remove are associated with the correct Automated instance.
* The cluster status must be **Available**.
* You can remove NFS storage shares from an existing NFS or vSAN cluster.

## Procedure to remove NFS storage from Automated instances
{: #vc_removingnfs-procedure}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the instance for which you want to contract capacity.
3. Click the **Infrastructure** tab.
4. In the applicable cluster table, click the cluster from which you want to remove NFS storage.
5. In the **Storage** section, select the storage share that you want to remove and click **Delete**.
6. Click **Remove** in the **Remove storage** window.

## Results after you remove NFS storage from Automated instances
{: #vc_removingnfs-results}

1. You might experience a slight delay on the console, while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to remove NFS storage is being processed. On the console, the status of the cluster that is associated with the NFS storage is changed to **Modifying**.
3. The NFS storage is fully reclaimed by {{site.data.keyword.cloud_notm}} infrastructure at the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle, which is typically 30 days.

   You are billed until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle for the removed NFS storage.
   {: note}

## Related links
{: #vc_removingnfs-related}

* [{{site.data.keyword.vcf-auto-short}} BOM](/docs/vmwaresolutions?topic=vmwaresolutions-vc_bom)
* [Planning for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_planning)
* [Ordering Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Deleting clusters from Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingclusters)
* [Place a host in maintenance mode](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-resource-management/GUID-8F705E83-6788-42D4-93DF-63A2B892367F.html?hWord=N4IghgNiBcIAoTAYwKYAIxoBYHsDOALmgJYB2aAtmGQSqWKapTgCYogC+QA){: external}
* [Enhanced vMotion Compatibility (EVC) processor support](https://knowledge.broadcom.com/external/article?legacyId=1003212){: external}
