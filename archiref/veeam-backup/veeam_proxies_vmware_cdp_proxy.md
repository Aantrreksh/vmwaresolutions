---

copyright:

  years: 2023

lastupdated: "2023-10-16"

keywords: vmware cdp proxy, VMware cdp proxy services, VMware cdp proxy components

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware CDP proxy
{: #veeam_proxies_vmware_cdp_proxy}

A VMware® CDP proxy is a component that operates as a data mover and transfers data between the source and target hosts. Basically, a VMware CDP proxy performs the following
tasks:

* Receives VM data from the production storage
* Aggregates changed data
* Prepares data for short-term restore points
* Compresses and deduplicates data
* Encrypts and decrypts data
* Sends data to the storage in the disaster recovery site or another VMware CDP proxy.

You can assign the role of a VMware CDP proxy to any windows-based or linux-based virtual or physical server added to your Veeam Backup and Replication infrastructure. We recommend that you configure at least two VMware CDP proxies: one (source proxy) in the production site and one (target proxy) in the disaster recovery site. To optimize performance of several concurrent tasks, you can use several VMware CDP proxies in each site. 

In this case, Veeam Backup and Replication distribute the restore workload between available proxies on a per-task basis, taking into account proxy connectivity and their current load. For more information about which proxies are considered the most appropriate for continuous data protection, see [How CDP Works](https://helpcenter.veeam.com/docs/backup/vsphere/cdp_hiw.html?ver=120){: external}.

## VMware CDP proxy services and components
{: #veeam_proxies_vmware_cdp_proxy_service}

VMware CDP proxies run light-weight services that take a few seconds to deploy. Deployment is fully automated. Veeam Backup and Replication installs the following
components and services:

* Veeam® CDP Proxy Service manages all CDP activities such as data aggregation, data compression and decompression, data transfer and other.
* Veeam Installer Service is an auxiliary service that is installed and started on any Windows server once it is added to the list of managed servers in the Veeam Backup and Replication console. The service analyzes the system, installs, and upgrades necessary components and services depending on the role selected for the server.
* Veeam Data Mover handles traffic that is sent during failback.

### VMware CDP proxy RAM and cache
{: #veeam_proxies_vmware_cdp_proxy_ram}

By default, a VMware CDP proxy stores the received data into RAM. If RAM is less or equal to 8 GB, the VMware CDP proxy uses 50% of the memory for the OS and 50% for data
processing. If RAM is larger than 8 GB, the VMware CDP proxy uses 4 GB for the OS and the rest of RAM for data processing. The VMware CDP proxy allocates at least 1 MB of RAM for each processed disk. 

This is a protective mechanism that guarantees that disk processing will not stop even if some disks produce too much data or cannot be processed. If a VMware CDP proxy runs out of the memory or cannot allocate space in the memory, the proxy starts storing data into the cache. If the cache and RAM get full and there is no available VMware CDP proxy, Veeam Backup and Replication uses the protective mechanism.
However, disk processing performance is low. Data is deleted from the cache or memory only after the proxy gets a notification that the target host has successfully saved data that is sent by the proxy.

## Requirements for VMware CDP proxy
{: #veeam_proxies_vmware_cdp_proxy_req}

Before you assign the role of a backup proxy, check the following requirements:

* For system requirements, see [System Requirements for VMware CDP Proxy Server](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#cdp_proxy){: external}.
* A VMware CDP proxy must be a Windows-based or Linux-based virtual or physical server.
* Before assigning the role of the VMware CDP proxy to a server, you must first add a vCenter server or VMware Cloud Director server to the backup infrastructure.
* For VMware CDP proxies deployed on physical servers, a fast network between hosts and VMware CDP proxies is required.

To create a VMware CDP proxy, complete the following steps:

1. Start the Veeam Backup and Replication console.
2. Click **Backup infrastructure** in the left pane.
3. Select **Backup proxies** on the left panel.
4. Click **Add proxy** and select **VMware CDP backup proxy**.
5. Select the backup server from the **Choose server** list and check the CDP host traffic port and CDP proxy traffic port. The range of available ports is 33032 – 33039.
6. Select the file path in the cache tab and cache size.
7. Add traffic rules.
8. Review the changes and click **Finish**.

## Related links
{: #veeam_proxies_vmware_cdp_proxy-links}

* [Add endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_req#veeam_proxies_req-links)
* [VMware backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_vmware_backup_proxy)
* [Transport modes](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes)
* [Backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_backup_proxy)

