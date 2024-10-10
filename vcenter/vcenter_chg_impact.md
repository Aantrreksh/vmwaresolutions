---

copyright:

  years:  2016, 2024

lastupdated: "2024-10-10"

keywords: change vCenter Server artifacts, automation ID, VMware resource

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Considerations about changing vCenter Server artifacts
{: #vcenter_chg_impact}

Changing users, resources, or subnets that are reserved for {{site.data.keyword.vmwaresolutions_full}} can impact management operations.

Do not edit the global permissions of the **ic4v-vCenter** group in the **Users and Groups** page on the VMware vSphere® Web Client. Such changes include changing the username, deleting the user, or changing its password.
Use the **root** host user ID. The **ic4vroot** host user ID is created for IBM use only.
{: important}

## automation ID
{: #vcenter_chg_impact-automation-id}
{: faq}

The **automation** ID is a user account that is used by the automated operations that are provided in the VMware Solutions console.

Users and passwords for the automated operations in the console must not be changed because the console operations that depend on those credentials might fail.

## Service-specific user accounts
{: #vcenter_chg_impact-service-usr-account}
{: faq}

Each service creates an internal user account in VMware vCenter Server®. This account is necessary so that management operations that are associated to a service can connect to vCenter Server to perform the operations on the service.

To prevent outages and connection problems, if you change the user ID, password, or password expiration settings for this user account, ensure that you also update the information in the associated service.
{: important}

The user ID for this account is in the format `service_name-truncated_service_uuid@test.local` or `service_name-truncated_service_uuid@example-domain.local`. For example, the user ID that the Veeam® service uses to connect to vCenter Server to perform scheduled backups is `Veeam-Veeam_uuid@test.local`.

The `service_name` value together with the `service_uuid` value are truncated to 20 characters.
{: note}

## VMware resources for instances V1.9 and later
{: #vcenter_chg_impact-vmware-resources-for-inst-v1.9-and-later}
{: faq}

If the status of the {{site.data.keyword.vcf-auto}} instance is **Available**, you can modify the VMware virtual data center, cluster, switches, port groups, and customer Network File System (NFS) datastore names from the VMware vSphere Web Client.

Review the following restrictions:
* Do not change the Automated instance name and the vCenter Server virtual machine name.
* Do not change the name of the management datastore from its default value. The default value is **vsanDatastore** for VMware vSAN™ instances and **management-share** for NFS instances.
* Do not change the names and do not delete any of the management subnets that are created for the Automated instances.
* Do not change the name of the network uplinks that are created during provisioning.
* Do not rename or remove NSX-T components. These operations might generate add and remove failures or delays. The NSX-T components with the names that are documented in [Naming conventions](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design#nsx-t-design-naming) are used when automation adds or removes hosts, clusters, and services.
* Do not change the VMware ESXi™ server names and the IP addresses because they are registered for Windows® DNS resolution. Changes might result in failure during deployment or failure of Automated instance functions.

## VMware resources for instances V1.8 and earlier
{: #vcenter_chg_impact-vmware-resources-for-inst-v1.8-and-earlier}
{: faq}

The following table lists the operations that might be impacted if the SSO administrator changes resources outside of the {{site.data.keyword.vmwaresolutions_short}} console. If a solution to recover is available, it is provided as well.

The following table is applicable to instances deployed in V1.8 and earlier, including the ones that were initially deployed in V1.8 and earlier and then upgraded to V1.9 or later.

| Attempted change | Impacted operations | Severity | Recovery method |
|:---------------- |:------------------- |:-------- |:--------------- |
| Change the VMware virtual data center name. | Adding a VMware virtual data center might fail because the new ESXi server cannot join the changed virtual data center. | Important | Change the VMware virtual data center name back to the original name. |
| Change any port group names. | Adding an ESXi server might fail. | Important | Change the port group name back to the original name. |
| Change the cluster name. | Adding an ESXi server might fail. | Important | Change the cluster name back to the original name.
| Change the public or private Distributed Virtual Switch (DVS) name. | Adding an ESXi server might fail. | Important | Change the public or private Distributed Virtual Switch (DVS) name to the original name.
| Change the vSAN datastore name in the instance that uses vSAN. | Adding an ESXi server might fail. \n \n Upgrading the instance might fail. | Important | Change the vSAN datastore name back to the original name, **vsanDatastore**.
| Change the management NFS datastore name in the instance that uses NFS. | Adding an ESXi server might fail. \n \n Upgrading the instance might fail. | Important | Change the NFS management datastore name back to the original name, **management-share**, and remount the NFS datastore as read-only on the ESXi server. |
{: caption="Operations that are impacted by changing VMware resources" caption-side="bottom"}

The following table lists the operations that might be impacted if SSH or shell access is disabled for various resources.

| Attempted change | Impacted operations  | Severity  | Recovery method |
|:---------------- |:-------------------- |:--------- |:--------------- |
| Disable SSH or shell access for vCenter Server or PSC | Pairing a primary and secondary instance might fail. | Important | |
{: caption="Operations that are impacted by SSH and shell access (local)" caption-side="bottom"}

If you choose to disable SSH or shell access, re-enable it temporarily before you complete the indicated operations.

## Management subnets for Automated instances
{: #vcenter_chg_impact-mgmt-subnets}
{: faq}

The following information discusses the subnets that are ordered by VMware Solutions and it provides options for you to order extra subnets for your own use.

With each {{site.data.keyword.cloud_notm}} bare metal server order, the following ranges of IP addresses are ordered by default:
*  A primary public range of 32 IP addresses
*  A primary private range of 64 IP addresses

In addition, the following management subnets are also reserved for {{site.data.keyword.vmwaresolutions_short}}:
*  Two portable private subnets of 64 IP addresses on the first VLAN - one for management and the other one for VTEPS
*  Two portable private subnets of 64 IP addresses on the second VLAN - one for VMotion and one for vSAN
*  A public portable subnet of 16 IP addresses on the public VLAN

   Do not use these components for other purposes, do not change their names, and do not delete them, or the stability of your environment is severely compromised.
   {: important}

If you need more subnets to use, you can obtain IP addresses to use in one of the following ways.
*  **Option 1 (recommended)** - Use VMware NSX® virtual network overlays. A sample VXLAN template is provided upon order. This VXLAN can be used as a starting point for building software-defined networking (SDN). For more information, see [Configuring your network to use the customer-managed NSX Edge](/docs/vmwaresolutions?topic=vmwaresolutions-vc_esg_config).
*  **Option 2** - Order your own portable public or private subnets to obtain IP addresses. To distinguish the subnets that you order from the management subnets, you can add notes to all the subnets that you are ordering.

## Related links
{: #vcenter_chg_impact-related}

* [Can I change the ESXi server names and IP addresses?](/docs/vmwaresolutions?topic=vmwaresolutions-faq_esxi#faq_esxi-change-name-ip)
* [Can I disable root access on my ESXi servers?](/docs/vmwaresolutions?topic=vmwaresolutions-faq_esxi#faq_esxi-disable-root)
