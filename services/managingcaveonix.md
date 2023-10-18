---

copyright:

  years:  2016, 2023

lastupdated: "2023-09-26"

keywords: Caveonix console, Caveonix RiskForesight license, login Caveonix console

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing Caveonix RiskForesight
{: #managingcaveonix}

## Accessing the Caveonix RiskForesight console
{: #managingcaveonix-access-console}

To manage the Caveonix RiskForesight™ service, you must access the Caveonix RiskForesight console by completing the following steps:

1. Use the {{site.data.keyword.cloud}} infrastructure VPN or a jump server to allow access to the IP address of the Caveonix RiskForesight virtual machine (VM). You can find the IP address on the service details page for Caveonix RiskForesight in the {{site.data.keyword.vmwaresolutions_short}} console. Complete the following steps:
   1. Create a VPN password from the {{site.data.keyword.cloud_notm}} infrastructure customer portal.
   2. Log in to the data center VPN portal by using the {{site.data.keyword.cloud_notm}} infrastructure VPN credentials.
   3. Add the IP address and the hostname mapping into the `hosts` file from your local computer. Use the following format:

      ```javascript
      RiskForesight_VM_IP_Address      RiskForesight_FQDN
      ```
2. To access the Caveonix RiskForesight console, click **View RiskForesight console** on the service details page for Caveonix RiskForesight. Then, log in by using the credentials that are listed on the same service details page.

## Applying updates to Caveonix RiskForesight
{: #managingcaveonix-update}

You are responsible for maintaining Caveonix RiskForesight to keep it updated to the most recent version. You can download the required updates from the [Caveonix service provider portal](https://support.caveonix.com/login){: external}.

To obtain a login ID for the Caveonix service provider portal for product release notes and downloads, open a support case with the [{{site.data.keyword.cloud_notm}} Support Center](https://cloud.ibm.com/unifiedsupport/supportcenter){: external}.

Provide the instance name that Caveonix is installed on, your company name, and an email address for your administrator for the support case. {{site.data.keyword.cloud_notm}} Support acquires the credentials for your login and email your administrator.

## Considerations when you delete Caveonix RiskForesight
{: #caveonix_considerations-remove}

Review the following considerations before you delete the service:

* Deleting Caveonix RiskForesight automatically deletes the initial Caveonix RiskForesight license that was originally associated with the service. However, you need to manually delete any other unwanted licenses from the **Caveonix RiskForesight licenses** table on the **Licenses** page in the {{site.data.keyword.vmwaresolutions_full}} console.
* When you delete the service, the {{site.data.keyword.vmwaresolutions_short}} automation deletes only the single all-in-one Caveonix virtual machine (VM) that was deployed and the dedicated private subnet that was ordered for it. Therefore,
   * If you scaled out the Caveonix VM into multiple VMs, those additional VMs are not deleted.
   * If you used the IP addresses of the dedicated private subnet on more VMs, those VMs must be assigned new IP addresses to continue to function.
   * If you delete the **vCenter Server instance A** with Caveonix RiskForesight installed, and you used the IP addresses of the dedicated private subnet that was ordered for the service in the **vCenter Server instance B**, the dedicated private subnet is canceled upon deletion of the **vCenter Server instance A**.
* If you installed the Caveonix RiskForesight service before VMware Solutions v4.0, and you then delete that service, you must manually remove the DNS entries. For more information, see [Manually removing the DNS entries](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices#vc_deletingservices-DNS-entries).

## Related links
{: #managingcaveonix-related}

* [Caveonix RiskForesight overview](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
* [Ordering Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_ordering)
