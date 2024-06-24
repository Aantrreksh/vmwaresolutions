---

copyright:

  years:  2021, 2024

lastupdated: "2024-05-21"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Veeam on bare metal server introduction
{: #veeam-bms-archi-intro}

The Veeam® on bare metal server for {{site.data.keyword.vmwaresolutions_full}} service can be used as a dedicated and all-in-one backup solution for {{site.data.keyword.vcf-auto}} instances or {{site.data.keyword.rw}}.

The Veeam on bare metal server solution is built on standard {{site.data.keyword.cloud_notm}} bare metal servers. The servers have a dedicated compute and a local dedicated storage. This solution provides a backup infrastructure that is physically isolated from other {{site.data.keyword.cloud_notm}} Storage services.

The solution uses Direct Attached Storage (DAS), that is, local SATA disks with RAID 6 attached to the bare metal server, as the Storage Repository for backups. For scaling up, customers can add more proxy servers to the solution to add backup capacity and performance. They can also use {{site.data.keyword.cloud_notm}} Object Storage together with Veeam's scale-out backup repository functions for redundancy (copying backups) or long-term retention (offload backups).

## Related links
{: #veeam-bms-archi-overview-intro}

* [Veeam Backup and Replication](https://www.veeam.com/vm-backup-recovery-replication-software.html?ad=menu-products){: external}
* [Veeam Help Center technical documentation](https://www.veeam.com/documentation-guides-datasheets.html?ad=menu-resources){: external}
