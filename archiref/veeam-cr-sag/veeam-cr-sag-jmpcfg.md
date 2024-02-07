---

copyright:

  years:  2022, 2024

lastupdated: "2024-01-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the jump server
{: #veeam-cr-sag-jmpcfg}

Now that the jump server is ordered and available for connection on its public IP address from your laptop, you can follow these steps:

1. [Change the Domain Name Services (DNS)](#veeam-cr-sag-jmpcfg-dns) client so that it points to the VMware vCenter Server® instances - Active Directory™ DNS (AD/DNS) server instead of the {{site.data.keyword.cloud}} DNS resolver. It allows name resolution for components, such as the vCenter appliance and VMware NSX-T™ Manager. The VSI has two Ethernet interfaces, one for the private network and one for the public network.
2. [Download software](#veeam-cr-sag-jmpcfg-sw) that enables administration functions, such as mRemoteNG and Firefox®.
3. [Install PowerCLI](#veeam-cr-sag-jmpcfg-powercli). PowerCLI is a collection of PowerShell Modules to manage VMware® infrastructure, including network, storage, virtual machine (VM), and guest OS.

## Changing DNS
{: #veeam-cr-sag-jmpcfg-dns}

1. From the {{site.data.keyword.vmwaresolutions_full}} console, click **Resources** > **vCenter Server** from the left navigation pane. Select the instance and click the **Access information** tab to capture the IP address of your AD/DNS servers `DNS1` and `DNS2`.
2. From your laptop, use an RDP client to access the jump server.
3. When connected to the jump server, open a PowerShell console with admin privileges.
4. Use `Get-DNSClientServerAddress` to display the interfaces and their parameters. You need to capture the Interface Indexes `IF1` and `IF2` for the Ethernet interfaces for use in the next command.
5. Use the following command to change the first interface: `Set-DNSClientServerAddress –interfaceIndex <IF1> –ServerAddresses (“<DNS1>”,“<DNS2>”)`. For example, `Set-DNSClientServerAddress –interfaceIndex 11 –ServerAddresses (“10.38.207.132”, “10.38.207.133”)`.
6. Use the following command to change the second interface: `Set-DNSClientServerAddress –interfaceIndex <IF2> –ServerAddresses (“<DNS1>”,“<DNS2>”)`. For example, `Set-DNSClientServerAddress –interfaceIndex 15 –ServerAddresses (“10.38.207.132”, “10.38.207.133”)`.
7. Use the command `Get-DNSClientServerAddress` to verify the interfaces and their parameters.

## Downloading the software
{: #veeam-cr-sag-jmpcfg-sw}

Open a PowerShell window and use the following commands to download and install mRemoteNG and Firefox.

```text
Invoke-WebRequest -Uri https://github.com/mRemoteNG/mRemoteNG/releases/download/v1.76.20/mRemoteNG-Installer-1.76.20.24615.msi -OutFile C:\Users\Administrator\Downloads\mRemoteNG-Installer-1.76.20.24615.msi
Invoke-WebRequest -Uri "https://download.mozilla.org/?product=firefox-msi-latest-ssl&os=win64&lang=en-GB" -OutFile C:\Users\Administrator\Downloads\firefox-msi-latest.msi
cd C:\Users\Administrator\Downloads
.\mRemoteNG-Installer-1.76.20.24615.msi
.\firefox-msi-latest.msi
```
{: codeblock}

## Installing PowerCLI
{: #veeam-cr-sag-jmpcfg-powercli}

PowerShell is installed by default with Windows® Server. However, PowerCLI needs to be installed from the PowerShell gallery.

1. Install VMware PowerCLI by entering `Install-Module -Name VMware.PowerCLI`.
2. At the prompts, enter `Y`.

## Related links
{: #veeam-cr-sag-jmpcfg-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
