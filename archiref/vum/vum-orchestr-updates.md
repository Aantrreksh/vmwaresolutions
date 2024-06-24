---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Orchestrated upgrades
{: #vum-orchestr-updates}

You can use orchestrated upgrades to upgrade the virtual hardware and VMware® Tools of virtual machines in the inventory after you update the vSphere® ESXi™ hosts. After the hosts are updated, the VMware Tools upgrade baseline runs first, followed by the virtual machine hardware upgrade baseline. You can use orchestrated upgrades at a cluster, a folder, or a data center level.

VMware Update Manager (VUM) allows you to perform orchestrated upgrades of hosts and then virtual machines by using baseline groups. A baseline group is used that contains a single host upgrade baseline and multiple patch or extension baselines. VUM first upgrades the hosts and then applies the patch or extension baselines. You perform an orchestrated upgrade of virtual machines by using a virtual machine baseline group that contains the following baselines:
* VM Hardware Upgrade to Match Host
* VMware Tools Upgrade to Match Host

VUM orchestrated upgrades upgrade the inventory objects in VMware vCenter® Server Appliance (VCSA) in a two-step process. First, the vSphere ESXi hosts are upgraded followed by the virtual machine upgrades. You can configure this two-step process on a cluster level or configure it at the individual vSphere ESXi host or virtual machine level for more granular control.

In the orchestrated upgrade, the cluster is remediated first against the host baseline group, which applies patches, extensions and upgrades and after upgraded, the virtual machines in the cluster are remediated against the virtual machine upgrade baseline group that contains the VM Hardware Upgrade to Match Host and VMware Tools Upgrade to Match Host baselines.

If the baseline group also contains an upgrade baseline, VUM first upgrades the vSphere ESXi hosts, then applies the patch or extension baselines as the patches are applicable to the specific host version. For the virtual machines, VMware tools are first updated, followed by the virtual hardware update.

During the VMware tools upgrade, VUM powers VMs on if they are in powered-off or suspended state, runs the upgrade, and then restores the original power state of them. Therefore, during the virtual hardware upgrade, the VMs must be in powered-off state. If there are VMs that are powered on, VUM shuts them down, upgrades virtual hardware, and then powers them back on.

By default, the remediation of vSphere ESXi hosts happens in sequential manner and remediates one host at a time. When the remediation is completed for one host, VUM starts it for the next host. If you have adequate failover capacity in your cluster, you can change the default remediation setting to enable parallel remediation so that more than one host can be remediated at a time.

If the vSphere ESXi hosts are part of a vSAN cluster, the remediation process is always sequential even if you selected parallel remediation in the remediation wizard because only one host from a vSAN cluster can be in maintenance mode at any time. VUM is intelligent and carries out a calculation on how many hosts can be remediated in parallel without disrupting DRS settings.

Alternatively, you can define the limit for number of hosts that can be remediated in parallel during the remediation wizard.

The following workflow describes the process to perform an orchestrated upgrade:

## Step 1
{: #vum-orchestr-updates-step1}

1. Use the vSphere Web Client to log in to the VCSA.
2. Click **Home > Update Manager**.
3. On the **Objects** tab, select an **Update Manager instance**.
4. Click the **Manage** tab, click the **Host Baselines** tab, and then click **New Baseline Group**.
5. Enter a unique name for the baseline group and click **Next**.
6. Select a host upgrade baseline to include it in the baseline group.
7. Optionally, create a new host upgrade baseline by clicking **Create a new Host Upgrade Baseline** on the **Upgrades** page, and then complete the **New Baseline** wizard. Click **Next**.
8. Select the patch baselines that you want to include in the baseline group.
9. Optionally, create a new patch baseline by clicking **Create a new Host Patch Baseline** on the **Patches** page, and then complete the **New Baseline** wizard. Click **Next**.
10. Select the extension baselines to include in the baseline group.
11. Optionally, create a new extension baseline by clicking **Create a new Extension Baseline** on the **Patches** page, and then complete the **New Baseline** wizard.
12. Review the **Ready to Complete** page, and then click **Finish**. The host baseline group is displayed in the **Baseline Groups** pane.

## Step 2
{: #vum-orchestr-updates-step2}

1. Create a virtual machine baseline group, containing the VMware Tools Upgrade to Match Host baseline and the VM Hardware Upgrade to Match Host baseline, VUM Administration view.
2. Attach the baseline group to a vCenter container object that contains the virtual machines you want to upgrade.
3. Scan the container object to view the compliance state of the virtual machines in the container. You can start the scan manually or schedule a scan task.
4. Review the scan results displayed in the VUM Client Compliance view.
5. Remediate the non-compliant virtual machines in the container object to make them compliant with the attached baseline group. You can start the remediation manually or schedule a remediation task.

   * During an upgrade of VMware Tools, the virtual machines must be powered on. If a virtual machine is in a powered off or suspended state before remediation, VUM powers on the virtual machine. After the upgrade is completed, VUM restarts the virtual machine and restores the original power state of it.
   * During a virtual machine hardware upgrade, the virtual machines must be shut down. After the remediation is completed, VUM restores the original power state of the virtual machines. If a virtual machine is powered on, VUM powers it off, upgrades its hardware, and then powers it on.

You can now use these baseline groups in the scan, review, staging, and remediation processes.

## Related links
{: #vum-orchestr-updates-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
