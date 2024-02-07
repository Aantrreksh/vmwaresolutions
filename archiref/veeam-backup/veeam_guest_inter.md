---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: guest interaction proxies

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Guest interaction proxies
{: #veeam_guest_inter}

The guest interaction proxy sits between the backup server and the processed virtual machine (VM). This component is needed if the backup or replication jobs perform the following processing of VMs:

* Application-aware processing
* Indexing of guest file system
* Transaction log processing

To interact with the VM guest OS, Veeam Backup and Replication installs nonpersistent runtime components or uses persistent agent components in each VM. The task of deploying these components in a VM is performed by the guest interaction proxy.

## Related links
{: #veeam_guest_inter-links}

* [Nonpersistent runtime components and persistent agent components](https://helpcenter.veeam.com/docs/backup/vsphere/runtime_process.html?ver=120){: external}
