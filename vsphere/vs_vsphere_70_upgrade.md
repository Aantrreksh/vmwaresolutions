---

copyright:

  years:  2016, 2023

lastupdated: "2023-12-07"

keywords: vSphere upgrade, NSX upgrade, PSC upgrade

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0
{: #vs_vsphere_70_upgrade}

VMware vSphere® is a streamlined and optimized ordering platform for VMware®. With this platform, you can build your own {{site.data.keyword.IBM}}-hosted VMware environment by customizing and ordering the VMware-compatible hardware based on your selected VMware components.
{: shortdesc}

The {{site.data.keyword.vmwaresolutions_full}} console filters the hardware automatically, based on the VMware components that you select. For example, when you create a new all-flash VMware vSAN™ cluster, only the hardware that is validated against the [VMware compatibility guide](https://www.vmware.com/resources/compatibility/search.php){: external} is presented.

VMware vSphere does not automate the installation, configuration, and bring-up of the optional VMware components. The platform allows maximum of flexibility to design and build your hosted VMware environment while you incorporate VMware-compatible hardware.

Use this offering to create a new instance of VMware ESXi™ servers or scale out an existing instance of ESXi servers in an {{site.data.keyword.cloud_notm}} data center. Depending on the VMware components that you select, you can start with just one ESXi server and then scale the instance later as needed.

You must apply patches and upgrade the VMware software periodically, over the lifecycle of a vSphere Server instance.

The following procedure provides the steps that are required to convert a VMware vSphere 6.5 or 6.7-based instance to a vSphere 7-based instance. These steps provide the initial upgrade to vSphere, and vSAN 6.7. After this upgrade, you might need to use the normal vSphere functions to upgrade virtual machine (VM) hardware levels and tools. 

The following procedure is for VMware vSphere instances or IaaS bare metal roll-your-own provisions, covering ESXi, vCenter, and VSAN. 
{: Important}

If you are using the VMware vCenter Server® offering, migrate your instances to a vSphere 7.x environment. For more information, see the following topics:
* [{{site.data.keyword.cloud_notm}} VMware NSX-T architecture](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design)
* [NSX-V to NSX-T migration overview](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-overview)

## Important considerations
{: #vs_vsphere_70_upgrade-considerations}

* You are responsible to ensure that all VMware ESXi™ servers have proper firmware and drivers to support vSphere 7. Broadwell and Skylake servers are not supported. Research and plan carefully for Cascade Lake servers.
* {{site.data.keyword.cloud_notm}} supports only Cascade Lake bare metal servers for newly deployed vSphere 7 instances.
* If you add clusters or hosts to a vSphere 7 instance from the VMware Solutions console, only Cascade Lake bare metal servers are provisioned.
* After you upgrade, your existing clusters will continue to use N-VDS switches, which are deprecated by VMware. Support for N-VDS (NSX-T Virtual Distributed Switch) will be removed in a future VMware NSX-T™ release.
* If you are using VMware NSX-V, familiarize yourself with VMware product lifecycle for NSX-V and make appropriate plans to migrate your workloads to NSX-T.
* vCenter Server is designed to allow for a “rolling” upgrade. That is, virtual machine (VM) workloads that are currently functioning continue to function without an outage if you complete the following procedure. Enterprises must engage their change management policies to enable a structured and communicated upgrade and plan for contingencies. However, during the upgrade process of certain management functions, such as vCenter Server and NSX Manager, temporary outages of management functions, configuration changes, powering off and on VMs, might be impacted.

## Before you begin
{: #vs_vsphere_70_upgrade-prereq}

The time to complete the upgrade is unknown. It is possible that it might take several maintenance windows to completely upgrade an environment. Running up-leveled and down-leveled versions of the SDDC software is supported by VMware during the upgrade process. However, some functions such as vMotion, maybe limited during this process.

Complete the following requirements before you begin the upgrade:  
* Upgrade any extensions or snap-ins within the vCenter Server environment. Review the following documentation before you plan your upgrade:
   * [VMware vSphere 7.0 release notes](https://docs.vmware.com/en/VMware-vSphere/7.0/rn/vsphere-esxi-vcenter-server-70-release-notes.html){: external}
   * [About VMware ESXi upgrade](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.esxi.upgrade.doc/GUID-65B5B313-3DBB-4490-82D2-A225446F4C99.html){: external}
* Set up vSphere Update Manager (VUM) within your vCenter Server instance to download updates from VMware vSphere. For more information, see [VMware Update Manager introduction](/docs/vmwaresolutions?topic=vmwaresolutions-vum-intro#vum-intro).
* Open a support ticket with the {{site.data.keyword.vmwaresolutions_short}} team to notify them that an upgrade is being planned. The ticket remains open until the instance is registered at the upgraded level in the {{site.data.keyword.vmwaresolutions_short}} console.
* Confirm whether the vCenter Server instance that you are upgrading is linked to another vCenter Server instance as primary or secondary in the {{site.data.keyword.vmwaresolutions_short}} console. All linked instances must have their Platform Services Controllers (PSCs) upgraded first as part of a particular site upgrade.
* Confirm the following requirements for vSAN based instances:
   * Ensure that the vSAN Health tool is enabled and reports no critical errors. If critical errors are present, contact the IBM Support team with the upgrade support ticket ID.
   * Ensure that each node has space to handle rebuilding redundancy of vSAN objects in case an ESXi host fails to come back up during the upgrade. You might need to either reduce disk usage or add an ESXi host before the upgrade.  
   * Verify whether the overall vSAN volume usage is higher than 70%. You might need to either reduce disk usage or add an ESXi host before the upgrade.
*  Verify that the vCenter Server root user ID with its credentials are visible on the console. If your vCenter Server instance was initially ordered in a VMware Solutions version between V2.5 and V5.7, only the `customerroot` account is visible on the console. For new instances, clusters, hosts, and vCenter Server VMs ordered in VMware Solutions V5.7 and later, the `customerroot` user is no longer created by the VMware Solutions automation.
* Confirm that you have a [My VMware](https://my.vmware.com){: external} user ID for which to download the required binary files to upgrade. If you don't, contact IBM Support with the upgrade support ticket ID.
* Confirm that VUM is configured to reach `https://www.vmware.com` to download patches. If it can't be configured because of security policies, then you must manually download the most recent patch sets and upload them into VUM. For more information, see [VMware Update Manager introduction](/docs/vmwaresolutions?topic=vmwaresolutions-vum-intro#vum-intro).

## Supported upgrade paths
{: #vs_vsphere_70_upgrade-upgrade-paths}

The following table is a summary of the supported upgrade paths:

| Deployment offering | Supported paths | Unsupported paths |
|:------------------- |:--------------- |:----------------- |
| vCenter Server (VCS) with NSX-V instances with vSphere V6 | **Preferred path** \n Provision a new vCenter Server with NSX-T instance with vSphere V7 and migrate workloads. See [NSX-V to NSX-T migration](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-overview). \n **Alternative path** \n Self-upgrade by using the [upgrade procedure](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade). \n - For Cascade Lake servers, upgrade from vSphere V6 to V7. \n - Open a support ticket to obtain new V7 licenses. \n - Cluster expansion uses Cascade Lake servers. \n **Before December 2023**, you must provision a new vCenter Server with NSX-T instance with vSphere V7 and migrate workloads. See [NSX-V to NSX-T migration](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-overview). | - Broadwell and Skylake servers are not supported. \n - Add-on services to upgraded instance are not supported. |
| vCenter Server (VCS) with NSX-T instances with vSphere V6 | **Preferred path** \n Provision a new vCenter Server with NSX-T instance with vSphere V7 and migrate workloads. See [NSX-V to NSX-T migration](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-overview). \n **Alternative path** \n Upgrade the instance by using the [upgrade procedure](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade). \n - For Cascade Lake servers, upgrade from vSphere V6 to V7. \n  - Open a support ticket to obtain new V7 licenses. \n - Cluster expansion uses Cascade Lake servers. \n **Before December 2023**, provision a new vCenter Server instance with NSX-T and vSphere V7 and migrate workloads. See [NSX-V to NSX-T migration](/docs/vmwaresolutions?topic=vmwaresolutions-v2t-overview). | - Broadwell and Skylake servers are not supported. \n - Add-on services to upgraded instance are not supported. \n - Conversion of vSphere switching from N-VDS to VDS is not supported. |
| VMware vSphere Server (VSS) | **Preferred path** \n Consider provision vSphere bare metal server and deploy a new [VSS bare metal server](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview) or a bare metal server within [VPC Architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-overview). \n Upgrade your VMware vSphere servers by using [the upgrade procedure](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade). \n - For Broadwell servers, provision new servers as this server type is not supported by vSphere V7. \n - For Cascade Lake servers, upgrade from vSphere V6 to V7. \n - Open a support ticket to obtain new V7 licenses. \n - Cluster expansion uses Cascade Lake servers. | - Broadwell and Skylake servers are not supported. |
| Roll-your-own (classic bare metals servers) | **Preferred path** \n Consider provision vSphere bare metal server and deploy a new bare metal server or a bare metal server within [VPC Architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-overview). \n - Provision a new bare metal server with VMware ESXi V7. \n - Swap out the ESXi V6 servers. \n - Reload OS image with ESXi V7. \n **Alternative path** \n Consider provision a new bare metal server within [VPC Architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-overview). | - In-place upgrade from V6 to V7 is not supported. |
{: caption="Table 1. Upgrade paths for VMware Solutions offerings" caption-side="bottom"}

### Preparing your jump server
{: #vs_vsphere_70_upgrade-prereq-jumpbox}

Because the {{site.data.keyword.cloud_notm}} client access VPN is limited to 512 Kbps, take one of the following actions.
* Provision an {{site.data.keyword.cloud_notm}} Windows® 2012-2016 server Virtual Server Instance (VSI).
* Set up a similar Windows VM on a separate vCenter Server environment within the same {{site.data.keyword.cloud_notm}} data center.
   The Windows VM is used as a jump server into the vCenter Server instance for the upgrade that downloads the binary files from https://my.vmware.com. Do not place this VM on the vCenter Server instance that is being upgraded.

Complete the following steps to download files to your jump server:
1. From the VMware portal, download the following product files onto your jump server:
   * For VMware vCenter Server Appliance, `VMware-VCSA-all-7.0.1-17327517.iso`.
   * For ESXi 7, `VMware-ESXi-7.0U1c-17325551-depot.zip`.
   * For Hypervisor, `VMware-VMvisor-Installer-7.0U1c-17325551.x86_64.iso`.
2. Download the `007.1316.0000.0000_Unified_StorCLI_PUL.zip` file from `https://docs.broadcom.com/docs/007.1316.0000.0000_Unified_StorCLI_PUL.zip`.

## Procedure to upgrade vCenter Server vSphere software from 6.5 or 6.7 to 7.0
{: #vs_vsphere_70-upgrade-procedure}

### Before you begin
{: #vs_vsphere_70_upgrade-procedure-before}

* If you encounter a problem during the upgrade process, use the {{site.data.keyword.vmwaresolutions_short}} upgrade ticket that you opened at the beginning of the process to contact IBM Support. IBM Support then opens tickets with VMware Support if required.
* You must follow the support process to ensure that {{site.data.keyword.vmwaresolutions_short}} provides VMware Support with all the information about the vCenter Server design and setup, and the {{site.data.keyword.cloud_notm}} information.
* By following the support process, you ensure that accurate information is shared with VMware Support, which shortens the support experience. After IBM Support provides the necessary information to VMware Support, you can interact with VMware Support directly.
* Ensure that you keep a record of all the new passwords and credentials that you create as part of the upgrade process. IBM Support requires these credentials at the end of the upgrade process to update their internal database.

### Procedure to set the cluster Distributed Resource Schedule to manual
{: #vs_vsphere_70_upgrade-procedure-drs}

You must set the cluster Distributed Resource Schedule (DRS) to manual to prevent unexpected migrations during the upgrade process.

Complete the following steps from the vCenter Server user interface.

1. Select **Host and Clusters > Cluster > Configure > DRS**.
2. Click **EDIT**.
3. Set the **DRS** field to **Manual**.

### Procedure to create a standard switch for the new vCenter Server Appliance
{: #vs_vsphere_70_upgrade-procedure-vcsa}

Temporarily install the new vCenter Server Appliance that you deploy onto a vSphere Standard Switch. One of the existing `vmnics` is reassigned from the distributed switch during the upgrade.

Complete the following steps from the vCenter Server user interface.

1. Select **Hosts and Clusters > HOST > Configure > Virtual Switches**. Select a host for the new vCenter Server Appliance.
2. For the private network switch, select **Managed Physical Adapters**. The private network switch name ends with `-private`.
3. Select **uplink1/vmnic2**, then click the **Close** icon ![Close icon](../../icons/close-icon.svg "Close") to delete the adapter. Click **OK**.
4. Return to the **Virtual Switches** panel and click **Add Networking**.
   1. Select **Virtual Machine Port Group** for a standard switch and click **Next**.
   2. For **New Standard Switch**, set the MTU to 9000 and click **Next**.
   3. Click the green **Add** icon ![Add icon](../../icons/add.svg "Add") to add an adapter. Click **OK**, then **Next** to accept `vmnic2`.
   4. For **Connection Settings**, keep the **VM Network** and **VLAN ID None** defaults. Click **Next**, then **Finish**. *Standard Switch: vSwitch0* is displayed in the list of switches.
5. Make a note of the Network Setting for the vCenter Server Appliance VM. You must update the new vCenter appliance to match.
   * From the vCenter Server user interface, click the VM for the vCenter appliance. Note the name, ending with `vc`.
   * From the middle pane, click the **Networks** tab. Note the name of the distributed port group, ending with `-dpg-mgmt`. 

### Procedure to upgrade vCenter Server
{: #vs_vsphere_70_upgrade-procedure-vcenter}

Follow the VMware instructions for upgrading vCenter. For more information, see [Upgrade a vCenter Server Appliance 6.5 or 6.7 with an embedded Platform Services Controller by using the GUI](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vcenter.upgrade.doc/GUID-6A5C596D-103E-4024-9353-5569263EB427.html){: external}.

Ensure to complete the following requirements during the upgrade:

* Mount the VMware-VCSA ISO, go to the `visa-ui-installer\win32` directory, and run the installer.
* In the vCenter Server 7.0 installer dialog, select the **Upgrade** flow and complete the steps in the installer.
* You must use the IP and credentials (administrator and root) for the current vCenter Server appliance. Use the IP and root password for the ESXi host of the current vCenter Server Appliance and the host where you want to deploy the new 7.0 vCenter Server Appliance. You must use a new temporary IP address, gateway, and subnet mask for the new vCenter Server Appliance during installation.
* Complete Stage 2 when prompted. Ensure to note any warnings and take the appropriate actions.

### Procedure to upgrade Stor VIB (Broadcom driver)
{: #vs_vsphere_70_upgrade-procedure-broadcom}

You must upgrade the Broadcom driver before you upgrade the ESXi host.

1. Extract the `007.1316.0000.0000_Unified_StorCLI_PUL.zip` file to a directory on your windows jump server.
2. Locate the `vmware-storcli.vib` file in the extracted file contents.
3. Copy the `.vib` file to either a vSAN or NFS data store that is mounted on the ESXi hosts for the instance. Use vCenter Server to reference the extracted file on your jump server.
4. SSH into each ESXi host and run the following VIB Upgrade command: 
   `esxcli software vib update -v /<path to vsan or nfs datastore from step 3>/vmware-storcli.vib --no-sig-check`
   The following installation results are displayed.
    `Message: Operation finished successfully.    Reboot Required: false    VIBs Installed: Broadcom_bootbank_vmware-storcli_007.1316.0000.0000-01    VIBs Removed: LSI_bootbank_vmware-storcli_007.0916.0000.0000-01    VIBs Skipped:`
5. Run the following command to validate the installation:
   `> esxcli software vib list |grep vmware-storcli
   vmware-storcli    007.1316.0000.0000-01    Broadcom  PartnerSupported  2020-04-16`
6. Repeat for each host.

### Procedure to upgrade the ESXi hosts
{: #vs_vsphere_70_upgrade-procedure-esxi-upgrade}

1. From the vCenter Server user interface, go to **LCM menu > LifeCycle Manager**.
2. Select **IMPORT ISO > IMPORT ISO**. Then, select the `VMware-VMvisor-Installer-7.0U1c-17325551.iso` file.
3. Create the baseline. Select **BASELINE > CREATE** and use the imported ISO from the previous step.
4. For each host, choose the host in the vCenter browser tree. Then, select **update** (located in the far left in the main window).
5. If the Zerto VRA is present on the host, put the host into maintenance mode first. Recent releases of Zerto stop the VRA, which otherwise would prevent the update.
6. Complete the update.  
   1. [ATTACH] Baseline, select the previously created baseline.
   2. Select Baseline and [REMEDIATE].
7. Remediate each host in turn. After remediation, ensure to pull the host out of maintenance mode.

If the upgrade process fails immediately and the `host cannot enter maintenance mode` error message is displayed, shut down the Zerto ZVAs and try again. The ZVRA VMs automatically start as each server comes out of remediation. For more information about continuing Zerto replication during the upgrade process, see [How to place a host with an associated VRA into maintenance mode](https://www.zerto.com/myzerto/knowledge-base/how-to-place-a-host-with-an-associated-vra-into-maintenance-mode/){: external}.
{: note}

### Updating vCenter Server and ESXi host licenses
{: #vs_vsphere_70_upgrade-license-update}

After you upgrade the vCenter Server and ESXi hosts to vSphere 7, you must update the licenses on the vCenter Server and the ESXi hosts. If you have a vSAN cluster, you must update the vSAN license. [Contact IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) to obtain the new licenses for vSphere 7.

#### Procedure to update the vCenter Server license
{: #vs_vsphere_70_upgrade-license-update-vcs}

Complete the following steps from the vCenter Server user interface.

1. Select **Administration menu > Licensing > Licenses**.
2. From the **Licenses** page, click **+ Add New Licenses**.
3. Enter the new vCenter Server 7.0 license key in the **New Licenses** field. Then, enter a name for the license and click **OK**.
4. From the **Assets** page, select the vCenter instance under **VCENTER SERVER SYSTEMS** and click **Assign License**. Then, select the new license and click **OK**.
5. From the **Licenses** page, find the license with the product name **VMware vCenter Server 6 Standard** and click **Remove Licenses**.

#### Procedure to update ESXi host licenses
{: #vs_vsphere_70_upgrade-license-update-esxi}

1. From the **Licenses** page, click **+ Add New Licenses**.
2. Enter the new vSphere 7 license keys in the **New Licenses** field. If you have multiple vSphere 7 license keys, input the all of the licenses in the **New Licenses** filed, enter a name for each license, and click **OK**.
3. Complete the following steps from the **Assets** page.
   1. Select **HOSTS**.
   2. Select the host and click **Assign License**.
   3. Select one of the new vSphere 7 license keys and click **OK**.
   4. Repeat this step for each upgraded host.
4. From the **Licenses** page, select all of the old vSphere 6 licenses and click **Remove Licenses**.

#### Procedure to update the vSAN cluster license
{: #vs_vsphere_70_upgrade-license-update-vsan}

1. From the **Licenses** page, click **+ Add New Licenses**.
2. Enter the new vSAN license keys in the **New Licenses** field. If you have multiple vSAN license keys, enter all the licenses in the **New Licenses** field, specify a name for each license, and then click **OK**.
3. Complete the following steps from the **Assets** page.
   1. Select **VSAN CLUSTERS**.
   2. Select the vSAN cluster and click **Assign License**.
   3. Select one of the new vSAN license keys and click **OK**.
   4. Repeat this step for each vSAN cluster.
4. From the **Licenses** page, select all the old vSAN cluster licenses and click **Remove Licenses**.

### Procedure to remove the temporary standard switch
{: #vs_vsphere_70_upgrade-procedure-remove-switch}

Reassign the `vmnic` that you temporarily used on the standard switch back to the distributed switch it was originally associated with.

Complete the following steps from the vCenter Server user interface.

1. Go to the new vCenter Server appliance.
2. Under **Actions** click **Edit Settings**.
3. For network adapter 1, browse to the name of the distributed port group that ends with `-dpg-mgmt` that you previously noted. Save the changes.
4. Go to the host where you deployed the new appliance. Select **Hosts and Clusters > HOST > Configure > Virtual Switches**. Then, click **MANAGE PHYSICAL ADAPTERS** for *vSwitch0*.
5. Select **vmnic2** and click the red **X** to delete the adapter. Click **OK**. The `There are no active physical network adapters for the switch.` warning is displayed. Click **OK**.
6. Click the **...** in the *vSwitch0* display and then select **Remove**. Click **OK** to confirm you want to remove the switch.
7. In the same display, select the private switch and click **MANAGE PHYSICAL ADAPTERS**.
8. Select **uplink1** and click **+**. `vmnic2` is displayed.
9. Click **OK**, and then **OK** again to exit the window.

## Related links
{: #vs_vsphere_70_upgrade-related}

* [About vCenter Server upgrade](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vcenter.upgrade.doc/GUID-9ED7B32A-019F-4A97-BC58-1A9BF7D16C57.html){: external}
* [About VMware ESXi upgrade](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.esxi.upgrade.doc/GUID-65B5B313-3DBB-4490-82D2-A225446F4C99.html){: external}
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
