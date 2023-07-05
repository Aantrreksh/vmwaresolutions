---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-16"

keywords: view vCenter Server, view instance, view instance details, vmware multizone, vcenter server multizone, view vCenter Server multizone, view multizone, view multizone instance details

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Viewing vCenter Server instances
{: #vc_viewinginstances}

View the summary and detailed information of the VMware vCenter Server® instances that are provisioned for different user accounts.

## Procedure to view summary for vCenter Server instances
{: #vc_viewinginstances-procedure-view-inst-summary}

To view a summary of all the vCenter Server instances that are provisioned for a user account, complete the following steps:

1. In the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources > vCenter Server** from the left navigation pane.
2. From the console banner, click the **Avatar** icon ![Avatar icon](../../icons/i-avatar-icon.svg "Avatar"), and then click the **Account** field. Select the user account that you want to check instances for.
3. In the **vCenter Server** table, view the list of instances that are provisioned in the selected user account.

| Item | Description |
|:---- |:----------- |
| Name | The name of the instance. |
| Type | The type of vCenter Server instance. Instance type is **Single-zone** or **VMware Security and Compliance Readiness Bundle**. |
| Version | The release version that the instance was deployed in, or upgraded to. |
| Location | The {{site.data.keyword.cloud_notm}} data center where the instance is hosted. |
| Creation time | The date and time when the instance was created. |
| Status | The status of the instance. |
{: caption="Table 1. vCenter Server instance items" caption-side="bottom"}

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
{: caption="Table 2. vCenter Server instances status descriptions" caption-side="bottom"}

## Procedure to view the property details for vCenter Server instances
{: #vc_viewinginstances-procedure-view-inst-property}

To view the property details of an instance, complete the following steps.

1. In the **vCenter Server** table, click an instance name.
2. Under **Properties**, view the details for the instance.

| Property | Description |
|:-------- |:----------- |
| Name | The name of the instance. |
| ID | The ID of the instance. |
| Multizone region[^multizone] | The {{site.data.keyword.cloud_notm}} data center region where the instance is hosted. |
| Location | The {{site.data.keyword.cloud_notm}} data center where the instance is hosted. \n \n **Note:** For multizone instances, locations are listed for each cluster type. Types include witness, consolidated, workload, and edge services. |
| Current version | The current version of {{site.data.keyword.vmwaresolutions_short}}. |
| vCenter version | The vCenter Server version. \n \n **Note:** The vCenter Server versions that are displayed on the {{site.data.keyword.vmwaresolutions_short}} console and the VMware vSphere® Web Client are slightly different. Both are correct. |
| VMware NSX® networking solution[^NSX] | Either NSX-T or NSX-V. |
| VMware vSphere version[^vsphere] | The version of VMware vSphere. |
| NSX for vSphere | The VMware NSX for vSphere product version. |
| _VMware component_ license | If you selected to use your own VMware® license for any of the VMware components on the **Licensing** page when you ordered the instance, the VMware component name and the license key that you entered for the component are displayed. \n \n Examples of VMware component licenses can include **NSX license**, **vCenter Server license**, and **vSAN license**. |
| NSX license edition | The version and edition of the VMware NSX license. |
| Root domain | The root domain name is the DNS domain name and the Microsoft® Active Directory™ (AD) forest root name. |
| SSO domain | The SSO domain is the vSphere single sign-on domain. The SSO domain name is fixed for all deployed vCenter Server instances with a value of **`vsphere.local`**. |
| Subdomain[^subdomain] | The subdomain is the DNS subdomain name of the root domain name where the local vCenter Server instance hostnames are located. The subdomain name is in the format `vcenter_server_instance_name.root.domain_name`. |
{: caption="Table 3. vCenter Server instance properties" caption-side="bottom"}

[^multizone]: Multizone instances only.

[^NSX]: Single-zone instances only.

[^vsphere]: Single-zone instances only.

[^subdomain]: The subdomain label is not used for VMware vSphere 7 instances.

## Procedure to view access information for vCenter Server instances
{: #vc_viewinginstances-procedure-view-access-info}

Under **Access information**, view the access information for the instance-related components. The passwords that are displayed are initial passwords that are generated by the system. If you change them outside of the {{site.data.keyword.vmwaresolutions_short}} console, they are not updated on the instance summary page.

| Component | Description |
|:--------- |:----------- |
| AD/DNS IP or IPs[^ips] | The IP address or addresses of the AD server or servers. |
| AD/DNS FQDN[^fqdn] | The AD/DNS server fully qualified domain names (FQDN). \n \n **Note:** The same administrator password can be used to connect to all the AD/DNS servers by using a remote desktop connection. |
| AD/DNS Remote Desktop[^nsxv] | For primary instances, it displays the username and password to access the AD server through a remote desktop connection. \n \n For secondary instances, click the **View on primary instance** link to be directed to the username and password information on the primary instance. \n \n **Note:** After the secondary instance is added to the primary DNS domain and replication occurs, the local administrator password on the primary instance might overwrite the local administrator password on the secondary instance. By clicking the **View on primary instance** link, you receive access to the correct administrator password. |
| vCenter/PSC IP | The IP address of the vCenter Server. |
| vCenter/PSC FQDN | The vCenter Server fully qualified domain name (FQDN). |
| vCenter/PSC ADMIN | The VMware vCenter SSO username and password that you can use to log in to the vCenter Server by using the vSphere Web Client. |
| vCenter/PSC SSH | The username and password that you can use to access the vCenter Server VM through SSH connection. |
| NSX Manager IP | The IP address of the NSX Manager. |
| NSX Manager FQDN | The NSX Manager fully qualified domain name (FQDN). |
| NSX Manager HTTP | The username and password that is used to access the NSX Manager web console. |
| NSX Controllers IPs[^nsxt3] | The IP address or addresses for the NSX node VM. |
| NSX Controllers SSH[^nsxt4] | The username and password that you can use to access the NSX node VM through KVM or SSH connection. |
| Customer Edge VM IPs[^nsxt1] | The IP address or addresses for the Customer Edge VM. |
| Customer Edge VM SSH[^nsxt2] | The username and password that you can use to access the Customer Edge VM through KVM or SSH connection. |
| NSX Service Edge VM IPs[^nsxt5] | The IP address or addresses for the Service Edge VM. |
| NSX Service Edge VM SSH[^nsxt6] | The username and password that you can use to access the Service Edge VM through KVM or SSH connection. |
{: caption="Table 4. vCenter Server access information for instance-related components" caption-side="bottom"}

[^nsxt1]: Single-zone instance, NSX-T only.

[^nsxt2]: Single-zone instance, NSX-T only.

[^nsxt3]: NSX-T only.

[^nsxt4]: NSX-T only.

[^nsxt5]: NSX-T only.

[^nsxt6]: NSX-T only.

[^ips]: For NSX-T, two IP addresses for the two AD servers. For NSX-V, one IP address for one server.

[^fqdn]: For NSX-T, two FQDNs for the two AD servers. For NSX-V, one FQDN for one server.

[^nsxv]: NSX-V only.

## Procedure to view deployment history for vCenter Server instances
{: #vc_viewinginstances-procedure-view-deploy-history}

Click the **Deployment history** tab to view the deployment history for the instance.

| Item        | Description       |  
|:------------- |:------------- |
| Date | The date and time when the instance status is changed. |
| Summary | The details of the change. |
{: caption="Table 5. vCenter Server instance deployment history" caption-side="bottom"}

### What to do if errors occur
{: #vc_viewinginstances-if-errors-occur}

If you see errors in the deployment history, the {{site.data.keyword.cloud_notm}} Support team is automatically notified. To inquire about the status of your ticket, follow the steps in [Contacting IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

## What to do next
{: #vc_viewinginstances-next}

Manage your instances from the {{site.data.keyword.vmwaresolutions_short}} console or the VMware vSphere Web Client.

Before you click **vCenter console** on the instance summary page to go to the vSphere Web Client and start managing your VMware ESXi™ servers, you must log in to the VPN portal of the {{site.data.keyword.cloud_notm}} data center. Hover over **vCenter console** and follow the instructions to ensure that you meet all requirements and you completed the necessary steps before you access the vSphere Web Client.
{: important}

Review the following topics for information to help you complete the login instructions:
*  For the requirements and necessary steps before you access the vSphere Web Client, see [Timeout reached while connecting to the vSphere Web Client](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_timeout_vc_console).
*  For a list of access points to log in to the {{site.data.keyword.cloud_notm}} infrastructure Private Network by using VPN, see [VPN access](https://www.ibm.com/cloud/vpn-access){: external}.
*  If you have problems when you deploy an OVF (Open Virtualization Format) file by using the vSphere Web Client, see [Deploying an OVF file using the vSphere Web Client](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_deploy_ovf).

## Related links
{: #vc_viewinginstances-related}

* [Ordering vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Adding clusters for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingclusters)
* [Adding ESXi servers to vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservers)
* [Deleting vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletinginstance)
