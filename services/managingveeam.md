---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-06"

keywords: Veeam console, Veeam backup restore, update Veeam license

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing Veeam
{: #managingveeam}

After the service is deployed into your instance, you can access the Veeam® console by using Remote Desktop Protocol. With Remote Desktop Protocol, you can manage the backup and restore of all the VMs (virtual machines) in your environment, including the management components. You can also upgrade the service by downloading and installing the Veeam updates from the Veeam website.

## Tasks that you can complete with Veeam 
{: #managingveeam-fivetasks_v10}

* Order a new instance with Veeam or install Veeam on an existing instance

   A Veeam stand-alone license is automatically deployed. The Veeam service installation starts only after the stand-alone license was successfully ordered. Veeam is installed on a bare metal server, VM, or VSI, depending on what you select.

* Uninstall Veeam from an existing instance

   If you uninstall an older version of Veeam, for example Veeam 9.5u4b, the license charge for that version is canceled because the license is attached to the older version. However, if you uninstall Veeam 10 or later, the stand-alone license instance is not deleted. To cancel the license charge, you must delete the license separately.

* Order a new Veeam stand-alone license

   An order is placed with the number of VMs to license. A license key is not displayed because no unique keys are generated.

* Delete a Veeam stand-alone license

   When you delete a Veeam stand-alone license, the license charge is canceled. Deleting the license has no effect on the Veeam installation. When you want to increase your usage, delete your old stand-alone instance after you order a new instance to avoid unnecessary charges.

   For more information about licenses, see [Managing Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses).

## Accessing the Veeam console by using Remote Desktop Protocol
{: #managingveeam-accessing}

To manage the Veeam service, access the Veeam console by completing the following steps:
1. Use Remote Desktop Protocol to connect to the Microsoft Windows® IP address.
2. Log in to the Windows console by using the Administrator credentials.
3. Access the Veeam console from the Windows console by using the Administrator credentials.

   You can find the Windows IP address and the Administrator credentials on the Veeam service details page.

For more information, see [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Backing up and restoring management components for instances with Veeam installations
{: #managing-veeam-backup-and-replication}

The Veeam service can be configured to back up the management components by using the Veeam console. For more information, see [Backing up components](/docs/vmwaresolutions?topic=vmwaresolutions-solution_backingup).

The configuration changes to your environment are not automatically backed up. Therefore, before you change the configuration of your environment, it is recommended that you back up the management components manually by running the management backup job in the Veeam console. For more information about backing up manually, see the [Veeam technical instructions](https://helpcenter.veeam.com/backup/vsphere/scheduing_manual.html){: external}.

When failures occur on the management components, you can restore the management components to a previous backup by using the Veeam console. For more information about restoring manually, see the [Veeam technical instructions]( https://helpcenter.veeam.com/backup/vsphere/performing_full_recovery.html){: external}.

## Applying updates to Veeam
{: #managingveeam-updates}

You are responsible for maintaining the Veeam software to keep it updated to the most recent version.

### Applying updates to instances deployed as a VM with public and private network
{: #managingveeam-updates-public-private}

If the Veeam service is installed on an instance as a VM with public and private network, you can check for and download the updates by using the Veeam software itself.

### Applying updates to instances deployed as a bare metal server or VSI, or deployed as a VM with private network only
{: #managingveeam-updates-private}

If the Veeam service is installed on an instance as a bare metal server or VSI, or deployed as a VM with private network only, you cannot check for or download updates by using the Veeam software. The reason is because the Veeam VSI or VM is configured with no public network access. Instead, you must download updates from the Veeam website, transfer them to the Veeam VM, and then install them.

### Updating Veeam licenses for instances that are deployed with public and private network
{: #managingveeam-update-license-public-private}

If the Veeam service is installed on an instance with public and private network, you can update your Veeam 9.5u4b license either automatically or manually. For Veeam, you must update your Veeam license automatically. You cannot update it manually. Follow the Veeam instructions at [Updating license](https://helpcenter.veeam.com/docs/backup/vsphere/license_update.html){: external}.

### Updating Veeam licenses for instances that are deployed as a bare metal server or VSI, or deployed as a VM with private network only
{: #managingveeam-update-license-private}

If the Veeam service is deployed on an instance as a bare metal server or VSI, or is deployed as a VM with private network only, take note of the expiration date for your license. When renewal is needed, [contact {{site.data.keyword.IBM}} Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) to get assistance with updating the license key.

### Known issue about license key message for automatic updating
{: #managingveeam-known-issue-message}

On the Veeam console, when you’re automatically updating a license before it expires, you might see a `License key is up-to-date` message that looks like an error. You can ignore the message because it's not an error.

## Considerations when you delete Veeam
{: #veeamvm_overview-remove}

Deleting the Veeam service stops all backups and deletes all the previous backups. The backup of the management VMs or VSIs stops and the deletion of previous backups is irreversible. If the management VMs or VSIs are corrupted, they can’t be restored.
{: important}

Review the following considerations before you delete the service:

* Deleting the Veeam service does not cancel the Veeam license. You must delete the Veeam license from the **Veeam licenses** table on the **Licenses** page in the {{site.data.keyword.vmwaresolutions_short}} console.
* When you delete the Veeam service, the VMware Solutions automation deletes only the single Veeam VM, VSI, or bare metal server that was deployed and the dedicated private subnet that was ordered for it. If you scaled out the Veeam VM or VSI into multiple ones, those additional VMs or VSIs are not deleted.
* If you order iSCSI storage, that storage is deleted when you delete the Veeam service. Therefore, any data within that storage is lost.

## Related links
{: #managingveeam-related}

* [Veeam on {{site.data.keyword.cloud_notm}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [Ordering Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering)
* [Ordering Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering_licenses)
* [Managing Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses)
* [Ordering and configuring {{site.data.keyword.cloud_notm}} Object Storage with Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-icos_ordering)
* [VMware Solutions FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Veeam Backup and Replication](https://www.ibm.com/cloud/architecture/architectures/virtualization_backup_veeam)
* [Veeam Backup and Replication FAQ](https://www.veeam.com/availability-suite-faq.html){: external}
* [Veeam Technical Documentation](https://www.veeam.com/documentation-guides-datasheets.html){: external}
