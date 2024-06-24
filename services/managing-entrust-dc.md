---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-12"

keywords: Entrust DataControl WebGUI, Entrust DataControl console, enable internet Entrust DataControl

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing Entrust DataControl
{: #managing-entrust-dc}

New installations of Entrust DataControl® (formerly known as HyTrust DataControl) are not supported for new or existing deployments of {{site.data.keyword.vcf-auto}} instances. You can still use or delete existing Entrust DataControl installations on your existing instances.
{: deprecated}

To manage Entrust DataControl, access the Entrust DataControl WebGUI from the {{site.data.keyword.vmwaresolutions_full}} console, or access the Entrust DataControl console from the vSphere® Web Client.

## Accessing the Entrust DataControl WebGUI from the VMware Solutions console
{: #managing-entrust-dc-accessing-webgui}

To log in to the WebGUI of the primary or secondary Entrust DataControl appliance, use the WebGUI credentials that are found on the Entrust DataControl service details page.

## Accessing the Entrust DataControl console from the vSphere Web Client
{: #managing-entrust-dc-accessing-console}

To access the Entrust DataControl console from the vSphere Web Client, use the following procedure:
1. In the vSphere Web Client, find the virtual machines that are named **KC1** and **KC2**.
2. Right-click **KC1** or **KC2**, and then click **Open Console**.
3. Log in to the console by using the console credentials that you can find on the Entrust DataControl service details page.

For more information, see [Ordering services for {{site.data.keyword.vcf-auto-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Enabling internet access for the Entrust DataControl virtual machines
{: #managing-entrust-dc-internet-access}

For Entrust DataControl v4.3.2 and later, {{site.data.keyword.vmwaresolutions_short}} provides automatic renewal support for Entrust licenses with the Call Home feature enabled. For {{site.data.keyword.vcf-auto-short}} instances that are not private-only, Entrust DataControl is deployed with firewall and SNAT (Source Network Address Translation) rules that are defined on the management services ESG **mgmt-nsx-edge**.

These rules enable internet access for the Entrust virtual machines (VMs). If internet access is not enabled, the license that is applied to your Entrust DataControl installation will expire after a year.

For private-only vCenter Server environments, the VMware® NSX Edge Services Gateway (ESG) **mgmt-nsx-edge** is not added. Therefore, the firewall and SNAT rules are not defined. As a result, internet connectivity cannot be enabled for private-only instances and Entrust licenses expire annually.
{: note}

### Procedure to find the firewall and SNAT rules defined
{: #managing-entrust-dc-proc-find-firewall}

1. Log in to the VMware vSphere® Web Client (FLEX) and find the ESG **mgmt-nsx-edge**.
2. Click **Home > Networking & Security > NSX Edges**.
3. Double-click the ESG **mgmt-nsx-edge** and click the **Manage** tab.
4. Go to the **Firewall** tab and find the Entrust rules. Note the source IP addresses, which are the IP addresses for the Entrust VMs.
5. Go to the **NAT** tab and find the SNAT rules that are created for the Entrust VMs. The source IP addresses match the IP addresses that you noted in the previous step.

### Procedure to enable internet connectivity for Entrust DataControl
{: #managing-entrust-dc-proc-enable-internet}

1. Complete steps 1 - 3 in the previous procedure.
2. Click **Settings** and then **Interfaces**. Note the IP address for the private uplink. This address becomes the new default gateway.
3. Click **Home > Hosts and Clusters** and find the Entrust VMs. Right-click one of the VMs and click **Open Console**.
4. Log in to the console by using the console credentials that you can find on the Entrust DataControl service details page on the {{site.data.keyword.vmwaresolutions_short}} console.
5. To get the current default gateway IP address from the VM, click **Manage Network Settings > Show Current Network Configuration**. Note the IP address that is listed for **Gateway**. This address becomes the gateway that is used for the static route.
6. To set a static route for the VM, click **Manage Network Settings > Manage Static Routes > Add Static Route**. Set **Network address** to `10.0.0.0/8` and **Gateway** to the IP address noted in the previous step.
7. To set the default gateway IP for the VM, click **Manage Network Settings > Change Current Network Configuration**. If you get a warning message, click **OK**, then click **Custom Configuration**. Set the **Gateway** field to the private uplink IP address noted in step 2 and click **OK**. Wait until the new network configuration is installed and the network services are restarted.
8. If you see a message that requests Entrust SecureOS reauthentication, click **OK** and enter the IP address of the other Entrust VM for this installation. If you are asked for a 16-character passphrase, press Enter to return to the main menu. Verify the current network configuration to ensure that your changes are applied.
9. To confirm that the VM has access to the internet, ping a public IP address or website. Click **Manage Network Settings > Network Diagnostic Tools > Test Inbound Ports of Another Server**. Type a public website address. For example, `www.ibm.com`, click **OK**, type `80 443` for the ports (or any other ports you want to test). You must get an immediate response that shows the inbound ports with a message similar to `80 (OK) 443 (OK)`.
10. Repeat steps 3 - 9 for the other Entrust VM.

## Considerations when you delete Entrust DataControl
{: #managing-entrust-dc_considerations-remove}

Review the following considerations before you delete the service:
* Before you delete Entrust DataControl, decouple all clients from using DataControl. After you delete the service, the keys might be deleted, and you might be locked out of your virtual machines.
* If you installed Entrust DataControl before VMware Solutions v4.0, and you delete the service, you must manually remove the DNS entries. For more information, see [Manually removing the DNS entries](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices#vc_deletingservices-DNS-entries).
