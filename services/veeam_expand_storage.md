---

copyright:

  years: 2023

lastupdated: "2023-08-17"

keywords: Block storage, Block storage for Classic, for classic, Endurance storage

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Expanding ordered endurance storage
{: #veeam_expand_storage}

If you ordered the Veeam® add-on service from the VMware Solutions console, you can expand backup storage as a Day 2 operation.

To expand the ordered endurance storage, complete the following steps:

1. From the {{site.data.keyword.cloud}} console, click the **menu** icon ![Navigation menu icon](../../icons/icon_hamburger.svg "Menu"). Then, click the **Infrastructure** icon ![Classic](../../icons/classic.svg "Classic") > **Storage** > **{{site.data.keyword.blockstorageshort}}**.
2. Select the iSCSI volume from the list and click the **ellipsis** icon ![Actions icon](../../icons/action-menu-icon.svg "Actions") > **Modify volume**.
3. Enter the new storage size in GB.
4. Review your selection and the new pricing.
5. Click **Modify**.

   Your new storage allocation is available in a few minutes.

## Expanding storage for the Windows VSI
{: #veeam_expand_storage_windows}

To expand storage for the Windows VSI, complete the following steps:

1. Go to **Server Manager**, click **Tools** > **iSCSI Initiator**.
2. In the window that opens, click the **Refresh** button in **Discovered targets**.
3. Open the **Computer Management** window and click **Disk Management**. The extended storage is shown as **Unallocated** disk.
4. Right-click the allocated volume and select **Extend Volume**. The extended volume size is shown on the **Selected** side.
5. Click **Next** and then **Finish**. The Extended storage size gets merged into the existing disk.
6. Rescan all Veeam repositories that are attached to this volume.

## Expanding storage for the Linux VSI or VM
{: #veeam_expand_storage_linux}

To expand storage for the Linux VSI or VM, complete the following steps:

1. After you modify the online logical unit size, rescan the logical unit to ensure that the system detects the updated size. To complete this operation for the iSCSI devices, run the following command:

   `# iscsiadm -m node --targetname target_name -R`

   Replace `target_name` with the name of the target where the device is located.

2. Rescan all Veeam repositories that are attached to this volume.

## Related links
{: ##veeam_expand_storage_related}

* [Veeam overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [Ordering Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering)
* [Managing Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-managingveeam)
