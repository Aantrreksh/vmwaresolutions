---

copyright:

  years:  2016, 2023

lastupdated: "2023-08-18"

keywords: KMIP for VMware, remove KMIP stand-alone, delete KMIP for VMware

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Deleting KMIP for VMware instances
{: #kmip_standalone_deleting}

Use this procedure to delete the KMIP™ for VMware® instances that you ordered for stand-alone use.

## Before you begin
{: #kmip_standalone_deleting-req}

You must remove encryption and configuration in the following sequence:
1. Decrypt all virtual machines or vSAN™ datastores that are protected by this KMIP for VMware instance, or rekey these resources by using a new Key Management Server (KMS).
2. Disable host encryption mode for your VMware vSphere® instance, or rekey your hosts by using a new KMS.
3. Remove the KMS configuration for all VMware vCenter Server® instances that are connected to this KMIP for VMware instance.
4. Remove the KMIP for VMware instance.
5. In your Key Protect or Hyper Protect Crypto Services (HPCS) instance, remove all standard keys that were in use by this KMIP for VMware instance.
6. (Optional) In your Key Protect or HPCS service instance, ensure that no other users are using the root key (CRK) that you are planning to remove, then remove the customer CRK that was in use by this KMIP for VMware instance.
7. (Optional) Ensure that no other users are using the Key Protect or HPCS service instance, then remove the Key Protect or HPCS service instance that was in use by this KMIP for VMware instance.

## Procedure to delete KMIP for VMware instances
{: #kmip_standalone_deleting-procedure}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources** > **KMIP for VMware** from the left navigation pane.
2. In the **KMIP for VMware** table, find the instance to delete.
3. In the **Actions** column, click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete").
4. In the **Delete instance** window, click **OK**.

   The status of the instance is changed to **Removing**. When the instance deletion is completed, the instance is no longer available in the **KMIP for VMware** table.

## Related links
{: #kmip_standalone_deleting-related}

* [Ordering KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_ordering)
* [Adding, viewing, and deleting certificates for KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_addingdeletingcert)
* [Viewing KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_viewing)
* [KMIP for VMware solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-overview)
* [Auditing events for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-at-events)
