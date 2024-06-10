---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Veeam backup proxy
{: #veeam-cr-sa-vp}

A backup proxy is a Veeam® component that sits between the backup server and other components of the backup infrastructure. While the backup server administers tasks, the proxy processes jobs and delivers backup traffic to the backup repository. Key design elements of backup proxies include the following details:

* By default, the role of the backup proxy is assigned to the backup server. It is recommended to deploy dedicated backup proxies.
* For scaling, backup proxies can be scaled-out or scaled-up.
* A backup proxy can be deployed on either a physical or virtual Windows®-based or Linux®-based server.
* In practice, performance differences don't exist between Windows and Linux proxies. Therefore, the OS decision can be based on such things as licensing.
* Backup proxies run the following components and services:
   * The Veeam Installer Service is an auxiliary service that is installed only on the Windows-based server and is used to analyze, install, and upgrade the components.
   * The Veeam Data Mover performs the data processing tasks that include retrieving virtual machine (VM) data from storage, compressing, de-duplicating, encrypting, and sending data to the backup repository.
* Ideally, plan for one physical core or one vCPU and 2 GB of RAM for each configured proxy task, where a proxy task processes one VM disk.
* For virtual backup proxy servers, it is recommended to configure proxies with maximum of 8 vCPUs to avoid scheduling issues.
* Typically, virtual backup proxy servers use 4, 6, or 8 vCPUs.
* For a physical backup proxy, consider a 20-core server with 48 GB RAM and dual 10 GB NICS.
* The traffic from the source to the backup proxy is not optimized, for example, compressed or de-duped. Therefore, 100% of the backup data is transferred over this connection.
* Between the backup proxy and backup repository, optimized data typically about 50% of the source data size is transferred over this connection.
* In the virtual appliance mode, Veeam uses the VMware SCSI HotAdd capability that allows attaching devices to a VM while the VM runs. During backup, replication or restore disks of the processed VM are attached to the backup proxy. VM data is retrieved or written directly from or to the data store, instead of going through the network.
* The virtual appliance or HotAdd mode is not efficient as the direct storage access mode. However, it provides better performance than the network mode.

The backup proxy can use different transport modes that enable traffic flow between the source and the backup proxy. The end-to-end traffic flow can be considered as:

* Source to backup proxy.
* Backup proxy to backup repository.

In order of the most efficient data transfer, the following backup proxy transport modes are preferred:

* Direct storage access allows the backup proxy to retrieve data directly from the storage by avoiding the vSphere® ESXi hosts and the network. The backup proxy can be physical or virtual if iSCSI or NFS connect storage. However, it must be physical for Fibre Channel SANs. This transport mode cannot be used for vSAN, VVols, or vSphere ESXi host local storage. Direct storage access has two modes:
   * Direct SAN access is recommended for VMs whose disks are on shared VMFS SAN LUNs that are connected to vSphere ESXi hosts over FC, FCoE, iSCSI, and on shared SAS storage. Direct SAN access uses VMware VADP to transport VM data directly to and from the storage. As VM data travels over the SAN, by avoiding vSphere ESXi hosts and the network, the Direct SAN access mode provides the fastest data transfer speed. It doesn't produces load on the production network either.
   * In the Direct NFS access mode, the backup proxy bypasses the vSphere ESXi host and directly accesses the NFS data stores through its local NFS client. VM data travels over the network. However, load doesn't exist on the vSphere ESXi host.
* Virtual appliance (HotAdd) allows the backup proxy to access VM disks on the data store by enabling network-free data transfer between the vSphere ESXi host and the backup proxy. For this transport mode:
   * The backup proxy must be a VM and it is the recommended mode for a VM based proxy.
   * It is not recommended for NFS data stores. Direct NFS Access must be used.
   * The backup server and backup proxy must have the latest version of VMware Tools installed.
   * SCSI 0:X controller must be present on a backup proxy.
* Network mode allows the backup proxy access to VM data over the network from the vSphere ESXi hosts by using the NBD/NDBSSL protocol. For this transport mode, the backup proxy can be either physical or virtual. In network mode, the backup proxy uses VMware Virtual Disk Development Kit (VDDK) to communicate with the ESXi host, which produces extra load on the vSphere ESXi host.
* Backup from storage snapshots mode allows the backup proxy to access VM disks when they are on a supported storage system and the storage system is managed by Veeam Backup and Replication. This method is not available if the production environment is in {{site.data.keyword.cloud}}.

For more information, see [Transport modes](https://helpcenter.veeam.com/docs/backup/vsphere/transport_modes.html?ver=120).

When you use a VM based backup proxy:

* If the production environment is not on {{site.data.keyword.cloud_notm}}, then the most efficient transport mode depends on the storage architecture.
* If the production environment is on {{site.data.keyword.cloud_notm}} and the {{site.data.keyword.vcf-auto}} instance is using NFS, then Direct NFS access mode is the most efficient.
* If the production environment is on {{site.data.keyword.cloud_notm}} and the {{site.data.keyword.vcf-auto-short}} instance is using vSAN, then the Virtual appliance (HotAdd) is the most efficient.

## Backup proxy in the immutable backup solution architecture
{: #veeam-cr-sa-vp-ib}

As the Veeam service deploys the Veeam simple deployment scenario, the backup proxy is deployed on the Veeam backup server alongside the other Veeam components. For the immutable backup solution architecture, the existing backup proxy is used. Depending on the scale of the production environment, you can deploy one or more backup proxies.

## Backup proxy in the isolated recovery environment solution architecture
{: #veeam-cr-sa-vp-ire}

For the isolated recovery environment solution architecture, backup proxies that are registered with the isolated recovery environment Veeam backup server must be deployed on the production vSphere environment.

## Related links
{: #veeam-cr-sa-vp-related}

* [Backup proxy](https://helpcenter.veeam.com/docs/backup/vsphere/backup_proxy.html?ver=120){: external}
* [Transport modes](https://helpcenter.veeam.com/docs/backup/vsphere/transport_modes.html?ver=120){: external}
* [Veeam VMware vSphere backup proxy](https://bp.veeam.com/vbr/2_Design_Structures/D_Veeam_Components/D_backup_proxies/vmware_proxies.html#veeam-vmware-vsphere-backup-proxy){: external}
