---

copyright:

  years: 2024

lastupdated: "2024-10-18"

keywords: vCenter upgrade, NSX upgrade, PSC upgrade, vcenter 8

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Upgrading to vCenter Server 8.0
{: #vc_vcs_80_upgrade}

You can upgrade the VMware vCenter Server® software on your instances to version 8.0. After that, you can migrate your NFS and gateway clusters to VMware vSphere® 8.0.

## Before you begin
{: #vc_vcs_80_upgrade-prereq}

{{site.data.content.para-vcs80upgrade-prereq}}

Complete the following requirements before you begin the upgrade:

* Open a support ticket with the {{site.data.keyword.vmwaresolutions_full}} team to notify them that an upgrade is being planned. The ticket remains open until the instance is registered at the upgraded level in the {{site.data.keyword.vmwaresolutions_short}} console.
* Verify that the vCenter Server `root` user ID and its credentials are visible on the console. If your instance was initially ordered in a VMware Solutions environment V2.5 to V5.7, only the `customerroot` account is visible on the console. For instances, clusters, hosts, and vCenter Server VMs ordered in VMware Solutions V5.7 and later, the `customerroot` user is no longer created by the VMware Solutions automation.
* If you encounter a problem during the upgrade process, use the {{site.data.keyword.vmwaresolutions_short}} upgrade ticket that you opened at the beginning of the process to contact IBM Support. IBM Support then opens tickets with VMware Support if required.
* Follow the support process to ensure that {{site.data.keyword.vmwaresolutions_short}} provides VMware Support with all the information about the vCenter Server design and setup, and the {{site.data.keyword.cloud}} information.
* By following the support process, you ensure that accurate information is shared with VMware Support, which shortens the support experience. After IBM Support provides the necessary information to VMware Support, you can interact with VMware Support directly.
* Ensure that you keep a record of all the new passwords and credentials that you create as part of the upgrade process. IBM Support requires these credentials at the end of the upgrade process to update its internal database.

## Procedure to upgrade to vCenter Server 8.0
{: #vc_vcs_80_upgrade-procedure-vcenter}

1. **Set the cluster Distributed Resource Schedule to Manual.** You must set the cluster Distributed Resource Schedule (DRS) to manual to prevent unexpected migrations during the upgrade process.
   Complete the following steps from the vCenter Server user interface.
   1. Select **Host and Clusters > Cluster > Configure > DRS**.
   2. Click **EDIT**.
   3. Set the **DRS** field to **Manual**.
2. **Create a standard switch for the new vCenter Server Appliance.** Temporarily install the new vCenter Server Appliance that you deploy onto a vSphere Standard Switch. One of the existing ``vmnics`` is reassigned from the distributed switch during the upgrade.
   Complete the following steps from the vCenter Server user interface.
   1. Select **Hosts and Clusters > HOST > Configure > Virtual Switches**. Select a host for the new vCenter Server Appliance.
   2. For the private network switch, select **Managed Physical Adapters**. The private network switch name ends with ``-private``.
   3. Select **uplink1/vmnic2**, then click **Close** ![Close icon](../../icons/close-icon.svg "Close") to delete the adapter. Click **OK**.
   4. Return to the **Virtual Switches** and click **Add Networking**.
      1. Select **Virtual Machine Port Group** for a standard switch and click **Next**.
      2. For **New Standard Switch**, set the MTU to 9000 and click **Next**.
      3. Click the green **Add** icon ![Add icon](../../icons/add.svg "Add") to add an adapter. Click **OK**, then **Next** to accept ``vmnic2``.
      4. For **Connection Settings**, keep the **VM Network** and **VLAN ID None** defaults. Click **Next**, then **Finish**. *Standard Switch: vSwitch0* is displayed in the list of switches.
   5. Make a note of the Network Setting for the vCenter Server Appliance VM. Update the new vCenter appliance to match.
      * From the vCenter Server user interface, click the VM for the vCenter appliance. Note the name that ends with ``vc``.
      * From the middle pane, click the **Networks** tab. Note the name of the distributed port group, ending with ``-dpg-mgmt``.
3. **Upgrade vCenter Server.** Follow the VMware instructions for upgrading vCenter Server. For more information, see [Upgrade a vCenter Server Appliance 6.7 with an Embedded Platform Services Controller or 7.0 by Using the GUI](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-vcenter-upgrade/GUID-6A5C596D-103E-4024-9353-5569263EB427.html){: external}.
   Ensure to complete the following requirements during the upgrade:
   * Mount the VMware-VCSA ISO, go to the `visa-ui-installer\win32` directory, and run the installer.
   * In the vCenter Server 8.0 installer window, select the **Upgrade** flow and complete the steps in the installer.
   * Use the IP and credentials (administrator and root) for the current vCenter Server Appliance. Use the IP and root password for the ESXi host of the current vCenter Server Appliance and the host where you want to deploy the new 8.0 vCenter Server Appliance. Use a new temporary IP address, gateway, and subnet mask for the new vCenter Server Appliance during installation.
   * Complete Stage 2 when prompted. Ensure to note any warnings and take the appropriate actions.

   After you upgrade to version 8, in the VMware vCenter Server Appliance, the details pane for the vCenter object takes several minutes to load. This problem is resolved if you enable the connection of the vCenter Server Appliance to the VMware update repository.
   {: important}

4. **Update vCenter Server and ESXi host licenses.** After you upgrade to vCenter Server 8.0, update the licenses on vCenter Server. If you have a vSAN™ cluster, you must also update the vSAN license. For more information about obtaining a new vCenter Server 8.0 license, see [Ordering VMware licenses](/docs/vmware?topic=vmware-ordering-vmware-license). For assistance with new licenses, [contact IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
   * **Procedure to update the vCenter Server license**:
      Complete the following steps from the vCenter Server user interface.
      1. Select the **Administration menu > Licensing > Licenses**.
      2. From the **Licenses** page, click **+ Add New Licenses**.
      3. Enter the new vCenter Server 8.0 license key in the **New Licenses** field. Then, enter a name for the license and click **OK**.
      4. From the **Assets** page, select the instance under **VCENTER SERVER SYSTEMS** and click **Assign License**. Then, select the new license and click **OK**.
      5. From the **Licenses** page, find the license with the product name **VMware vCenter Server 6 Standard** and click **Remove Licenses**.
   * **Procedure to update the vSAN cluster license**:
      1. From the **Licenses** page, click **+ Add New Licenses**.
      2. Enter the new vSAN license keys in the **New Licenses** field. If you have multiple vSAN license keys, enter all the licenses in the **New Licenses** field, specify a name for each license, and then click **OK**.
      3. Complete the following steps from the **Assets** page.
         1. Select **VSAN CLUSTERS**.
         2. Select the vSAN cluster and click **Assign License**.
         3. Select one of the new vSAN license keys and click **OK**.
         4. Repeat this step for each vSAN cluster.
      4. From the **Licenses** page, select all the old vSAN cluster licenses and click **Remove Licenses**.
5. **Remove the temporary standard switch.** Reassign the ``vmnic`` that you temporarily used on the standard switch back to the distributed switch it was originally associated with.
   Complete the following steps from the vCenter Server user interface.
   1. Go to the new vCenter Server appliance.
   2. Under **Actions** click **Edit Settings**.
   3. For network adapter 1, browse to the name of the distributed port group that ends with ``-dpg-mgmt`` that you previously noted. Save the changes.
   4. Go to the host where you deployed the new appliance. Select **Hosts and Clusters > HOST > Configure > Virtual Switches**. Then, click **MANAGE PHYSICAL ADAPTERS** for *vSwitch0*.
   5. Select **vmnic2** and click the red **X** to delete the adapter. Click **OK**. The ``There are no active physical network adapters for the switch.`` warning is displayed. Click **OK**.
   6. Click the **...** in the *vSwitch0* display and then select **Remove**. Click **OK** to confirm you want to remove the switch.
   7. In the same display, select the private switch and click **MANAGE PHYSICAL ADAPTERS**.
   8. Select **uplink1** and click **+**. `vmnic2` is displayed.
   9. Click **OK**, and then **OK** again to exit the window.

## Procedure to migrate from vSphere 7.0 to vSphere 8.0
{: #vc_vcs_80_migrate-procedure-vsphere}

You cannot migrate a vSAN cluster to vSphere 8.0.
{: important}

If you have a gateway cluster with vSphere 7.0 and you want to migrate it to vSphere 8.0, complete the following tasks:
1. Create a new vSphere 8.0 gateway cluster.
2. Carefully coordinate the migration of your gateway virtual machines and configuration from the old cluster to the new cluster. This way your protected VLANs do not lose service or connectivity. This action includes migration of the virtual machines and their configuration, or creation of new virtual machines with duplicate configuration. As part of this sequence, remove your protected VLANs from protection of the old cluster and assign them to the new cluster.
3. Remove the original gateway cluster.

If you have an NFS cluster with vSphere 7.0 and you want to migrate it to vSphere 8.0, perform a rolling replacement of servers in the cluster. For each vSphere 7.0 server, complete the following tasks:
1. Create a new vSphere 8.0 server.
2. Ensure that the vSphere 8.0 server is configured to your needs and remove it from maintenance mode.
3. Put the vSphere 7.0 server into maintenance mode.
4. Remove the vSphere 7.0 server from your cluster.









## Related links
{: #vc_vcs_80_upgrade-related}

* [About vCenter Server upgrade](https://docs.vmware.com/en/VMware-vSphere/8.0/vsphere-vcenter-upgrade/GUID-9ED7B32A-019F-4A97-BC58-1A9BF7D16C57.html){: external}
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [Upgrading vCenter Server vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade)
