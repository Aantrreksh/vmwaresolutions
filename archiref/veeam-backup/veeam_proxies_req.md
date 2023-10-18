---

copyright:

  years: 2023

lastupdated: "2023-10-13"

keywords: connection to storage, requirements vmware backup proxy, limitations proxy linux

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Requirements and limitations for VMware backup proxies
{: #veeam_proxies_req}

The backup proxy is the component that reads the data from the source infrastructure, elaborates, and transfers it to the final destination: either the backup repository or the DR infrastructure (in case of replication).

Before you assign the role of a VMware® backup proxy, check the following prerequisites and limitations.

## Connection to storage
{: #veeam_proxies_req_connect}

The following list shows possible connections between the machine and storage that keeps backups of this machine. The first connection is the most efficient, the last one is the least efficient.

* A machine used as a VMware backup proxy should have direct access to the storage on which VMs reside or the storage where VM data is written. This way, the VMware backup proxy retrieves data directly from the data store bypassing LAN.
* The VMware backup proxy can be a VM with HotAdd access to VM disks on the data store. This type of proxy also enables LAN-free data transfer between the host and the VMware backup proxy.
* If neither of the above scenarios is possible, you can assign the role of the VMware backup proxy to a machine whose network is located closer to the source or the target storage to which the proxy will connect. In this case, VM data will be transported over LAN using the NBD protocol.

## General requirements and limitations
{: #veeam_proxies_req_general}

* The role of a VMware backup proxy can be assigned to the following machines:

   * Physical or virtual Microsoft Windows® machine
   * Physical or virtual Linux® machine

* Before assigning the role of the VMware backup proxy to a machine, you must first add a vCenter server to the backup infrastructure. 
* The machine must meet the system requirements. For more information, see the [System Requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#proxy/){: external}.
* The account that you specify when adding a server must have permissions that are described in [Permissions](https://helpcenter.veeam.com/docs/backup/vsphere/required_permissions.html?ver=120){: external}.
* It is recommended that you balance the number of tasks on backup proxies and backup repository to avoid the situation where some backup infrastructure resources remain idle while others are overloaded.
* You must add the machine to the Veeam Backup and Replication console as a managed server.
* If you back up proxies that use the Virtual appliance (HotAdd) mode to process VMdata, the change block tracking mechanism (CBT) will be disabled. For more information about CBT, see the [Changed Block Tracking](https://helpcenter.veeam.com/docs/backup/vsphere/changed_block_tracking.html?ver=120){: external}.
* If you back up encrypted VMs that use the Virtual appliance (HotAdd) mode, make sure that backup proxies are also encrypted. For more information, see the [Encrypted VMs](https://helpcenter.veeam.com/docs/backup/vsphere/encrypted_vms_backup.html?ver=120){: external}.
* A VMware backup proxy should be as close to the source data as possible with a high-bandwidth connection. Consider a good connection between proxy and repository.

## Requirements and limitations for VMware Backup proxy on Linux
{: #veeam_proxies_req_linux}

In addition to the general requirements and limitations, the following ones apply to Linux backup proxies:
* Linux backup proxies use the transport service for connection with backup infrastructure components. If the transport service cannot be installed, Linux backup proxy requires SSH connection.
* You can assign the role of a VMware backup proxy to a Linux server added with single-use credentials. For this configuration, only the Network mode (NBD) is supported, other transport modes will not be available for selection.
* Linux backup proxies cannot be used with VMware Cloud on AWS. This is because VDDK settings required by VMware cannot be enabled on Linux backup proxies.
* Linux backup proxies that use virtual appliance (HotAdd) transport mode do not support the VM copy scenario.
* Linux backup proxies cannot be used for guest interaction.
* For [Direct SAN with iSCSI access](https://test.cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes#veeam_proxies_transp_modes_dir_san), Linux backup proxies must have the Open-iSCSI initiator enabled.
* For [Direct NFS access](https://test.cloud.ibm.com/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes#veeam_proxies_transp_modes_dir_nfs_access), review the following information:
   * Linux backup proxies must have the NFS client package installed.
   * Debian-based backup proxies must have the nfs-common package installed.
   * RHEL-based backup proxies must have the nfs-utils package installed.
   
For more information about recommendations for VMware backup proxy parameters, see the [Veeam Backup and Replication best practice guide](https://bp.veeam.com/vbr/2_Design_Structures/D_Veeam_Components/D_backup_proxies/vmware_proxies.html){: external}.

## Related links
{: #veeam_proxies_req-links}

* [Transport modes](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes)
* [Backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_backup_proxy)
