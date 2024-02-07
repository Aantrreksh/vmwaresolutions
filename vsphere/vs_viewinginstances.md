---

copyright:

  years:  2023, 2024

lastupdated: "2024-01-26"

keywords: view vmware vSphere, view instance, view instance details, instance view vmware vSphere

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Viewing VMware vSphere instances
{: #vs_viewinginstances}

View the summary and detailed information of the VMware vSphere® instances that are provisioned for different user accounts.

## Procedure to view summary for VMware vSphere instances
{: #vs_viewinginstances-procedure-view-inst-summary}

To view a summary of all the VMware vSphere instances that are provisioned for a user account, complete the following steps:

1. In the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > VMware vSphere** from the left navigation pane.
2. From the console banner, click the **Avatar** icon ![Avatar icon](../../icons/i-avatar-icon.svg "Avatar"), and then click the **Account** field. Select the user account that you want to check instances for.
3. In the **VMware vSphere** table, view the list of instances that are provisioned in the selected user account.

| Item | Description |
|:---- |:----------- |
| Name | The name of the instance. |
| Location | The {{site.data.keyword.cloud_notm}} data center where the instance is hosted. |
| Creation time | The date and time when the instance was created. |
| Status | The status of the instance. |
{: caption="Table 1. VMware vSphere summary" caption-side="bottom"}

The instance can have different statuses.

| Status | Description |
|:------ |:----------- |
| Creating | The instance is being created. |
| Building | The instance is being configured. |
| Available | The instance is ready to use. |
| Modifying | The instance is being modified. |
| Failed | The creation, configuration, or modification process failed. |
| Deleting | The instance is being deleted. |
| Deletion error | An error occurred when the instance was being deleted. |
| Deleted | The instance is deleted. |
{: caption="Table 2. VMware vSphere statuses" caption-side="bottom"}

## Procedure to view details for VMware vSphere instances
{: #vs_viewinginstances-procedure-view-inst-property}

To view the property details of an instance, complete the following steps.

1. In the **VMware vSphere** table, click an instance name.
2. On the **Summary** tab, view the details for the instance.

   | Property | Description |
   |:-------- |:----------- |
   | Name | The name of the instance. |
   | ID | The ID of the instance. |
   | Location | The {{site.data.keyword.cloud_notm}} data center where the instance is hosted. |
   | VMware vSphere version | The vSphere version. \n \n **Note:** The vSphere versions that are displayed on the {{site.data.keyword.vmwaresolutions_short}} console and the VMware vSphere® Web Client are slightly different. Both are correct. |
   | Root domain | The root domain name is the DNS domain name and the Microsoft® Active Directory™ (AD) forest root name. |
   | Subdomain[^subdomain] | The subdomain is the DNS subdomain name of the root domain name where the local vSphere instance hostnames are located. The subdomain name is in the format `vsphere_instance_name.root.domain_name`. |
   {: caption="Table 3. VMware vSphere instance properties" caption-side="bottom"}

   [^subdomain]: Existing vSphere 6 instances only

3. Click the **Infrastructure** tab to view the ESXi server and the network interface details.

   | Item | Description |
   |:---- |:----------- |
   | Name | The name of the ESXi server is in the following format: `<host_prefix><n>.<root_domain>`, where `n` is the sequence of the ESXi server. |
   | Hardware | The hardware specification. |
   | Credentials | The user name and password to access the ESXi server. |
   | Private IP | The private IP address of the ESXi server. |
   | Status | The status of the ESXi server, which can be one of the following values: \n **Available** The ESXi server is ready to use. \n **Adding** The ESXi server is being added. \n **Deleting** The ESXi server is being deleted. |
   {: caption="Table 4. ESXi server details" caption-side="bottom"}
   {: class="simple-tab-table"}
   {: #table1}
   {: tab-title="ESXi server details"}
   {: tab-group="Infrastructure details"}

   | Item | Description |
   |:---- |:----------- |
   | VLAN number | The unique VLAN number.  |
   | Description | The description of the VLAN.  |
   | Location | The data center location. |
   | Primary route | The primary route of the VLAN. |
   {: caption="Table 4. Network interface - VLAN details" caption-side="bottom"}
   {: class="simple-tab-table"}
   {: #table2}
   {: tab-title="Network interface details"}
   {: tab-group="Infrastructure details"}

4. Click **View resource** to access the VLAN details, including the subnet and IP address details.

   | Item | Description |
   |:---- |:----------- |
   | Name | The subnet name. Click the name to access the subnet details. |
   | Type | The type of subnet: primary or portable. |
   | Description | The description of the subnet. |
   {: caption="Table 5. Network interface - Subnet details" caption-side="bottom"}
   {: class="simple-tab-table"}
   {: #vlan-table1}
   {: tab-title="Subnet details"}
   {: tab-group="Network interface VLAN details"}

   | Item | Description |
   |:---- |:----------- |
   | IP | The IP address. |
   | Status | The status of the IP address. |
   | Description |The description of the IP address.  |
   {: caption="Table 5. Network interface - IP details" caption-side="bottom"}
   {: class="simple-tab-table"}
   {: #vlan-table2}
   {: tab-title="IP details"}
   {: tab-group="Network interface VLAN details"}

5. Click the **Licensing** tab to view details about the existing licenses. You can also add licenses if any are available that you haven’t purchased yet.

6. Click the **Deployment history** tab to view the deployment history for the instance.

   If you see errors in the deployment history, the {{site.data.keyword.cloud_notm}} Support team is automatically notified. To inquire about the status of your ticket, follow the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

## What to do next
{: #vs_viewinginstances-next}

Manage your instances from the VMware Solutions console or the VMware vSphere Web Client.

Review the following topics for information to help you complete the login instructions:
* For the requirements and necessary steps before you access the vSphere Web Client, see [Timeout reached while connecting to the vSphere Web Client](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_timeout_vc_console).
* For a list of access points to log in to the {{site.data.keyword.cloud_notm}} infrastructure Private Network by using VPN, see [Getting started with {{site.data.keyword.cloud_notm}} Virtual Private Networking](/docs/iaas-vpn?topic=iaas-vpn-getting-started).
* If you have problems when you deploy an OVF (Open Virtualization Format) file by using the vSphere Web Client, see [Deploying an OVF file using the vSphere Web Client](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_deploy_ovf).

## Related links
{: #vs_viewinginstances-related}

* [Procedure to order VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-procedure)
* [Adding ESXi servers to VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_addingservers)
* [Deleting VMware vSphere instances](/docs/vmwaresolutions?topic=vmwaresolutions-vs_deletinginstance)
