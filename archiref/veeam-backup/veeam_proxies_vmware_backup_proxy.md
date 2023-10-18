---

copyright:

  years: 2023

lastupdated: "2023-10-13"

keywords: vmware backup proxy, vmware backup proxy deployment, vmware backup proxy services, vmware backup proxy components

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware backup proxy
{: #veeam_proxies_vmware_backup_proxy}

A VMware® backup proxy is an architecture component that sits between the backup server and other components of the backup infrastructure. While the backup server administers tasks, the proxy processes jobs and delivers backup traffic.

Basic VMware backup proxy tasks include:

* Retrieving VM data from the production storage
* Compressing
* Deduplicating
* Encrypting
* Sending it to the backup repository (for example, if you run a backup job) or another VMware backup proxy (for example, if you run a replication job).

Depending on your backup architecture, a VMware backup proxy can use one of the following data transport modes:

* Direct storage access
* Virtual appliance
* Network

If the VM disks are on the storage system and the storage system is added to the Veeam Backup and Replication console, the VMware backup proxy can also use the backup from storage snapshots mode. You can explicitly select the transport mode or let Veeam Backup and Replication automatically choose the mode.

## VMware backup proxy deployment
{: #veeam_proxies_vmware_backup_proxy_dep}

By default, the role of the proxy is assigned to the backup server itself. However, this is sufficient only for small installations with low traffic load. For large installations, it is recommended to deploy dedicated backup proxies. To optimize the performance of several concurrent jobs, you can use several backup proxies. In this case, Veeam Backup and Replication distribute the backup workload between available backup proxies. You can deploy backup proxies both in the primary site and in remote sites. To deploy a proxy, you need to add a Windows-based or Linux-based server to Veeam Backup and Replication and assign the role of the VMware backup proxy to the added server. For requirements and limitations that backup proxies have, see [Requirements and Limitations for backup proxies](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_req).


## VMware Backup proxy services and components
{: #veeam_proxies_vmware_backup_proxy_services}

Backup proxies run light-weight services that take a few seconds to deploy. Deployment is fully automated. Veeam Backup and Replication installs the following components and services:

* Veeam® Installer Service is an auxiliary service that is installed and started on any Windows server once it is added to the list of managed servers in the Veeam Backup and Replication console. This service analyzes the system, installs, and upgrades necessary components and services depending on the role selected for the server.
* Veeam Data Mover is a component that performs data processing tasks on behalf of Veeam Backup and Replication. For instance, retrieving source VM data, performing data deduplication and compression, and storing backed-up data on the target storage.

To create a VMware Backup Proxy, complete the following steps:

1. Start the Veeam Backup and Replication console.
2. Click **Backup infrastructure** in the left pane.
3. Select **Backup proxies** on the left panel.
4. Click **Add proxy** and select **VMware backup proxy**.
5. Select the backup server from the **Choose Server** list and add choose the transport mode and the connected data stores that you want.
6. Select **Max concurrent tasks**.
7. Add traffic rules.
8. Review the changes and click **Finish**.

Sometimes, the backup proxy might not be able to use some transport modes due to known limitations. For more information, see [Transport modes](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes). If you assign the backup proxy role to a hardened repository, only the Network mode will be available. Other transport modes are grayed out.
{: note}

## Related links
{: #veeam_proxies_vmware_backup_proxy-links}

* [Add endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_req#veeam_proxies_req-links)
* [VMware CDP proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_vmware_cdp_proxy)
* [Transport modes](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes)
* [Backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_backup_proxy)



