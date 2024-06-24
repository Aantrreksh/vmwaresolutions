---

copyright:

  years:  2023, 2024

lastupdated: "2024-06-05"

keywords: vmware cloud editions, order vmware cloud editions, order vmware cloud editions on IBM Cloud, vmware cloud foundation

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-ordering}

{{site.data.keyword.vcf-vpc}} offers flexible options to help you deploy VMware's software-defined data center, {{site.data.keyword.vcf-vpc-short}}, into your {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) environment.

## Requirements for {{site.data.keyword.vcf-vpc-short}} instances
{: #vpc-vcf-ordering-req}

Review the information in [Requirements for {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-order-req).

## Components and subscriptions
{: #vpc-vcf-ordering-subscriptions}

For more information about the components that are provided, see [Supported {{site.data.keyword.vcf-vpc-short}} products in {{site.data.keyword.vpc_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw#vpc-vcf-ovw-supported-edition).

### On-demand subscription
{: #vpc-vcf-ordering-ondemand}

For the on-demand offering, you are billed hourly based on your {{site.data.keyword.vpc_short}} bare metal server capacity usage.

### 1-year and 3-year subscriptions
{: #vpc-vcf-ordering-1-year}

For the 1-year or 3-year subscription, use [this form](https://www.ibm.com/account/reg/us-en/subscribe?formid=MAIL-platformvmware) to contact an IBM representative for product pricing, discounts, or more information.

### VMware Cloud Foundation version
{: #vpc-vcf-ordering-version}

VMware Cloud Foundation™ 5.1.1 is installed on your {{site.data.keyword.vcf-vpc-short}} instance. For more information, see [Software BOM for {{site.data.keyword.vcf-vpc-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw-bom#vpc-vcf-ovw-bom-software).

### Architecture
{: #vpc-vcf-ordering-archi}

For the **Consolidated** architecture, instances are deployed with a management domain. To deploy a workload domain with your instance, select the **Standard** architecture.

For more information, see [Supported {{site.data.keyword.vcf-vpc-short}} architectures in {{site.data.keyword.vpc_short}}](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw#vpc-vcf-ovw-supported-arch).

## Deployment
{: #vpc-vcf-ordering-deployment}

Review the deployment settings.

### Instance name
{: #vpc-vcf-ordering-instance-name}

The instance name is preset to **myvcf**. The instance name is also used as the Schematics workspace name, which is created during deployment.

You can also specify an instance name that meets the following requirements:
* Only alphanumeric, hyphen (-), and underscore (_) characters are allowed.
* The maximum length of the instance name is 64 characters.

### Resource name prefix
{: #vpc-vcf-ordering-resource-prefix}

The prefix for all names of the resources to be created in the {{site.data.keyword.vpc_short}} infrastructure that your {{site.data.keyword.vcf-vpc-short}} instance is based on. By default, the prefix **vcf** is added.

You can also specify a resource name prefix that meets the following requirements:
* Only alphanumeric and hyphen (-) characters are allowed.
* The maximum length of the resource name prefix is 10 characters.
* Must start with an alphabetic character and end with an alphanumeric character.

### Resource group
{: #vpc-vcf-ordering-resource-group}

Use resource groups to organize the resources in your account for access control and billing purposes. By default, **Create new** is selected and a **vcf-_xxx_-rg** resource group is created in your account. Ensure that you have permission to create a new resource group in the current account.

You can also select other resource groups according to your needs. You must have permission to add resources to the selected resource group. If you don't have the required permission, contact the account owner to be assigned the Editor or Administrator role on a resource group in the account. For more information, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).

The resource group that you select cannot be changed after the instance is created.
{: important}

### Tags
{: #vpc-vcf-ordering-tags}

The tags added to your new created resources in {{site.data.keyword.cloud_notm}}. For more information about how to use tags and tagging rules, see [Working with tags](/docs/account?topic=account-tag&interface=ui).

### Location
{: #vpc-vcf-ordering-location}

Locations are composed of regions (specific geographic areas) and zones (fault tolerant data centers within a region). Select the location where you want to deploy your instance. For the supported locations, see [{{site.data.keyword.cloud_notm}} region and zone availability for {{site.data.keyword.vcf-vpc-short}} deployment](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-plan#vpc-vcf-plan-region).

## Management domain
{: #vpc-vcf-ordering-mgmt-domain}

The management domain is the first domain that is deployed in a {{site.data.keyword.vcf-vpc-short}} environment. The management domain contains the infrastructure components that are required to manage the entire {{site.data.keyword.vcf-vpc-short}} deployment.

### Root domain name
{: #vpc-vcf-ordering-dns-root-domain}

By default, an {{site.data.keyword.cloud_notm}} DNS service is ordered and a DNS zone and DNS records are created for all VMware components in the selected {{site.data.keyword.vpc_short}} zone.
The root domain name must meet the following requirements:
   * The domain name must consist of three or more strings that are separated by a period (.) with a maximum of 50 characters.
   * The first string (NetBIOS name) must start with a lowercase alphabetic character and end with a lowercase alphabetic or numeric character. It must not exceed 15 characters.
   * All strings, except for the last one, can contain only lowercase alphabetic, numeric, and hyphen (-) characters.
   * No consecutive hyphens are allowed.
   * The last string can contain only lowercase alphabetic characters.
   * The length of the last string must be 2-24 characters.

### Management host profile
{: #vpc-vcf-ordering-mgmt-profile}

The bare metal server profile that is used by the hosts in the management domain. For the supported profiles, see [{{site.data.keyword.cloud_notm}} region and zone availability for {{site.data.keyword.vcf-vpc-short}} deployment](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-plan#vpc-vcf-plan-region).

### Management host list
{: #vpc-vcf-ordering-mgmt-host-list}

Typically, the management domain is deployed as a cluster of vSphere ESXi hosts, which are managed by a {{site.data.keyword.vcf-vpc-short}} instance.

#### Number of management hosts
{: #vpc-vcf-ordering-mgmt-host-number}

The management domain requires a minimum of 4 hosts and it allows a maximum of 25 hosts.

The quota for bare metal servers is set to 25 per account by default. To increase the quota for a resource, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: note}

#### Hostname suffix and name
{: #vpc-vcf-ordering-mgmt-host-suffix}

The hostname suffix is the bare metal server name suffix. The hostname suffix can contain only lowercase alphanumeric characters and can have a maximum length of 6. Ensure that the suffix of each bare metal server is unique. The bare metal server hostname is preset to **_resource name prefix_-mgmt-esx-_host name suffix_**.

### Application Virtual Network (AVN)
{: #vpc-vcf-ordering-mgmt-avn}

An Application Virtual Network (AVN) is a software-defined networking concept based on NSX-T Data Center that allows the hosting of management applications on NSX segments. It must be deployed before you can deploy Aria Suite components or implement the Identity and Access Management for {{site.data.keyword.vcf-vpc-short}} validated solution. For more information, see [Deploying Application Virtual Networks in {{site.data.keyword.vcf-vpc-short}}](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-59E5BEE3-B157-426D-A40C-F21171586863.html){: external}.

#### VCF AVN local region network
{: #vpc-vcf-ordering-mgmt-avn-local}

Two NSX segments (local region and X region) on the NSX Edge cluster are deployed in the default management vSphere cluster. Those NSX segments are used when you deploy the Aria Suite products. Local region segments are local instance NSX segments. {{site.data.keyword.vpc_short}} custom routes are created for it pointing to the Tier 0 gateway of the management domain. By default, the route destination is `172.27.16.0/24`.

#### VCF AVN X region network
{: #vpc-vcf-ordering-mgmt-avn-x}

X region segments are cross-instance NSX segments. {{site.data.keyword.vpc_short}} custom routes are created for it pointing to the Tier 0 gateway of the management domain. By default, the destination of the route is `172.27.17.0/24`.

### Management overlay networks
{: #vpc-vcf-ordering-mgmt-overlay}

Management overlay networks are subnets that are allocated in the NSX overlay on the management domain. {{site.data.keyword.vpc_short}} custom routes are created for these subnets that point to the Tier 0 gateway of the management domain. By default, the destination of the route is `172.16.0.0/16`.

### Public floating IPs
{: #vpc-vcf-ordering-mgmt-floating-ips}

The number of public floating IP addresses you want to reserve for the management domain. After the floating IP addresses are ordered, they are associated with the first Bare Metal Server.

### Optional management domain settings
{: #vpc-vcf-ordering-mgmt-optional}

With these settings, you can configure your management domain in a more flexible way based on your requirements.

#### VCF appliance sizing
{: #vpc-vcf-ordering-mgmt-vcf-appliance}

Review the VCF appliance sizing settings.

##### Management vCenter VM size
{: #vpc-vcf-ordering-mgmt-vcf-vc-vm}

The size of the vCenter Server appliance deployed in the management domain, which determines the number of CPUs and the amount of memory of the appliance. By default, the vCenter Server appliance in the management domain is deployed in small size. For more information, see [Deployment model for vCenter Server for the management domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-management-domain-design/GUID-D635D474-D4E9-4743-A83B-84957C9B3FF0.html){: external}.

##### Management vCenter storage size
{: #vpc-vcf-ordering-mgmt-vcf-vc-storage}

When you deploy the vCenter Server appliance, you must determine the required storage according to the size of the environment, the storage size, and the disk provisioning mode. For more information, see [Deployment model for vCenter Server for the management domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-management-domain-design/GUID-D635D474-D4E9-4743-A83B-84957C9B3FF0.html){: external}.

##### Management NSX-T size
{: #vpc-vcf-ordering-mgmt-vcf-nsxt-vm}

A highly available NSX Global Manager instance is deployed in the {{site.data.keyword.vcf-vpc-short}} location instance. You also select an NSX Global Manager appliance size according to the number of anticipated objects that are required to run the management components of the private cloud. For more information, see [Deployment model for NSX Global Manager for the management domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-management-domain-design/GUID-3345887C-649D-4269-8DDA-9BD6F12505EE.html){: external}.

#### VCF deployment
{: #vpc-vcf-ordering-mgmt-vcf-deployment}

Review the VCF deployment settings.

##### VCF data center name
{: #vpc-vcf-ordering-mgmt-vcf-dc-name}

The data center name in your {{site.data.keyword.vcf-vpc-short}} instance. The default value is `dc01`. The {{site.data.keyword.vcf-vpc-short}} data center name can contain only alphanumeric characters, must start with a letter, and can have a maximum length of 10 characters.

#### Management domain backup
{: #vpc-vcf-ordering-mgmt-domain-backup}

To enable the virtual server for backing up SDDC Manager, vCenter Server, and NSX Manager, toggle the **Backup server** switch on.

##### SSH keys
{: #vpc-vcf-ordering-mgmt-ssh-keys}

You can choose existing SSH keys from the list or create a new one by clicking the **Create SSH key** button. After creating it, refresh the list to see the new SSH key. For more information about VCF backup, see [Backup and restore of VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/5.1/vcf-admin/GUID-F8634D37-FA26-40DF-A135-62D0265DA4FA.html){: external}.

## Workload domain
{: #vpc-vcf-ordering-wl-vcf}

A workload domain is a logical construct that represents a set of resources that are dedicated to a specific application or set of applications. Each Workload Domain is deployed as a separate vSphere cluster within the {{site.data.keyword.vcf-vpc-short}} environment and can be customized to meet the specific needs of the applications that are deployed. Workload Domains can be used to separate workloads based on characteristics such as security, compliance, performance, or management requirements.

The workload domain is created when you select the {{site.data.keyword.vcf-vpc-short}} Standard architecture, and it requires a minimum of 3 hosts.
{: important}

### Workload host profile
{: #vpc-vcf-ordering-wl-profile}

The bare metal server profile that is used by the hosts in the workload domain. For the supported profiles, see [{{site.data.keyword.cloud_notm}} region and zone availability for {{site.data.keyword.vcf-vpc-short}} deployment](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-plan#vpc-vcf-plan-region).

### Workload host list
{: #vpc-vcf-ordering-wl-host-list}

The workload domain is deployed as a cluster of vSphere ESXi hosts, which are managed by a {{site.data.keyword.vcf-vpc-short}} instance.

#### Number of workload hosts
{: #vpc-vcf-ordering-wl-host-number}

The workload domain requires a minimum of 3 hosts and can have a maximum of 25 hosts.

The quota for bare metal servers is 25 per account by default. To increase the quota for a resource, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: note}

#### Host name suffix and name
{: #vpc-vcf-ordering-wl-host-suffix}

Bare metal server name suffixes. By default, the bare metal server hostname is **_resource name prefix_-wl-esx-_host name suffix_**.

The hostname suffix can contain only lowercase alphanumeric characters and can have a maximum length of 10 characters. Ensure that the suffix of each bare metal server is unique.

### Workload overlay networks
{: #vpc-vcf-ordering-wl-overlay}

Workload overlay networks are subnets that are allocated in the NSX overlay on the workload domain. {{site.data.keyword.vpc_short}} custom routes are created for these subnets pointing to the Tier 0 gateway of the workload domain. By default, the destination of the route is `172.17.0.0/16`.

### Public floating IPs
{: #vpc-vcf-ordering-wl-floating-ips}

The number of public floating IP addresses that you want to reserve for the workload domain. After the floating IP addresses are ordered, they are associated with the first Bare Metal Server.

### Optional workload domain settings
{: #vpc-vcf-ordering-wl-optional}

With these settings, you can configure your workload domain in a more flexible way based on your requirements.

#### VCF appliance sizing
{: #vpc-vcf-ordering-wl-vcf-appliance}

Review the VCF appliance sizing settings.

##### Workload vCenter VM size
{: #vpc-vcf-ordering-wl-vcf-vc-vm}

The size of the vCenter Server appliance that is deployed in the workload domain, which determines the number of CPUs and the amount of memory of the appliance. By default, the vCenter Server appliance in the workload domain is deployed in small size. For more information, see [Deployment model for vCenter Server for a Virtual Infrastructure workload domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-vi-workload-domain-design/GUID-CD8F5B55-AFB6-4AE3-A258-425E82147EF1.html){: external}.

##### Workload vCenter storage size
{: #vpc-vcf-ordering-wl-vcf-vc-storage}

When you deploy the vCenter Server appliance, you must determine the required storage according to the size of the environment, the storage size, and the disk provisioning mode. For more information, see [Deployment model for vCenter Server for a Virtual Infrastructure workload domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-vi-workload-domain-design/GUID-CD8F5B55-AFB6-4AE3-A258-425E82147EF1.html){: external}.

##### Workload NSX-T size
{: #vpc-vcf-ordering-wl-vcf-nsxt-vm}

A highly available NSX Global Manager instance is deployed in the {{site.data.keyword.vcf-vpc-short}} location instance. You can also select an NSX Global Manager appliance size according to the number of anticipated objects that are required to run the workload components of the private cloud. For more information, see [Deployment model for NSX Manager for a VI workload domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-vi-workload-domain-design/GUID-F7044DCA-6780-4C9B-8822-C9CA4382F5AA.html){: external}.

##### Workload NSX Edge VM size
{: #vpc-vcf-ordering-wl-nsx-edge-vm}

You can determine the size of the NSX Edge appliances for the VI workload domain according to the design objectives of your organization and aggregated requirements of the customer workloads of the SDDC. For more information, see [Deployment Model for the NSX Edge Nodes for a Virtual Infrastructure Workload Domain](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-vi-workload-domain-design/GUID-28FCCC3C-5B34-4EB0-9D2F-EFFE9C718E17.html){: external}.

## Network interface
{: #vpc-vcf-ordering-network}

Review the network interface settings.

### DNS records
{: #vpc-vcf-ordering-network-dns-records}

Additional DNS records to be created in your {{site.data.keyword.vpc_short}} for VMware components or the virtual machine (VM) that you want to deploy on {{site.data.keyword.vcf-vpc-short}} instance. For more information, see [Managing DNS records](/docs/dns-svcs?topic=dns-svcs-managing-dns-records&interface=ui).

#### VPC zone prefix
{: #vpc-vcf-ordering-network-vpc-zone}

An address prefix that is assigned to the VMware components that are deployed in your selected {{site.data.keyword.vpc_short}} zone. This prefix helps organize and manage the IP address space for the VMware components within the {{site.data.keyword.vpc_short}} zone. It is recommended to use a `/22` prefix for approximately 120 hosts or a `/23` prefix for approximately 60 hosts. The value is preset to `10.100.0.0/22`.

#### VPC zone prefix Tier 0 uplinks
{: #vpc-vcf-ordering-network-vpc-zone-t0}

The NSX-T uplink address prefix for your selected {{site.data.keyword.vpc_short}} zone. The value is preset to `192.168.10.0/24`.

#### VPC name
{: #vpc-vcf-ordering-network-vpc-name}

The identifier used to define the name of the newly created {{site.data.keyword.vpc_short}}. The {{site.data.keyword.vpc_short}} name has the format `<resource name prefix>-<3-character random string>-<vpc name>`. The default value is `vpc`. This identifier can have only letters, numbers, and hyphen (-) characters, it must start with a letter, it cannot end with a hyphen, and can have a maximum length of 10 characters.

### Customer private routes
{: #vpc-vcf-ordering-network-priv-routes}

A list of private routes created on NSX-T Tier-0 gateway, which includes all private ones that are created for {{site.data.keyword.vcf-vpc-short}} components.

## Advanced integration settings
{: #vpc-vcf-ordering-adv-settings}

Review the advanced settings.

### Jump server
{: #vpc-vcf-ordering-adv-settings-jump}

Determines whether a Windows VM is created in your {{site.data.keyword.vpc_short}}. The Windows Server is configured with a public floating IP address to access the {{site.data.keyword.vpc_short}} internal network. For security considerations, the Windows VM is not created by default.

### IAM access group
{: #vpc-vcf-ordering-adv-settings-iam}

Determine whether to create an {{site.data.keyword.cloud_notm}} Access Group with an access policy for granting access to the resources deployed in your selected resource group. By default, it will not create the access group and access policy, but you can create them after the deployment. For more information about {{site.data.keyword.cloud_notm}} Access Group, see [Assigning access to resources by using access groups](/docs/account?topic=account-access-getstarted).

### Observability
{: #vpc-vcf-ordering-adv-settings-log}

For {{site.data.keyword.vcf-vpc-short}} deployment, you can determine whether to use {{site.data.keyword.la_full}} with 7-day pricing plan for viewing the logs of {{site.data.keyword.vcf-vpc-short}} deployment. If you want to view logging of {{site.data.keyword.vcf-vpc-short}} deployment with your existing {{site.data.keyword.la_full_notm}} instance, you can configure the instance ingestion key, then the log is populated to your existing instance. By default, the {{site.data.keyword.la_short}} service is not ordered. For more information about {{site.data.keyword.la_short}} and its pricing plans, see [Getting started with {{site.data.keyword.la_short}}](/docs/log-analysis?topic=log-analysis-getting-started) and [Service plans](/docs/log-analysis?topic=log-analysis-service_plans).

## Procedure to order {{site.data.keyword.vcf-vpc-short}} instances on {{site.data.keyword.vpc_short}}
{: #vpc-vcf-ordering-procedure}



1. In the VMware Solutions console, click the **VMware Cloud Foundation (VCF) for VPC** card in the **Create a resource** section. {: #step-1}
1. On the **Create** tab, review the software components included by clicking **View components**.
1. Choose the subscription type.
1. Select the {{site.data.keyword.vcf-vpc-short}} architecture.

1. Specify the **Deployment** settings.
   1. Enter the instance name and the resource name prefix.
   1. Keep the default value of the resource group or select an existing resource group from the list.
   1. Enter any tags that you might want.
   1. Select the location, including geography, region, and zone.

1. Specify the **Management domain** settings.
   1. Specify the root domain name.
   1. Select the {{site.data.keyword.vpc_short}} bare metal profile for hosts in the management domain.
   1. Specify the number of bare metal servers.
   1. Specify the hostname suffix of each host.
   1. Specify the {{site.data.keyword.vpc_short}} routes for NSX-T AVN networks.
   1. Specify the {{site.data.keyword.vpc_short}} routes for NSX overlay network in the management domain.
   1. Specify the number of public floating IP addresses.
   1. Specify the **Optional management domain settings**: the vCenter appliance size and storage size in the management domain and the NSX-T manager appliance size, the VCF data center name for the VCF deployment, and the backup server for the management domain backup.

1. Specify the **Workload domain** settings.

   The workload domain configuration applies only to the **Standard** architecture.
   {: note}

   1. Specify the workload domain name.
   1. Select the {{site.data.keyword.vpc_short}} bare metal profile for hosts in the workload domain.
   1. Specify the number of bare metal servers.
   1. Specify the hostname suffix of each host.
   1. Specify the {{site.data.keyword.vpc_short}} routes for NSX overlay network in the workload domain.
   1. Specify the number of public floating IP addresses.
   1. Specify the **Optional workload domain settings**: the vCenter appliance size and storage size in the workload domain and the NSX-T manager appliance size.

1. Specify the **Network interface** settings.
   1. Enter the additional **DNS records** for the Aria Suite components or appliances that you want to deploy on {{site.data.keyword.vcf-vpc-short}}.
   1. Enter the {{site.data.keyword.vpc_short}} zone prefix and the {{site.data.keyword.vpc_short}} zone prefix Tier 0 uplinks.
   1. Enter the identifier for the newly created {{site.data.keyword.vpc_short}}.
   1. Enter the private and public routes that you want to create in {{site.data.keyword.vpc_short}}.

1. Specify the **Advanced integration settings**.
   1. Specify whether you want to create a Windows VM.
   1. Specify whether you want to create an IAM access group.
   1. Specify whether you want to deploy or use an existing {{site.data.keyword.la_short}} instance for the {{site.data.keyword.vcf-vpc-short}} deployment logs.

1. On the **Summary** pane, review the instance settings and the estimated price.
1. To place the order, ensure that the account to be charged is correct, review and accept the terms, and then click **Create**.

## Results after you placed an order
{: #vpc-vcf-ordering-procedure-result}

1. After you place the order, you are redirected to the {{site.data.keyword.vcf-vpc-short}} page and the status of the newly created instance is **Creating**.
2. After {{site.data.keyword.vpc_short}} resources and required cloud services are deployed, the {{site.data.keyword.vcf-vpc-short}} instance will be installed. When deployment is successful, the instance status is **Available**.
3. The deployment result is sent to the current user by email.

## Related links
{: #vpc-vcf-ordering-related}

* [Getting started: {{site.data.keyword.bplong_notm}}](/docs/schematics?topic=schematics-getting-started)
* [VPC network design](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-vpc-deployment)
* [Getting started with {{site.data.keyword.cloud_notm}} DNS Services](/docs/dns-svcs?topic=dns-svcs-getting-started&interface=ui)
* [Managing logging instances in the Observability UI](/docs/log-analysis?topic=log-analysis-observe)
* [{{site.data.keyword.vcf-vpc-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw)
