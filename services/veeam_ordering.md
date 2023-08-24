---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-28"

keywords: Veeam, Veeam configuration, order Veeam

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering Veeam
{: #veeam_ordering}

You can include the Veeam® service with a new VMware vCenter Server® instance or add the service to your existing instance.

## Ordering Veeam for a new instance
{: #veeam_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. Veeam is in the **Recommended services** category and is already selected.
2. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering#veeam_ordering-config), then click **Save**.

## Ordering Veeam for an existing instance
{: #veeam_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **Veeam** service in the **Business continuity and migration** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering#veeam_ordering-config), then click **Save**.

## Veeam configuration
{: #veeam_ordering-config}

When you order the service, provide the following settings.

### Name
{: #veeam_ordering-name}

Specify a name for this service instance. The name must be unique across all Veeam service instances and all instances in the {{site.data.keyword.cloud}} account.

### Deployment type
{: #veeam_ordering-depl-type}

Select one of the following options:
* **Windows Server VM with iSCSI storage**. This option is not supported by VMware® Regulated Workloads instances.
* **Single Windows VSI with iSCSI storage**. This option is not supported by Security and Compliance Readiness Bundle instances or VMware Regulated Workloads instances.
* **Bare metal server with local storage**. This option requires VMware vSphere 7.

### Storage size
{: #veeam_ordering-config-storage-size}

The capacity that meets your storage needs. This option is not applicable to the **Bare metal server with local storage** deployment type.

For an example that shows what the capacity might be like, see [Capacity planning for backup repositories](https://helpcenter.veeam.com/docs/one/reporter/capacity_planning_for_repositories.html?ver=100){: external}.

### Storage performance
{: #veeam_ordering-config-storage-performance}

The IOPS (input/output operations per second) per GB based on your workload requirements. This option is not applicable to the **Bare metal server with local storage** deployment type.

### Backup disk
{: #veeam_ordering-config-backup-disk}

The backup disks are used as storage repositories for backups. This option is applicable only to the **Bare metal server with local storage** deployment type.

### Linux hardened repository
{: #veeam_Linux_hardened_repository}

You can order a Linux® hardened repository (LHR) to use for immutable storage. If you select a Linux hardened repository, a list of backup disk size options is displayed. Select the disk size that you want to order.

The Linux hardened repository is only supported for vSphere 7 NSX-T instances.

For more information, see [Hardened Repository](https://helpcenter.veeam.com/docs/backup/vsphere/hardened_repository.html?ver=120){: external} in the Veeam documentation.

### Number of VMs to license
{: #veeam_ordering-config-vms}

Enter the number of VMs (virtual machines) to license (minimum 1).

You can order a maximum of 3,000 licenses. If you need to have multiple licenses under a single license key, you must first purchase them. Then, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) to request that the license keys are consolidated into a single key.

## Related links
{: #veeam_ordering-related}

* [Veeam Backup and Replication 12 overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [Managing Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-managingveeam)
* [Ordering Veeam stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering_licenses)
* [Managing Veeam licenses](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_managing_licenses)
* [Ordering and configuring IBM Cloud Object Storage with Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-icos_ordering)
* [Veeam Backup and Replication](https://www.ibm.com/cloud/architecture/architectures/virtualization_backup_veeam)
* [Veeam website](https://www.veeam.com/){: external}
* [Veeam Help Center](https://www.veeam.com/documentation-guides-datasheets.html){: external}
