---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-17"

keywords: vCenter Server Hybridity add cluster, view cluster vCenter Server Hybridity, delete cluster vCenter Server Hybridity

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding, viewing, and deleting clusters for vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters}

The VMware ESXi™ servers that you configured when you ordered an instance are grouped as **cluster1** by default.

You can add clusters to your VMware vCenter Server® with Hybridity Bundle instance to expand the compute and storage capacity. Within a cluster, manage the ESXi servers for better resource allocation and high availability. When no longer needed, delete the added clusters from your instance.

## Adding clusters to vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-adding}

Adding clusters to instances with VMware vSphere® 6.5 is not supported.
{: note}

### Before you add clusters
{: #vc_hybrid_addingviewingclusters-before-add}

* {{site.data.content.para-vcenteraddclusters}}
* The number of clusters, hosts, and VMs determines the maximum number of clusters that you can add. You must remain within the VMware® sizing guidelines and limits for your deployment. For more information, see [VMware Configuration Maximums](https://configmax.vmware.com/home){: external}.

### System settings
{: #vc_hybrid_addingviewingclusters-adding-sys-settings}

When you add a cluster for a vCenter Server with Hybridity Bundle instance, you must specify the following settings.

#### Cluster name
{: #vc_hybrid_addingviewingclusters-adding-cluster-name}

The cluster name must meet the following requirements:
* Only alphanumeric and dash (-) characters are allowed.
* The cluster name must start and end with an alphanumeric character.
* The maximum length of the cluster name is 30 characters.
* The cluster name must be unique within the vCenter Server with Hybridity Bundle instance.

#### Data center location
{: #vc_hybrid_addingviewingclusters-adding-dc-location}

The {{site.data.keyword.cloud_notm}} data center location of the cluster is set to the {{site.data.keyword.cloud_notm}} data center of the vCenter Server instance by default. You can deploy the cluster to a different {{site.data.keyword.cloud_notm}} data center than the deployed instance. However, you must ensure that the network latency between the two {{site.data.keyword.cloud_notm}} data centers is less than 150 ms.

If you deploy the cluster to a different {{site.data.keyword.cloud_notm}} data center or {{site.data.keyword.cloud_notm}} infrastructure pod, three more VLANs are ordered for use with the ordered {{site.data.keyword.cloud_notm}} bare metal servers.

### Bare metal server settings
{: #vc_hybrid_addingviewingclusters-adding-bare-metal}

You can choose a **Cascade Lake** bare metal server, with options for the **CPU model** and **RAM**. Options might differ depending on the version that your instance was initially deployed in.

Cascade Lake bare metal servers are available only for VMware vSphere Enterprise Plus 6.7u3 instances.
{: note}

| CPU model options | Cores     | GHz     | RAM options |
|:----------------- |:----------|:--------|:----------- |
| Dual Intel Xeon Silver 4210 | 20 | 2.2 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 | 32 | 2.3 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 | 40 | 2.5 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6250 | 16 | 3.9 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 | 48 | 2.4 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 | 80 | 2.5 | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 | 96 | 2.4 | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 1. Options for Cascade Lake bare metal servers" caption-side="bottom"}

The Quad Intel Xeon Gold 6248 processor is available only if you add new clusters or new ESXi servers to existing instances.
{: note}

### Number of bare metal servers
{: #vc_hybrid_addingviewingclusters-adding-bare-metal-number}

You can order 4-59 servers. All servers have the same configuration.

### vSAN storage settings
{: #vc_hybrid_addingviewingclusters-adding-vsan-storage-settings}

VMware vSAN™ 6.6 was included with your initial vCenter Server with Hybridity Bundle instance order. Specify the following vSAN options:
* **Size for vSAN capacity disks** - Select an option for the capacity disks that you need.
* **Number of vSAN capacity disks** - Specify the number of capacity disks that you want to add.
* If you want to add more capacity disks, select the **High performance with Intel Optane** checkbox. This option provides two extra capacity disk bays that are useful for workloads that require less latency and higher IOPS throughput.
* Review the **Disk Type for vSAN Cache Disks** and **Number of vSAN cache disks** values. These values depend on whether you selected the **High performance with Intel Optane** checkbox.
* **vSAN license** - Select the VMware vSAN 6.6 license edition (Advanced or Enterprise).

### Licensing settings
{: #vc_hybrid_addingviewingclusters-adding-licensing-settings}

IBM-provided licenses for the following VMware components:
* vSphere Enterprise Plus 6.7u3
* VMware NSX® Service Providers 6.4 (Advanced or Enterprise edition)

### Network interface settings
{: #vc_hybrid_addingviewingclusters-adding-network-interface-settings}

Network interface card (NIC) settings are based on your selection of either **Public and private network** or **Private network only**. The following add-on services require public NICs and aren't available with the private option:
* F5® BIG-IP®
* FortiGate® Virtual Appliance

### Summary
{: #vc_hybrid_addingviewingclusters-adding-order-summary}

Based on your selected configuration for the cluster, the estimated price is instantly generated and displayed in the **Summary** pane. Click **Pricing details** to generate a PDF document with the price summary for the {{site.data.keyword.vmwaresolutions_short}} resources.

You can also add the provisioned resources to the {{site.data.keyword.cloud_notm}} estimate tool, by clicking **Add to estimate**. The tool is useful if you want to estimate the price of the selected {{site.data.keyword.vmwaresolutions_short}} resources together with other {{site.data.keyword.cloud_notm}} resources that you might consider purchasing.

## Procedure to add clusters to vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-adding-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance to view the clusters in it.

   Ensure that the instance status is **Available**. Otherwise, you can't add clusters to the instance.
   {: important}

3. Click the **Infrastructure** tab and click **Create** at the upper right of the **Clusters** table.
4. On the **Create cluster** page, enter the cluster name.
5. You can host the cluster in a different {{site.data.keyword.cloud_notm}} data center than the one that the instance is hosted in. To do so, under **Bare metal server**, toggle the **Select a different location** switch on and choose the {{site.data.keyword.cloud_notm}} data center to host the cluster.
6. Select the **CPU model**, the amount of **RAM**, and the **Number of bare metal servers** for the bare metal configuration.
7.  Select **vSAN storage** and specify the disk types for the capacity and cache disks and the number of disks. If you want more storage, select the **High performance with Intel Optane** checkbox.
8. Select the license edition for VMware vSAN for the license configuration.
9. Select the network setting of either **Public and private network** or **Private network only**.
10. On the **Summary** pane, verify the cluster configuration before you add the cluster.
    1. Review the settings for the cluster.
    2. Review the estimated price of the cluster. Click **Pricing details** to generate a PDF summary. To save or print your order summary, click the **Print** or **Download** icon on the upper right of the PDF window.
    3. Click the link or links of the terms that apply to your order, and confirm that you agree with these terms before you add the cluster.
    4. Click **Create**.

### Results after you add clusters to vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-adding-results}

1. The deployment of the cluster starts automatically and the status of the cluster is changed to **Initializing**. You can check the status of the deployment by viewing the deployment history on instance details page.
2. When the cluster is ready to use, its status changes to **Available**. The newly added cluster is enabled with vSphere High Availability (HA) and vSphere Distributed Resource Scheduler (DRS).

You can't change the cluster name. Changing the cluster name might cause the add or delete ESXi servers operations in the cluster to fail.
{: important}

## Procedure to view clusters in vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-viewing-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance to view the clusters in it.
3. Click the **Infrastructure** tab. In the **CLUSTERS** table, view the summary about the clusters.
   * **Name** - The name of the cluster.
   * **ESXi servers** - The number of ESXi servers in the cluster.
   * **CPU** - The CPU specification of the ESXi servers in the cluster.
   * **Customized vSAN disks** - The number of vSAN disks in the cluster, including the disk type and capacity.
   * **Memory** - The total memory size of the ESXi servers in the cluster.
   * **Data center location** - The {{site.data.keyword.cloud_notm}} data center where the cluster is hosted.
   * **Pod** - The pod where the cluster is deployed.
   * **Status** - The status of the cluster. The status can have one of the following values:
      * Initializing - The cluster is being created and configured.
      * Modifying - The cluster is being modified.
      * Available - The cluster is ready to use.
      * Deleting - The cluster is being deleted.
      * Deleted - The cluster is deleted.
4. Click a cluster name to view the ESXi servers, storage, and network interface details:
   * ESXi servers details
      * **Name** - The name of the ESXi server is in the format `<host_prefix><n>.<subdomain_label>.<root_domain>`, where:

           `host_prefix` is the hostname prefix,

           `n` is the sequence of the server,

           `subdomain_label` is the subdomain label, and

           `root_domain` is the root domain name.

      * **Version** - The version of the ESXi server.
      * **Credentials** - The username and password to access the ESXi server.
      * **Private IP** - The private IP address of the ESXi server.
      * **Status** - The status of the ESXi server, which can be one of the following values:
         * Available - The ESXi server is ready to use.
         * Adding - The ESXi server is being added.
         * Deleting - The ESXi server is being deleted.

   * Storage details
      * **Name** - The data store name.
      * **Size** - The capacity of the storage.
      * **IOPS/GB** - The performance level of the storage.
      * **NFS protocol** - The NFS version of the storage.
   * Network Interface - VLAN details
      * **VLAN number** - The unique VLAN number.
      * **Description** - The description of the VLAN.
      * **Location** - The data center location.
      * **Primary route** - The primary route of the VLAN.
       Click **View resource** to access the VLAN details.
   * Network Interface - Subnet details
      * **Name** - The subnet name. Click the name to access the subnet details.
      * **Type** - The type of subnet, primary or portable.
      * **Description** - The description of the subnet.
   * Network Interface - IP details
      * **IP** - The IP address.
      * **Status** - The status of the IP address.
      * **Description** - The description of the IP address.

## Deleting clusters from vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-deleting}

You might want to delete a cluster from an instance when it's no longer needed.

Deleting clusters from instances with vSphere 6.5 is not supported.
{: note}

### Before you delete clusters from vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-deleting-prereq}

* {{site.data.content.para-vcenterremoveclusters}}
* You can delete any cluster except for the first cluster (the one that is created during initial deployment).
* You can delete multiple clusters at a time. You can also delete a cluster while another cluster is being created or deleted.
* Ensure that all nodes in a cluster are powered on and operational before you delete the cluster.
* When you delete a cluster, all VMs (virtual machines) from the cluster are also deleted and they can't be recovered. If you want to keep the VMs, migrate them to other clusters.

## Procedure to delete clusters from vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingviewingclusters-deleting-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance that you want to delete clusters from.

   Ensure that the instance status is **Available**. Otherwise, you cannot delete clusters from the instance.
   {: important}

3. Click the **Infrastructure** tab. In the **CLUSTERS** table, locate the cluster that you want to delete and click the **Delete** icon in the **Actions** column.
