---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Virtual machine vSAN redundancy
{: #vum-vsan-redundancy}

When you place a vSphere® ESXi™ host into maintenance mode on a vSAN™ cluster, you are required to select a data evacuation mode. The selection of the mode can have an impact upon the virtual machines (VMs) and appliances that are using the vSAN datastore:
* A **full data migration** evacuates all data from the host and moves it to the other vSphere ESXi hosts in the vSAN cluster. This evacuation mode results in the largest amount of data transfer and uses the most time and resources. All the components on the local storage of the selected host are migrated elsewhere in the cluster. When the host enters maintenance mode, all VMs and appliances have access to their storage components and are still compliant with their assigned storage policies. Full data evacuation can take a long time and can make the maintenance window for an upgrade long in duration.
* The **ensure accessibility data evacuation** mode is the default option and when the vSphere ESXi host is placed in maintenance mode, vSAN ensures that all accessible VMs or appliances on the host remain accessible. As only partial data evacuation occurs, the VM or appliance might no longer be fully compliant to a VM storage policy during evacuation and it might not have access to all its replicas. If a failure occurs while the host is in maintenance mode and the primary level of failures to tolerate is set to 1, data loss occurs, and the VM or appliance might be unavailable.
* In the **no data migration** mode, vSAN does not evacuate any data from the host while it enters maintenance mode. While this reduces the time to enter maintenance mode and hence reduces the duration of the maintenance window, some VMs or appliances might become inaccessible.

This section creates a new VM storage policy that allows the **ensure accessibility data evacuation** mode to be selected to reduce maintenance windows, but reducing the risk that a failure of a host while another is in maintenance mode makes a VM or appliance inaccessible. For any VM or appliance, where becoming nonredundant when a vSAN host is placed into maintenance mode is not acceptable, complete the following process before you complete any remediation actions. A cluster with at least six hosts is required.

1. Create a vSAN profile with the settings of RAID 5/6 and FTT =2 (RAID 6), and then apply this policy against the required VMs or appliances.

2. Wait until vSAN completed syncing before you initiate any remediation actions. The completion status can be checked by navigating to the **vSAN Virtual Objects monitoring page** for the cluster and reviewing the **Completion Status**.

## Related links
{: #vum-vsan-redundancy-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
