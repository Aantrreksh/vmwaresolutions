---

copyright:

  years: 2023

lastupdated: "2023-10-13"

keywords: network attached storage, smb share, requirements for nfs backup repositories, limitations for nfs backup repositories

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Network attached storage
{: #veeam_repo_net_storage}

A backup repository is a storage location where Veeam® keeps backup files, VM copies, and metadata for replicated VMs. You can use direct attached storage to configure a backup repository.

You can add network shares as backup repositories in SMB share and NFS share.

## SMB (CIFS) Share
{: #veeam_repo_net_storage_smb}

To communicate with an SMB backup repository, Veeam Backup and Replication uses two Veeam Data Movers that are responsible for data processing and transfer:
* Veeam Data Mover on the VMware backup proxy
* Veeam Data Mover on the gateway server

An SMB share cannot host Veeam Data Movers. For this reason, to communicate with the SMB share, you need to deploy a gateway server. Veeam Backup and Replication will automatically deploy a Veeam Data Mover on this gateway server. When any job addresses the SMB backup repository, Veeam Data Mover on the gateway server establishes a connection with Veeam Data Mover on the VMware® backup proxy, enabling efficient data transfer over LAN or WAN. If you plan to move VM data to an off-site SMB repository over a WAN link, it is recommended that you deploy an extra gateway server in the remote site, closer to the SMB repository.

## NFS backup repository deployment
{: #veeam_repo_net_storage_nfs}

To communicate with an NFS backup repository, Veeam Backup and Replication uses two Veeam Data Movers that are responsible for data processing and transfer:
* Veeam Data Mover on the VMware backup proxy
* Veeam Data Mover on the gateway server

Windows-based gateway servers cannot be used for NFS shares with **krb5i** and **krb5p** support. 
{: note}

An NFS share cannot host Veeam Data Movers. For this reason, to communicate with the NFS share, you need to deploy a gateway server. Veeam Backup and Replication will automatically deploy a Veeam Data Mover on this gateway server. When any job addresses the NFS backup repository, Veeam Data Mover on the gateway server establishes a connection with Veeam Data Mover on the VMware backup proxy, enabling efficient data transfer over LAN or WAN. If you plan to move VM data to an off-site NFS repository over a WAN link, it is recommended that you deploy an extra gateway server in the remote site, closer to the NFS repository.

## Requirements and limitations for NFS backup repositories
{: #veeam_repo_net_storage_nfs_req}

A machine performs the role of an NFS repository must meet the following requirements:
* The machine must meet the system requirements. For more information, see the [System Requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#target){: external}.
* The role of the NFS repository can be assigned to a Microsoft Windows® or Linux machine (physical or virtual) or to NAS storage supporting the NFS protocol.
* The NFS repository must present read and write access rights to the gateway.

Veeam Backup and Replication does not support multipathing for NFS repository.
{: note}

## Requirements for Gateway server
{: #veeam_repo_net_storage_gateway}

A machine performing the role of a gateway server for communication with the NFS backup repository must meet the following requirements:
* The role of the gateway server can be assigned to a Microsoft Windows or Linux® machine (physical or virtual). The machine must meet the system requirements. For more information, see the [System Requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#gateway){: external}.
* You must add the machine to the Veeam Backup and Replication console as a managed server.
* For automatic gateway selection: The backup server must have read and write access in the NFS repository.
* For automatic gateway selection: If you configure automatic gateway selection for NFS repository, Veeam Backup and Replication might use the same machines as gateways for the repository and as proxies for backup jobs. Make sure that the backup proxies meet the following requirements:
   * If you explicitly choose backup proxies for backup jobs, provide read and write access rights to all proxies chosen for backup jobs that are targeted to the NFS repository.
   * If you configure automatic proxy selection for backup jobs, provide read and write access rights to all proxies in the Veeam Backup and Replication infrastructure.
   * If backup jobs that are targeted to the NFS repository use Linux proxies, check that the NFS client package is installed on the Linux proxy server.

## Requirements and limitations for Linux Gateway server
{: #veeam_repo_net_storage_gateway_linux}

In addition to the general requirements, the Linux gateway server must meet the following
requirements:
* The Linux gateway server must have the NFS client package installed.
* The credentials to authenticate with the Linux gateway server must have root or elevated to root permission.
* Veeam Backup and Replication uses the highest NFS protocol version that is supported by the gateway and the repository.

The suffix indicating the NFS version in the NFS share properties might not be displayed correctly.
{: note}

## Related links
{: #veeam_repo_net_storage-links}

* [Direct attached storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_dir_storage)
* [Create backup repository](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_create)
* [Add endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_endurance_storage)
* [Expanding ordered endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_expand_storage)


