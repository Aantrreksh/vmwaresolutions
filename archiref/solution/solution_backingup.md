---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-31"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Backing up components
{: #solution_backingup}

You are responsible for the configuration, management, and monitoring of all software components, including the backup and availability of your management infrastructure and workloads.

As part of the solution, you can optionally deploy the Veeam® add-on service to satisfy the requirement for backing up your management components.

These add-on services are deployed together with {{site.data.keyword.cloud}} Endurance storage. The services help you back up your workloads and the management components.

Different solution components require different strategies for backup. Some components are protected by using image-level backup, and other components are protected by using file-based backup for their configuration and data.

## File server for file-based backup
{: #solution_backingup-fileserver-backup}

Some components, such as VMware vCenter Server® and VMware NSX®, require their configuration to be backed up to a file server.

To host these backups, deploy a Linux® file server into your cluster by using the following steps:

1. Order a private portable subnet from the {{site.data.keyword.cloud_notm}} infrastructure and locate it on the same VLAN as your system components. It is the private VLAN on which the management IP addresses for your hosts exist.
2. Upload an operating system image to your VMware® management datastore, such as Ubuntu Server 18.04 LTS, from the {{site.data.keyword.cloud_notm}} private mirror.
3. Deploy this virtual machine (VM) into your cluster on the management port group by using a private portable IP address ordered previously. Ensure that the VM is configured to point to your AD/DNS servers and optionally add the VM to your DNS domain.
4. Create a nonroot backup user ID on this server and ensure that all the necessary services are configured and started for file transfers. For example, FTP or SSH.
5. Ensure that this VM is included in your Veeam management backup job.

## vCenter file-based backup
{: #solution_backingup-vcenter}

VMware vCenter Server provides an appliance management user interface and API to export the database and configuration to a file server that uses various protocols. For more information, see [File-Based Backup and Restore of vCenter Server Appliance](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vcenter.install.doc/GUID-3EAED005-B0A3-40CF-B40D-85AD247D7EA4.html){: external}.

VMware documents an example of how you can configure the API to run periodically as a cron job directly on the vCenter Server Appliance.

VMware requires the backup location to be an empty folder, so plan for your backup rotation or automation to leave the location empty for each subsequent backup job.
{: note}

## NSX file-based backup
{: #solution_backingup-nsx}

Proper backup of all NSX components is crucial to restoring the system to its working state if a failure occurs. The design requires you to configure NSX backup through the NSX Manager backup function. For this purpose, you can configure NSX Manager to regularly perform backups to your file server. Ensure that your file server or its data is backed up correctly, and ensure the rotation of old NSX backups.

## Image-based backup of management VMs
{: #solution_backingup-image}

After you deployed your instance and deployed the Veeam backup service, configure a backup job for your management VMs. Plan to back up the following VMs with at least seven days of daily backups.

* If present, VMware SDDC Manager
* If present, Active Directory servers
* File backup server

Plan to allocate enough Veeam licenses to back up these VMs, and plan for at least 2 TB of backup storage for the VMs.

## Add-on services
{: #solution_backingup-addons}

If you deploy add-on solution components into your instance, plan for the backup of these components as part of your management backup strategy.

* Zerto Virtual Replication - The Zerto Virtual Manager (ZVM) system is deployed as an {{site.data.keyword.cloud_notm}} virtual server instance (VSI) and its backup is not supported by Veeam. If your disaster recovery strategy requires you to recover the ZVM without you perform a site failover, use your preferred Windows® backup solution to back up and restore the ZVM.
* F5® BIG-IP - F5 recommends [file-based backup of the F5 configuration](https://my.f5.com/manage/s/article/K13132){: external}, which you can direct to your file server.
* FortiGate® Security Appliance or VM - Fortinet recommends [performing a configuration backup](https://docs.fortinet.com/document/fortigate/6.4.0/best-practices/262994/performing-a-configuration-backup){: external}, which you can direct to your file server.
* VMware HCX™ - Use the HCX appliance management interface to create and download a file-based backup of the HCX Manager configuration similar to the vCenter Server Appliance.

## More considerations
{: #solution_backingup-considerations}

If you choose to deploy your AD/DNS server as an {{site.data.keyword.cloud_notm}} virtual server instance (VSI), you cannot back it up by using Veeam. In this case, use your preferred Microsoft Windows® backup solution for backup and restore operations. Or, plan to deploy your instance by using AD/DNS VMs within your VMware cluster, which can be backed up by Veeam.

Beginning with VMware vCenter 6.5u2, VMware supports the backup of the vCenter Postgres database by using image-based backups. These backups use integrated suspend and resume scripts for the database during the backup window to ensure database integrity. If you want to use this method, choose to use Veeam to back up your vCenter Server. Use this service instead of using file-based backups. If you do so, you must use the Veeam quiesce feature to ensure database integrity.

## Restoring from backup
{: #solution_backingup-restore}

Review the following special considerations when you restore your management backups.

* For vCenter, VMware provides an installer that can deploy a new virtual appliance and restore the configuration from backup.
* When you restore an appliance from backup, the installer detects the type of appliance (vCenter Server) based on the backup information you provide.
* Because you deploy directly to one of your hosts, you might not be able to deploy to a distributed switch or port group. Create a temporary standard switch and port group for deploying the recovered appliances. Then, migrate one of your vmnics temporarily to this switch to provide network connectivity for your VMs. After deployment, you can migrate the VMs to the distributed port group and return the vmnic to the dvSwitch.
* For NSX, you might need to redeploy your NSX Manager and controllers before you restore the configuration from backup.
* Ensure that you familiarize yourself with the VMware considerations and limitations for vCenter backup and restore.

## Summary
{: #solution_backingup-summary}

With proper planning, you can ensure that your VMware instance can suffer the loss of its management components and recover successfully. Ensure to regularly monitor the success of your backup jobs and availability of your backup data. Ensure to test your backup and restore plan regularly, for both your management infrastructure and your workloads.

## Related links
{: #solution_backingup-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
* [Design overview](/docs/vmwaresolutions?topic=vmwaresolutions-design_overview)
* [Scaling capacity](/docs/vmwaresolutions?topic=vmwaresolutions-solution_scaling)
