---

copyright:

  years:  2020, 2024

lastupdated: "2024-10-10"

keywords: vmware solutions shared, get started shared, tech specs shared

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Operating {{site.data.keyword.vm-shared}}
{: #shared_vcd-ops-guide}

{{site.data.content.shared-deprecated-note}}

## VMware Cloud Director tenant portal overview
{: #shared_vcd-ops-guide-port-ovv}

The VMware® Cloud Director tenant portal is used for administration of your organization and to create and configure virtual machines (VMs), vApps, and networks within vApps.

You can also configure advanced networking capabilities that are provided by VMware NSX® for vSphere® within a VMware Cloud Director environment. With the tenant portal, you can also create and manage catalogs, vApps, and virtual data center templates.

### Roles, permissions, and users
{: #shared_vcd-ops-guide-roles}

The tenant portal includes a preconfigured set of user roles and their privileges. The roles that can access the tenant portal are created by default when an organization is created along with other roles that are created by the organization administrator. Users who are assigned the following organization roles can access the tenant portal. The objects that they see and the actions that they can take depend on the privileges that are associated with a role.

* Organization Administrator
* Catalog Author
* vApp Author
* vApp User
* Console Access Only

For more information about roles and permissions, see [VMware Cloud Director tenant portal roles and rights](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-754BD24F-63C7-422F-83BC-BFA275CEDA8E.html){: external}.

#### Managing users
{: #shared_vcd-ops-guide-roles-procedures}

Use the tenant portal to create a user or change passwords or roles for an existing user. For more information about accessing the tenant portal, see [Log in to the VMware Cloud Director tenant portal](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-28972197-D45B-4156-A733-5966730B5E03.html){: external}.

For more information about creating and modifying tenant portal users, see [Managing users](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FE38C285-7605-4473-870C-6AD44D8BF42E.html){: external}.

#### Modifying your email settings
{: #shared_vcd-ops-guide-roles-email}

The Organization Administrator must modify email notification settings to the organization SMTP server.

For more information about modifying SMTP server settings, see [Modify your email settings](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-726D40D7-4251-47AD-B945-2030E489165F.html){: external}.

## Catalogs
{: #shared_vcd-ops-guide-catalogs}

A catalog is a container for vApp templates and media files in an organization. Organization administrators and catalog authors can create catalogs in an organization. Catalog contents can be shared with other users or organizations in the {{site.data.keyword.vm-shared}} installation. Or they can be published externally for access by organizations outside the {{site.data.keyword.vm-shared}} installation.

{{site.data.keyword.vm-shared}} contains private catalogs, shared catalogs, and externally accessible catalogs. Private catalogs include vApp templates and media files that you can share with other users in the organization. If a system administrator enables catalog-sharing for your organization, you can share an organization catalog to create a catalog accessible to other organizations in the {{site.data.keyword.vm-shared}} installation.

If a system administrator enables external catalog publishing for your organization, you can publish an organization catalog for access by organizations outside the {{site.data.keyword.vm-shared}} installation. An organization outside the {{site.data.keyword.vm-shared}} installation must subscribe to an externally published catalog to access its contents.

### {{site.data.keyword.vm-shared}} public catalog
{: #shared_vcd-ops-guide-public-cat}

Each organization has access to the {{site.data.keyword.vm-shared}} public catalog. The catalog contains IBM-compliant images that are configured, secured, and ready for use.

Review the following considerations for {{site.data.keyword.vm-shared}}:

* Operating system licensing costs apply for usage. For more information about how commercial operating system license rentals are billed, see [{{site.data.keyword.vm-shared}} pricing](/docs/vmwaresolutions?topic=vmwaresolutions-shared_pricing).
* Public templates that are configured to services on the IBM private network require an extra configuration step to enable VM access to the IBM Services network. For more information, see [Enabling VM access to {{site.data.keyword.cloud_notm}} Services by using the private network](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-enable-access).
* Public templates require a minimum level of customization to establish the initial administrator password. For more information, see [Changing the guest OS customization properties of a VM](#shared_vcd-ops-guide-customization).

The public catalog contains vApp templates for the following components:

| Image | Version |
|---|---|
| CentOS | 7.x and 8.x |
| Microsoft® Windows® | 2022 Standard |
| Microsoft Windows | 2019 Standard |
| Microsoft Windows | 2016 Standard |
| Red Hat Enterprise Linux® | 8.1 |
| Red Hat Enterprise Linux | 7.7 |
{: caption="vApp templates" caption-side="bottom"}

#### CentOS templates
{: #shared_vcd-ops-guide-public-cat-centos}

The CentOS templates that are provided in the public catalog have the following characteristics:

* Latest updates installed
* VMware tools installed
* YUM repository enabled configured to the IBM private network YUM repository
* NTP server that is configured to the IBM private network NTP Server

#### Microsoft Windows templates
{: #shared_vcd-ops-guide-public-cat-windows}

The Microsoft Windows templates that are provided in the public catalog have the following characteristics:
* Latest updates installed
* Windows update enabled configured to the IBM private network Windows update server
* VMware tools installed
* Windows Remote Desktop disabled
* Firewall activated
* Windows Defender activated
* NTP server that is configured to the IBM private network NTP Server
* Windows license configured to activate and receive updates by using the IBM Service Network Microsoft Key Management Server (KMS) and not the internet Microsoft KMS

#### Red Hat Enterprise Linux templates
{: #shared_vcd-ops-guide-public-cat-rhel}

The Red Hat Enterprise Linux templates that are provided in the public catalog have the following characteristics:

* Latest updates installed
* VMware tools installed
* Firewall activated
* NTP server that is configured to the IBM private network servers

After you deploy the VM on the tenant portal, register the Red Hat VM with your RHEL activation key in IBM RHEL Capsule Server. To register the Red Hat VM with your RHEL activation key, you must enable VM access to connect to the IBM service network. For more information, see [Enabling VM access to {{site.data.keyword.cloud_notm}} Services by using the private network](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-enable-access).
{: important}

Complete the following steps to register the Red Hat VM with your RHEL activation key. For more information about accessing virtual data center details, see [Procedure to view the virtual data center summary](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary#shared_viewing-vdc-summary-procedure).

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click the virtual data center name in the **{{site.data.keyword.vm-shared}}** virtual data center table.
2. On the virtual data center details page, locate and make note of the **Red Hat activation key**.
3. Run the following commands from the Red Hat VM.
     1. `rpm -ivh http://52.117.132.7/pub/katello-ca-consumer-latest.noarch.rpm`
     2. `uuid = uuidgen`
       Where the character that is used around `uuidgen` is the grave accent or backtick.
     3. `echo '{"dmi.system.uuid": "'$uuid'"}' > /etc/rhsm/facts/uuid_override.facts`
     4. `cat /etc/rhsm/facts/uuid_override.facts`
       Ensure the contents of the `uuid_override.facts` contains a generated UUID.
     5. `subscription-manager register --org="customer" --activationkey="ACTIVATION_KEY" --force`
       Where `ACTIVATION_KEY` is the Red Hat activation key that is on the virtual data center details page.

You can still use another RHEL Capsule Server or a satellite server if you already have an RHEL subscription outside of IBM. Charges for the RHEL license are incurred against RHEL VMs that are running in a virtual data center.
{: note}

### Defining catalogs and policies
{: #shared_vcd-ops-guide-policies}

To create a catalog, you must have either the **Organizational Administrator** or **Catalog Author** tenant portal role.

For more information about defining catalogs and policies, see [Working with catalogs](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-6424C4A7-EA95-49A0-B673-9DDB971AB566.html){: external}.

### Uploading your media or templates
{: #shared_vcd-ops-guide-customer}

OVF packages can be uploaded to a catalog as a vApp template to make the template available to users. For more information, see [Create a vApp template from an OVF file](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-5EA412C4-179A-42CF-9B30-1B81C23551E6.html){: external}.

Media files, such as ISO disk images and FLP diskette drive images, can be uploaded to a catalog as a media file. For more information, see [Working with media files](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-A7530A4B-F782-4848-90FC-BBDE41E3AE85.html){: external}.

The maximum import size is 750 GB. Large image files or templates might take a long time to upload. For assistance with files larger than 750 GB, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: note}

## Virtual machines
{: #shared_vcd-ops-guide-machines}

When you use the tenant portal, you can create a virtual machine (VM) or provision a VM from a template.

For more information, see [Create a standalone virtual machine](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-64CFBEFC-8E3D-49FC-B1BD-16CCE7493544.html){: external}.

### Customizing virtual machine properties
{: #shared_vcd-ops-guide-cust-properties}

You can edit the properties of a VM, including the VM name and description, hardware and network settings, and operating system settings for a guest.

For more information about working with VMs, see [Working with virtual machines](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-DF0C111D-B638-4EC3-B805-CC33994F8D53.html){: external}.

If you use the tenant portal **Password Reset** field to change your Windows Administrator password, ensure that you adhere to Windows complexity requirements. If you change the password in the tenant portal without doing so, the password does not work in the Windows VM template.
{: important}

#### Changing the general properties of a virtual machine
{: #shared_vcd-ops-guide-change-properties}

You can change the name, description, storage policy, and other general properties of a VM.

##### Switching between storage properties
{: #shared_vcd-ops-guide-change-properties-storage}

Some disk settings cannot be changed while the VM is powered on. For example, you can increase the disk size while the VM is powered on, but you cannot decrease the disk size unless the VM is powered off. A message displays if you must power off the VM before you modify a disk setting. For more information, see [Power off a virtual machine](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-2323B049-4E36-4510-999E-F2D4A77AC0F9.html){: external}.

For more information about changing a storage policy, see [Change the general properties of a virtual machine](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FA8C101E-241E-41A5-A3C3-83BDBB4467F1.html#GUID-8301D672-8333-4FD2-B132-2D4A42E11216__GUID-BE9430B7-40F8-43F7-AED4-1080F9E04E34){: external}.

If you must power off the VM before you change a storage policy, power the VM back on after the VM is moved to the new storage policy. For more information, see [Power on a virtual machine](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-33C22124-A610-4C3E-8F40-26CAC570F958.html){: external}.

#### Enabling a compute policy
{: #shared_vcd-ops-guide-compute-policy}

Compute policies are applied for VMware stretched vSAN virtual data centers. When you create a new VM in a stretched location, it uses the `compute_policies` available for that virtual data center. Additionally, you can change from one compute policy to another by editing your VM hardware properties.

During a failover, a VM moves to a secondary site. When the preferred site is recovered, the VM automatically returns back to the preferred site with the compute policies restored.

You can select the compute policy that you prefer for each VM and VMware Solutions attempts to keep the VM on the preferred data center if it is up and running.

1. From the tenant portal, click **Virtual Machines** from the left panel.
2. Click **Hardware** to expand the list and click **Compute**.
3. Locate **Placement Policy** and click **EDIT**.
4. Select the compute policy and click **Save**.

#### Changing the hardware properties of a virtual machine
{: #shared_vcd-ops-guide-hardware}

You can change the hardware properties of a VM, number of vCPUs, memory, hard disk allocation, and network configuration.

#### Changing the Guest OS Customization properties of a virtual machine
{: #shared_vcd-ops-guide-customization}

Guest OS customization is optional for all platforms. It is required for VMs that must join a Windows domain when the VMs are being powered on.

When you use an IBM template to create the VM, use the **Guest OS Customization** pane to acquire or set the unique password for the OS instance. Ensure that the option **Enable guest customization** is selected and then use one of the **Password Reset** options to establish the initial administrator credential.

For more information, see [Change the guest OS customization properties of a virtual machine](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FA8C101E-241E-41A5-A3C3-83BDBB4467F1.html#GUID-2B7A04E8-7479-4EE9-99B0-1A46751BE46F__GUID-658C5607-04BA-4BE1-87D3-8553DD2601EE){: external}.

#### Changing the advanced properties of a virtual machine
{: #shared_vcd-ops-guide-advanced}

In the Advanced settings, you can configure the resource allocation settings (shares, reservation, and limit) to determine the amount of virtual CPU (vCPU), memory, and storage resources provided for a VM.

For more information, see [Edit virtual machine properties](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FA8C101E-241E-41A5-A3C3-83BDBB4467F1.html){: external}.

### Using IBM templates
{: #shared_vcd-ops-guide-ibm-templates}

Password requirements apply if the VM is deployed from the IBM templates that are provided in the public catalog. You must use the initial password that was generated during power-on when you first log in to the VM. You can find this password on the VM details page.

If you use the tenant portal **Password Reset** field to change your Windows Administrator password, ensure that you adhere to Windows complexity requirements. If you change the password in the tenant portal without doing so, the password does not work in the Windows VM template.
{: important}

1. From the **Guest OS Customization** pane, click **EDIT**.
2. From the **Edit Guest Properties** pane, locate the password in the **Specify password** field.
3. After a successful login with the initial password, return to the **Edit Guest Properties** pane to reset the password and log in again with the new password.

## vApps
{: #shared_vcd-ops-guide-vapps}

A vApp consists of one or more VMs that communicate over a network and use resources and services in a virtual data center. Create the vApp and then add VMs and networks.

For more information about vApps, see [Working with vApps](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-AC48FB5E-4ADC-4835-AACE-B949B297A147.html){: external}.

## Networking
{: #shared_vcd-ops-guide-networking}

Every {{site.data.keyword.vm-shared}} virtual data center comes configured with one edge gateway with five public IP addresses and one private IBM Services network IP address. You can open an {{site.data.keyword.cloud_notm}} Support ticket to request five more public IP addresses or an entire subnet for your virtual data center.

Include the following details in your support ticket:
* Virtual data center region and location
* Organization ID
* Virtual data center name
* Number of IP addresses required

For more information about opening a support ticket, follow the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

The edge gateway services are customer configurable and require configuration to allow network traffic in and out of their Organization virtual data center. Configuration is required for access to the internet and the IBM Services network. The five public addresses are used for public facing vApps for inbound and outbound public internet traffic.

The service address is used for access to a number of {{site.data.keyword.cloud_notm}} infrastructure services on the {{site.data.keyword.cloud_notm}} internal private network. The list includes the following services:
* NTP
* Windows operating system licensing and updates
* Red Hat operating system licensing and updates
* Cloud Object Storage

Two types of Organization virtual data center networks are available in the {{site.data.keyword.vm-shared}} virtual data center: routed and internal.

### Routed network
{: #shared_vcd-ops-guide-routed}

Accessible only by the same Organization virtual data center. Only VMs in this Organization virtual data center can connect to this network. This network also provides controlled access to an external network. An organization administrator can configure Network Address Translation (NAT), firewall, and VPN settings to make specific VMs accessible from the external network.

### Internal or isolated network
{: #shared_vcd-ops-guide-internal}

Accessible only by the same Organization virtual data center. Only VMs in this Organization virtual data center can connect to and see traffic on the internal Organization virtual data center network.

The isolated Organization virtual data center network provides an Organization virtual data center with an isolated, private network that multiple VMs and vApps can connect to. This network provides no connectivity to VMs outside the Organization virtual data center. VMs that are outside of the Organization virtual data center have no connectivity to VMs that are in the Organization virtual data center.

### Creating a network
{: #shared_vcd-ops-guide-create-network}

From the tenant portal, use the following procedures to create a sample network topology that includes: configuring DHCP services, defining Source NAT (SNAT) and Destination NAT (DNAT) rules, and creating firewall rules on the edge gateway to allow access to the internet. Complete these procedures from the tenant portal **Data Centers** tab.

![{{site.data.keyword.vmwaresolutions_short}} network topology](../images/vcd-sample-topology.svg "{{site.data.keyword.vmwaresolutions_short}} network topology"){: caption="{{site.data.keyword.vmwaresolutions_short}} network topology" caption-side="bottom"}

#### Creating a routed Organization virtual data center network
{: #shared_vcd-ops-guide-routed-organization}

For more information about how to create a routed organization, see [Add a routed organization virtual data center network](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-74C4D27F-9E2A-4EB2-BBE1-CDD45C80E270.html){: external}.

Review the following notes for creating a routed Organization virtual data center network.

* Virtual data centers can share networks only if they are in the same region. You can choose to set the **Shared** option when an application within an Organization virtual data center has a reservation or allocation pool set as the allocation model. In this case, it might not have enough room to run more VMs. As a solution, you can create a secondary Organization virtual data center with on-demand and run more VMs on that network on a temporary basis.
* From the **Edge Connection** page, select the edge that was created when the virtual data center was created.
* Select **Distributed** for the **Interface Type**.
* Repeat the procedure to create another Organization virtual data center network. Give the network a different **Name**, such as `App` and a different **Gateway CIDR**, such as `192.168.101.1/24`.

#### Validating that the network is connected to the edge
{: #shared_vcd-ops-guide-validate-network}

Use the steps to add a static route to validate that the Organization virtual data center networks that you defined earlier are listed as static routes. When you click **Create (+)**, locate the **Next Hop** field, and confirm that `52.117.132.2` is displayed. This value is the internal interface of the edge gateway.

 For more information, see [Add a static route](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-1C8D8FF7-7C24-4A44-875B-04DB961FB780.html){: external}.

#### Configuring DHCP on the edge gateway
{: #shared_vcd-ops-guide-configure-dhcp}

Optionally, you can configure DHCP on the edge gateway to assign IP addresses automatically to the VMs connected to the Organization virtual data center networks. This step is not necessary if you are using static IP addresses.

From the virtual data center for that edge gateway, configure the DHCP. Repeat the procedure for extra Organization virtual data center networks that are attached to the edge that requires DHCP services. For more information, see [Add a DHCP IP pool](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-EF0B4C79-F6F7-4C75-825C-0B76B888856D.html){: external}.

Review the following notes for configuring DHCP on the edge gateway.

* The **IP Range** is a range from the Organization virtual data center network that is attached to the edge.
* You can define the names for the **Primary Name Server** and the **Secondary Name Server** now or update the names later.
* The **Default Gateway** is the gateway CIDR or the Organization virtual data center network that is attached to the edge.
* Ensure to set the DHCP service status to enabled.


#### Connect the VMs to the network
{: #shared_vcd-ops-guide-connect-vm}

Stand-alone VMs, or VMs in a vApp, can connect to an Organization virtual data center network.

From the tenant portal, access the hardware properties of the VMs and add the new network interface to the **NICs** field. Repeat the procedure for extra VMs. For more information, see [Change the hardware properties of a virtual machine](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FA8C101E-241E-41A5-A3C3-83BDBB4467F1.html#GUID-BB95EAB5-13D7-4C4A-BDA3-AA1338BC01CA__GUID-A3963005-8914-4F8E-A4AC-007C88E52EE8){: external}.

After the VMs are connected to the Organization virtual data center network, they are able to communicate with each other. You can ping from one of the VMs to another to test. If the ping command does not respond, check the OS firewalls to see whether ICMP is allowed.

#### Enable inbound and outbound traffic
{: #shared_vcd-ops-guide-enable-traffic}

To enable VMs on the Organization virtual data center network to reach an external network, configure a SNAT (Source Network Address Translation) rule and a firewall policy to allow the VM traffic outbound. To allow inbound traffic from an external network, you must configure a DNAT (Destination Network Address Translation) rule and a firewall policy.

Before you create the firewall and NAT rules, capture the information that is necessary for subsequent steps.

1. From the tenant portal, click **Data Centers**.
2. On the main page, under **Virtual Data Center**, click the virtual data center for that edge gateway.
3. In the left pane under **Networking**, click **Edges**.
4. Under Configuration, select **Gateway Interfaces**. Copy the values in the table for the tenant external and the Service networks. With the tenant external addresses, you can route to the external network, and with the service network addresses, you can route to the IBM private network.
5. Return to the {{site.data.keyword.vmwaresolutions_short}} console. From the **Resources > {{site.data.keyword.vm-shared}}** page, copy the public IP addresses that were assigned to your virtual data center.

##### Create the Organization virtual data center network firewall rule to allow access to the external network
{: #shared_vcd-ops-guide-create-vdc-network-rule-extnetwork}

From the virtual data center for that edge gateway, create the network firewall rule. For more information, see [Add an NSX data center for vSphere Edge Gateway firewall rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-97ADAF42-598B-44B2-80EF-8B215B743C78.html){: external}.

Review the following notes for creating the Organization virtual data center network firewall rule to allow access to the external network.

* For **Source**, you can use an IP address, a range of addresses, or an object.
* In the **Browse objects of Type** menu, select **Org Vdc Networks**. Select the Organization virtual data center network that you created as the **Source** cell. Click the right arrow to move the Organization virtual data center network into the **Filter** column.
* Keep all remaining default selections.
* For **Action**, select **Accept**.
* To define a source IP address or range, click the **IP** in the **Source** cell and set the IP address, or range to allow everything on that subnet. For example, ``192.168.100.2`` or ``192.168.100.0/24``. Destination and services are set to **Any** when you choose the defaults.

##### Source NAT definitions to the external network
{: #shared_vcd-ops-guide-source-nat-ext}

A source NAT rule is necessary to allow traffic from the Organization virtual data center network outbound to the internet. From the virtual data center for that edge gateway, create NAT44 Rules. For more information, see [Add a SNAT or a DNAT rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-1DE460AE-DCCC-4BC8-96AC-52D06A4AFDE3.html){: external}.

Review the following notes for source NAT definitions.

Under the **NAT44 Rules**, click **SNAT Rule** and create the configuration by using the following selections.
* For **Applied On**, select the Organization virtual data center external network.
* For **Original Source IP/Range**, enter your Organization virtual data center Gateway CIDR.
* For **Translated Source IP/Range**, click **SELECT**. Then, for **Select IP Address Network**, select the external network and choose one of the external network addresses that were assigned to your virtual data center.
* Optionally, enter a destination port.
* Optionally, enter a description. A description can be useful to identify the SNAT rule later.
* Set to **Enabled**.
* Optionally, enable logging. Logs are not preserved. If you want to have historical data, you must set up a syslog server.

##### Create the Organization virtual data center network firewall rule to allow access to the {{site.data.keyword.cloud_notm}} Services Network
{: #shared_vcd-ops-guide-create-vdc-network-rule-ibm-services-network}

From the virtual data center for that edge gateway, create the network firewall rule. For more information, see [Add an NSX data center for vSphere Edge Gateway firewall rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-97ADAF42-598B-44B2-80EF-8B215B743C78.html){: external}.

Review the following notes for creating the Organization virtual data center network firewall rule to allow access to the {{site.data.keyword.cloud_notm}} Services Network.

* For **Source** you can use an IP address, a range of addresses, or an object.
* In the **Browse objects of Type** menu, select **Org Vdc Networks**. Select the Organization virtual data center network that you created as the **Source** cell. Click the right arrow to move the Organization virtual data center network into the **Filter** column.
* The destination can be an IP address, a range of addresses, or an object. In the **Destination** column, click the **+** in the upper right of the cell when you hover your mouse in the field. In the **Browse objects of Type** menu, select **Gateway Interfaces**. Select the service network available to your virtual data center. Click the right arrow to move the service network into the right side filter column.
* For **Action**, select **Accept**.
* To define a destination IP address or range, click the **IP** in the destination cell and set the IP address or range to allow everything on that subnet. For example, ``192.168.100.2`` or ``192.168.100.0/24``.

##### Source NAT definitions to the IBM Service Network (Private)
{: #shared_vcd-ops-guide-source-nat-int}

A source NAT rule is necessary to allow traffic from the Organization virtual data center network into the {{site.data.keyword.cloud_notm}} Service Network. This rule is used to enable VM access to {{site.data.keyword.cloud_notm}} Services such as update servers, DNS servers, NTP servers, or to get to the {{site.data.keyword.cloud_notm}} Object Storage.

From the virtual data center for that edge gateway, create the source NAT definitions to the IBM Service Network (Private). For more information, see [Add a SNAT or a DNAT rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-1DE460AE-DCCC-4BC8-96AC-52D06A4AFDE3.html){: external}.

Under the **NAT44 Rules**, click **SNAT Rule** and create the configuration by using the following selection.
* For **Applied On**, select the service network.
* For **Original Source IP/Range**, enter your Organization virtual data center Gateway CIDR.
* For **Translated Source IP/Range**, click **SELECT**. In the **Select IP Address** Network menu, select the service network and choose one of the service network addresses that were assigned to your virtual data center.
* Optionally, enter the destination IP addresses.
* Optionally, enter the destination port.
* Optionally, enter the description. A description can be useful to identify the SNAT rule later.
* Set to **Enabled**.
* Optionally, enable logging. Logs are not preserved. If you want to have historical data, you must set up a syslog server.

If the DHCP services are enabled on the edge, you can test for internet connectivity by logging in to one of the VMs that are attached to the network for which the firewall and DNAT rules are defined.

The steps differ depending on the VM operating system and network configuration:
* For a Windows VM, renew the DHCP lease. Open a command line and issue the `ipconfig /renew` command.
* For a Linux VM, type `systemctl restart NetworkManager.service`. Depending on the type and version of Linux, this command might vary. From the command line, ping ``8.8.8.8`` or ``9.9.9.9``. If everything is configured correctly, you receive a reply. If the name resolution is required and no DNS server was defined yet, you can configure either ``9.9.9.9`` or ``8.8.8.8`` on the VM, edit the DHCP pool and define it there.

##### Destination NAT definition and port forwarding
{: #shared_vcd-ops-guide-destination-nat}

A destination NAT allows an outside host, in this case on the internet, to connect to an inside host on the Organization virtual data center network. The destination NAT maps one IP address or port to another IP address or port. The following instructions are an example of configuring DNAT and port forwarding to allow a Windows remote desktop connection to a Windows VM in the Organization virtual data center. Port forwarding is optional.

From the virtual data center for that edge gateway, create the destination NAT definition. For more information, see [Add a SNAT or a DNAT rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-1DE460AE-DCCC-4BC8-96AC-52D06A4AFDE3.html){: external}.

Under the **NAT44 Rules**, click **DNAT Rule** and create the configuration by using the following selection.
* For **Applied On**, select the ``<datacenter>-w<idx>-tenant-external`` interface, for example, ``dal13-w02-tenant-external``.
* For **Original Source IP/Range**, select one of the IP addresses from the Suballocated Public IP address range. Click **SELECT**, and select an IP from the **IP Address** menu. This value is the `tenant-external IP address` referenced in future steps. Click **KEEP**.
* Optionally, select port forwarding. Click the **Protocol** menu arrow and select **TCP**.
* Select a port that is not previously used with the original IP address or range. The **Original Port** in this example is ``8000``. Ports that are lower than 1024 are reserved.
* If ICMP is selected in the **Protocol** menu, select the **ICMP Type**.
* For **Translated IP/Range**, type the IP address of the VM on the private Organization virtual data center that you want to connect.
* For **Translated Port**, select the port on the previous VM that the servicer is listening on. In the Windows RDP example, port 3389 is the default remote desktop port.
* Optionally, provide a description.

From the virtual data center for that edge gateway, add a firewall rule to enable port forwarding. For more information, see [Add an NSX data center for vSphere Edge Gateway firewall rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-97ADAF42-598B-44B2-80EF-8B215B743C78.html){: external}.

Review the following notes for destination NAT definition and port forwarding.

* For **Source**, optionally define the source if you want to restrict access to the internal Organization virtual data center VM to a specific IP or IP range.
* For **Destination**, set the value to the `tenant-external IP address` used for **Original IP/Range** in the DNAT rule.
* For **Service**, set the **Protocol** to TCP and the **Destination Port** to the `tenant-external IP address` used in the DNAT rule. In the example, port ``8000`` is used.

To test the configuration, use the remote desktop client and connect to the ``tenant-external IP address:port number`` as the destination in the **Computer** field.

#### Enabling VM access to {{site.data.keyword.cloud_notm}} Services by using the private network
{: #shared_vcd-ops-guide-enable-access}

You can configure vApps and VMs running inside of the virtual data center to use the {{site.data.keyword.cloud_notm}} private network to access {{site.data.keyword.cloud_notm}} services. Accessing {{site.data.keyword.cloud_notm}} services through a private network can save on outbound public networking costs and can provide a higher degree of reliability and security. Virtual data centers route to the {{site.data.keyword.cloud_notm}} private network through a virtual data center service network that is configured as an available external network on virtual data centers edge.

{{site.data.keyword.vm-shared}} fully enables access to IaaS endpoints for {{site.data.keyword.cloud_notm}} Virtual Private Cloud (VPC). For more information, see [Endpoints available for VPC](/docs/vpc?topic=vpc-service-endpoints-for-vpc).

The following services are available:

| Service | IP address (Endpoint) |
|:------- |:--------------------- |
| Microsoft Windows Update Server | 52.117.132.5 |
| Microsoft Key Management Server | 52.117.132.4 |
| Red Hat Capsule Server | 52.117.132.7 |
| DNS | 161.26.0.10 (`rs1.adn.networklayer.com`) and 161.26.0.11 (`rs2.adn.networklayer.com`) |
| Ubuntu and Debian APT Mirrors | 161.26.0.6 (mirrors.adn.networklayer.com) |
| RHEL and CentOS YUM repo | 161.26.0.6 (mirrors.adn.networklayer.com) |
| NTP | 161.26.0.6 (time.adn.networklayer.com) |
| [{{site.data.keyword.cloud_notm}} Object Storage](/docs/vpc?topic=vpc-connecting-vpc-cos) | `s3.direct.xxx.cloud-object-storage.appdomain.cloud` |
{: caption="Available services" caption-side="bottom"}

Enabling access to the service network is done in two edge configuration steps.

##### Adding the NAT rule for VMware Solutions Shared
{: #shared_vcd-ops-guide-nat-rule}

Add a NAT rule for translating internal network addresses into the service network IP address space.
1. Log in to the VMware Cloud Director tenant portal.
2. Click the virtual data center **Edges** tab and open the single preconfigured edge.
3. In the **External Networks** section, click the **IP Settings** link. Find the name of the service network and the IP address that is assigned for the service network interface from the table displayed. The format for the service network name is `<datacenter>-w<idx>-service<idx>`, for example, `dal13-w02-service02`.
4. Click **SERVICES** to open the Edge Gateway configuration page. Click the **NAT** tab and click **+ SNAT RULE** to add a SNAT rule.
5. Select the service network next to the **Applied on** field and add the IP addresses or range from one of the virtual data center Organization networks to the **Original Source IP/Range** field.
6. In the **Translated Source IP/Range** field, click **Select**. From the **Network** menu, select the service network. From the **IP Address** menu, select the service IP address that you want to use.
7. Optionally define the **Description** field.
8. Verify that **Enabled** is selected and click **KEEP**.
9. Click **Save Changes**.

##### Adding the NAT rule for {{site.data.keyword.vcf-aas}}
{: #shared_vcd-ops-guide-nat-rule-vmwaas}

Add a NAT rule for translating internal network addresses into the service network IP address space.
1. Log in to the VMware Cloud Director tenant portal.
2. From the main page under **Virtual Data Center**, click the virtual data center where you want to add the NAT rule.
3. In the left pane under **Networking**, click **Edges** and open the single preconfigured edge.
4. Under the **Services** section, click the **NAT** tab and click **NEW** to add an SNAT rule.
5. Complete the following configuration in the **Add NAT Rule** window:
   1. Enter a name for the NAT rule.
   2. Select `SNAT` in the **Interface Type** field.
   3. In the **External IP** field, click the information icon to view the available IP addresses and enter the external IP address that you want to use.
   4. In the **Internal IP** field, enter the internal IP address, including the CIDR to be translated. Typically, a subnet from the `RFC1918` private range is best, but not required. For example, `192.168.10.0/24`.
6. Verify the **Advanced Settings** fields and click **Save**.

##### Adding the firewall rule for VMware Solutions Shared
{: #shared_vcd-ops-guide-firewall-rule}

Add a firewall rule to allow the traffic from the internal network to the service network.
1. Click the **Firewall** tab and click **+** to add a firewall rule.
2. Add the IP addresses or range from your internal network to the **Source** field.
3. Add `52.117.132.1/24` in the **Destination** field.
4. Specify `Any` for the **Service** field and `Accept` for the **Action** field.
5. Click **Save changes**.

After the previous configuration is completed, you can use the supported {{site.data.keyword.cloud_notm}} services on the VMs in your virtual data center.

If your vApp or VM is deployed from the IBM templates that are provided in the public catalog, the services are already configured on the VM. To enable the connection, you must complete the previous steps in **Adding the NAT rule** and **Adding the firewall rule**.

##### Adding the firewall rule for {{site.data.keyword.vcf-aas}}
{: #shared_vcd-ops-guide-firewall-rule-vmwaas}

Add a firewall rule to allow the traffic from the internal network to the service network. Before you add the firewall rule, you must define the IP set.
1. Define the IP set.
   1. Log in to the VMware Cloud Director tenant portal.
   2. From the main page under **All Edge Gateways**, click the virtual data center where you want to add the firewall rule.
   3. In the left pane under **IP Management**, click **IP Allocations**. Make note of the external allocated IPs.
   4. In the left pane under **Security**, click **IP Sets**. Then, click **NEW**.
   5. In the **Edit IP Set** window, enter the name of the IP set and add the IP address to use. Then, click **Save**.
2. Add the firewall rule.
   1. Under the **Services** section, click the **Firewall** tab and click **EDIT RULES**. Then, click **NEW ON TOP** to add a firewall rule.
   2. Add the IP addresses or range from your internal network to the **Source** field.
   3. Add the IP set in the **Destination** field.
   4. Select `Allow` in the **Action** field.
   5. Click **Save**.

After the previous configuration is completed, you can use the supported {{site.data.keyword.cloud_notm}} services on the VMs in your virtual data center.

If your vApp or VM is deployed from the IBM templates that are provided in the public catalog, the services are already configured on the VM. To enable the connection, you must complete the previous steps in **Adding the NAT rule** and **Adding the firewall rule**.

#### Creating a vApp Network for VMware Solutions Shared
{: #shared_vcd-ops-guide-vapp-network}

If not already completed, create a vApp containing at least two VMs. For more information, see [Working with vApps](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-AC48FB5E-4ADC-4835-AACE-B949B297A147.html){: external}.

1. From the tenant portal, click the **Menu** icon at the upper left of the page and select **Data Centers**.
2. From the main page under **Virtual Data Center**, click the virtual data center where you want to create the vApp network.
3. In the left pane under **Compute**, click **vApps**.
4. Click **Details** on the vApp that you want to add a vApp network to.
5. Click the **Network** tab, and click **New** in the **vApp Fencing** section.
6. Select **vApp Network**.
7. Complete the **Name** and **Gateway CIDR** fields. For example, `Web` and `192.168.33.1/24`.
8. (Optional) Provide the DNS information.
9. Leave the **Static IP Pools** section blank.
10. Set the slider to **Connect to an organization VDC network**.
11. Click **Add**.

For more information, see [Working with networks in a vApp](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FCBC791B-3183-4CD9-A194-856E98CC32D3.html).

#### Creating a vApp Network for {{site.data.keyword.vcf-aas}}
{: #shared_vcd-ops-guide-vapp-network-vmaas}

If not already completed, create a vApp containing at least two VMs. For more information, see [Working with vApps](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-AC48FB5E-4ADC-4835-AACE-B949B297A147.html){: external}.

1. From the tenant portal, click the **Menu** icon at the upper left of the page and select **Data Centers**.
2. From the main page under **Virtual Data Center**, click the virtual data center where you want to create the vApp network.
3. In the left pane under **Compute**, click **vApps**.
4. Click the vApp that you want to add a vApp network to.
5. Click the **Networks** tab, and click **NEW** in the **vApp Fencing** section.
6. On the **Add Network to** window, select **OrgVDC Network** and select the network name.
7. Click **Add**.

For more information, see [Working with networks in a vApp](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-FCBC791B-3183-4CD9-A194-856E98CC32D3.html).

## Configuring a private network endpoint
{: #shared_vcd-ops-guide-pne}

Every private network endpoint comes configured with one private network IP address that can be used to configure your virtual data center.

### Prerequisites for configuring a private network endpoint
{: #shared_vcd-ops-guide-pne-prereqs}

* Review [{{site.data.keyword.vcf-aas}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-aas-overview).
* You must have a running VM.
* The VM must be connected to a routed Organization virtual data center network. For more information, see [Creating a routed Organization virtual data center network](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-routed-organization) and [Connect the VMs to the network](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-connect-vm).
* You must have virtual routing and forwarding and service endpoints that are enabled on the account that the allow listed IP or subnet belong to. For more information, see [Enabling VRF and service endpoints](/docs/account?topic=account-vrf-service-endpoint).

### Collecting network IP addresses
{: #shared_vcd-ops-guide-pne-IPs}

Collect the service network and private network IP addresses to configure the firewall and DNAT rules.

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > {{site.data.keyword.vm-shared}}** from the left navigation pane.
2. In the **{{site.data.keyword.vm-shared}}** table, click the virtual data center to configure.
3. In the **Private Network Endpoint** section, collect the **Service network IP** address and **Private network IP** address.

### Configuring firewall rules for the VMware NSX Edge Services Gateway
{: #shared_vcd-ops-guide-pne-firewall-rules}

The firewall rule allows traffic from the private network IP to go through your Edge Service Gateway. You might need to repeat this process (steps 5 - 10) to allow different traffic to enter your virtual data center, depending on which ports and protocols you need to open up.

1. From the tenant portal, click **Data Centers**.
2. From the main page under **Virtual Data Center**, click the virtual data center where you want to configure the private network.
3. In the left pane under **Networking**, click **Edges**.
4. In the right pane, select the network and click **SERVICES**.
5. Click the **Firewall** tab and click **+** to add a firewall rule.
6. Add the private network IP that you collected from the {{site.data.keyword.cloud_notm}} virtual data center details page to the **Source** field.
7. Add the service network IP that you collected from the {{site.data.keyword.cloud_notm}} virtual data center details page to the **Destination** field.
8. Select the **Protocol** (TCP, UDP, or Any) and specify **ports** for the **Service** field.
9. Select **Accept** for the **Action** field.
10. Click **Save changes**.

For more information, see [Add an NSX data center for vSphere Edge Gateway firewall rule](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-97ADAF42-598B-44B2-80EF-8B215B743C78.html){: external}.

### Configuring DNAT rules for the NSX Edge Services Gateway
{: #shared_vcd-ops-guide-pne-dnat-rules}

A Destination NAT rule is necessary to allow traffic from a private network endpoint to the virtual data center.

1. From the **Edge Gateway Services** pane, click the **NAT** tab.
2. Under the **NAT44 Rules**, click **+ DNAT Rule**.
3. Find the name of the service network that is assigned for the service network interface from the **IP Addresses** table in the **Edge Gateway Settings** section. The format for the service network name is ``w<idx>-service<idx>``, for example, ``w02-service02``.
4. Click the **Applied On** arrow and select the **service network** interface.
5. Add the Service network IP to the **Original Source IP/Range**.
6. Click **Protocol** and select the port type for inbound traffic.
7. For the ``TCP`` or ``UDP`` protocols, click **Original Port** and enter the port range that you want to allow. Skip this step for the ``Any`` protocol.
8. The **Translated Source IP/Range** is the IP addresses of the VM connected to the routed Organization virtual data center.
9. For the ``TCP`` or ``UDP`` protocols, select the **Translated Port** to route the traffic to. Skip this step for the ``Any`` protocol.
10. Skip the **ICMP Type** and optionally enter a description. Click **KEEP**.
11. Click **Save changes**.

### Validating the private network endpoint connection
{: #shared_vcd-ops-guide-pne-validate}

To validate the private network endpoint connection, log in to the virtual server instance resource in your {{site.data.keyword.cloud_notm}} infrastructure account. To connect to a VM in the virtual data center, use SSH, RDP, or Ping (if ICMP is enabled).

Ensure that the Organization virtual data center network type is `routed`.
{: important}

For more information about creating a private network endpoint, see [Order a private network endpoint to connect your IBM account to your {{site.data.keyword.vm-shared}} virtual data center](https://mlwiles.github.io/vmwaresolutions/vcd/order-pne/){: external}. An example of a successful configuration is also provided.

## Using Network High Availability
{: #shared_vcd-ops-guide-network-ha}

Use Network High Availability to anchor your VMware Cloud Director network in two data centers.

You must access data center groups to use the Network High Availability feature. A data center group acts as a cross-virtual data center router that provides the following.
* Centralized networking administration
* Configuration for multiple Egress points in multiple virtual data centers
* East-west traffic between all networks within the group

For more information, see [Managing organization virtual data center networks](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-B208CDD2-5D46-4841-8F3C-BED9E4F27F07.html){: external}.

The data center groups do not require physical separation. However, for optimal redundancy, the recommended implementation of a data center group has the Egress points in two different physical data centers, for example, **Dallas 10** and **Dallas 12**.

### Procedure to create a local data center group
{: #shared_vcd-ops-guide-network-ha-create}

1. From the main navigation bar of the {{site.data.keyword.vmwaresolutions_short}} console, select **Data Centers > Data Center Groups**, then click **New Data Center Group**.
2. Complete the configuration of the new data center group.
   1. On the **Name** tab, enter the name of the data center group and select **Create Local Group**. Click **NEXT**.
   2. On the **Network Pool** tab, select the network pool. Click **NEXT**.
   3. On the **Data Centers** tab, select the virtual data centers to include in the data center group. Click **NEXT**.
   4. On the **Review** tab, confirm your configuration and click **FINISH**.

The data center group is created and an NSX Distributed Logical Router (DLR) is associated to the group.

### Procedure to add an Egress point
{: #shared_vcd-ops-guide-network-ha-egress}

The NSX Edge Service Gateways (ESG) must have a free interface (vNIC) that is used to attach to the DLR. If the ESG does not have any available interfaces, the **Add Egress Point** or **Add StandBy Egress Point** task fails.
{: important}

1. From the main navigation bar of the {{site.data.keyword.vmwaresolutions_short}} console, select **Data Centers > Data Center Groups**, then click **Details** for the data center group.
2. On the **Network Topology** tab, click **Add Egress Point** or **Add Stand By Egress Point**.
3. Select one of the ESGs from the virtual data centers that were added and click **ADD**. The Egress point is created.

If the Egress points must change roles, **Swap Egress Points** is displayed instead of **Add Egress Point** or **Add Stand By Egress Point**.
{: note}

From the tenant portal, the BGP Configurations are modified. In the ESG settings for the active and stand-by Egress points, click **Routing > BGP**. Review the changes for **Enable BGP**, **Enable Graceful Restart**, and **Enable Default Originate**.

A new neighbor is created and managed. If **Local AS** was previously set to a value other than `65010`, it is overwritten. The new neighbor is the group that is created by using the DLR interfaces to each ESG. The network is `192.168.253.0/30` and it cannot be changed currently or the DCG feature does not work as described. The active ESG weight is `60` and the stand-by weight of `30`.

### Procedure to add a stretched network
{: #shared_vcd-ops-guide-network-ha-stretched}

Add a stretched network to use the cross-virtual data center networking.

1. From the main navigation bar of the {{site.data.keyword.vmwaresolutions_short}} console, select **Data Centers**.
2. On the **Stretched Networks** tab, click **ADD**.
3. For **New Stretched Network** enter a name, the gateway CIDR, and click **CREATE**. The new network is now available for BGP across the virtual data centers of the data center group.

You are now ready to put VMs on the cross-virtual data center network and build out your use case.

## Enabling VMware Chargeback
{: #shared_vcd-ops-guide-vrops-app}

The VMware Chargeback (formerly VMware Aria® Operations™ Tenant App for VMware Cloud Director) feature is enabled by default when your organization is provisioned. From the Cloud Director tenant portal, click **More > Operations Manager** to access VMware Chargeback.

If the **Operations Manager** option is not available in the **More** menu, open an IBM ServiceNow ticket, and submit a request to enable the VMware Chargeback feature in your organization.

After the VMware Chargeback feature is enabled for an organization, the users who are defined in the organization have access to it.

For more information, see [Using VMware Chargeback as a tenant](https://docs.vmware.com/en/Management-Packs-for-vRealize-Operations/8.10/vmware-chargeback-for-vcd-for-a-tenant/GUID-4D7030B6-AF73-464B-8FE8-75B879EE76B8.html){: external}.

The billing link in VMware Chargeback is disabled. All billing for {{site.data.keyword.vm-shared}} is processed through the VMware Solutions console.
{: note}

## Deleting the OpenID Connect configuration in your VMware Cloud Director Organization
{: #shared_vcd-ops-guide-delete-oidc}

You must delete all OpenID Connect (OIDC) users and imported groups with the OIDC type, then the OIDC provider before you can reset the IAM integration for a {{site.data.keyword.vm-shared}} instance site.

Single sign-on is available only when your site VMware Cloud Director Organization is integrated with IAM.
{: note}

1. From the VMware Cloud Director Console, click **SIGN IN WITH SINGLE SIGN-ON** to log in to the portal.
2. Click **Administration** on the top menu bar.
3. Under **Access Control** on the left navigation pane, click **Users**.
4. In the **Users** panel, select all OIDC type users and click **DELETE**.
5. Under **Access Control** on the left navigation pane, click **Groups**.
6. In the **Groups** panel, select all groups with the **OIDC** type and click **DELETE**.
7. Under **Identity Providers** on the left navigation pane, click **OIDC**.
8. In the **OpenID Connect** panel, click **DELETE**.

## Related links
{: #shared_vcd-ops-guide-related}

* [{{site.data.keyword.vm-shared}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [VMware Cloud Director](https://docs.vmware.com/en/VMware-Cloud-Director/10.5/VMware-Cloud-Director-Tenant-Guide/GUID-74C9E10D-9197-43B0-B469-126FFBCB5121.html){: external}
