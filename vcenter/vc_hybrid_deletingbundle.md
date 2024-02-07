---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-06"

keywords: vCenter Server Hybridity delete instance, delete vCenter Server Hybridity, remove vCenter Server Hybridity

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Removing the Hybridity Bundle from a vCenter Server instance
{: #vc_hybrid_deletingbundle}

To remove the Hybridity Bundle license from your VMware vCenter Server® instance, you must replace the VMware NSX® and VMware vSAN™ rental license keys with Bring Your Own License (BYOL) keys in the VMware vSphere® Web Client. Additionally, you must open a support ticket to cancel charges for the rental licenses.

Reverting your license to an earlier version might cause your vCenter Server instance to fail. You can choose to revert a license to an earlier version at your own risk, but first consider the functions that are not available when you are reverting. For more information, see [Comparison chart for VMware component editions](/docs/vmwaresolutions?topic=vmwaresolutions-solution-appendix).
{: attention}

## Important considerations before you remove the Hybridity Bundle from a multisite environment
{: #vc_hybrid_deletingbundle-considerations}

Review the following considerations before you remove the Hybridity Bundle from a multisite environment:

* You must apply BYOL licenses to all multisite deployments before you remove rental licenses.
* You must combine VMware NSX licenses and have enough capacity to use across all multisite deployments.
* You must create a single support ticket to remove the Hybridity Bundle from all multisite deployments.

When you remove the Hybridity Bundle from a multisite environment, BYOL licenses are applied. It is your responsibility to ensure that the license editions are consistent across all sites in the multisite configuration.
{: important}

## Before you remove the Hybridity Bundle
{: #vc_hybrid_deletingbundle-prereq}

Verify the following requirements before you remove the Hybridity Bundle:

* You have a V2.4 or later vCenter Server instance with the Hybridity Bundle enabled.
* The VMware HCX™ service is not installed on your vCenter Server instance.
* You have access to the VMware vSphere Web Client as Administrator.
* If not already applied, you have BYOL keys available to apply for VMware NSX and each VMware vSAN cluster.
* Optionally and if not already applied, you have BYOL keys available to apply for the VMware vCenter Server and VMware vSphere Enterprise Plus licenses.

## Procedure to remove the Hybridity Bundle
{: #vc_hybrid_deletingbundle-procedure}

1. Log in as **Administrator** to the VMware vSphere Web Client where you want to remove the Hybridity Bundle.
2. Click **Home > Administration > Licensing > Licenses**.
3. Click the **Assets** tab.
4. Complete the following steps to install a VMware NSX BYOL:
   1. Click the **Solutions** tab.
   2. Select NSX for vSphere and click **All Actions > Assign license**.
   3. Click the **Add** icon and type the license key. Click **Next**.
   4. Type the name for the license and click **Next**. Click **Finish** to add the license.
   5. Select the new license key.
   6. Write down the full license keys for both the license that is applied and the license that is replaced.
      You must have the license details available to use later in this procedure.
      {: important}

   7. Click **OK** to assign the license.
5. Complete the following steps to install a VMware vSAN BYOL:
   1. Click the **Clusters** tab.
   2. Complete the following steps for each vSAN cluster that is associated with your vCenter Server instance:
      1. Select a vSAN cluster and click **All Actions > Assign license**.
      2. Click the **Add** icon and type the license key. Click **Next**.
      3. Type the name for the license and click **Next**. Click **Finish** to add the license.
      4. Select the new license key.
      5. Write down the cluster name and full license keys of both the license that is applied and the license that is replaced.
         You must have the license details available to use later in this procedure.
         {: important}

      6. Click **OK** to assign the license.
6. Optionally complete the following steps to install a VMware vCenter Server BYOL:
   1. Click the **vCenter Server systems** tab.
   2. Select vCenter Server and click **All Actions > Assign license**.
   3. Click the **Add** icon and type the license key. Click **Next**.
   4. Type the name for the license and click **Next**. Click **Finish** to add the license.
   5. Select the new license key.
   6. Write down the full license keys of both the license that is applied and the license that is replaced.
      You must have the license details available to use later in this procedure.
      {: important}

   7. Click **OK** to assign the license.
7. Optionally complete the following steps to install a VMware vSphere Enterprise Plus BYOL:
   1. Click the **Hosts** tab.
   2. Complete the following steps for each cluster that is associated with your vCenter Server instance or complete for all clusters at the same time if the same license is being applied to all clusters associated to your vCenter Server:
      1. Select all hosts that are associated to the cluster and click **All Actions > Assign license**.
      2. Click the **Add** icon and type the license key. Click **Next**.
      3. Type the name for the license and click **Next**. Click **Finish** to add the license.
      4. Select the new license key.
      5. Write down the cluster name and full license keys of both the license that is applied and the license that is replaced.
         You must have the license details available to use later in this procedure. If license keys are not same across all clusters, ensure to write down the cluster name that is associated to each license key.
         {: important}

      6. Click **OK** to assign the license.
8. Remove the rental licenses.
   1. Click the **Licenses** tab.
   2. Select the licenses that you replaced in steps 4 - 7.
   3. Click the **Remove Licenses** icon.
9. Open a support ticket and provide the following information to cancel charges for the rental licenses:
   * The name of your vCenter Server instance or instances.
   * The ID associated with your vCenter Server instance or instances.
   * A list of the BYOL license keys that you installed in this procedure. Where applicable, provide the instance and cluster name with license keys for vSphere and the vSAN clusters.
   * A list of the rental license keys that you removed in this procedure. Where applicable, provide the instance and cluster name with license keys for vSphere and vSAN clusters.

   The IBM Support team accesses the vCenter management layer of your {{site.data.keyword.cloud_notm}} infrastructure account to verify that the rental licenses are removed before you cancel the Hybridity Bundle rental license charges.
   {: note}

