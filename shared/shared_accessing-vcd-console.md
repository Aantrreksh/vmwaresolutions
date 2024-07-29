---

copyright:

  years:  2021, 2024

lastupdated: "2024-07-29"

keywords: manage shared resources, access the VMware Cloud Director Management console

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Accessing the VMware Cloud Director Management console
{: #shared_accessing-vcd-console}

{{site.data.content.shared-deprecated-note}}

You can use the VMware Cloud Director Management console to manage the {{site.data.keyword.vmwaresolutions_full}} Shared virtual data centers. You can access the VMware Cloud Director console from the virtual data center details page.

## Before you begin
{: #shared_accessing-vcd-console-prereq}

- The first time that you access the VMware Cloud Director console for the virtual data center region, you must set the **admin** credentials to generate an initial, complex, and random password. After the first **admin** password is generated, the **VMware Cloud Director console** option is enabled on the virtual data center details page.
- You do not need to generate an **admin** password for each virtual data center. Reuse the same password for all virtual data centers in the same region.

{{site.data.keyword.vmwaresolutions_short}} does not store the **admin** password. After a password is generated, you must capture it. If the password is lost or you get locked out of your account, you can generate a new password at any time.
{: note}

## Procedure to access the VMware Cloud Director Management console
{: #shared_accessing-vcd-console-procedure}

1. From the **Properties** pane on the site details page, click **Set Site Admin Password** to generate a random password.
2. On the upper right of the site details page, click **VMware Cloud Director console** to access the console.
3. Use the **admin** username and password to log in to the VMware Cloud Director console.

   After the **admin** is logged in to the VMware Cloud Director console, you can create extra users who have roles that allow them to access the VMware Cloud Director console.

   All virtual data centers in the same region have the same **admin** password. Resetting the password on a virtual data center resets the **admin** password for accessing the VMware Cloud Director Management console for all virtual data centers in the same region.
   {: important}

## Related links
{: #shared_accessing-vcd-console-related}

* [Resizing virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_resize)
* [Operating {{site.data.keyword.vm-shared}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [Deleting {{site.data.keyword.vm-shared}} virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_deletinginstance)
* [Viewing the virtual data center summary](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary)
* [Viewing virtual data center details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-details)
* [VMware Cloud Director](https://www.vmware.com/products/cloud-infrastructure/cloud-director){: external}
