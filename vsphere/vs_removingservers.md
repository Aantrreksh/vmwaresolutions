---

copyright:

  years:  2023

lastupdated: "2023-06-20"

keywords: vmware vSphere remove hosts, vmware vSphere remove ESXi servers, delete server

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting ESXi servers from VMware vSphere instances
{: #vs_removingservers}

You can contract the capacity of your VMware vSphere® instance according to your business needs by deleting VMware ESXi™ servers.

## Before you delete ESXi servers from VMware vSphere instances
{: #vs_removingservers-prereq}

Before you delete ESXi servers, ensure that you remove your workloads from these servers:
1. First, place the ESXi servers to delete in maintenance mode and migrate the VMs running on them manually using the VMware vSphere Web Client.
2. After that, delete the ESXi servers by using the VMware Solutions console.

## Procedure to delete ESXi servers from VMware vSphere instances
{: #vs_removingservers-procedure}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > vSphere** from the left navigation pane.
2. In the **vSphere** table, click the instance for which you want to contract capacity.
3. Click the **Infrastructure** tab.
4. In the **ESXi servers** section, select the servers that you want to delete and click **Delete**.
5. Click **Delete** in the **Delete ESXi server** window.

## Results after you delete ESXi servers from VMware vSphere instances
{: #vs_removingservers-results}

1. You might experience a slight delay on the console, while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to delete ESXi servers is being processed. On the console, the status of the instance is changed to **Modifying**.
3. The ESXi servers are fully reclaimed by {{site.data.keyword.cloud_notm}} infrastructure at the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle, which is typically 30 days.

   You are billed until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle for the deleted ESXi servers.
   {: note}

## Related links
{: #vs_removingservers-related}

* [Planning for VMware vSphere](/docs/vmwaresolutions?topic=vmwaresolutions-vs_planning)
* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [Place a host in maintenance mode](https://docs.vmware.com/en/VMware-vSphere/6.0/com.vmware.vsphere.resmgmt.doc/GUID-8F705E83-6788-42D4-93DF-63A2B892367F.html){: external}
* [Enhanced vMotion Compatibility (EVC) processor support](https://kb.vmware.com/s/article/1003212){: external}
