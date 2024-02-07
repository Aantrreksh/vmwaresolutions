---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: scale-out backup repositories

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Scale-out backup repositories
{: #veeam_repo_scale_backup}

A scale-out backup repository is a repository system with horizontal scaling support for multitier storage of data. A scale-out backup repository has different tiers, or logical levels of storage.
* **Performance tier** - This level is used for fast access to data. It consists of one or more backup repositories or object storage repositories called performance extents.
* **Capacity tier** - Additional level for storing data that needs to be accessed less frequently. However, you can still restore your data directly from it. The capacity tier consists of cloud-based or on-premises object storage repositories called capacity extent.
* **Archive tier** - Additional level for archive storage of infrequently accessed data. Applicable data can be transported ether from the capacity or archive tier. For restorability from the archive tier, data must undergo a preparation process. {{site.data.keyword.cloud}} object storage cannot be used for the Veeam archive tier. Only Amazon S3 Glacier or Microsoft® Azure Archive Storage can be used.

During service deployment, the automation deploys a scale-out backup repository, which is created by using either the local repository or the Linux® hardened repository.

## Related links
{: #veeam_repo_scale_backup-links}

* [Performance tier](https://helpcenter.veeam.com/docs/backup/vsphere/backup_repository_sobr_extents.html?ver=120){: external}
* [Capacity tier](https://helpcenter.veeam.com/docs/backup/vsphere/capacity_tier.html?ver=120){: external}
* [Archive tier](https://helpcenter.veeam.com/docs/backup/vsphere/archive_tier.html?ver=120){: external}
