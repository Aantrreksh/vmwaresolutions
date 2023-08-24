---

copyright:

  years:  2021, 2023

lastupdated: "2023-08-17"

keywords: vCenter Server add NFS storage, add nfs

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding NFS storage to vCenter Server instances
{: #vc_addingnfs}

You can expand the capacity of your VMware vCenter Server® instance according to your business needs by adding Network File System (NFS) storage.

## Before you add NFS storage to vCenter Server instances
{: #vc_addingnfs-prereq}

* Adding NFS storage to vCenter Server instances with VMware vSphere® 6.5 is not supported.
* Do not add NFS storage from the VMware vSphere Web Client. The changes that you make on the vSphere Web Client are not synchronized with the {{site.data.keyword.vmwaresolutions_full}} console.
* IBM does not manage NFS file shares that you add manually to an instance.
* You can add or remove NFS storage shares to or from an existing NFS or vSAN cluster.
* If you mount {{site.data.keyword.cloud_notm}} Endurance NFS storage to your cluster, consider the following steps:
   * Ping the NFS server for the storage and note the subnet for the server IP address.
   * Review the VMKernel adapters for the hosts that will use the storage and make note of the subnet for `vmk3`. Use the [File Storage list](https://cloud.ibm.com/cloud-storage/file) to authorize the `vmk3` subnet to access the NFS datastore.
   * Review the static routes defined on the hosts with the `esxcli network ip route ipv4 list` command. A static route must be displayed for the NFS server IP subnet to the gateway for the `vmk3` subnet listed in the previous step.

## Procedure to add NFS storage to vCenter Server instances
{: #vc_addingnfs-procedure}

1. From the VMware Solutions console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance for which you want to expand capacity.
3. Click the **Infrastructure** tab.
4. In the **Clusters** table, click the cluster to which you want to add NFS storage.
5. In the **Storage** section, click **Add**.
6. In the **Add NFS storage** side panel, complete the storage configuration.
   * To add and configure the same settings to all file shares, specify the **Number of shares**, **Size (GB)**, and **Performance**.
   * To add and configure file shares individually, toggle the **Configure shares individually** switch on. Then, click **Add shared storage** and select the **Size (GB)** and **Performance** for each individual file share. You must select at least one file share. For more information, see [NFS storage](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-consold-cluster#vc_orderinginstance-nfs-storage).
7. Review the estimated price and click **Add**.

## Results after you add NFS storage to vCenter Server instances
{: #vc_addingnfs-results}

1. You might experience a slight delay on the console while the instance status changes from **Available** to **Modifying**. Allow the operation to complete before you make more changes to the instance.
2. You are notified by email that your request to add NFS storage is being processed. On the console, the status of the cluster that is associated with the NFS storage is changed to **Modifying**.
3. If you do not see that the new NFS storage is added to the list in the cluster, check your email or view the console notifications to find more details.

## Related links
{: #vc_addingnfs-related}

* [vCenter Server BOM](/docs/vmwaresolutions?topic=vmwaresolutions-vc_bom)
* [Planning for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_planning)
* [Requirements for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Adding clusters to vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingclusters)
* [Place a host in maintenance mode](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.resmgmt.doc/GUID-8F705E83-6788-42D4-93DF-63A2B892367F.html){: external}
