---

copyright:

  years:  2016, 2023

lastupdated: "2023-08-17"

keywords: troubleshooting, vSphere timeout, timeout console

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Why did I time out while I was connecting to the VMware vSphere Web Client?
{: #trbl_timeout_vc_console}
{: troubleshoot}
{: support}

When you try to connect to the VMware vSphere® Web Client, you might get the following timeout error:
{: tsSymptoms}

> The server at <IP_address> is taking too long to respond.

Use the following steps to investigate and fix the problem.
{: tsResolve}

1. Ensure that you completed the steps from the tooltip that gets displayed when you hover over the **vCenter console**. For
   your convenience, these steps are also listed as follows:
   1. [Create a VPN password](/docs/iaas-vpn?topic=iaas-vpn-getting-started#set-vpn-password).
   2. [Log in to the data center VPN](/docs/iaas-vpn?topic=iaas-vpn-getting-started#login-to-the-vpn) by using the {{site.data.keyword.cloud}} infrastructure VPN credentials.
   3. Add the IP address and the hostname mapping of the VMware vCenter Server® into the `hosts` file on your local computer. Use the following format:

      ```javascript
      IP_Address              Host_Name
      ```

2. Take note of the IP address that is displayed because you need it in one of the next steps.
3. Ensure that you have access to the {{site.data.keyword.cloud_notm}} infrastructure VPN. Complete the following steps on the {{site.data.keyword.slportal}}:
   1. Click **Account > VPN Access**.
   2. Click the **SSL link** in the **VPN Access** column.
   3. On the **VPN Access for username** page, set the **Subnet Access** option to **Manual**.
   4. On the same page, locate the subnet for the IP address/host name pair. For more information, see **Step 2**.    

      For example, if the IP address for your instance is `xx.yyy.zz.15` and the IP address for vCenter is `xx.yyy.zz.10`, you must grant access for the subnet `xx.yyy.zz.0/26`.

   5. Select the **Grant Access** checkbox for that subnet and click **Save**.
