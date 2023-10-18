---

copyright:

  years: 2023

lastupdated: "2023-10-16"

keywords: add endurance storage, create endurance storage, attach storage, attach storage to windows VSI, attach storage to linux VSI

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Adding endurance storage
{: #veeam_endurance_storage}

If you ordered the Veeam® add-on service from the VMware® Solutions console, you can add endurance storage as a Day 2 operation.

## Creating endurance storage
{: #veeam_endurance_storage_create}

To allocate the Endurance storage that hosts the Veeam Backup and Replication backup repository, complete the following steps:

1. From the [{{site.data.keyword.cloud_notm}} catalog](https://cloud.ibm.com/catalog){: external}, click **Storage**.
2. Select **Block storage for classic** under **Block storage**. 
3. On the **Create order** page, select **Location > Details > IOPS Profile**.
4. Click **Create**.

The storage location must be the same as the Veeam VSI instance. 
{: note}

## Attaching storage to Veeam VSI
{: #veeam_endurance_storage_vsi}

Endurance storage supports multi-path I/O, which you can enable within the Veeam VSI instance by following the procedure:

1. After logging in to your VSI instance, open **Windows Server Manager**. Select **Local server** and scroll to the **Roles and Features** section. Select **Tasks** and then **Add Roles and Features**.
2. In the **Features** window, select **Multipath I/O**. Next, select **Restart the destination server automatically if required** and install.
3. Once the multipath I/O feature is added, VSI will likely require a restart. When the restart is complete, log back in and a feature installation confirmation appears to validate the installed multipath I/O feature.
4. To configure the Windows iSCSI initiator, select **Tools** and then **iSCSI Initiator** from the server manager dashboard. If the iSCSI initiator service has not been previously enabled, a prompt to enable the service is displayed.
5. Go to the **Cloud Infrastructure portal**, navigate to the storage information page. To authorize the Veeam VSI instance, select **Authorize Host** from the storage **Actions** menu for the endurance storage provisioned for the Veeam backup repository. Select the Veeam VSI for instance.

## Attaching storage to Windows VSI
{: #veeam_endurance_storage_windows}

1. Once authorization is complete, select the storage instance, scroll to the **Authorized Hosts** section and copy the host IQN. In the Windows iSCSI initiator, choose the **Configuration** tab. Select **Change** and then paste the new IQN into the **New Initiator name** field.
2. In the Windows iSCSI initiator, choose the **Discovery** tab and select **Discover Portal.** Copy the storage **Target Address** into the **IP address or DNS name** field in the **Discover target Portal** window and then select **Advanced**. Select **Enable CHAP log on**, copy the **username** entry from the {{site.data.keyword.cloud_notm}} Infrastructure **Authorized Hosts** section to the iSCSI initiator **Name** field. Copy the password entry from the storage **Authorized Hosts** section to the iSCSI **Target secret** field. Choose **OK** twice to finalize the discovery settings.
3. In the Windows iSCSI initiator, choose the **Target** tab and select the discovered storage IQN, which should show an **Inactive** status. Select **Connect** and enable multi-path. 
4. Select **Advanced** and repeat the process for enabling CHAP as before.
5. If the settings are all applied correctly, the storage should now show a **Connected** status.
6. To enable operating system visibility to the attached storage, go to the Windows **Computer Management** application directly or through the Server manager. Go to **Disk Management** and the new storage will appear as an offline disk. Right-click on the disk and bring the storage online. You will also need to right-click and initialize any storage not previously in use. Right-click within the volume field and choose **New Simple Volume**. Next, allocate the full capacity of the LUN and assign a drive letter. For the partition format options select ReFS and the 64K block size. These settings will ensure optimal performance and reliability with your Veeam deployment.

The volume is ready to use as a Veeam repository.

## Attaching storage to Linux VSI or VM
{: #veeam_endurance_storage_linux}

1. Install `iscsi-initiator-utils`:
   ```psh
   yum install iscsi-initiator-utils
   ```
   {: pre}

2. Discover the target. Use the target's IP address; the following one is used as an example.
   ```psh
   ~]# iscsiadm -m discovery -t sendtargets -p 192.168.1.1
   Starting iscsid: [ OK ]
   192.168.1.1:3260,1 iqn.2015-06.com.example.test:target1
   ```
   {: pre}  

   The previous example shows the target's IP address and IQN address. The IQN address is needed in future steps.

3. Connect to the target:
   ```psh
   ~]# iscsiadm -m node -T iqn.2015-06.com.example:target1 --login
   Logging in to [iface: default, target: iqn.2015-06.com.example:target1, portal:
   192.168.1.1,3260] (multiple)
   Login in to [iface: default, target: iqn.2015-06.com.example:target1, portal:
   192.168.1.1,3260] successful.
   ```
   {: pre}  

4. Find the iSCSI disk name:
   ```psh
   ~]# grep "Attached SCSI" /var/log/messages
   Jun 19 01:30:26 test kernel: sd 7:0:0:1 [sdb] Attached SCSI disk
   ```
   {: pre}  

5. Create a file system on that disk:
   ```psh
   ~]# mkfs.ext4 /dev/sdb
   ```
   {: pre}  

6. Mount the file system:
   ```psh
   ~]# mkdir /mnt/iscsiTest
   ~]# mount /dev/sdb /mnt/iscsiTest
   ```
   {: pre}  

7. Make it persistent across reboots by editing the `/etc/fstab` file.
   ```psh
   ~]# blkid /dev/sdb
   /dev/sdb: UUID="766a3bf4-beeb-4157-8a9a-9007be1b9e78" TYPE="ext4"
   ~]# vim /etc/fstab
   UUID=766a3bf4-beeb-4157-8a9a-9007be1b9e78 /mnt/iscsiTest ext4
   _netdev 0 0
   ```
   {: pre}  

To create a Veeam Repository on this storage, follow the steps in [Adding backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_add_storage).

## Related links
{: #veeam_endurance_storage-links}

* [Expanding ordered endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_expand_storage)


