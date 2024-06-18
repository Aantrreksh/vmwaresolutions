---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-12"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# KMIP for VMware implementation and management
{: #kmip-implementation}

## Planning
{: #kmip-implementation-planning}

You are not charged for the KMIP™ for VMware service. To review the Key Protect and Hyper Protect Crypto Services pricing plans, see the [Key Protect](https://cloud.ibm.com/catalog/services/key-protect) and [Hyper Protect Crypto Services](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services) catalog pages.

If you are using VMware vSAN™ encryption, plan to use one root key in Key Protect or Hyper Protect Crypto Services, and two standard keys for each vSAN cluster that you encrypt.

If you are using VMware vSphere® encryption, plan to use one root key, one standard key per vSphere cluster, and one standard key per encrypted virtual machine (VM).

Key Protect and Hyper Protect Crypto Services are available in multizone regions (MZRs) only. Hyper Protect Crypto Services (HPCS) is available in selected MZRs only. KMIP for VMware® is automatically deployed in the same region as your Key Protect or HPCS instance. VMware vCenter Server® can tolerate high latency to the KMIP service, so distance is usually not be a cause for concern.

## Connecting the key management server
{: #kmip-implementation-connecting-kms}

To enable vSphere encryption or vSAN encryption by using KMIP for VMware, you need to complete the following tasks:

1. [Enable service endpoints in your account](/docs/account?topic=account-vrf-service-endpoint#service-endpoint).
2. Create a key manager instance, by using either [IBM Key Protect](/docs/key-protect?topic=key-protect-getting-started-tutorial) or [{{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-get-started#get-started). If you are using Hyper Protect Crypto Services (HPCS), be sure to [initialize your crypto instance](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-hsm) so that Hyper Protect Crypto Services can provide key-related functions.
3. Create a customer root key (CRK) within your key manager instance.
4. If you are using Key Protect, create an Identity and Access Management (IAM) [API key for a service ID](/docs/account?topic=account-serviceidapikeys&interface=ui#create_service_key) for use with KMIP for VMware. Grant this service ID both Platform **Viewer** access and Service **Write** access to your Key Protect instance.
5. [Create a KMIP for VMware instance](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_ordering) from the {{site.data.keyword.vmwaresolutions_short}} console.
6. If you are using HPCS, create an IAM service authorization for your KMIP for VMware instance to your HPCS instance. Grant your KMIP for VMware instance both Platform **Viewer** access and Service **VMware KMIP Manager** access to your HPCS instance.
7. Configure your KMIP for VMware instance to connect to your Key Protect or HPCS instance and select which CRK to use with KMIP.
8. Within vCenter Server, create a key provider cluster.
   * If you are using Key Protect, configure this cluster with two servers, one for each KMIP for VMware endpoint in your chosen region.
   * If you are using HPCS, configure this cluster to connect to the hostname and port that is uniquely assigned to your KMIP for VMware instance.
9. Select one of the VMware methods to generate or install a KMS client certificate in vCenter Server.
10. Export the public version of the certificate and configure it as an allowed client certificate in your KMIP for VMware instance. The key manager instance has a maximum interval of 5 minutes to get the configured client certificates. Therefore, if you are unable to build KMS trust to vCenter Server, wait for 5 minutes and try again.

## Enabling encryption
{: #kmip-implementation-enable-encrypt}

To use vSAN encryption, edit the vSAN general settings in your vCenter Server cluster and select the encryption checkbox.

The vSAN health check might send periodic warnings that it is unable to connect to the KMS cluster from one or more of your vSphere hosts. These warnings occur because the vSAN health check connection times out too quickly. You can ignore these warnings. For more information, see [vSAN KMS health check intermittently fails with SSL handshake timeout error](https://knowledge.broadcom.com/external/article?legacyId=67115){: external}.
{: note}

To use vSphere encryption, edit your VM storage policies to require disk encryption.

## Important caveats
{: #kmip-implementation-important-caveats}

Some VMs require special planning for encryption, especially if they are involved in a possible circular dependency to obtain the key material to operate themselves. Consider the following information:

- vCenter Server is involved in retrieving encryption keys. This VM must not be encrypted by using vSphere encryption and must not be on an encrypted vSAN datastore.
- The Microsoft Windows® Active Directory controllers in your environment are used for hostname resolution to connect to key management. Do not encrypt them by using vSphere encryption or place them on an encrypted vSAN datastore unless you are prepared to provide an alternate hostname resolution if you need to restart your environment.
- VMware does not recommend encrypting VMware NSX® VMs by using vSphere encryption.

## Key rotation
{: #kmip-implementation-key-rotation}

Rotate your [Key Protect](/docs/key-protect?topic=key-protect-rotate-keys#rotate-keys) or [Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-rotate-keys) customer root key (CRK) by using the {{site.data.keyword.cloud_notm}} console or API.

* For vSAN encryption, rotate your VMware key encryption keys and data encryption keys (optionally) from the vSAN general settings in your vCenter Server cluster.
* For vSphere encryption, rotate your VMware key encryption keys and data encryption keys (optionally) by using the **Set-VMEncryptionKey** PowerShell command.

## Key revocation
{: #kmip-implementation-key-revocation}

You can revoke all keys in use by KMIP for VMware by deleting your chosen CRK from your key manager.

When keys are revoked, all data that is protected by these keys and by your KMIP for VMware instance is cryptographically shredded by this method. VMware preserves some keys while an ESXi host is powered on, so you need to restart your vSphere cluster to ensure that all encrypted data is no longer in use.
{: important}

KMIP for VMware stores individual wrapped KEKs in your Key Protect or Hyper Protect Crypto Services instance by using names that are associated with the key IDs that are known to VMware. You can delete individual keys to revoke the encryption of individual disks or drives.

VMware does not delete keys from the KMS when a VM having encrypted disks is removed from inventory. This process is to allow recovery of that VM from backup or if it is restored to inventory. If you want to reclaim these keys and cryptographically invalidate all backups, you need to delete the keys from your key manager instance after you delete your VMs.
{: note}

## Related links
{: #kmip-implementation-related}

* [Solution overview](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-overview)
* [Solution design](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-design)
* [High availability and disaster recovery](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-hadr)
* [IBM Key Protect](/docs/key-protect?topic=key-protect-getting-started-tutorial)
* [{{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-get-started#get-started)
