---

copyright:

  years:  2023

lastupdated: "2023-09-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Planning the deployment
{: #veeam-cr-sag-planning}

Plan the deployment by capturing information for use in the subsequent steps. Select the planning tasks for the deployment environment that you intend to build:

* [Immutable backup plan](#veeam-cr-sag-planning-ib)
* [Isolated recovery environment plan](#veeam-cr-sag-planning-ire)

## Immutable backup planning
{: #veeam-cr-sag-planning-ib}

Capture the following details of the VMware vCenter Server® instance and Veeam® service instance:

| Parameter | Description |
|-----------|-------------|
| `<root_domain>` | The vCenter Server instance domain name. For example, `test.ibmcloud.local` |
| `<sub_domain>` | The vCenter Server instance subdomain name. For example, if the root domain is `test.ibmcloud.local`, then the subdomain is `test`. | 
| `<dc_code>` | The code for the data center in which the vCenter server instance is deployed into, such as DAL10. |
| `<public_vlan_number>` | The `Public VLAN` number can be obtained from the UI by browsing to the Resources > vCenter Server > Infrastructure page. |
| `<public_vlan_id>` | The ID can be found from the VLAN number and the {{site.data.keyword.cloud}} CLI. For example, for VLAN number `1344`, `ibmcloud sl vlan list` `awk '/1344/ { print "Public_VLAN_ID: " $1 }'`. |
| `<private_vlan_number>` | The Private VLAN number can be obtained from the UI by browsing to the Resources > vCenter Server > Infrastructure page. The `Secondary Private VLAN` number is not required. |
| `<private_vlan_id>` | The ID can be found from the VLAN number and the {{site.data.keyword.cloud_notm}} CLI. For example, for VLAN number `1607`, `ibmcloud sl vlan list` `awk '/1607/ { print "Private_VLAN_ID: " $1 }'` |
| `<private_subnet>` | The `Primary subnet for hosts and virtual server instances` on the `Private VLAN` can be obtained from the UI by browsing to the Resources > vCenter Server > Infrastructure page. |
| `<private_subnet_id>` | The ID can be found from the subnet identifier and the {{site.data.keyword.cloud_notm}} CLI. For example, for subnet `10.38.207.128`, `ibmcloud sl subnet list` `awk '/10.38.207.128/ { print "Private_Subnet_ID: " $1 }'`. |
| `<public_subnet>` | The `Primary subnet for hosts and virtual server instances` on the `Public VLAN`. |
| `<public_subnet_id>` | The ID can be found from the subnet identifier and the {{site.data.keyword.cloud_notm}} CLI. For example, for subnet `169.60.242.0`, `ibmcloud sl subnet list` `awk '/169.60.242.0/ { print "Public_Subnet_ID: " $1 }'`|
| `<addns_fqdn>` | The FQDN can be obtained from the UI by browsing to the Resources > vCenter Server > Summary page. |
| `<addns_1>` | The IP address of the first AD/DNS server can be obtained from the UI by browsing to the Resources > vCenter Server > Summary page. |
| `<addns_2>` | The IP address of the second AD/DNS server can be obtained from the UI by browsing to the Resources > vCenter Server > Summary page. |
| `<vbr_ip>` | The IP address of the Veeam Backup and Replication server. |
{: caption="Table 1. Capture parameters for Immutable backup planning" caption-side="bottom"}

Define the following parameters:

| Parameter | Description |
|-----------|-------------|
| `jmp_security_group_name` | The required name for the security group to protect the jump server. |
| `as_security_group_name` | The required name for the security group to protect the automation server. |
| `js_hostname` | The required jump server hostname. |
| `as_hostname` | The required automation server hostname. |
| `ansible_ip` | The IP address of the automation server. |
| `lhbr_hostname` | The required Linux® hardened repository server hostname. |
| `sa_veeam_cyber_admin_password` | A complex password used for the Veeam service account `sa-veeam-cyber-admin` account. |
| `your_username` | A username for the account on the automation server so that you can SSH to the server. |
| `timezone` | The time zone to be configured in the Linux hardened repository. For more information, see the [time zone catalog](http://manpages.ubuntu.com/manpages/focal/man3/DateTime::TimeZone::Catalog.3pm.html){: external}. |
| `lhbr_root_password` | This password is the {{site.data.keyword.cloud_notm}} supplied initial root password that is provided after provisioning of the Linux bare metal server. It is used to initially connect to the server for configuration and stored in the Ansible® vault file. |
| `sa_ansible_password` | A complex password that is stored in the Ansible vault file that is used for the `sa-ansible` service account on the Veeam backup server. |
| `immutability_period` | The required immutability period for the Linux Hardened repository. For example, `30` for 30 days. |
| `max_concurrent_jobs` | Specifies the maximum allowed number of concurrent tasks for the backup repository. For example, Veeam recommends one task = one CPU core and 2 GB RAM per core. For more information, see [Task limitation for backup repositories](https://helpcenter.veeam.com/docs/backup/vsphere/limiting_tasks.html?ver=120){: external}. |
{: caption="Table 2. Define parameters for Immutable backup planning" caption-side="bottom"}

## Isolated recovery environment planning
{: #veeam-cr-sag-planning-ire}

The following information is needed for the isolated recovery environment planning:

| Parameter | Description |
|-----------|-------------|
| `<public_key>` | A public key for vSRX user. |
| `<vSRX_private_ip>` | The private IP of the vSRX that is reachable from the automation server. |
| `<proxy_1_ip>` | The IP address of the Veeam cyber-proxies in the production environment. Multiple proxies are possible. |
| `<lhbr_ip>` | The IP address of the Linux hardened repository server. |
| `<vcsa_fqdn>` | The FQDN or IP address of the vCenter appliance in the production environment. |
| `<vcsa_user>` | The username of the account in vCenter appliance in the production environment. |
| `<vcsa_user_password>` | The password for the `vcsa_user`. |
| `<sub_domain>` | The subdomain of the root domain of the vCenter appliance in the production environment. |
{: caption="Table 3. Parameters for Isolated recovery environment planning" caption-side="bottom"}

## Related links
{: #veeam-cr-sag-planning-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions/?topic=vmwaresolutions-veeam-cr-sa-overview)
