---

copyright:

  years: 2023

lastupdated: "2023-10-16"

keywords: transport modes, direct storage access, direct SAN acces, requirements for direct SAN access mode, limitations for direct SAN access mode, virtual appliance (HotAdd), network mode

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Transport modes
{: #veeam_proxies_transp_modes}

A transport mode is a method that is used by the Veeam® Data Mover to retrieve VM data from the source and write VM data to the target. Job efficiency and time that is required for job completion greatly depend on the transport mode. 

For data retrieval, Veeam Backup and Replication offers the following modes (starting from the most efficient):
* Direct storage access
* Virtual Appliance (HotAdd)
* Network

The Veeam data mover responsible for data retrieval runs on a VMware® backup proxy. Correspondingly, the transport mode can be defined in the settings of the VMware backup proxy that performs the job. 

When you configure VMware backup proxy settings, you can manually select a transport mode, or let Veeam Backup and Replication select the most appropriate mode automatically. If you use automatic mode selection, Veeam Backup and Replication scan VMware backup proxy configuration and its connection to the VMware vSphere® infrastructure to choose the optimal transport mode. If several transport modes are available for the same VMware backup proxy, Veeam Backup and Replication choose the mode in the following order:

`Direct storage access > Virtual appliance > Network`

The selected transport mode is used for data retrieval. For writing data to the target, Veeam Backup and Replication picks the transport mode automatically, based on the configuration of the VMware backup proxy and transport mode limitations. Veeam Backup and Replication uses VMware vStorage APIs for Data Protection (VADP) for all transport modes except for backup from storage snapshots, the direct NFS transport mode and the virtual appliance transport mode. VADP can be used for VMware vSphere starting from version 4.

## Direct storage access
{: #veeam_proxies_transp_modes_dir_access}

In the Direct storage access mode, Veeam Backup and Replication reads and writes data directly from the storage system where VM data or backups are located. This mode comprises two transport modes:
* Direct NFS access
* Direct SAN access


### Direct NFS access
{: #veeam_proxies_transp_modes_dir_nfs_access}

The Direct NFS access is a recommended transport mode for VMs whose disks are on NFS data stores. The Direct NFS access mode provides an alternative to the Network mode. When Veeam Backup and Replication processes VM data in the Network mode, it uses VMware VDDK to communicate with the ESXi host. This produces additional load on the ESXi host.

In the Direct NFS access mode, Veeam Backup and Replication bypasses the ESXi host, reads and writes data directly from and to NFS data stores. To perform this, Veeam Backup and Replication deploys its native NFS client on the VMware backup proxy and uses it for VM data transport. VM data still travels over LAN but there is no load on the ESXi host. The Direct NFS access mode can be used for all operations where the VMware backup proxy is engaged:
   * Backup
   * Replication
   * Quick migration
   * VM copy
   * Entire VM restore
   * VM disk restore
   * Replica failback

### Requirements for the Direct NFS access mode
{: #veeam_proxies_transp_modes_req_nfs_access}

*  Direct NFS access mode can be used in VMware vSphere environments running NFS version 3 and 4.1.
*  The VMware backup proxy that is used for VM data processing must have access to the NFS data stores where VM disks are located.
*  If NFS volumes are mounted on the ESXi host under names, not IP addresses, the volume names must be resolved by DNS from the VMware backup proxy. 

### Limitations for Direct NFS access mode 
{: #veeam_proxies_transp_modes_lim_nfs_access}

*  Veeam Backup and Replication cannot parse delta disks in the Direct NFS access mode. For this reason, the Direct NFS access mode has the following limitations:
   * The Direct NFS access mode cannot be used for VMs that have at least one snapshot.
   * Veeam Backup and Replication uses the Direct NFS transport mode to read and write VM data only during the first session of the replication job. During subsequent replication job sessions, the VM replica will already have one or more snapshots. For this reason, Veeam Backup and Replication uses another transport mode to write VM data to the data store on the target side. The source side proxy keeps reading VM data from the source data store in the Direct NFS transport mode.
*  If you enable the **Enable VMware tools quiescence** option in the job settings, Veeam Backup and Replication will not use the Direct NFS transport mode to process running Microsoft Windows® VMs that have VMware Tools installed. The Direct NFS transport mode is not used because during VM quiescence VMware creates a snapshot with two delta disks per virtual disk.
*  If a VM has some disks that cannot be processed in the Direct NFS access mode, Veeam Backup and Replication processes these VM disks in the Network transport mode.

### VMware backup proxy for Direct NFS access mode
{: #veeam_proxies_transp_modes_direct_nfs_access}

To instruct the VMware backup proxy to use the Direct NFS access mode, you must choose the **Automatic selection** or **Direct storage access** option in the VMware backup proxy settings. To read and write data in the Direct NFS transport mode, the VMware backup proxy must meet the following requirements:
* The VMware backup proxy must have access to the NFS datastore.
* The VMware backup proxy must have ReadOnly and Write permissions and root access to the NFS datastore. 

Veeam Backup and Replication deploys its NFS agent on every VMware backup proxy when you assign the VMware backup proxy role to a Microsoft Windows server (physical or virtual). Linux backup proxies must have NFS client package installed. Veeam Backup and Replication selects backup proxies working in the Direct NFS access transport mode with the help of the following rules:

* If you instruct Veeam Backup and Replication to select a **VMware backup proxy** automatically for a job or task, it will select a VMware backup proxy with the minimum number of hops to the NFS datastore. If there are several backup proxies with equal number of hops in the backup infrastructure, Veeam Backup and Replication picks the least busy VMware backup proxy in the backup infrastructure. If all backup proxies with the minimum number of hops are busy at the moment, it will wait until these backup proxies are free. Veeam and Backup and Replication does not pick a VMware backup proxy that has a greater number of hops to the NFS datastore and works in the Direct NFS access or Virtual appliance transport mode.
* If you select one or more backup proxies explicitly for a job or task, Veeam Backup and Replication does not regard the number of hops to the NFS datastore. Veeam Backup and Replication picks the least busy VMware backup proxy working in the Direct NFS access transport mode. If all backup proxies working in the Direct NFS access transport mode are busy, Veeam Backup and Replication waits until these backup proxies are free. Veeam Backup and Replication does not pick a VMware backup proxy working in the Virtual appliance transport mode.

To detect the number of hops from a VMware backup proxy to the NFS datastore, Veeam Backup and Replication uses the host discovery process. During host discovery, Veeam Backup and Replication obtains information about the number of hops, checks which NFS datastores wehether the VMware backup proxy has access, and what permissions the VMware backup proxy has on NFS datastores. 

The host discovery process rescans all machines to which the VMware backup proxy role is assigned. The process starts automatically every 4 hours. Host discovery is also triggered when you change the transport mode settings and choose to use the **Direct storage access** for the VMware backup proxy. If necessary, you can start the host discovery process manually. If necessary, you can start the host discovery process manually. To do this, perform the **Rescan operation** for a machine where the VMware backup proxy role is assigned. For more information, see [Rescanning backup repositories](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage#veeam_repo_man_storage_rescanning)

### Direct SAN access
{: #veeam_proxies_transp_modes_dir_san}

The Direct SAN access transport mode is recommended for VMs whose disks are on shared VMFS SAN LUNs that are connected to ESXi hosts over iSCSI, and on shared SAS storage. 

In the Direct SAN access transport mode, Veeam Backup and Replication uses VMware VADP to transport VM data directly from and to iSCSI storage over the SAN. VM data travels over the SAN, bypassing ESXi hosts and the LAN. The Direct SAN access transport method provides the fastest data transfer speed and produces no load on the production network.

Direct SAN is not a typical transport mode for storage access in the {{site.data.keyword.cloud_notm}} environment.
{: note}

The Direct SAN access transport mode can be used for all operations where the VMware backup proxy is engaged:
* Backup
* Replication
* VM copy
* Quick migration
* Entire VM restore
* VM disk restore
* Replica failback

### Requirements for the Direct SAN access mode
{: #veeam_proxies_transp_modes_req_dir_san}

To use the Direct SAN access transport mode, make sure that the following requirements are met:

* It is recommended that you assign the role of a VMware backup proxy working in the Direct SAN access mode to a physical machine. If you assign this role to a VM, the VMware backup proxy performance might not be optimal.
* A VMware backup proxy that uses the Direct SAN access transport mode must have a direct access to the production storage that uses a hardware or software HBA. If a direct SAN connection is not configured or not available when a job or task starts, the job or task fail.
* Direct SAN storage volumes presented as VMware datastores must be exposed to the OS of the VMware backup proxy that works in the Direct SAN access transport mode. 

   The volumes must be visible in **Disk Management** but must not be initialized by the OS. Otherwise, the VMFS file system is overwritten with NTFS, and volumes become unrecognizable by ESXi hosts. To prevent volume initialization, Veeam Backup and Replication automatically sets the SAN Policy within each proxy to Offline Shared and also sets the SAN LUNs to the Offline state.

* For restore operations: A VMware backup proxy must have write access to LUNs where VM disks are located.

### Limitations for the Direct SAN access mode
{: #veeam_proxies_transp_modes_lim_dir_san}

*  The Direct SAN access transport mode can be used to restore only thick VM disks.
*  The transport mode is used for the entire VM, not for the virtual disk. It means that one VM can be processed in one transport mode only. If there are VM disks that cannot be processed in the Direct SAN access transport mode, then the rest of the disks also cannot be processed in this transport mode.
*  You cannot use the Direct SAN access mode in the following cases:

   * For VMs residing on vSAN. You can use Virtual appliance and Network transport modes to process such VMs. For more information about vSAN restrictions, see the [VDDK release notes](https://vdc-download.vmware.com/vmwb-repository/dcr-public/1ad87f77-0120-44f0-9517-4da7a9161679/53034008-3cbc-4b67-8d60-37b52fd4fc51/VDDK-703-ReleaseNotes.html#compatibility){: external}. 
   * If at least one VM disk is on a VVol.
   * For Veeam Cloud Connect Replication because in this scenario Veeam Backup and Replication always creates VM replicas with thin disks.
   * For incremental restore due to [VMware limitations](https://docs.vmware.com/en/VMware-vSphere/8.0/vsan-administration/GUID-E9984893-DF64-49EC-B0DB-44F8C271BCFE.html?hWord=N4IghgNiBcIQlgW3gFzC+B7AdgZxAL5A){: external}. Either disable CBT for VM virtual disks during the restore process or select another transport mode for incremental restore.
   * For backing up VM templates.

*  Veeam Backup and Replication uses the Direct SAN access transport mode to read and write VM data only during the first session of the replication job. During subsequent replication job sessions, Veeam Backup and Replication uses the Virtual appliance or Network transport mode on the target side. The source side proxy keeps reading VM data from the source data store in the Direct SAN access transport mode.
*  Veeam Backup and Replication writes VM data to the target data store in the Direct SAN access transport mode only if disks of a VM replica are thick-provisioned. If disks are thin-provisioned, Veeam Backup and Replication write VM data in the Network or Virtual appliance mode. By default, Veeam Backup and Replication replicates VM disks in the thin format. To write VM data to the target data store in the Direct SAN access transport mode, select to convert VM disks to the thick format at the **Destination** step of the replication job wizard.
*  IDE and SATA disks can be processed in the Direct SAN access transport mode.

## Virtual Appliance (HotAdd)
{: #veeam_proxies_transp_modes_hotadd}

The Virtual appliance mode is not as efficient as the Direct storage access mode but provides better performance than the Network mode. The Virtual appliance mode is recommended if the role of a VMware backup proxy is assigned to a VM.
In the Virtual appliance mode, Veeam Backup and Replication uses the VMware SCSI HotAdd capability that allows attaching devices to a VM while the VM is running. During backup, replication or restore disks of the processed VM are attached to the VMware backup proxy.
VM data is retrieved or written directly from/to the data store, instead of going through the network. The Virtual appliance transport mode can be used for all operations where the VMware backup proxy is engaged:

* Backup
* Replication
* VM copy
* Quick migration
* Entire VM restore
* VM disk restore
* Replica failback

### Requirements for the Virtual Appliance mode
{: #veeam_proxies_transp_modes_hotadd_req}

To use the Virtual appliance transport mode, make sure that the following requirements are met:

   * The role of a VMware backup proxy must be assigned to a VM.
   * The VMware backup proxy and processed VMs must reside in the same data center.
   * The VMware backup proxy must have access to the disks of the VM that this proxy processes. For example, in a replication job, the source VMware backup proxy must have access to the disks of the source VM, the target proxy — to the disks of the replica. If a VMware backup proxy acts as both source and target proxy, it must have access to the disks of the source VM and replica. In restore operations, the VMware backup proxy must have access to disks of the restored VMs.
   * For NFS 3.0: If you plan to process VMs that store disks on the NFS data store, you must configure Veeam Backup and Replication to use the proxy on the same host as VMs. This is required due to an issue described in [Virtual machines residing on NFS storage become unresponsive during a snapshot removal operation](https://kb.vmware.com/s/article/2010953){: external}. For more information about how to configure the proxy, see [VM Loses Connection During Snapshot Removal](https://www.veeam.com/kb1681){: external}. As an alternative, you can use ESXi 6.0 or higher and NFS 4.1.
   * The VMware backup proxy must have the latest version of VMware Tools installed. The backup server installed on a VM can also perform the role of the VMware backup proxy that uses Virtual appliance transport mode. In this case, make sure the backup server has the latest version of VMware Tools installed.
   * SCSI 0:X controller must be present on a VMware backup proxy. In the opposite case, VM data processing in the Virtual appliance transport mode will fail.

### Limitations for the Virtual Appliance mode
{: #veeam_proxies_transp_modes_hotadd_lim}

*  If a VMware backup proxy used to process a source VM resides on a VMFS 3 data store, it must be formatted with proper block size to be able to mount the largest virtual disk of HotAdded VMs:

   * 1 MB block size — 256 GB maximum file size
   * 2 MB block size — 512 GB maximum file size
   * 4 MB block size — 1024 GB maximum file size
   * 8 MB block size — 2048 GB maximum file size
*  This limitation does not apply to VMFS-5 volumes that always have 1 MB file block size.
*  For vSphere 5.5 and later: The maximum supported VMDK size is 62 TB.
*  For Microsoft Windows proxy: Before running a data protection task, Veeam Backup and Replication disables the volume automount feature, and it remains disabled after the data protection task is completed.
*  Backup and restore of IDE disks in the Virtual appliance mode is not supported.
*  Backup and restore of SATA disks in the Virtual appliance mode is supported if you use VMware vSphere 6.0 and later.
*  For quick migration during Instant Recovery: Virtual appliance (HotAdd) transport mode cannot be used if the role of the backup proxy and mount server or backup repository where the backup file is stored are assigned to the same VM.

### Proxy recommendations from {{site.data.keyword.cloud_notm}}
{: #veeam_proxies_transp_modes_hotadd_proxy_rec}

* In an {{site.data.keyword.cloud}} environment, HotAdd mode is recommended as a common best practice unless there are special circumstances.
* It is recommended to use the same VM for both backup and CDP proxy unless you have special circumstances, especially if you are using HotAdd for backup proxy.

## Network mode
{: #veeam_proxies_transp_modes_network}

The Network mode can be used with any infrastructure configuration. In this mode, data is retrieved through the ESXi host over LAN using the Network Block Device protocol (NBD). The Network mode has low data transfer speed over LAN. To take the load off the LAN, Veeam Backup and Replication provides two alternative modes: Direct Storage
Access and Virtual Appliance. However, the Network mode is the only applicable mode when the VMware backup proxy role is assigned to a physical machine and the host uses
local storage. Also, the Network mode can be the best choice if you have a large virtual environment with hundreds of small VMs, with 10 Gb Ethernet networks and a small change rate.

The process of data retrieval in Network mode includes the following steps:

1. The VMware backup proxy sends a request to the ESXi host on which the processed VM is registered to locate the VM on the data store.
2. The ESXi host locates the processed VM on the data store.
3. Veeam Backup and Replication instructs VMware vSphere to create a VMware vSphere VM snapshot.
4. ESXi host copies VM data blocks from the source storage and sends them to the VMware backup proxy over LAN. The real data transfer speed might be less than the available speed because the VMware backup proxy and the ESXi host communicate over the ESXi management network.
5. The VMware backup proxy sends the data to the target. Veeam Backup and Replication processes VM disks in parallel. If VM disks are on different storage types (for example, on the SAN and local storage), Veeam Backup and Replication uses different transport modes to process VM disks. In such scenario, it is recommended that you select the **Failover to network mode** if primary mode fails, or is unavailable when configuring the mode settings for the VMware backup proxy. You can instruct Veeam Backup and Replication to switch to the Network transport mode and transfer VM data over LAN if the primary transport mode — Direct storage access or Virtual appliance — fails during the job session. This option is enabled by default to ensure that jobs and tasks can be completed successfully in any situation.

In Veeam, backup proxies can be created as:
* Backup Proxy
* VMware Backup Proxy
* VMware CDP Proxy

## Related links
{: #veeam_proxies_transp_modes-links}

* [Add endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_req#veeam_proxies_req-links)
* [Backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_backup_proxy)
* [VMware backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_vmware_backup_proxy)
* [VMware CDP proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_vmware_cdp_proxy)
