---

copyright:

  years:  2021, 2024

lastupdated: "2024-05-21"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Overview of application support with Veeam
{: #veeam-bms-archi-app-support}

For applications hosted on the VMs, Veeam® requires network access to the VMs to provide application aware backups. In the Veeam Backup and Replication console, to enable the application-aware image-processing or the guest file system indexing options in the backup job, you need network access between customer overlay and the Veeam bare metal server management network (primary subnet on private VLAN 1). If you want to use these capabilities, routing must be designed and implemented between the customer NSX-T™ overlay networks.

The guest interaction proxy is a backup infrastructure component that sits between the backup server and processed VM. This component is needed if the backup or replication jobs perform the following processing of VMs:
* Application-aware processing
* Guest file system indexing
* Transaction logs processing

The guest interaction proxy deploys the runtime process only in Microsoft® Windows® VMs. In VMs with another guest OS, the runtime process is deployed by the backup server.

For Windows virtual machine (VM) file level restores, Veeam first tries to connect to the Guest VM through the network, and since the network is isolated, the VMware vSphere® Guest Interaction API is then used to complete a network-less restore.

For Linux® VM file level restores, a File Level Restore (FLR) appliance needs to be deployed before you attempt the file level restore by the {{site.data.keyword.IBM_notm}} Backup Administrator. Otherwise, the first time a tenant tries to restore a file, they receive an error in the Veeam Backup and Replication Console. For two of the three restore options, the FLR appliance requires network connectivity to the Linux VM where the file is to be restored, since the network is isolated. Therefore, only the download option is applicable to this service. This download needs to be moved to the correct place in the file system.

For more information about file level restore, see the Veeam documentation.

## Related links
{: #veeam-bms-archi-app-support-related}

* [Veeam Backup and Replication](https://www.veeam.com/vm-backup-recovery-replication-software.html?ad=menu-products){: external}
* [Veeam Help Center technical documentation](https://www.veeam.com/documentation-guides-datasheets.html?ad=menu-resources){: external}
