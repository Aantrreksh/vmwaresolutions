---

copyright:

  years:  2021, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Veeam solution components
{: #veeam-bms-archi-components}

Review the Veeam® software components.

## Backup server
{: #veeam-bms-archi-components-vbr}

The Veaam Backup server (VBR) is a Windows®-based server on which Veeam Backup and Replication is installed. VBR is the core component in the backup infrastructure that coordinates and manages the configuration and interaction of the other components of the system. This component includes the backup infrastructure, connections to the hypervisors, and the agents that run on customer hosts. This infrastructure eliminates much of the configuration that is traditionally required to be done across several systems into one single pane of glass that streamlines deployment and management. The VBR is backed by the MS SQL 2016 database, which holds the metadata.

The VBR is accessed primarily by way of the Veeam console application, with authentication enabled PowerShell access and authentication enabled API access. Network traffic rules are defined on the VBR server to encrypt all network traffic between Veeam components required for VM backup jobs.

In this design, the all-in-one {{site.data.keyword.cloud_notm}} bare metal server with Windows 2019 operating system is used to host the VBR server component.

## Enterprise Manager
{: #veeam-bms-archi-components-em}

Enterprise Manager is a management and reporting component for managing multiple Veeam Backup and Replication installations from a single web console. Enterprise Manager is an optional component of this design.

Enterprise Manager runs as an application on Windows 2019 operating system. You can install Enterprise Manager on the all-in-one server, or alternatively to a server in another suitable backup location based on their design. The customers need to remember, that Enterprise Manager requires a configuration database, which needs to be considered when you deploy Enterprise Manager.

## Backup proxy
{: #veeam-bms-archi-components-proxy}

The Veeam proxy is a component that sits between the backup server and the other components of the backup infrastructure, such as storage repository. While the VBR server administers the individual backup tasks, the proxy processes these jobs and delivers the backup traffic. The Veeam Proxy is the high-performance data mover in the Veeam system. The Veeam proxy connects to the customer ESXi™ hypervisor and transfers data between the hypervisor and the various Veeam components as needed. This transfer can be to the local storage repository (local backup) or to a remote proxy (backup copy job or VM DR replication). All customer virtualized data is sent through at least one proxy at some point.

The initial all-in-one {{site.data.keyword.cloud_notm}} bare metal server includes a Veeam proxy and is sized to handle up backups for approximately 500 VMs of nominal size. The solution can be scaled by deploying more {{site.data.keyword.cloud_notm}} bare metal proxies. The extra proxy servers provide the same function as the embedded proxy but specifically for additional compute and network transfer resources to perform intensive VM replication that might exceed the resources that are provided by the all-in-one server build.

## Veeam Backup and Replication configuration database
{: #veeam-bms-archi-components-database}

The VBR is backed by an MS SQL 2016 database. By default, the design uses the Express version, which comes bundled with the standard Veeam installation. Express version is sufficient in size and performance through about 500VMs of nominal size before a full installation of MS SQL 2016 Standard would be required. The automation supports only local MS SQL 2016 Express as part of the service.

The MS SQL 2016 server requires a dedicated RAID 1 protected disk array in the all-in-one bare metal server.

Review the layout and volume and drive sizes for disks and volumes for MS SQL in all-in-one deployment:
- 2 x 1 TB SATA disks in RAID 1
   - VBR database
      - Database drive 250 GB
      - Log drive 100 GB
   - Enterprise Manager database (optional)
      - Database drive 250 GB
      - Log drive 100 GB

For {{site.data.keyword.vcf-auto}}, you are responsible for backing up the database. By default, VBR's backup is configured to use the RAID 6 array of the all-in-one server as the backup repository.

## Veeam Backup and Replication console
{: #veeam-bms-archi-components-console}

Veeam provides a self-service interface through the Veeam Console that is Role Based Access Controls (RBAC) enabled. The solution is deployed with one local administrator by default, and the solution can be integrated post deployment with the Infrastructure Active Directory™ of the {{site.data.keyword.vcf-auto-short}} instance. The design allows you to define more users on the Active Directory and assign them roles such as: system admin, reporting focal, or dba. Those users can then perform actions such as initiating restores and their scope is limited to the systems or data types for which they are responsible.

## Backup repository and scale-out backup repository
{: #veeam-bms-archi-components-scaleout}

The backup repository is a storage location where Veeam keeps backup files, VM copies, and metadata for replicated VMs. This design relies on DAS (local SATA disks) to store the operational copy of customer data. Data is written to the disk in deduplicated and compressed format.

Veeam supports various scaling methods and (virtually) unlimited scaling with Scale-out backup repository functions. The scale-out backup repository is a logical entity. It groups several backup repositories (called extents) to create a pool of storage devices and systems, summarizing their capacity. This design uses scale-out backup repository functions in the backup infrastructure and one scale-out backup repository is created for a customer by default. It is recommended that no more than 300 TB is used in the scale-out backup repository with the all-in-one MS SQL Express database.

The customer backup data that is stored in the scale-out repository is encrypted with Veeam's own encryption and the encryption keys are password protected.

For long-term storage needs, the scale-out repository helps to offload data from the performance tier (local DAS on the {{site.data.keyword.cloud_notm}} bare metal servers), to a capacity tier by using buckets in {{site.data.keyword.cloud_notm}} Object Storage. The offload traffic is encrypted and it flows over the internal {{site.data.keyword.cloud_notm}} private network. Each {{site.data.keyword.cloud_notm}} Object Storage bucket is encrypted with customer-specific keys and passwords based on customer's preference. Ordering {{site.data.keyword.cloud_notm}} Object Storage, or configuring {{site.data.keyword.cloud_notm}} Object Storage with Veeam is not part of the automation.

For more information about ordering and configuration, see the {{site.data.keyword.cloud_notm}} documentation and the Veeam documentation.

## Related links
{: #veeam-bms-archi-components-related}

* [Veeam Backup and Replication](https://www.veeam.com/vm-backup-recovery-replication-software.html?ad=menu-products){: external}
* [Veeam Help Center technical documentation](https://www.veeam.com/documentation-guides-datasheets.html?ad=menu-resources){: external}
