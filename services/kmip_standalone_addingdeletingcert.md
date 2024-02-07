---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-06"

keywords: KMIP certificate, add certificate KMIP, delete certificate KMIP

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Managing certificates for KMIP for VMware instances
{: #kmip_standalone_addingdeletingcert}

You can view the certificates that you added to your KMIP™ for VMware® instance. When you no longer need a certificate, you can also delete it from your instance.

## Procedure to view certificates for KMIP for VMware instances
{: #kmip_standalone_addingdeletingcert-view}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources** > **KMIP for VMware** from the left navigation pane.
2. In the **KMIP for VMware** table, click the instance to view the certificates for.
3. View the list of added certificates under the **Client SSL certificates** section.
4. To view the content of a particular certificate, click **Download**.

## Procedure to delete certificates from KMIP for VMware instances
{: #kmip_standalone_addingdeletingcert-delete}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources** > **KMIP for VMware** from the left navigation pane.
2. In the **KMIP for VMware** table, click the instance that you want to delete certificates from.
3. In the **Client SSL certificates** table, locate the certificate that you want to delete and click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete").

   The client immediately loses access to all keys for encrypting and decrypting data or backup data. For the client to gain access again, you must add the client SSL certificate again.
   {: attention}

## Related links
{: #kmip_standalone_addingdeletingcert-related}

* [Viewing KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_viewing)
* [Ordering KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_ordering)
* [Deleting KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_deleting)
* [Auditing events for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-at-events)
