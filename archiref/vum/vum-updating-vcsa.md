---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-02"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VCSA update and SSO-linked vCenters
{: #vum-updating-vcsa}

## PSC and VCSA update
{: #vum-updating-vcsa-psc-vcsa-update}

Both the vCenter Server® Appliance (VCSA) and the Platform Services Controller (PSC) are VCSA appliances but with different roles. When you upgrade vSphere® with an external PSC, upgrade in the following sequence:
1. PSC
2. VCSA
3. ESXi™ hosts
4. The hardware versions and VMware® Tools in the virtual machines (VMs)

VMware Update Manager (VUM) does not update the PSC or the VCSA. The following information describes the process of updating these appliances. The PSC or VCSA deployed in a VMware vCenter Server instance has no internet access, so the update bundle must be downloaded to a jump server first.

The PSC or VCSA is updated via appliance management console, not the vSphere Web Client. The PSC or VCSA appliance management console is accessed by using a browser, the PSC or VCSA IP address, and port 5480.

You must initiate a snapshot of the appliance or a backup of the PSC or VCSA before you update. Ensure that everything works as expected, and then remove the snapshot within a few days, to avoid performance degradation. Additionally, review the VMware release notes before you attempt any upgrade to understand any specific instructions for the specified release.

To update the PSC or VCSA, follow these steps:
1. You can download updates by going to the [VMware Patch Download Center](https://www.vmware.com/patchmgr/findPatchByReleaseName.portal), logging in and choosing VC from the **Search by Product** menu. Select the appropriate patch and click **Download**.
2. Using the vSphere Web Client, upload the ISO file to the vCenter data store repository.
3. Mount the update ISO file to the vCenter Server.
4. Take a snapshot of your vCenter Server.
5. Log in to vCenter appliance management console at `https://pscip:5480` (for the PSC) or `https://vcenterip:5480` (for the VCSA)
6. Go to the **Update** section and select **Check Updates** and then **Check CDROM**. The update is listed.
7. Select **Install Updates** and **Accept** the EULA. The update installs.
8. After the update is complete, you must go back to the appliance management console and select to restart the console.
9. Log back into the vSphere Web Client and check for any errors. Complete the following steps to scan VUM manually:
   1. Go to **Home > Hosts and Cluster**.
   2. Select a data center or cluster, click the **Update Manager** tab, and then click **Scan for Updates**.

10. After testing, if you need to back out, revert to snapshot or restore the vCenter with a previous backup.

## SSO-linked vCenter Server instances
{: #vum-updating-vcsa-sso-vcenter}

If you have primary and secondary vCenter Server instances, then your VCSAs are configured to be in a single vCenter Single Sign-On (SSO) domain. Each VCSA has a deployed VUM instance. The configuration properties that you modify are applied only to the VUM instance that you specify and are not propagated to the other instances in the group.

You can specify a VUM instance by selecting the name of the VCSA with which the VUM instance is registered from the navigation bar. You can also manage baselines, baseline groups, scan, and remediate only the inventory objects that are managed by the VCSA with which the VUM instance is registered.

## Related links
{: #vum-updating-vcsa-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
