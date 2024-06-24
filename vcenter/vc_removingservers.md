---

copyright:

  years:  2021, 2024

lastupdated: "2024-05-16"

keywords: vcf classic remove hosts, vcf automated remove ESXi servers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting ESXi servers from Automated instances
{: #vc_removingservers}

You can contract the capacity of your {{site.data.keyword.vcf-auto}} instance according to your business needs by deleting VMware ESXi™ servers.

## Before you delete ESXi servers from Automated instances
{: #vc_removingservers-prereq}

* Deleting ESXi servers from instances with VMware vSphere® 6 is not supported.
* For the gateway cluster, you cannot add or delete ESXi servers.

{{site.data.content.para-vcenterremoveESXiservers}}

* When you delete ESXi servers, the servers are placed in maintenance mode, and then, all the virtual machines (VMs) running on the servers are migrated before they are deleted from vCenter Server. For maximum of control over the relocation of VMs, place the ESXi servers in maintenance mode and migrate the VMs running on them manually using the VMware vSphere Web Client. After that, delete the ESXi servers by using the VMware Solutions console.
* If you are using NFS storage, NSX-T™ instances require at least three ESXi servers for a consolidated cluster or at least two servers for any other cluster. NSX-V instances require at least two ESXi servers.
* If you are using vSAN storage, at least four ESXi servers are required.
* (NSX-V only) If F5® BIG-IP® or FortiGate® Virtual Appliance is installed on your ESXi server, you must migrate the F5 BIG-IP and FortiGate VMs to a different ESXi server than the one that is hosting the VMs.
* (NSX-V only) If IBM Spectrum® Protect Plus is installed on your ESXi server, ensure that there are no active (failed or in progress) backup or restore operations. These active operations might prevent the ESXi server from being deleted.

## Procedure to delete ESXi servers from Automated instances
{: #vc_removingservers-procedure}

1. From the VMware Solutions console, click **Resources > {{site.data.keyword.vcf-classic-short}}** from the left navigation pane.
2. In the **{{site.data.keyword.vcf-classic}}** table, click the instance for which you want to contract capacity.
3. Click the **Infrastructure** tab.
4. In the applicable cluster table, click the cluster from which you want to delete ESXi servers.
5. In the **ESXi servers** section, select the servers that you want to delete and click **Delete**.
6. Click **Delete** in the **Delete ESXi server** window.

## Results after you delete ESXi servers from Automated instances
{: #vc_removingservers-results}

1. You might experience a slight delay on the console, while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to delete ESXi servers is being processed. On the console, the status of the cluster that is associated with the ESXi servers is changed to **Modifying**.
3. The ESXi servers are fully reclaimed by {{site.data.keyword.cloud_notm}} infrastructure at the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle, which is typically 30 days.

   You are billed until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle for the deleted ESXi servers.
   {: note}

## Related links
{: #vc_removingservers-related}

* [{{site.data.keyword.vcf-auto-short}} BOM](/docs/vmwaresolutions?topic=vmwaresolutions-vc_bom)
* [Planning for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_planning)
* [Ordering Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Deleting clusters from Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingclusters)
* [Place a host in maintenance mode](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-resource-management/GUID-8F705E83-6788-42D4-93DF-63A2B892367F.html?hWord=N4IghgNiBcIAoTAYwKYAIxoBYHsDOALmgJYB2aAtmGQSqWKapTgCYogC+QA){: external}
* [Enhanced vMotion Compatibility (EVC) processor support](https://knowledge.broadcom.com/external/article?legacyId=1003212){: external}
