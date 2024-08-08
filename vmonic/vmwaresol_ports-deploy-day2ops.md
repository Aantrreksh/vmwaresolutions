---

copyright:

  years:  2020, 2024

lastupdated: "2024-08-08"

keywords: VLAN ports, vmware solutions ports, ports usage vmware solutions

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ports that are used for deployment and Day 2 operations
{: #vmwaresol_ports-deploy-day2ops}

The following table provides information about the ports for deployment and Day 2 operations. For more information about the ports that are used by the add-on services, see [Ports for services](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-services).

Review the following information about the ports described in the [table](#vmwaresol_ports-deploy-day2ops-table):

* Windows® Active Directory™ has two options: single Windows Virtual Service Instance (VSI) and two HA dedicated Windows Server virtual machines (VMs). For single Windows VSI, the VSI is in the primary subnet. For Windows Server VMs, the VMs are in the [infrastructure VMs](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-vlans-subnets) subnet.
* {{site.data.keyword.cloud}} infrastructure services network subnets vary from data center to data center. For more information, see [{{site.data.keyword.cloud_notm}} IP ranges](/docs/cloud-infrastructure?topic=cloud-infrastructure-ibm-cloud-ip-ranges).
* Some Windows resources in your environment might use classic infrastructure services in Dallas.
* {{site.data.keyword.cloud_notm}} endpoint service network includes `166.8.0.0/14`.
* IBM CloudDriver is an ephemeral VSI that is deployed by the {{site.data.keyword.cloud_notm}} automation to configure your instance. While IBM CloudDriver is being bootstrapped, it uses an ephemeral primary IP address. However, after bootstrapping, it uses a predictable portable IP address that you can find on your instance details page. For more information, see [IBM CloudDriver](/docs/vmwaresolutions?topic=vmwaresolutions-design_infrastructuremgmt#design_infrastructuremgmt-cloud-driver).
* Infrastructure VMs refer to the private portable subnet allocated for use by vCenter, NSX manager, the cloud driver
* Depending on your mode of deployment, your Windows Active Directory domain controllers can be VSIs on a primary subnet, or VMs on a portable subnet.

For more information about {{site.data.keyword.redhat_openshift_full}} (OCP) networking, see [About the OpenShift SDN network plugin](https://docs.openshift.com/container-platform/4.14/networking/openshift_sdn/about-openshift-sdn.html){: external}.



| Source | Subnet, IP range | Target | Subnet, IP range | Port | Protocol | Purpose | Service |
|:------ |:---------------- |:------ |:---------------- |:---- |:-------- |:------- |:------- |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} Service - Cloud Object Storage \n `10.1.129.0/24`[^vssreqa] | {{site.data.keyword.cloud_notm}} infrastructure services network | 443 | TCP | Use {{site.data.keyword.cloud_notm}} Object Storage service | HTTPS |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} Service - RabbitMQ `166.9.59.6` \n `166.9.90.7` \n `166.9.58.162` \n {{site.data.keyword.cloud_notm}} Service - {{site.data.keyword.la_short}}[^vssreqb] | {{site.data.keyword.cloud_notm}} endpoint service network | 443, 30560 | TCP | Use {{site.data.keyword.cloud_notm}} RabbitMQ and {{site.data.keyword.la_short}} services | |
| IBM CloudDriver | Private primary subnet | vCenter Server | Infrastructure VMs | | ICMP | Install and configure vCenter Server | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | vCenter Server | Infrastructure VMs | 22 | TCP | Set up and configure vCenter Server | SSH |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | vCenter Server | Infrastructure VMs | 443 | TCP | Install and configure vCenter Server and cluster | SSH |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | vCenter Server | Infrastructure VMs | 9443 | TCP | Install and configure vCenter Server and cluster | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | vCenter Server | Infrastructure VMs | 5489 | TCP | Install and configure vCenter Server and cluster | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | ESXi™ host | Private primary subnet | 22 | TCP | Set up, configure, and apply patches to ESXi host | SSH |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | ESXi vMotion | vMotion traffic | | ICMP | Set up ESXi network | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | ESXi vSAN™ | vSAN traffic | | ICMP | Set up ESXi network | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | ESXi shared storage | Shared storage traffic | | ICMP | Set up ESXi network | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | Customer edge private | Customer edge gateway private | | ICMP | Set up NSX edge network | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | Windows Active Directory | Private primary subnet (for Windows VSI)/ \n Infrastructure VMs (for Windows VMs) | 5986 | TCP | Set up and configure Windows Active Directory and DNS | |
| IBM CloudDriver | Private primary subnet | NSX Manager | Infrastructure VMs | | ICMP | Install and set up NSX Manager | |
| IBM CloudDriver | Private primary subnet | NSX Manager | Infrastructure VMs | 443 | TCP | Set up and configure NSX Manager | HTTPS |
| IBM CloudDriver | Private primary subnet | NSX Manager | Infrastructure VMs | 80 | TCP | Set up and configure NSX Manager | HTTP |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure provisioning API \n `10.0.80.0/25` | {{site.data.keyword.cloud_notm}} infrastructure services network | 443 | TCP | Order and provision {{site.data.keyword.cloud_notm}} infrastructure resources | HTTPS |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure DNS service \n `10.0.80.11` \n `10.0.80.12` | {{site.data.keyword.cloud_notm}} infrastructure services network | 53 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure DNS service | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure NTP service. | {{site.data.keyword.cloud_notm}} infrastructure services network. For more information, see [NTP overview](/docs/cloud-infrastructure?topic=cloud-infrastructure-ntp-service-overview). | 123 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure NTP service | |
| IBM CloudDriver | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure endurance storage | {{site.data.keyword.cloud_notm}} infrastructure services network | Any | ICMP and TCP | Set up endurance storage for ESXi host | |
| Windows Active Directory | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure DNS service \n `10.0.80.11` \n `10.0.80.12` | {{site.data.keyword.cloud_notm}} infrastructure services network | 53 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure DNS service | |
| Windows Active Directory | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure NTP service | {{site.data.keyword.cloud_notm}} infrastructure services network | 123 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure NTP service | |
| Windows Active Directory | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure WSUS service | {{site.data.keyword.cloud_notm}} infrastructure services network | 80 | TCP | Use {{site.data.keyword.cloud_notm}} infrastructure WSUS service | HTTP |
| Windows Active Directory | Private primary subnet \n Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure Windows KMS service | {{site.data.keyword.cloud_notm}} infrastructure services network | 1688 | TCP | Use {{site.data.keyword.cloud_notm}} infrastructure Windows KMS service | |
| ESXi host | Private primary subnet | {{site.data.keyword.cloud_notm}} infrastructure NTP service | {{site.data.keyword.cloud_notm}} infrastructure services network | 123 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure NTP service | |
| vCenter Server | Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure NTP service | {{site.data.keyword.cloud_notm}} infrastructure services network | 123 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure NTP service | |
| NSX Manager | Infrastructure VMs | {{site.data.keyword.cloud_notm}} infrastructure NTP service | {{site.data.keyword.cloud_notm}} infrastructure services network | 123 | UDP | Use {{site.data.keyword.cloud_notm}} infrastructure NTP service | |
| NSX Manager | Infrastructure VMs | TEP subnet | TEP traffic | 443 |  |  |  |
| NSX Manager | Infrastructure VMs | Customer edge subnet | Customer edge private traffic | 443 |  |  |  |
| ESXi host shared storage | ESXi shared storage | {{site.data.keyword.cloud_notm}} infrastructure endurance storage | {{site.data.keyword.cloud_notm}} infrastructure services network | 111, 635, and 2049 | TCP and UDP | Use {{site.data.keyword.cloud_notm}} infrastructure endurance storage | |
| IBM CloudDriver \n Windows Active Directory (VSI) | Private primary subnet | {{site.data.keyword.cloud_notm}} infrastructure engine | {{site.data.keyword.cloud_notm}} infrastructure services network | 80 | TCP | Provision IBM CloudDriver and Windows Active Directory (VSI) | |
| {{site.data.keyword.cloud_notm}} infrastructure engine | {{site.data.keyword.cloud_notm}} infrastructure services network | IBM CloudDriver \n Windows Active Directory (VSI) | Private primary subnet | Any | TCP and UDP | Provision IBM CloudDriver and Windows Active Directory (VSI) |
| {{site.data.keyword.cloud_notm}} infrastructure engine | {{site.data.keyword.cloud_notm}} infrastructure services network | ESXi host management0 | Private primary subnet | 623 | TCP and UDP | {{site.data.keyword.cloud_notm}} infrastructure IPMI |   |
| IBM CloudDriver |   | {{site.data.keyword.cloud_notm}} Service \n `10.221.68.39` |   | 514 | TCP |   |   |
| IBM CloudDriver |   | Internet |   |   |   |   | HTTPS |
{: caption="Table 1. Ports for deployment and Day 2 operations" caption-side="bottom"}
{: #vmwaresol_ports-deploy-day2ops-table}

[^vssreqa]: Flexible instances require access to Cloud Object Storage, RabbitMQ, and {{site.data.keyword.la_short}}.
[^vssreqb]: Flexible instances require access to Cloud Object Storage, RabbitMQ, and {{site.data.keyword.la_short}}.

## Related links
{: #vmwaresol_ports-deploy-day2ops-related}

* [Ports used by VMware components](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-vmwareuses)
