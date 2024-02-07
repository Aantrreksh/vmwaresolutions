---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-02"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Scanning and review
{: #vum-scanning}

When you scan hosts, virtual machines (VMs), and virtual appliances (VAs), you evaluate them against baselines and baseline groups to determine their levels of compliance. Inventory objects are scanned, and the results are reviewed to determine how they comply with the baselines and baseline groups. Scan results can be filtered by text search, group selection, baseline selection, and compliance status selection. You can initiate the following scans:
* **Manually Initiate a Scan of vSphere ESXi Hosts** - You can scan vSphere® ESXi™ hosts in the vSphere inventory against attached baselines and baseline groups.
* **Manually Initiate a Scan of Virtual Machines and Virtual Appliances** - You can scan VMs and VAs in the vSphere inventory against attached baselines and baseline groups.
* **Manually Initiate a Scan of a Container Object** - Starts a simultaneous scan of hosts, VMs, and VAs, by scanning a container object that is a data center or a data center folder.
* **Schedule a Scan** - You can configure the vSphere Web Client to scan VMs, VAs, and ESXi hosts at specific times or at intervals as needed.

## Manually initiating a scan of vSphere ESXi hosts
{: #vum-scanning-scan-hosts}

1. Click **Scan for Updates**, select **Patches and Extensions and Upgrades**, then click **OK**.
2. When the scan completes, select **Critical Host Patches**. In the lower pane, review the patch details for each host by clicking the number in **Number of Patches**. A window shows the patch information.
3. Review and repeat for **Non-Critical Patches**.

   The VMware Update Manager (VUM) log files are at _/var/log/vmware/vmware-updatemgr/vum-server/vmware-vum-server-log4cpp.log_.

## Manually initiating a scan of virtual machines and virtual appliances
{: #vum-scanning-scan-vm-va}

You can scan VMs and virtual appliances in the vSphere inventory against attached baselines and baseline groups. The VMs and appliances that you select are scanned against the attached baselines, depending on the options that you select. All child objects are scanned, so the larger the virtual infrastructure and the higher up in the object hierarchy that you initiate the scan, the longer the scan takes and the more accurate the compliance view is.

1. Using the vSphere Web Client, select **Home** > **VMs and Templates**.
2. Right-click a virtual machine, virtual appliance, or a folder of virtual machines and appliances and click **Scan for Updates**.
3. Select the types of updates to scan for. The options are Virtual Appliance upgrades, VM Hardware upgrades, and VMware Tools upgrades.
4. Click **Scan**.

## Manually initiating a scan of a container object
{: #vum-scanning-scan-container}

Start a simultaneous scan of hosts, VMs, and virtual appliances, by scanning a container object that is a data center or a data center folder.
1. Using the vSphere Web Client, select **Home** > **VMs and Templates**.
2. Right-click a datacenter or datacenter folder and click **Scan for Updates**.
3. Select the types of updates to scan for. The options are Virtual Appliance upgrades, VM Hardware upgrades, and VMware Tools upgrades.
4. Click **Scan**.

## Scheduling a scan
{: #vum-scanning-schedule}

You can configure the vSphere Web Client to scan VMs, virtual appliances, and vSphere ESXi hosts at specific times or at intervals that are convenient for you.

1. Using the vSphere Web Client, select an object from the inventory. All child objects of the object that you select are also scanned.
2. Select the **Monitor** tab and click **Task & Events**.
3. Select **Scheduled Tasks** and click **Schedule a New Task**.
4. Select **Scan for Updates** from the list that appears.
5. On the Edit Settings page, select the types of updates to scan the inventory object for. You must select at least one scan type. On the Scheduling options page, describe and schedule the scan task.
6. Enter a unique name, and optionally, a description for the scan task. Click **Change** to set the frequency and the start time for the scan task. Click **OK**.

The scan task is listed in the Scheduled Tasks view of the vSphere Web Client.

## Related links
{: #vum-scanning-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [VMware Solutions on {{site.data.keyword.cloud_notm}} Digital Technical Engagement](https://www.ibm.com/products/vmware)
