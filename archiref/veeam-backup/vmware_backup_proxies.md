---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: vmware backup proxy, proxies, direct storage access, virtual appliance, network, nfs cluster

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware backup proxies
{: #vmware_backup_proxies}

A VMware® backup proxy sits between the backup server and other components of the backup infrastructure. While the backup server administers tasks, the proxy processes jobs and delivers backup traffic.

VMware backup proxy tasks include the following procedures:

* Retrieving virtual machine (VM) data from the production storage.
* Compressing, deduplicating, and encrypting.
* Sending data to the backup repository, if you run a backup job.
* Sending data to another VMware backup proxy, if you run a replication job.

During service deployment, the automation configures a VMware backup proxy on the backup server. Consider deploying more VMware backup proxies for availability and scaling. You have the following choices:

* **VM** – For most use-cases, the use of a VM is recommended.
* **Virtual server instances** – Not typically recommended due to their 1 GB interfaces.
* **Bare metal server** – A good choice if you are deploying a combined proxy and repository or by using Direct NFS storage access.

A VMware backup proxy can use one of the following data transport modes:

* **Direct storage access** – In {{site.data.keyword.cloud}} only direct NFS storage mode is suitable.
    * For direct storage access consider:
      * As the NFS share is presented to the VMware backup, a local admin or root account can delete all files in the share.
      * A bare metal server with 10 Gbps NICs provides high throughput.
      * Ignore any warnings in vCenter that mention that another workload is recognized.

* **Virtual appliance** – This mode uses the HotAdd mode and only a VM can operate in the appliance mode, and it is recommended in {{site.data.keyword.cloud_notm}}.
    * For vSAN clusters consider creating:
      * One VMware backup proxy for each ESXi host in the vSAN cluster to reduce the workload on the ESXi I/O stack during backup.
      * A VM-Host Affinity rule to prevent the VMware backup proxy from being moved from its assigned ESXi host.

For NFS 3 clusters, see [VMs residing on NFS storage become unresponsive during a snapshot removal](https://knowledge.broadcom.com/external/article?legacyId=2010953){: external} operation, which advises placing backup appliances on the same host where the VM being backed up is located.

* **Network** – This mode is the default mode of VMware backup proxies and they fall back to this mode if other modes fail. The proxy connects to the vSphere host’s vmdk0 port and uses NBD transport. In terms of bandwidth, NBD is the slowest mode. This mode works best for VMware backup proxies that are hosted on virtual server instances and bare metal servers as they get deployed onto the same subnet as the vSphere hosts.

## Related links
{: #vmware_backup_proxies-links}

* [Backup proxies and transport modes](https://www.veeam.com/blog/vmware-backup-proxy-transport-modes-configuration.html){: external}
* [Optimizing Veeam Backup and Replication configuration for VMware vSAN](https://www.veeam.com/kb2273){: external}
* [VM loses connection during snapshot removal](https://www.veeam.com/kb1681){: external}
