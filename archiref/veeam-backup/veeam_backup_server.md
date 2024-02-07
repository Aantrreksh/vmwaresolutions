---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-04"

keywords: requirements for vmware backup proxies, limitations for vmware backup proxies, backup proxies

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Backup server
{: #veeam_backup_server}

The backup server is a Windows-based machine on which Veeam Backup and Replication is installed. It is the core component in the backup infrastructure and performs all types of administrative activities, including:

* Coordinates backup, replication, recovery verification, and restore tasks.
* Controls job scheduling and resource allocation.
* It is used to set up and manage backup infrastructure components as well as specify global settings for the backup infrastructure.

During service deployment, the Veeam Backup and Replication software is deployed on the virtual machine (VM), VSI, or bare metal server. The distributed deployment scenario is recommended for large geographically dispersed virtual environments with multiple Veeam Backup and Replication servers that are installed across different sites. These backup servers are federated under **Veeam Backup Enterprise Manager**, which provides centralized management and reporting for the backup servers through a web interface. 

Additional backup servers can be added manually to create a Veeam® distributed scenario deployment.
{: note}

## Console
{: #veeam_backup_server_con}

The Veeam Backup and Replication console provides access to the backup server. Log in to Veeam Backup and Replication and perform data protection and disaster recovery operations on the backup server. During service deployment, the Veeam Backup and Replication console is deployed onto the Veeam Backup and Replication server. 

The console can be removed from the server and can be deployed on one or more dedicated machines to access the backup server remotely.
{: note}

## Related links
{: #veeam_backup_server-links}

* [Distributed deployment](https://helpcenter.veeam.com/docs/backup/vsphere/distributed.html?ver=120){: external}
* [Veeam Backup Enterprise Manager](https://helpcenter.veeam.com/docs/backup/vsphere/enterprise_manager.html?ver=120){: external}
* [Installing Veeam Backup and Replication](https://helpcenter.veeam.com/docs/backup/vsphere/install_vbr.html?ver=120){: external}
* [Backup and Replication console](https://helpcenter.veeam.com/docs/backup/vsphere/backup_console.html?ver=120){: external}
* [Installing Veeam Backup and Replication console](https://helpcenter.veeam.com/docs/backup/vsphere/install_console.html?ver=120){: external}
