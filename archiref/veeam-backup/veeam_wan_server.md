---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: wan accelerators, log shipping servers

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# WAN accelerators
{: #veeam_wan_server}

Veeam® WAN acceleration is a technology that optimizes data transfer to remote locations, specifically for off-site backup copy and replication jobs. It combines the following operations to optimize the data transfer and reduce the amount of data flow over the WAN:

* Network traffic compression
* Multi-streaming upload
* Global data deduplication
* Variable block size deduplication

{{site.data.keyword.cloud}} bare metal servers with 10 Gb interfaces are recommended for WAN accelerators. For more information, see [WAN accelerators](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#wan){: external}.

## Log shipping servers
{: #veeam_wan_server_log}

Log shipping servers are dedicated components that Veeam Backup and Replication uses for backup of Microsoft SQL Server transaction logs, PostgreSQL WAL files, and Oracle archive logs. They establish a direct connection between the guest OS and the backup repository. If possible, log files are shipped directly from the guest OS to the backup repository. If you don't have any direct connection, the files are shipped through log shipping servers. You can instruct Veeam Backup and Replication to choose a log shipping server automatically from the list of available servers or use a specific server.

## Related links
{: #veeam_wan_server-links}

* [Adding WAN accelerator](https://helpcenter.veeam.com/docs/backup/vsphere/wan_add.html?ver=120){: external}
* [Log shipping servers](https://helpcenter.veeam.com/docs/backup/vsphere/log_shipping_server.html?ver=120){: external}
* [Microsoft SQL Server log backup](https://helpcenter.veeam.com/docs/backup/vsphere/sql_backup.html?ver=120){: external}
* [PostgreSQL WAL files backup](https://helpcenter.veeam.com/docs/backup/vsphere/postgresql_backup.html?ver=120){: external}
* [Oracle log backup](https://helpcenter.veeam.com/docs/backup/vsphere/oracle_backup.html?ver=120){: external}

