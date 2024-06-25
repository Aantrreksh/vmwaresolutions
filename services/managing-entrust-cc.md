---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-09"

keywords: Entrust CloudControl WebGUI, Entrust CloudControl console, enable internet Entrust CloudControl

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing Entrust CloudControl
{: #managing-entrust-cc}

New installations of Entrust CloudControl™ (formerly HyTrust CloudControl) are not supported for new or existing deployments of {{site.data.keyword.vcf-auto}} instances. You can still use or delete existing Entrust CloudControl installations on your existing instances.
{: deprecated}

To manage Entrust CloudControl, access the Entrust CloudControl WebGUI from the {{site.data.keyword.vmwaresolutions_full}} console, or access the Entrust CloudControl console from the VMware vSphere® Web Client.

## Accessing the Entrust CloudControl WebGUI from the VMware Solutions console
{: #managing-entrust-cc-accessing-webgui}

To log in to the WebGUI of the primary or secondary Entrust CloudControl appliance, use the WebGUI credentials that are found on the Entrust CloudControl service details page.

## Accessing the Entrust CloudControl console from the vSphere Web Client
{: #managing-entrust-cc-accessing-console}

To access the Entrust CloudControl console from the vSphere Web Client, use the following procedure:
1. In the vSphere Web Client, find the virtual machines (VMs) that are named **CC1** and **CC2**.
2. Right-click **CC1** or **CC2**, and then click **Open Console**.
3. Log in to the console by using the console credentials that you can find on the Entrust CloudControl service details page.

For more information, see [Ordering services for {{site.data.keyword.vcf-auto-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Considerations when you add and remove hosts and clusters
{: #managing-entrust-cc-consider-addremove-hostsclusters}

When you add and remove hosts and clusters to your instance, VMware Solutions does not manage the Entrust CloudControl inventory and credentials for you. {{site.data.keyword.cloud_notm}} assumes that you take steps to lock {{site.data.keyword.cloud_notm}} automation from having access to your Entrust CloudControl deployment.

## Procedure to find the firewall and SNAT rules defined (NSX-T only)
{: #managing-entrust-cc-proc-find-firewall-nsxt}

1. Log in to the NSX-T Manager, and click **Networking** in the menu.
2. Click **NAT** from the left navigation pane.
3. Select the T0 consolidated gateway from the **Gateway** list.

   The EntrustCC SNAT rules are displayed in the NAT rules table.

## Known issue about Network Time (Entrust CloudControl 5.x only)
{: #managing-entrust-cc-known-issue-ntp}

On the Entrust CloudControl 5.x web console, if you go to **General > Health**, the **Network Time (NTP)** value in the **Services** section might be shown as disabled. Although the value shows disabled on the console, NTP is working as expected.

## Enabling internet access for the Entrust CloudControl VMs (Entrust CloudControl 5.x only)
{: #managing-entrust-cc-internet-access}

{{site.data.keyword.vmwaresolutions_short}} provides automatic renewal support for Entrust licenses with the Call Home feature enabled. For {{site.data.keyword.vcf-auto-short}} instances that are not private-only, Entrust CloudControl is deployed with firewall and SNAT (Source Network Address Translation) rules that are defined on the management services ESG **mgmt-nsx-edge**.

These rules enable internet access for the Entrust VMs. If internet access is not enabled, the license that is applied to your Entrust CloudControl installation will expire after a year.

For private-only vCenter Server environments, the VMware NSX® Edge Services Gateway (ESG) **mgmt-nsx-edge** is not added. Therefore, the firewall and SNAT rules are not defined. As a result, internet connectivity cannot be enabled for private-only instances and Entrust licenses expire annually.
{: note}

### Procedure to find the firewall and SNAT rules defined (Entrust CloudControl 5.x and NSX-V only)
{: #managing-entrust-cc-proc-find-firewall}

1. Log in to the VMware® vSphere Web Client (FLEX) and find the ESG **mgmt-nsx-edge**.
2. Click **Home > Networking & Security > NSX Edges**.
3. Double-click the ESG **mgmt-nsx-edge** and click the **Manage** tab.
4. Go to the **Firewall** tab and find the Entrust rules. Note the source IP addresses, which are the IP addresses for the Entrust VMs.
5. Go to the **NAT** tab and find the SNAT rules that are created for the Entrust VMs. The source IP addresses match the IP addresses that you noted in the previous step.

### Procedure to enable internet connectivity for Entrust CloudControl (Entrust CloudControl 5.x only)
{: #managing-entrust-cc-enable-internet}

The following steps apply for updating the Entrust CloudControl network settings on the primary VM, which is used for the license upgrades. You don't need to update the settings for the secondary VM.
{: note}

1. Complete steps 1-3 in the previous procedure.
2. Click **Settings** and then click **Interfaces**. Note the IP address for the private uplink, which becomes the new default gateway.
3. Go to the Entrust CloudControl service details page, click **View Entrust CloudControl Web UI** and log in with the credentials from the service details page.
4. Note the existing default gateway. Click **Configuration > Network**. Note the gateway IP address that is listed, which becomes the gateway for the static route.
5. Add a static route. Click **Configuration > Static Routes**. Click **Add**, enter the following information, and click **OK**.

   ```text
   Network Address: 10.0.0.0
   Mask: 255.0.0.0
   Gateway: IP noted in step 4
   Device: Network 1
   ```

6. Change the default gateway. Click **Configuration > Network** and replace the IP address in the **Gateway** field with the one you noted in Step 3 and click **Save**. 

   Ensure that you set the static route before you change the default gateway, otherwise the web console might become unreachable.
   {: important}

   The primary VM has access to the Internet now.

7. To confirm that the primary VM has internet access, run a `wget` command to a public IP address or website. To do so, go back to vCenter Server and right-click **CC1 > Open Console**. Log in to the console by using the console credentials from the Entrust CloudControl service details page. Run a `wget` command such as `wget www.ibm.com` to receive an immediate response. Confirm that the request was sent and a `200` response was received.

## Considerations when you delete Entrust CloudControl
{: #managing-entrust-cc_considerations-remove}

Review the following considerations before you delete the service:
* Before you delete Entrust CloudControl, disable **Root Password Vaulting** if configured, and delete all protected hosts from Entrust CloudControl.
* As part of the Entrust CloudControl service configuration, global PIP was enabled. Sample users and groups were preconfigured in Active Directory (AD) and are displayed on the service details page. If you delete Entrust CloudControl, the sample users are deleted from AD too. A sample trust manifest is set up that gives single sign-on (SSO) permissions to the sample users that are created. You can customize this setting for your own requirements.
* If you installed Entrust CloudControl before VMware Solutions v4.0 and you delete the service, you must manually remove the DNS entries. For more information, see [Manually removing the DNS entries](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices#vc_deletingservices-DNS-entries).
