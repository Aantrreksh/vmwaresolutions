---

copyright:

  years:  2016, 2024

lastupdated: "2024-09-18"

keywords: vcf automated networking, networking components, networking vcf classic

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Networking considerations for {{site.data.keyword.vcf-auto-short}}
{: #vc_networkingonvcenterserver}

Review the following information for details about networking considerations and requirements for your {{site.data.keyword.vcf-auto}} instances. Ensure that you meet the requirements so that your instance functions properly.

## Networking components for {{site.data.keyword.vcf-auto-short}}
{: #vc_networkingonvcenterserver-networking-components}
{: faq}

To review the networking components that are included in your Automated instance, see [Technical specifications for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview#vc_vcenterserveroverview-specs).

## Firewall considerations
{: #vc_networkingonvcenterserver-firewall-considerations}
{: faq}

If you're using firewalls, you must configure rules for all communications from the {{site.data.keyword.IBM}} CloudDriver virtual server instance (VSI) and the SDDC Manager virtual machines (VMs). These rules must allow all protocols to communicate on the IP addresses `10.0.0.0/8` and `161.26.0.0/16`. Examples of such firewalls are NSX Distributed Firewalls (DFW) or vSRX gateway cluster firewalls.

Some components might attempt to connect to the public network, although they are deployed to your private network. In some cases, such as Zerto Virtual Replication or FortiGate-VM, this connection is required for licensing or to report usage. These components are configured to connect either by using the instance NAT or a proxy you provide. You might need to allow these connections in your firewall. In other cases, these connection attempts are only for diagnostic and usage data, and the connections fail since no public connectivity is available or configured.

## Using NSX with your virtual machines
{: #vc_networkingonvcenterserver-using-nsx-with-vm}
{: faq}

During {{site.data.keyword.vcf-auto-short}} instance deployment, VMware NSX® is ordered, installed, licensed, and configured in your instance. Also, NSX Manager, VMware NSX Controllers™, and NSX Transport Zone are set up, and each VMware ESXi™ server is configured with the NSX components.

A VMware NSX Edge™ cluster is also deployed to be used by your workload VM or VMs. For more information, see [Configuring your network to use the customer-managed NSX edge cluster with your VMs](/docs/vmwaresolutions?topic=vmwaresolutions-vc_esg_config).

## Considerations when you change passwords for NSX components
{: #vc_networkingonvcenterserver-change-nsx-component-password-considerations}

Review the following considerations before you attempt to change the passwords for the NSX Manager, NSX Controllers, and NSX Edges.

### Considerations when you change passwords for NSX-T components
{: #vc_networkingonvcenterserver-change-pwd-nsx-t}
{: faq}

* You can change the NSX Manager root password. This password is not displayed in the VMware Solutions console. However, the password is the same as the one for the root user for NSX Controllers, which is displayed in the console.
* You can change the passwords for the root user for NSX Controllers. The root credentials are displayed in the VMware Solutions console.
* You can change the passwords for the admin user and the root user for the customer-managed VMware NSX edge nodes. The admin credentials are displayed in the VMware Solutions console, but the root credentials are not displayed. The passwords for the root user and the admin user are the same.
* You can change the passwords for admin user and root user for management services edge nodes. The admin credentials are displayed in the VMware Solutions console, but the root credentials are not displayed. The passwords for the root user and the admin user are the same.

### Considerations when you change passwords for NSX-V components
{: #vc_networkingonvcenterserver-change-pwd-nsx-v}
{: faq}

* You can change the NSX Manager password. This password is displayed on the **Summary** page of the instance in the VMware Solutions console.
* You can change the NSX Controller password. This password is not displayed in the VMware Solutions console, but you can set a new password without the old password. For more information, see [Change Controller password](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.2/NSX-Data-Center-for-vSphere-62.zip){: external}.
* You can change the password and the SSH settings for the customer-managed edge. This password is not displayed in the VMware Solutions console, but you can set a new password without the old password. For more information, see [Change CLI credentials](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.4/com.vmware.nsx.admin.doc/GUID-1DB9DE43-6B54-4FD1-903A-2DFFB87CD7FA.html?hWord=N4IghgNiBcIKYBMDmcAEAHMBnLB3A9gE4IgC+QA){: external}.
* Do not change the passwords for the management VMware NSX ESG and the related Distributed Logical Router.

## Related links
{: #vc_networkingonvcenterserver-related}

* [Overview of NSX-T Data Center](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/installation/GUID-10B1A61D-4DF2-481E-A93E-C694726393F9.html){: external}
* [Resetting the passwords of an appliance](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-8816B842-2EC4-40A8-A618-F68DB29FABD2.html){: external}
* [Manage local user’s password or name using the CLI](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-DB31B304-66A5-4516-9E55-2712D12B4F27.html){: external}
