---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-12"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# IBM Spectrum Protect Plus overview
{: #spp_considerations}

New installations of the IBM Spectrum® Protect Plus service are no longer supported for new or existing deployments of {{site.data.keyword.vcf-auto}} instances. You can still use or delete existing IBM Spectrum Protect Plus installations on your existing instances. If you want to install IBM Spectrum Protect Plus yourself, see [IBM Spectrum Protect Plus documentation](https://www.ibm.com/docs/en/spp).
{: deprecated}

The IBM Spectrum Protect Plus service provides an efficient and scalable solution for data protection, data reuse, and data recovery for virtual environments. You can implement the service as a stand-alone solution or you can integrate it with your IBM Spectrum Protect environment to offload copies for long-term storage and data governance.
{: shortdesc}

## Technical specifications for IBM Spectrum Protect Plus
{: #spp_considerations-specs}

The following components are included in the IBM Spectrum Protect Plus service:

### vCenter Server resources
{: #spp_considerations-vcenter}

* Server VM running IBM Spectrum Protect Plus server
   * Linux® 4.19.65-1c.el7.x86_64 operating system
   * 8 x 2.0 GHz cores
   * 48 GB RAM
   * 528 GB disk
* Secondary VM running IBM Spectrum Protect Plus vSnap server and VADP proxy
   * Linux 4.19.65-1c.el7.x86_64 operating system
   * CPU and RAM configured based on the selected storage size and the sizing guidance in [IBM Spectrum Protect Plus Blueprints](https://www.ibm.com/support/pages/node/1119489){: external}
   * 278 GB disk

### Storage for backups
{: #spp_considerations-backup-storage}

Customizable storage for backups with the following options.
* Amount of file storage: 1 - 10
* Each endurance file storage: 500, 1000, 2000, 4000, 8000, or 12000 GB
* Storage performance: 0.25, 2, or 4 IOPS/GB

For planning and sizing information, see [IBM Spectrum Protect Plus Blueprints and Sizing Spreadsheet](https://www.ibm.com/support/pages/node/1119489){: external}.

### Storage for management
{: #spp_considerations-mgmt-storage}

One 1000 GB, 2 IOPS/GB endurance file storage that hosts the IBM Spectrum Protect Plus virtual machine and running on the same subnet as the backup storage.

### Networking
{: #spp_considerations-network}

Two portable private IP addresses.

### Licenses and fees
{: #spp_considerations-license}

* IBM Spectrum Protect Plus (10 to a maximum of 1000 VM licenses in increments of 10)
* IBM Spectrum Protect Plus license offered through the {{site.data.keyword.vmwaresolutions_short}} console (number of VMs in packages of 10) or as BYOL

## Considerations when you delete IBM Spectrum Protect Plus
{: #spp_considerations-remove}

Review the following considerations before you delete the IBM Spectrum Protect Plus service:
* Before you delete the service, you must remove any personal VMs from storage that are deployed with this service.
* Ensure that all the backup job configurations are removed along with active backup or restore operations.
* When you delete the service, the storage for the backup repository is deleted from the IBM Spectrum Protect Plus VM and the storage order is canceled, which deletes the backup repository data permanently.
* When you delete the service, the backup storage that is ordered for the service is deleted too. All the backups become inaccessible during service deletion.
