---

copyright:

  years:  2021, 2024

lastupdated: "2024-09-17"

keywords: data encryption in VMware Solutions, data storage for VMware Solutions, bring your own keys for VMware Solutions, BYOK for VMware Solutions, key management for VMware Solutions, key encryption for VMware Solutions, personal data in VMware Solutions, data deletion for VMware Solutions, data in VMware Solutions, data security in VMware Solutions

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Securing your data in VMware Solutions
{: #data-security-mng-data}

Know what data is stored and encrypted and how to delete any stored data to ensure that you can securely manage your personal data when you use {{site.data.keyword.vmwaresolutions_full}}. 
{: shortdesc}

## Data storage and encryption in VMware Solutions
{: #data-security-data-storage}

When a user onboards to VMware Solutions and orders instances, we store and manage user data of configuration and metadata that is associated with the user and ordered instances. That user data includes the following items.

* For both {{site.data.keyword.vcf-auto}} and {{site.data.keyword.vm-shared}} instances, the user data includes the following items:
   * IBMid (email)
   * Instance configuration information
   * Instance access information such as login credentials to VMware Cloud Director, VMware vCenter Server®, and VMware NSX® Manager.
* Additionally for {{site.data.keyword.vcf-auto-short}}, the user data also includes the {{site.data.keyword.cloud_notm}} classic infrastructure credentials (username and API key).

This configuration data and metadata is stored and managed by IBM. It is encrypted at REST and in transit. Additionally, sensitive data such as API keys and access information are encrypted with customer–specific encryption keys.

For {{site.data.keyword.vcf-auto-short}}, you can bring your own data to {{site.data.keyword.cloud_notm}} bare metal servers and {{site.data.keyword.filestorage_full_notm}} and {{site.data.keyword.cloud_notm}} {{site.data.keyword.blockstorageshort}} that is managed by your VMware instance. All of this data is managed by you and not managed by IBM, and you have the option of encrypting it using various solutions.

These solutions include the following options:
* KMIP™ for VMware service along with {{site.data.keyword.cloud_notm}} Key Protect or {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services to enable vSAN™ or VMware vSphere® encryption for your workloads
* Other self–managed VMware–compatible encryption technologies

For {{site.data.keyword.vm-shared}}, your workload data exists in an IBM–managed cloud infrastructure account. You are provided with the default vSphere encryption option for your VMs, which uses IBM–managed keys that are backed by the {{site.data.keyword.cloud_notm}} KMIP for VMware and Hyper Protect Crypto Services. You can optionally implement your own encryption solutions within your VMware workloads.

## Data storage and encryption in Veeam Availability Suite service for {{site.data.keyword.vm-shared}}
{: #data-security-data-veeamshared}

{{site.data.content.shared-deprecated-note}}

If you have a {{site.data.keyword.vm-shared}} instance, you can get extra services, such as Veeam Availability Suite™, which is relevant to data storage and encryption.

The Veeam Availability Suite backup storage uses a unique scale-out backup repository (SOBR) object for each customer. The SOBR is programmatically configured for each customer, with a dedicated location on each disk and a generated backup file encryption password. The SOBR includes an extent that is backed by {{site.data.keyword.blockstoragefull}} in each of the physical data centers within the specific region. For example, if the virtual data center is in **Dallas 10**, the SOBR has extents in **Dallas 10**, **Dallas 12**, and **Dallas 13**. The SOBR includes a customer-specific Cloud Object Storage bucket for more cost-effective long-term storage and as a second copy. Depending on the regions and compliance requirements of each geography, the Cloud Object Storage buckets remain in the same country, which is sometimes the same physical site.

When you decide to use the Veeam self-service portal to create backup jobs, identify which vApp and VM instances from any virtual data center in the organization participate in the backup job. Those backups are stored in the organizations SOBR.

You can manage (restore or delete) backups in the Veeam self-service portal. All backups are deleted if a virtual organization is deleted.

## IBM policy for data protection with Veeam
{: #data-security-veeam-policy}

You can configure the Veeam service in various ways. Some options include self-service, but in all cases IBM defaults to keeping backup restore points and chains. Consider the following IBM policies for data protection with Veeam.

### Backup job creation
{: #data-security-backup-job-create}

When you create a backup job, you add VMs or vApps to the job for data protection and also define the backup job schedule. The IBM policy is to never remove your VMs or vApps from your backup jobs or to delete any backups without your permission.

### Removal of backups
{: #data-security-backup-remove}

To remove backups, you can choose to remove VMs or vApps from the backup job or delete VMs or vApps that were previously backed up. In either case, you are responsible for deleting the old restore points. Before you remove VMs or vApps or delete the restore points, consider the following information.

#### Backup chain format
{: #data-security-backup-remove-chain}

Starting with Veeam 12, the IBM policy uses per-machine backup with separate metadata files for backup chain format. For more information, see [Backup Chain Formats](https://helpcenter.veeam.com/docs/backup/vsphere/per_vm_backup_files.html?ver=120){: external}.

#### Backup job retention policy
{: #data-security-backup-remove-retention}

The backup retention policy defines how many restore points to retain on disk. After the allowed number of restore points is exceeded, Veeam applies the retention policy to remove the earliest restore point from the backup chain. Depending on your business requirements, it is your responsibility to set the retention policy when you create the backup job. For more information, see [Short-Term Retention Policy](https://helpcenter.veeam.com/docs/backup/vsphere/retention_policy.html?ver=120){: external}.

You can update the retention policy later. However, the new settings are applied only to the new data and cannot be applied to previous data that maintains the previous retention policy setting.
{: note}

#### Removal of restore points
{: #data-security-backup-remove-restore-points}

Veeam keeps at least one full backup chain and doesn't remove old restore points until a second full backup (synthetic or active) is created and a new backup chain starts. For more information, see [Removal of Restore Points](https://helpcenter.veeam.com/docs/backup/vsphere/retention_separate_vms.html?ver=120){: external}.

#### Retention policy for deleted items
{: #data-security-backup-remove-ret-delete}

Veeam has the **Remove deleted items data after** setting available for each backup job to delete restore points for deleted items after a set number of days. The IBM policy does not enable this setting by default, but can enable the setting when a support case is opened. You must provide the following information in the support case to enable the setting.

* The names of the backup jobs where you want to enable the setting.
* The value, in days, to set for the **Remove deleted items data after** setting.

When this option is enabled, the restore points for any VM or vApp that is no longer processed by the backup job is permanently deleted after the set number of days.
{: important}

For more information, see [Retention Policy for Deleted Item](https://helpcenter.veeam.com/docs/backup/vsphere/retention_deleted_vms.html?ver=120){: external}.

The retention policy is applied only if the job stops creating backups for the entire vApp. Therefore, a removal of VMs within vApps does not result in automatic deletion of those restore points. It is your responsibility to delete the restore points.
{: note}

### Moving items between backup jobs
{: #data-security-backup-moving-between}

You can move VMs or vApps between backup jobs. Any VM or vApp that you move to a new backup job results in a new backup chain and restore points under the new backup job. Removing the original backup and restore points in this case falls into the same category as removing backups. You are responsible for deleting the original restore points.

## Protecting your sensitive data in VMware Solutions
{: #data-security-data-encryption}

### {{site.data.keyword.cloud_notm}} Support access
{: #data-security-ibm-access}

{{site.data.keyword.cloud_notm}} Support has access to your VMware virtualization environment.

For {{site.data.keyword.vcf-auto-short}}, IBM maintains this access to enable automated Day 2 operations such as capacity expansion, and to enable support for problem resolution. For more information, see [Policy for accessing clients' instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_compl_info#vc_compl_info-policy-for-access-client-inst) and [Consent to accessing client environments](/docs/vmwaresolutions?topic=vmwaresolutions-vc_compl_info#vc_compl_info-consent-to-access-client-environment).

For {{site.data.keyword.vcf-auto-short}}, you can take steps to limit {{site.data.keyword.cloud_notm}} access to your instance. These steps can include the following actions:

* You must create a functional {{site.data.keyword.cloud_notm}} account to own the API key that you provide to VMware Solutions for provisioning. Ensure that you monitor the mailbox of this account for notices.
* You can regenerate this API key to revoke automation and support access to your API key. When you need to restore {{site.data.keyword.cloud_notm}} access, for example, to deploy a new host, you must reenter the API key on the **Settings** page of the VMware Solutions console.
* {{site.data.keyword.cloud_notm}} retains a set of [user IDs](/docs/vmwaresolutions?topic=vmwaresolutions-audit_user_ids) in your instance. You can disable or revoke these user IDs. When you need to restore {{site.data.keyword.cloud_notm}} access, for example, to deploy a new host, you must re-enable these accounts. If you changed the password for these accounts, you must open a support ticket to provide the updated password to {{site.data.keyword.cloud_notm}}.

For {{site.data.keyword.vm-shared}}, {{site.data.keyword.cloud_notm}} manages the virtualization environment and this access cannot be revoked.

### About customer-managed keys
{: #data-security-about-encryption}

* For {{site.data.keyword.vcf-auto-short}}, envelope encryption is used to offer customer–managed keys.
* For {{site.data.keyword.vm-shared}}, envelope encryption is used but with IBM–managed rather than customer–managed keys.

Envelope encryption within VMware Solutions uses the [KMIP for VMware service](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations) to provide key management for vSphere or vSAN encryption.

In both cases, these offerings use {{site.data.keyword.cloud_notm}} Key Protect or {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services for key wrapping and unwrapping. Key Protect offers Bring Your Own Key (BYOK) capability by using FIPS 140–2 level 3 certified hardware security modules (HSMs). Hyper Protect Crypto Services offers Keep Your Own Key (KYOK) capability by using FIPS 140–2 level 4 certified HSMs.

### Enabling customer-managed keys for VMware Solutions
{: #data-security-using-byok}

You can use {{site.data.keyword.cloud_notm}} key management with vSphere or vSAN encryption. For more information, see the [KMIP for VMware implementation guide](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-implementation).

### Working with customer-managed keys for VMware Solutions
{: #data-security-working-with-keys}

For more information about considerations for VMware key management, key revocation, and key rotation, see:
* [KMIP for VMware considerations](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-design#kmip-design-considerations)
* [KMIP for VMware management guide](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-implementation#kmip-implementation-key-rotation)

## Deleting your data in VMware Solutions
{: #data-security-data-delete}

### Deleting VMware Solutions instances
{: #data-security-service-delete}

* When you delete a {{site.data.keyword.vcf-auto-short}} instance, all associated customer workload data is deleted. The underneath IaaS resources are also deleted at the end of the corresponding billing cycle. 
* When you delete a {{site.data.keyword.vm-shared}} instance, all associated customer data is deleted immediately.

Along with the instance deletion, the instance's configuration and metadata are also marked as "inactive". You can request complete deletion of the metadata through a "secure wipe" ticket.  

### Restoring deleted data for VMware Solutions
{: #data-security-data-restore}

You are responsible to make provision for backup and recovery of all data you bring to VMware Solutions. {{site.data.keyword.cloud_notm}} does not back up your workload data and cannot restore it after deletion.

## Related links
{: #data-security-related}

* [Managing IAM access for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-iam)
* [Auditing events for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-at-events)
