---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-02"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Applying native NIC drivers
{: #vum-applying-nic}

`ixgben` is a native driver that replaces the `vmklinux net-ixgbe` driver but does not support SR-IOV and SW FcOE. The ICVS automation would not enable this driver when your vSphere® ESXi host was provisioned. It is advisable to enable this driver for the performance benefits it brings. The following procedure described in this appendix, shows you how to enable and disable the native drivers by using the vSphere Command-Line (vCLI).

Before you start this task, retrieve all the physical hosts IPMI IP addresses, login IDs, and passwords from the [{{site.data.keyword.cloud}} infrastructure customer portal](https://control.softlayer.com/devices). This is required in a back out or to check on the progress of an upgrade, where no direct network access to the host exists.

For each host, successively:
1. Use the vSphere Web Client to place the vSphere ESXi host into maintenance mode by, selecting **Home** > **Hosts and Clusters**. In the Navigator pane, select the vSphere ESXi host and right-click the host and select **Maintenance Mode** > **Enter Maintenance Mode**. As the host is part of an automated DRS cluster, virtual machines are migrated to different hosts when the host enters maintenance mode.
2. SSH into the vSphere ESXi host, by using the details from the {{site.data.keyword.vmwaresolutions_short}} console.
3. Run the following vCLI command to enable the ixgben native drivers:
   `esxcli system module set --enabled=true --module=ixgben`
4. Run the following vCLI command to restart the vSphere ESXi host:
   `system shutdown reboot --reason “Install ixgben driver”`
5. After the vSphere ESXI host reboots using SSH log back into the host, issue the following vCLI command and check that the ixgben driver is “loaded” (first column) and “enabled” (second column):
   `esxcli system module list |grep ixg`
6. If the drivers are enabled, then by using the vSphere Web Client select the host in the Navigator pane, right-click, and select **Maintenance Mode** > **Exit Maintenance Mode**. Select the next host and enable the drivers until all the hosts are done.
7. If the change does not work, then to revert, run the following command:
   `esxcli system module set --enabled=false --module=ixgben`

8. If you can't connect to the host over the network, run the previous command from the IPMI console by using the {{site.data.keyword.cloud_notm}} control window.
9. After you reboot the vSphere ESXi host, you now observe the default ixgbe driver that is loaded and enabled.

If you need to revert, and you can't SSH to the vSphere ESXi host, then you need to log in to the KVM console for the host that needs the revert via the {{site.data.keyword.cloud_notm}} control window.

Use the ID and password that are listed in the {{site.data.keyword.cloud_notm}} control window with the IPMI IP address to log in to the IPMI web interface. You need to be connected to the data center where the host is located through VPN. For more information, see [Getting started with {{site.data.keyword.cloud_notm}} SSL Virtual Private Networking](/docs/iaas-vpn?topic=iaas-vpn-getting-started).

1. Go to the **Device Details, Remote Mgmt** page for the vSphere ESXi host and select **Actions** > **KVM Console**. Enter the IPMI user and password.
2. Select **Remote Control** > **iKVM/HTML5** and click **iKVM/HTML5** to restart. You can now be able to access the vSphere ESXi host’s console.
3. If the host is responding to commands, use **ALT-F1** in the console to access the ESXi host console. Use the host credentials to log in.
4. If the host is not responding, use the IPMI menus to power cycle the host.
5. Watch the HTML5 console carefully as the host restarts. You have only a few seconds to go into recovery mode when ESXi restarts.
6. Press **CMD + R** keys simultaneously to enter recovery mode.
7. Type **Y** to enter recovery mode and boot the ESXi server with the previous version.
8. Monitor its progress through the console. The boot can take 10 - 20 minutes.

## Related links
{: #vum-applying-nic-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
