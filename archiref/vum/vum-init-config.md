---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Initial configuration
{: #vum-init-config}

The {{site.data.keyword.vcf-auto}} automation configures the VMware vCenter® Server Appliance (VCSA) with a default gateway set to the {{site.data.keyword.cloud_notm}} Backend Customer Router (BCR). However, no route to the internet though the BCR exists. The standard route to the internet from the {{site.data.keyword.vcf-auto-short}} instance for management components is through the services T0. As it isn't advised changing the configuration of the VCSA or the services T0, a proxy server implementation on the customer subnet is recommended to enable VMware Update Manager (VUM).

This approach means that you don't need to reconfigure the VCSA or the services T0, however, a small virtual machine (VM) must be installed. A proxy server is a system, which sits between two endpoint devices and acts as an intermediate device. In this case, it sits between the VCSA and the update servers at VMware.

When VUM requests a resource from the update server at VMware, the request is sent to the proxy server first, and the proxy server then sends the request to the update server. After the resource is obtained by the proxy server, it sends the resource to VUM. A proxy server can be used to facilitate security, administrative controls, and caching services.

You can use a proxy server based on Linux and Squid. Squid Proxy is an open source caching proxy for the web and supports many protocols that include HTTP and HTTPS. A number of VM and appliance-based proxies are available, and you must select the appropriate one based on your enterprise’s requirements and install and configure following the vendor’s guidance. If you select to use a Squid implementation, continue with the following process.

* Download the Linux ISO to a jump server.
* Create a vCenter Library.
* Upload the ISO to the vCenter Library.
* Create a VM, install, and configure Linux, and install Squid.

## Finding the subnet information
{: #vum-init-config-subnet}

Before you can start this task, collect the information to populate the following table. Review the suggested values and ensure that they are appropriate for your environment.

To find your customer private portable subnet details, complete the following steps:

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources** > **VCF for Classic** from the left navigation pane.
2. Select the required instance.
3. Click the **Infrastructure** tab and select the required cluster.
4. Select **Private VLAN** and locate the subnet that is labeled `Private subnet for customer workload edge`.
5. Select the subnet to view the subnet details page that displays the IP addresses and their allocations.
6. By using the information, select a nonallocated IP address and update the **Note** with appropriate comments. Use this IP address for the `proxy ip` parameter in the following table.

| Parameter | Suggested value | Notes |
|:--------- |:---------------- |:----- |
| Proxy CPU | 1 vCPU | Squid has no minimum requirements. |
| Proxy RAM | 2 GB | Squid has no minimum requirements. |
| Proxy Disk | 25 GB | Squid has no minimum requirements. |
| Hostname | `Proxy01` | |
| Address | Proxy IP | A spare IP address must be used from the Customer, private portable subnet assigned during the provisioning process. |
| Netmask | 255.255.255.192 | None |
| Gateway| Customer T0 uplink1 virtual IP address | This parameter is the default gateway setting for the proxy server, which is the private uplink IP address of customer T0. The IP address can be found by reviewing details in the {{site.data.keyword.vmwaresolutions_short}} console by browsing to the Portable private subnet for customer workload edge. |
| DNS Server | AD/DNS IP | This IP address can be found in the {{site.data.keyword.vmwaresolutions_short}} console by browsing to the **Resources** > **VCF for classic** > Summary page. |
| BCR IP | BCR IP| On the same page where you selected the proxy IP, note the address that is labeled **Gateway**. This address is the IP address of the {{site.data.keyword.cloud_notm}} Backend Customer Router and is the gateway for `10.0.0.0/8`, `161.26.0.0/16`, and `166.8.0.0/14`. You use this address later in a static route in the proxy server so that it can reach the VCSA and the AD/DNS server. |
| NAT IP | T1 SNAT address | The public T1 SNAT address of the customer workload edge serves as the public NAT address for the proxy. This IP address can be found by reviewing details in the {{site.data.keyword.vmwaresolutions_short}} console by browsing to the Portable public subnet for customer workload edge. |
{: caption="Table 1. Deployment values" caption-side="bottom"}
{: #vum-init-config-subnet-table-deployvalues}

## Configuring NSX
{: #vum-init-config-config-nsx}

NSX-T customer workload T0 firewall and NAT settings are required to enable proxy server traffic.

### Setting up the firewall
{: #vum-init-config-firewall}

Add a gateway firewall policy and rule by using the parameters in the following table. For more information, see [Add a gateway firewall policy and rule](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-DE6FE8CB-017E-41C8-85FC-D71CF27F85C2.html){: external}.

| Parameter | Suggested values |
|:--------- |:---------------- |
| Name | `Outbound Proxy01` |
| Source | Proxy server IP |
| Destination | Any |
| Service | HTTP/HTTPS/ICMP Echo |
| Action | Allow |
{: caption="Table 2. Firewall rule" caption-side="bottom"}

### Defining the NAT rule
{: #vum-init-config-nat}

Add a NAT rule by using the parameters in the following table. For more information, see [Configure SNAT/DNAT/No SNAT/No DNAT/Reflexive NAT](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-DDB35A76-BD12-4F09-8D88-2490E4DAA8F6.html){: external}.

| Parameter | Suggested values |
|:--------- |:---------------- |
| Name | `Proxy01 SNAT` |
| Action | SNAT |
| Source IP | Proxy server IP |
| Destination IP | Any |
| Translated IP address | NAT IP |
| Enabled | Yes |
{: caption="Table 3. NAT rule" caption-side="bottom"}

## Installing and configuring a proxy server
{: #vum-init-config-inst-cfg-proxy}

The following steps deploy a Linux VM hosting Squid from the Content Library. In this example, a Windows® VSI is provisioned for use as a jump server and Remote Desktop Protocol to the VSI’s public interface is being used to access the jump server.

* Download the Linux ISO file from the distributions' repository.
* Configure a vCenter Content library and populate it with the Linux ISO file.
* Configure the VM and install Linux and Squid.

### Downloading the Linux ISO file
{: #vum-init-config-download-linux}

Using a browser on your jump server download the required Linux ISO file.

### Configuring a content library and populating it with the CentOS ISO file
{: #vum-init-config-config-content-library}

Create a local vCenter content library, see [Create a library](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-2A0F1C13-7336-45CE-B211-610D39A6E1F4.html){: external}. The library is accessible only in the {{site.data.keyword.vcf-auto-short}} instance where it is created. Populate the library with the Linux ISO. See [Import Items to a Content Library](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-897EEEC2-B378-41A7-B92B-D1159B5F6095.html){: external}.

### Configuring the VM and installing CentOS and Squid
{: #vum-init-config-config-proxy}

1. Create a VM. For more information, see [Create a VM with the new virtual machine wizard](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-AE8AFBF1-75D1-4172-988C-378C35C9FAF2.html){: external}.
2. Attach the ISO to the VM's CD/DVD drive by using the `Content Library ISO File` option. For more information, see [Add or modify a VM CD or DVD drive](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vm_admin.doc/GUID-C58B93A7-52CF-456D-95C1-8B5A906C9619.html){: external}.
3. Install Linux by following the instructions provided by the Linux distributor.
4. Install Squid. The installation of Squid varies depending on the Linux distribution. Use the following code as an example only:

```bash
yum -y update
yum -y install epel-release
yum -y update
yum clean all
yum -y install squid
systemctl start squid
systemctl enable squid
systemctl status squid
firewall-cmd –add-port=3128/tcp –permanent
firewall-cmd –reload
```

## Setting up VUM initially
{: #vum-init-config-init-setup-vum}

Configure the VCSA to use the proxy. For more information, see [Configure the DNS, IP address, and proxy settings](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.vcenter.configuration.doc/GUID-7576FBBE-8B67-4D3F-B859-C9688E9442D7.html){: external}.

## Related links
{: #vum-init-config-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
