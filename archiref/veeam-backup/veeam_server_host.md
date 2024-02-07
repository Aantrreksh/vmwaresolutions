---

copyright:

  years: 2023, 2024

lastupdated: "2024-01-05"

keywords: servers and hosts, virtualization servers and hosts

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Virtualization servers and hosts
{: #veeam_server_host}

The virtualization servers and hosts are an infrastructure that must be integrated with Veeam® managed infrastructure. During service deployment, the vCenter Server instance is automatically registered. You can add the following types of servers and hosts to the backup infrastructure:

* [VMware vSphere Server](https://helpcenter.veeam.com/docs/backup/vsphere/add_vmware_server.html?ver=120){: external}
* [VMware Cloud Director](https://helpcenter.veeam.com/docs/backup/vsphere/adding_vcloud_director.html?ver=120){: external}
* [Microsoft Windows Server](https://helpcenter.veeam.com/docs/backup/vsphere/add_windows_server.html?ver=120){: external}
* [Linux Server](https://helpcenter.veeam.com/docs/backup/vsphere/add_linux_server.html?ver=120){: external}
* [Hyper-V servers](https://helpcenter.veeam.com/docs/backup/hyperv/add_hyperv_server.html?ver=120){: external}
* [Veeam Backup for AWS servers](https://helpcenter.veeam.com/archive/vbaws/6a/vbr_integration/deployment.html){: external}
* [Veeam Backup for Microsoft Azure servers](https://helpcenter.veeam.com/archive/vbazure/5a/vbr_integration/deployment.html){: external}
* [Veeam Backup for Google Cloud servers](https://helpcenter.veeam.com/archive/vbgc/40/vbr_integration/deployment.html){: external}
* [Nutanix AHV clusters](https://helpcenter.veeam.com/archive/vbahv/40/userguide/deployment.html){: external}
* [Kasten K10 instances](https://helpcenter.veeam.com/docs/backup/kasten_integration/deployment.html?ver=120){: external}


## General-purpose backup proxies
{: ##veeam_server_host_gen}

A general-purpose backup proxy is a component that operates as a data mover. The backup proxy processes jobs and delivers backup and restore traffic. General-purpose backup proxies can be used for the following operations:
* **NAS backup** - General-purpose backup proxies transfer data between a shared source file and a backup repository. In {{site.data.keyword.cloud}}, a general-purpose backup proxy needs to be deployed if you are backing up {{site.data.keyword.cloud_notm}} File services in Classic or VPC environments.
* **Veeam agent and integration of storage system snapshot** - General-purpose backup proxies transfer data between a storage system and a backup repository. You cannot integrate any storage system in {{site.data.keyword.cloud_notm}}. During service deployment, a general-purpose backup proxy is deployed on the Veeam backup server.


## Related links
{: #veeam_server_hosts-links}

* [General-purpose backup proxies](https://helpcenter.veeam.com/docs/backup/vsphere/backup_proxy_general.html?ver=120){: external}
