---

copyright:

  years: 2016, 2024

lastupdated: "2024-07-23"

keywords: user IDs vCenter, PSC user, user ID service

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# IBM user IDs
{: #audit_user_ids}

{{site.data.keyword.vmwaresolutions_full}} maintains a set of users in your account for use by {{site.data.keyword.cloud_notm}} automation when you run operations such as adding hosts, clusters, or storage to your provisioned instance. Users in your account can also be used for installation and configuration of services by {{site.data.keyword.cloud_notm}} services automation. Review the following sections for {{site.data.keyword.cloud_notm}} automation user IDs.

VMware instance operations fail if IBM user IDs are deleted, disabled, or if their passwords are changed.
{: attention}

## vCenter Server user IDs
{: #audit_user_ids-vcenter-psc}

{{site.data.keyword.vmwaresolutions_short}} uses the following user IDs to add an identity source, which is embedded by default, into VMware vCenter Server®.

| User     | User ID      | Method | Description |
|:---------|:-------------|:-------|:------------|
| IBM      | `root`       | SSH    | Used for VMware configuration such as setting up VMware High Availability and creating distributed switches. Used post deployment to pair primary and secondary {{site.data.keyword.vcf-auto}} instances. |
| IBM      | `automation@root_domain`  \n (Active Directory™ user) | HTTP | Used post deployment to add and remove hosts and clusters and to deploy and configure virtual machines (VMs) for services. |
| Customer | `administrator@vsphere.local` | HTTP | Created for customer use only. |
{: caption="Table 1. vCenter Server and Platform Services Controller user IDs" caption-side="bottom"}

HTTP is used for vCenter Server setup, configuration, and VMware operations such as adding hosts, clusters, or storage for vCenter management of resources.
{: note}

## NSX Manager user IDs
{: #audit_user_ids-nsx-mgr}

| User     | User ID      | Description |
|:---------|:-------------|:------------|
| IBM      | `automation@root_domain`  \n (Active Directory user) | Used post deployment to manage NSX VTEP IP addresses, manage host, and cluster configuration when you add and remove hosts and clusters. Also used to manage ESG configuration for services that require public network access for licensing, activation, or usage reporting. |
| Customer | `admin` | Created for customer use only. |
{: caption="Table 2. NSX Manager user IDs" caption-side="bottom"}

## ESXi host user IDs
{: #audit_user_ids-esxi}

| User     | User ID      | Description |
|:---------|:-------------|:------------|
| IBM      | `ic4vroot` - deprecated  | Used for existing deployments. |
{: caption="Table 3. ESXi host user IDs" caption-side="bottom"}

## Microsoft Active Directory user IDs
{: #audit_user_ids-ad}

| User     | User ID       | Description |
|:---------|:------------- |:------------|
| IBM      | `automation`  | Used to add a host, add a VM for service, and set up Active Directory™ and DNS entries. |
| Customer | `administrator` | Created for customer use only. |
{: caption="Table 4. Microsoft® Active Directory user IDs" caption-side="bottom"}

## Service user IDs
{: #audit_user_ids-services}

| User ID                                    | Description |
|:------------------------------------------ |:----------- |
| `prod-BigIP-dynamicID-@domainName` | Used for installation and configuration of the F5® service. |
| `prod-Caveonix-dynamicID-@domainName` | Used for installation and configuration of the Caveonix RiskForesight™ service. |
| `prod-Fortigate-dynamicID-@domainName` | Used for installation and configuration of the FortiGate® Security Appliance service. This service is deprecated. |
| `prod-FortigateVM-dynamicID-@domainName` | Used for installation and configuration of the FortiGate Virtual Appliance service. |
| `prod-HyTrustCC-shortID-@domainName` | Used for the configuration of the Entrust CloudControl™ service. |
| `prod-HyTrustDC-shortID-@domainName` | Used for the configuration of the Entrust DataControl® service. |
| `prod-HyTrustKC-shortID-@domainName` | Used for the configuration of the Entrust KeyControl™ service. |
| `prod-KMIPAdapter-dynamicID-@domainName` | Used for installation and configuration of the KMIP™ for VMware service. |
| `prod-ICP-dynamicID-@domainName` | Used for installation and configuration of the {{site.data.keyword.cloud_notm}} Private Hosted service. |
| `prod-SPPlus-dynamicID-@domainName` | Used for installation and configuration of the IBM Spectrum® Protect Plus service. |
| `prod-Veeam-dynamicID-@domainName` | Used for installation and configuration of the Veeam® service. |
| `prod-HCX-dynamicID-@domainName` | Used for installation and configuration of the VMware HCX™ service. |
| `prod-Zerto-dynamicID-@domainName` | Used for installation and configuration of the Zerto service. |
{: caption="Table 5. Service user IDs" caption-side="bottom"}
{: #audit_user_ids-services-table}

In the [previous table](#audit_user_ids-services-table), the following notations are used:
* `dynamicID` The 8 - 10 characters that generated dynamically during the service installation.
* `shortID` The 5 characters that generated dynamically during the service installation.
* `domainName` The domain name of your instance.

## Related links
{: #audit_user_ids-related}

* [Considerations about changing vCenter Server artifacts](/docs/vmwaresolutions?topic=vmwaresolutions-vcenter_chg_impact#vcenter_chg_impact-automation-id)
* [Auditing events for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-at-events)
