---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: vmware cdp proxy, VMware cdp proxy operation

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware CDP proxy
{: #vmware_cdp_proxy}

A VMware® CDP proxy operates as a data mover and transfers data between the source and target hosts. VMware CDP proxy performs the following tasks:

* Receives virtual machine (VM) data from the production storage.
* Aggregates changed data.
* Prepares data for short-term restore points.
* Compresses and deduplicates data.
* Encrypts and decrypts data.
* Sends data to the storage in the disaster recovery site or another VMware CDP proxy.

You can assign the role of a VMware CDP proxy to any Windows-based or Linux-based virtual or physical server to your Veeam Backup and Replication infrastructure.

In {{site.data.keyword.cloud}} consider using:
* A VM and the HotAdd mode.
* The same VM for both backup and CDP proxy.


## Related links
{: #vmware_cdp_proxy-links}

* [Adding Microsoft Windows Servers](https://helpcenter.veeam.com/docs/backup/vsphere/add_windows_server.html?ver=120){: external}
* [Adding Linux Servers](https://helpcenter.veeam.com/docs/backup/vsphere/add_linux_server.html?ver=120){: external}
* [Adding VMware CDP proxies](https://helpcenter.veeam.com/docs/backup/vsphere/cdp_proxy_add.html?ver=120){: external}
* [How CDP works](https://helpcenter.veeam.com/docs/backup/vsphere/cdp_hiw.html?ver=120){: external}
* [System requirements for VMware CDP proxy](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#cdp_proxy){: external}

