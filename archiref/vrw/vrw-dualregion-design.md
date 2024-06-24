---

copyright:

  years:  2021, 2024

lastupdated: "2024-06-04"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Dual region Disaster Recovery design
{: #vrw-dualregion-design}

The design uses the following structure:
* Network
* vCenter
* VMware NSX® Manager
* Caveonix RiskForesight™
* VMware Aria Operations™ for Logs
* VMware Aria Operations™ for Networks
* VMware Aria® Operations™ Manager
* AD/DNS/NTP
* Veeam®
* KMIP for VMware®
* Hyper Protect Crypto Service

## Network design
{: #vrw-dualregion-design-network}

As the design uses two VMware Regulated Workloads instances, the network design is at each region and is documented at [Underlay networking](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-underlay-network) and [Overlay networking](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-overlay-network).

The key design element at the network level is the adoption of cross-region network for the use of the VMware Aria Operations Manager analytic cluster. The cross-region network is a layer 3 construct that allows the use of the same IP subnet space at either the protected region or the recovery region. In normal operations, the cross-region network is tethered to the vSRX or FortiGate in the protected region that is, the default gateway for this network is the vSRX or FortiGate. The protected region vSRX or FortiGate then advertises this network so that it is reachable from other networks. In recovery operations, the cross-region network is tethered to the vSRX or FortiGate in the recovery region. The recovery region vSRX or FortiGate then advertises this network so that it is reachable from other networks. The use of the cross-region network allows the VMware Aria Operations Manager Analytic cluster to retain the same IP addresses when they are recovered to the recovery region.

Review the following network design decisions:
* The {{site.data.keyword.cloud}} classic network environment does not allow the stretching of VLANs across data centers. Therefore, this design does not use stretched VLANs at the physical network infrastructure level.
* While some VMware NSX™ designs can stretch segments across geographically distant vSphere clusters, these designs require a common NSX cluster, which does not meet the design requirements for independence between regions.
* It's possible to stretch networks between geographically dispersed vSRX appliances. However, this design does not present this use case.
* Recovered management components use the same IP addressing to minimize recovery effort.
* To provide isolation of traffic, the design uses tunnels (GRE or IPsec driven by customer requirements) between regions and also between the region and the SaaS consumer and SaaS provider.
* BGP is used between the regions and the SaaS provider and SaaS consumer to advertise the required routes at the appropriate locations during normal operations and disaster recovery invocation.
* The VMware Aria Operations Manager DR design requires that the analytics cluster is restarted in the recovery region by using the same IP addresses for the cross-region subnet. This process is achieved by "moving" the cross-region {{site.data.keyword.cloud_notm}} portable subnet to the recovery region. This process is possible because the default gateway for this subnet is the vSRX. However, this subnet is not natively reachable externally to the vSRX unless through the SaaS Provider VPN tunnel.

## vCenter Server
{: #vrw-dualregion-design-vcenter}

Each region has a vCenter Server instance for the management of the ESXi hosts within the region. Each instance is a separate SSO domain. The {{site.data.keyword.cloud_notm}} design uses a vCenter Server Appliance (VCSA) with an embedded Platform Services Controller (PSC). The use of one vCenter per region with separate SSO domains provides service isolation.

Within each region, vSphere High Availability (HA) provides availability of the appliance. For business resiliency, image level and file level backups of the appliance are recommended. These backups are stored locally in the region to allow for quick restore.

It is recommended to also configure Veeam backup copy jobs. If a failure of the Veeam Repository server occurs, a copy of the appliance backup at the other region is available.

Veeam is used to take an image level backup of the appliance. However, this type of backup does not quiesce the database and in rare occasions the image might not be usable. Therefore, a scheduled file level backup is also recommended.

To restore the VCSA image, configure the Veeam Backup and Replication Manager to attach to an ESXi host in the management cluster first, as the connection through the VCSA is not available. Within the Veeam UI restore wizard, select Entire VM, select the VCSA, then select Restore to a new location and then select the ESXi server.

It is good practice to back up the vDS switch configuration as part of the backup, which can be achieved through a script that is triggered by the backup job. For more information, see [PowerCLI Gather complete Virtual Distributed Switch (VDS) information from VMware vCenter](http://vcloud-lab.com/entries/powercli/powercli-gather-complete-virtual-distributed-switch-vds--information-from-vmware-vcenter){: external}.

The VCSA supports a file-based backup and restore mechanism that helps with the recovery of the appliance after a failure. It is only possible to do a file-based backup by using the VCSA management user interface (UI). In the design, an SFTP/SMB share on the Repository server is used as the target directory. This directory, through a Veeam file copy job, is copied to the other region for extra resiliency.

For a file-based restore, the process consists of deploying a new VCSA and restoring the data from the file-based backup to the new appliance.

## NSX Manager
{: #vrw-dualregion-design-nsxmanager}

NSX Manager provides the user interface and the API for creating, configuring, and monitoring the NSX components, such as virtual network segments, Tier-0 and Tier-1 gateways. NSX Manager implements both the management and the control planes for the NSX infrastructure. In the design, the protected region and the recovery region have their own NSX Manager cluster and the span of the Transport Zones is limited to the region. NSX managers per region enable service isolation so that each region is considered to be independent.

The use of the cluster virtual IP address provides high availability of the user interface and API of the NSX Manager cluster. The use of vSphere HA enables business continuity of a failed appliance.

Image-based backups of NSX manager are not supported. Therefore, it is recommended to configure a scheduled NSX appliance backup by using an SFTP server, as the only option with NSX. In the design, the SFTP server destination is a directory on the local Veeam Repository server. This Windows® server is configured as an SFTP server and used for the recovery of the backup files when needed. To limit the number of components needed, a separate stand-alone SFTP server is not used and instead the SFTP service within the Windows OS of the Veeam Repository server is used.

If the Veeam Repository server fails, then VCSA and NSX Manager backups are lost. Therefore, Veeam file copy jobs are used to copy the files from the local region to the remote region, which provides an off-site copy of the backup.

While the NSX Manager appliance is inoperable, the data plane is not affected, however, configuration changes are not possible. The restore process restores one node first and then prompts you to add the other nodes.

As region management is independent, network configurations in the protected region and the recovery region need to be in sync according to the customer's network resiliency strategy and overlay network design. You can choose different network resiliency strategies for the workload networks. After recovery, you might require some workloads to use the same IP addresses or a different IP addressing scheme.

It is recommended to use automation to create overlay network components so that both regions can be configured consistently. It is recommended that configuration management automation (such as PowerCli, Ansible, or Terraform) is used to provide the required synchronization.

## Caveonix RiskForesight
{: #vrw-dualregion-design-caveonix}

The {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads automation deploys a Caveonix RiskForesight all-in-one appliance in both the protected region and the recovery region. In the dual region design only the recovery region appliance is used, and is reconfigured so that the protected region vCenter, NSX manager are configured as Asset Repositories. The use of a single instance of Caveonix RiskForesight to manage compliance and cyberrisk across both the protected and recovery regions allows a single view of all environments. By placing the single instance of Caveonix RiskForesight in the recovery region, that instance is available when in DR invocation without any DR activities.

vSphere HA provides availability of the RiskForesight instance and for business resiliency. For image-level backups of the VM, configure and store them in the recovery region of the Veeam Repository server. Configure a Veeam backup copy job to copy the backup to the protected site so you can provide an off-site copy of the backup.

If you are using Caveonix RiskForesight to manage compliance and cyberrisk of the workload VMs, review the scaling of the RiskForesight instance. Replace the all-in-one deployment with the appropriate deployment to match the availability and retention requirements. For more information, see [Deployment models for Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix-deploy).

## VMware Aria Operations for Logs
{: #vrw-dualregion-design-vrli}

The {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads automation deploys a VMware Aria Operations for Logs environment that consists of four appliances with an integrated load balancer in each of the two regions. For more information, see [VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-vrli).

In the dual region design, each region is configured to forward log information to the VMware Aria Operations for Logs instance in the other region. Due to this forwarding configuration, either of the VMware Aria Operations for Logs clusters can be used to query the available logs from either of the regions. As a result, failover configuration is not required for the VMware Aria Operations for Logs clusters, and each cluster remains associated with the region in which it was deployed. This approach minimizes failover configuration in a DR invocation.

The use of a VMware Aria Operations for Logs cluster plus the use of vSphere HA provides high availability within a region. For business continuity, configure an image level backup of the cluster nodes by using Veeam.

## VMware Aria Operations for Networks
{: #vrw-dualregion-design-vrni}

The VMware Aria Operations for Networks service is an optional manual installation for {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads. For more information, see [VMware Aria Operations for Networks](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-vrni).

In the dual region design, install a VMware Aria Operations for Networks instance manually in each region for the monitoring and management of that region. Recovery of the instance in the protected region to the recovery region is not required. VMware Aria Operations for Networks instances are deployed per region to enable service isolation so that each region is considered to be independent.

The use of a VMware Aria Operations for Networks cluster and the use of vSphere HA provides high availability within a region. For business continuity, configure a file level backup. While VMware support image level backups, they recommend that the VMware Aria Operations for Networks appliances are shut down. This process is practical during an upgrade, but not for regular backups. Therefore, it is recommended to configure file level backup, which supports SSH backups. Configure VMware Aria Operations for Networks for scheduled backups with the Veeam Repository server as the target. Configure a Veeam file copy job to copy the backup to the protected site so you can provide an off-site copy of the backup.

## VMware Aria Operations Manager
{: #vrw-dualregion-design-vrops}

The {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads automation deploys a consolidated VMware Aria Operations Manager analytics cluster of four nodes: one primary node, one primary replica node, and two data nodes in each of the regions. For more information, see [VMware Aria Operations Manager design](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-vrops).

The dual region design uses this deployed architecture and requires some post-provisioning tasks to create the required design:

* Protected region
   * The four-node analytics cluster is reused and two extra remote collectors are deployed on an extra private portable subnet.
   * The analytics cluster is protected with Veeam Replication and fails over to the recovery region. IP addresses are not changed.
   * The remote collectors do not fail over and are region-specific.

* Recovery region
   * The four-node analytic cluster is deleted and two remote collectors are deployed on the existing private portable subnet.
   * The vSRX is configured so that the same subnet that hosts the analytics cluster is available in the recovery region. In normal operations, no VMs are hosted on this network and this network is isolated. On DR invocation, this network, and the recovered analytics cluster, becomes reachable from the remote collectors. This network is not reachable directly from the {{site.data.keyword.cloud_notm}} underlay network outside of the vSRX, but it is reachable through the VPN connections.

Review the following design decisions:
* The reuse of the automated deployment of VMware Aria Operations at the protected region reduces post deployment tasks.
* By using the VMware multiregion design for VMware Aria Operations that has the concept of region specific and cross-region components, you can recover the VMware Aria Operations analytic appliances to an identical network configuration. Re-IPing the appliances is possible but adds complexity.
* By deploying two remote collector nodes per region, the load is removed from the analytics cluster from collecting metrics from applications that do not fail over between regions.
* The use of Veeam Replication provides a replica of the VMware Aria Operations analytics cluster to allow recovery at the recovery region.
* Only the Analytics cluster needs to be backed up with Veeam, as remote collectors do not store data, however, for ease of redeployment a backup is taken.

## AD, DNS, and NTP
{: #vrw-dualregion-design-ad}

The VMware Regulated Workloads automation deploys a pair of Microsoft® Windows VMs in each instance. These VMs are configured as AD, DNS, and NTP servers. These services are independent in each region, a separate AD forest for each region, and recovery of the protected region services to the recovery region is not required.

vSphere HA provides availability of the VMs themselves and the Microsoft domain concept provides the availability of the Microsoft Windows services that runs on them. For business resiliency, configure image-level backups of the VMs and store them in the region's Veeam repository server. Configure a Veeam backup copy job to copy the backup to the other site so you can provide an off-site copy of the backup.

## Veeam
{: #vrw-dualregion-design-veeam}

The following use cases are expected for Veeam Backup and Replication in {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads dual region:
* Case 1. Backup and replication of management components only.
* Case 2. Backup and replication of management components and backup of workloads.
* Case 3. Backup and replication of management components and backup and replication of workloads.

The {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads dual region design focuses on use case 1. However, guidelines are provided so that use cases 2 and 3 can be solved for the individual needs of workload backup and replication.

Configure Veeam encryption for data at rest and data in transit so that VM data is not stored or transmitted unencrypted (which is the default setting). Veeam encryption requires the use of a password or passphrase and does not use the HPCS instance for the management of keys. When the VM is restored, select the encrypted storage policy to ensure that the VM is encrypted in the vSphere datastore.

The use of Veeam Backup and Replication in the regulated Workloads dual region design means that protected region encryption keys are not required in the recovery region. Therefore, separate HPCS, and KMIP for VMware services can be used.

The following post deployment activities are required to create the deployment scenario used in the dual region pattern:
* Remove the Veeam VMs at each region.
* Order a Windows bare metal server in each region. The specification of this server is documented in [Veeam on bare metal server introduction](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-bms-archi-intro). The small server is adequate for use case 1.

For use cases 2 and 3, the number and sizing of the bare metal servers needs to be calculated. For more information, see [Repository storage](https://bp.veeam.com/vbr/2_Design_Structures/D_Veeam_Components/D_backup_repositories/repositories%20storage.html){: external}.

The protected region bare metal Windows server hosts the following components:
* Proxy - A proxy is a “data mover” component that is used to retrieve VM data from the source datastore, process it and deliver to the target. As a rule, have the proxy as close as possible to the source data. This proxy is used for management components that are located in the protected region.
* Repository - A location used to store backup files for the management components in the protected region and also the target for backup copy jobs from the recovery region.
* SFTP/SMB server - These servers are not Veeam services but native Windows services that are used for file-level backups of some of the management components. A Veeam file copy job copies files to the recovery region for extra protection.

The recovery region bare metal Windows server hosts the following components:
* Backup server - In a two-site environment where replication is used, best practice is to install the Veeam Backup server component in the DR site. In a disaster situation, the backup server is available to start the recovery.
* Veeam Backup and Replication Database - Veeam Backup and Replication stores information about backup infrastructure, jobs settings, job history, sessions, and other configuration data in a Microsoft SQL Server database.
* Enterprise Manager - Enterprise Manager provides centralized management and reporting for one or multiple backup servers through a web interface. While this design has only one backup server instance, it is recommended to deploy Enterprise Manager when encryption is used for backup or backup copy jobs. It is advised to install the Enterprise Manager server on the recovery site so it is available for disaster recovery.
* Proxy server - This proxy is used for management components that are located in the recovery region.
* Repository - A location used to store backup files for the management components in the recovery region and also the target for backup copy jobs from the protected region.
* SFTP/SMB server - These servers are not Veeam services but native Windows services that are used for file-level backups of some of the management components. A Veeam file copy job copies files to the protected region for extra protection.

Review the following Veeam design decisions:
* For optimal performance and availability, placing the Veeam components on separate virtual and physical servers is considered best practice. However, this practice increases complexity in smaller environments. Therefore, the all-in-one deployment scenario for use case 1 is selected.
* As the total number of protected VMs is low, the embedded database option for the database for use case 1 is selected.
* The bare metal servers with direct attached storage option are used as it provides a backup infrastructure that is separated from the virtualized infrastructure compute and storage.
* In a two-site environment, it is best practice to install the Veeam Backup server component in the DR site. In a disaster situation, Veeam Backup server is available to start the recovery.
* Deploy Enterprise Manager to use password loss protection. Enterprise Manager administrators can unlock backup files by using a challenge-response mechanism.
* It is recommended that the proxy is as close as possible to the source data with a high-bandwidth connection. The traffic from the source to the proxy is not yet optimized, meaning that 100% of the backup data is transferred over this link. A good connection is required between proxy and repository as optimized data (normally ~50% of the source data size) is transferred across this link. Therefore, place proxies in both the protected and recovery regions.
* Proxies can be hosted on Windows Server or Linux OS with almost no performance differences. For the all-in-one deployment scenario, a Windows OS is used.
* For the repository server, a bare metal server is recommended to maximize performance and to separate the production environment that needs to be protected from the backup storage. It is also recommended to combine this practice with the proxy role to keep overheads on the virtual environment and on the network to a minimum. Best practice is to avoid the usage of the same storage for backups and for the virtualized infrastructure because the loss of this single system might lead to the loss of both copies of the data, the production and the backups.
* Repository servers can be either Windows or Linux. For the all-in-one deployment scenario, a Windows OS is used. Additionally, for Microsoft Windows-based repositories, Veeam uses the Windows Crypto API complying with the Federal Information Processing Standards (FIPS 140). For Linux-based repositories, Veeam uses a statically linked OpenSSL encryption library, without the FIPS 140 support.
* For bare metal servers, the block storage device can be a local disk or a LUN provided through a SAN by using iSCSI. For the VMware Regulated Workloads design, SAN that uses iSCSI is not supported. Therefore, local disk is used.
* Configure a scheduled, encrypted backup of the Veeam Backup and Replication configuration and use a Veeam file copy job to copy the file to the protected region. This way, if a failure occurs, the Veeam Backup server can be rebuilt and the configuration can be restored from an off-site copy.
* A capacity tier that uses {{site.data.keyword.cloud_notm}} Object Storage is not configured as the storage requirements for use case 1 are low.

The following guidance applies to use cases 2 and 3:
* Deploy more bare metal servers hosted on the workload cluster primary subnet to enable separation and scaling of backup repositories and allow better performance.
* For optimal performance and availability, placing the Veeam components on separate virtual and physical servers is considered best practice. Consider the use of a virtual machine for the Veeam Backup server as it provides high availability through vSphere HA. It also provides great flexibility in sizing and scaling as the environment grows.
* Microsoft SQL Server 2016 Express edition is included in the Veeam Backup and Replication standard installation. In environments with more than 500 protected VMs, consider the use of a different version of Microsoft SQL Server.
* For large storage requirements, it is recommended to not size volumes larger than 200 TB to keep failure domains small and manageable. For larger repositories, use a Scale-Out Backup Repository with multiple extents.
* The {{site.data.keyword.cloud_notm}} Object Storage repository cannot be used on its own but can be configured as Capacity Tier in the Veeam Scale-out Backup Repository. Consider this type of repository for large deployments or for deployments with a large archive requirement.

## KMIP for VMware
{: #vrw-dualregion-design-kmip}

The Key Management Interoperability Protocol (KMIP) for VMware service provides a 24x7 highly available service to allow the interconnection of vCenter to the Hyper Protect Crypto Service. For more information about the encryption design in for VMware® Regulated Workloads, see [Encryption](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-encryption).

KMIP is a region-based service. Therefore, in the {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads dual region design a separate KMIP instance is used and interfaced into vCenter and Hyper Protect Crypto Service. The available regions are Dallas, Washington DC, Sydney, London, Frankfurt, and Tokyo. When you order the KMIP service, select the KMIP instance in the region where the {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads instance is deployed.

## Hyper Protect Crypto Service
{: #vrw-dualregion-design-hpcs}

The IBM Hyper Protect Crypto Service (HPCS) is backed by a FIPS 140-2 level 4 certified hardware security module. It allows the {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads SaaS provider and SaaS consumer to manage their encryption keys.

For more information, see:
* [Getting started with {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-get-started)
* [Encryption](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-encryption)

Currently, HPCS is available in the following regions: Dallas, Washington DC, Sydney, and Frankfurt. It is possible, but not ideal, to use an HPCS instance in a different region for {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads instances in London and Tokyo.

The VMware Regulated Workloads design has two use cases for encryption:
* SaaS Provider - VMware vSphere encryption used to encrypt the management and workload VMs. These keys are managed by the SaaS Provider.
* SaaS Consumer - An optional, application level encryption that is used to encrypt application data in addition to the VM encryption. These keys are managed by the SaaS Consumer.

In the {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads dual region design for SaaS Provider key management, two separate HCPS instances are used along with the region-specific KMIP for VMware Service. The keys are not shared between HCPS instances.

Veeam Backup and Replication has access to the unencrypted data, and backup or replication data does not need the source encryption keys. When the backup is restored or the replica is configured, specify the target encrypted storage policy.

In the VMware Regulated Workloads dual-zone design, the following steps describe the backup and restore process between regions:
1. The protected VM is encrypted with VMware vSphere encryption in the VMware datastore.
2. A backup of the protected VM is taken.
3. VM backup files are encrypted on disk in the Protected Region Veeam Repository with Veeam encryption that is protected by a password that is stored in the Veeam database.
4. If a local restore is needed, the VMware datastore encryption storage policy is used to reencrypt the VM by using an encryption key from the protected region HPCS instance through the KMIP for VMware service.
5. Veeam network encryption is used for file and backup copy jobs to the recovery region.
6. VM backup files are encrypted on disk in the recovery region Veeam Repository with Veeam encryption.
7. If a restore is needed in the recovery region, the Veeam datastore encryption storage policy is used to reencrypt the VM by using an encryption key from the recovery region HPCS instance through the KMIP for VMware service.

For more information about Veeam encryption, see [Encryption standards](https://helpcenter.veeam.com/archive/backup/100/vsphere/encryption_standards.html){: external}.

In the {{site.data.keyword.cloud_notm}} for VMware® Regulated Workloads dual region design for SaaS Consumer key management, then the same encryption keys are required in the recovery region as used in the protected region. Currently, HPCS does not support the same encryption keys in two regions. If a failure of the first HPCS instance occurs, keys can be restored to another HPCS instance in another region.

For more information, see:
* [HPCS cross-region disaster recovery](/docs/hs-crypto?topic=hs-crypto-ha-dr#cross-region-disaster-recovery)
* [Restoring your data from another region](/docs/hs-crypto?topic=hs-crypto-restore-data)

## Related links
{: #vrw-dualregion-design-related}

* [Caveonix integration](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-caveonix)
* [Veeam on {{site.data.keyword.cloud_notm}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [Veeam Backup and Replication best practices](https://bp.veeam.com/vbr/){: external}
