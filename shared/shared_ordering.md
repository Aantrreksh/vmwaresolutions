---

copyright:

  years:  2020, 2024

lastupdated: "2024-10-10"

keywords: shared order resource, order on demand shared, order on demand resources

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering virtual data centers
{: #shared_ordering}

{{site.data.content.shared-deprecated-note}}

{{site.data.keyword.vmwaresolutions_full}} Shared offers either a standardized or customizable deployment option of VMware® virtual data center environments. Choose the **On-demand** or **Reserved** option.

## System settings
{: #shared_ordering-sys-settings}

You must specify the following system settings when you order a {{site.data.keyword.vm-shared}} virtual data center.

### Pricing plans
{: #shared_ordering-pricing}

The pricing plan is based on your selection of **On-demand** or **Reserved**.

#### On-demand
{: #shared_ordering-pricing-on-demand}

For the On-demand offering, virtual data center virtual CPU (vCPU) and RAM are allocated as needed. The amount of time that the allocation takes depends on global usage of the virtual data center vCPU and RAM.

* The limits that are established for the amount of vCPU and RAM are maximum values that can be used at any time.
* You can increase and decrease the vCPU and RAM resources on a virtual data center later as required.
* The price is calculated hourly and it is based on the resource usage in the virtual data center.
* The amount of storage that can be allocated and used in the virtual data center is limited to 200 TB for each storage policy. Charges are calculated per hour and are based on GB of allocated storage.
* The amount of inbound and outbound public networking is unlimited. Public outbound bandwidth is charged per GB.

#### Reserved
{: #shared_ordering-pricing-reserved}

For the Reserved offering, the vCPU and RAM virtual data center reservations are pre-allocated and their availability is guaranteed.

* The price is calculated monthly for the full reservation and it is based on the allocation size of the virtual data center.
* vCPU and RAM resources can be increased and decreased later as required.
* The amount of storage that can be allocated and used in the virtual data center is unlimited. Charges are calculated per hour and are based on GB of allocated storage.
* The amount of inbound and outbound public networking is unlimited. Public outbound bandwidth is charged per GB.

For more information, see [{{site.data.keyword.vm-shared}} pricing](/docs/vmwaresolutions?topic=vmwaresolutions-shared_pricing).

### Virtual data center name
{: #shared_ordering-inst-name}

The virtual data center name is set to **vdc-_xx_** by default, where _xx_ represents two randomly generated alphabetic characters.

You can also specify a virtual data center name that meets the following requirements:
* The maximum length is 128 characters.
* Only alphanumeric, hyphen (-), and underscore (_) characters are allowed.
* The name must be unique within all active virtual data centers in your account. You can create a virtual data center that has the same name as a previously deleted virtual data center.

### Resource group
{: #shared_ordering-resource-group}

Use resource groups to organize the resources in your account for access control and billing purposes. The default resource group in your account is selected by default. You can also select another resource group according to your needs. The resource group that you select cannot be changed after the virtual data center is created.

If **No resource group available** is displayed in this field, you currently do not have the permission to add the virtual data center to any resource group in this account. Contact the account owner to be assigned an Editor or Administrator role on a resource group in the account. For more information, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).

## Deployment topology
{: #shared_ordering-deploytop}

* **Single-zone VMware virtual data center** deploys your virtual data center in a single-zone data center.
* **Multizone VMware virtual data center** deploys your virtual data center across two availability zones in an {{site.data.keyword.cloud_notm}} multizone region if a single-zone data center failure occurs.

## Data center location
{: #shared_ordering-dc}

Select the {{site.data.keyword.cloud_notm}} data center settings. For more information, see [{{site.data.keyword.cloud_notm}} data center availability](/docs/vmwaresolutions?topic=vmwaresolutions-shared_planning#shared_planning-dc-availability).

### Geography
{: #shared_orderinginstance-dc-region}

Select the region where your virtual data center instance is hosted.

### Site
{: #shared_orderinginstance-dc-site}

Select the {{site.data.keyword.cloud_notm}} data center site where the virtual data center is hosted.

### Location
{: #shared_orderinginstance-dc-location}

Select the {{site.data.keyword.cloud_notm}} data center where the virtual data center is hosted.

## Networking
{: #shared_ordering-networking}

You must specify the following network settings for your virtual data center.

### Networking type
{: #shared_ordering-networking-type}

Select either **Private only** or **Public and private**. Public networking is delivered through a generic routing encapsulation enablement tunnel system.

## Virtual data center capacity
{: #shared_ordering-cpu}

Virtual data center capacity is based on your selection of the **On-demand** or **Reserved** pricing plan.

If you selected **On-demand**, select the vCPU and RAM limits.

If you selected **Reserved**, your vCPU model settings are based on your selection of **Preconfigured** or **Customizable**.

If you selected **Preconfigured**, you have the following options for allocated vCPU and RAM limits.

| Size    | vCPU      | RAM      |
|:------- |:-------- |:------ |
| Small | 64-cores | 512 GB |
| Medium | 128-cores | 1024 GB |
| Large | 256-cores | 2048 GB |
{: caption="Preconfigured vCPU and RAM options" caption-side="bottom"}

If you selected **Customizable**, you can customize your reserved vCPU and RAM limits.

The vCPU maximum number is limited to the 40 cores with hyperthreading on each host. This limit allows for a maximum of 80 vCPU virtual machines.
{: important}

## Recommended services
{: #shared_ordering-services}

The following services are preinstalled and ready to use in all virtual data centers. Service charges are incurred only if you choose to use the service.

* Veeam® Availability Suite and Veeam Cloud Connect Replication
* Zerto

For more information, see [Managing Veeam for {{site.data.keyword.vm-shared}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_veeam) and [Managing Zerto for {{site.data.keyword.vm-shared}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-portal).

## Summary
{: #shared_ordering-summary}

Based on your selected configuration for the virtual data center, the estimated price is instantly generated and displayed in the **Summary** pane.

You can also add the provisioned resources to the {{site.data.keyword.cloud_notm}} estimate tool, by clicking **Add to estimate**. The tool is useful if you want to estimate the price of the selected {{site.data.keyword.vm-shared}} resources together with other {{site.data.keyword.cloud_notm}} resources that you might consider purchasing.

## Procedure to order {{site.data.keyword.vm-shared}} On-demand
{: #shared_ordering-procedure-ondemand}
{: help}
{: support}

1. In the VMware Solutions console, click the **{{site.data.keyword.vm-shared}}** card in the **Platforms** section.
2. On the **Create** tab of the **{{site.data.keyword.vm-shared}}** page, select **On-demand**.
3. Enter the virtual data center name and select a resource group.
4. Select a deployment topology according to your needs.
5. For data center location, click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") and select the geography, site, and location to host the instance.
6. Select the network type.
7. Select the vCPU and RAM limits according to your requirements.
8. On the **Summary** pane, verify the configuration and estimated price before you place the order.
9. Click **Create**.

## Procedure to order {{site.data.keyword.vm-shared}} Reserved
{: #shared_ordering-procedure-reserved}

1. In the VMware Solutions console, click the **{{site.data.keyword.vm-shared}}** card in the **Platforms** section.
2. On the **Create** tab of the **{{site.data.keyword.vm-shared}}** page, select **Reserved**.
3. Enter the virtual data center name and select a resource group.
4. Select a deployment topology according to your needs.
5. For data center location, click the **Edit** icon ![Edit icon](../../icons/edit-tagging.svg "Edit") and select the geography, site, and location to host the instance.
6. Select the network type.
7. Complete the resource reservation.
   * If you select **Preconfigured**, select the preconfigured vCPU model and RAM size.
   * If you select **Customizable**, specify the reserved vCPU and RAM limits according to your requirements.
8. On the **Summary** pane, verify the configuration and estimated price before you place the order.
9. Click **Create**.

## Results after you order {{site.data.keyword.vm-shared}}
{: #shared_ordering-results}

* The deployment of the resources starts automatically and you receive confirmation that the order is being processed. You can check the deployment status, including any issues that might require your attention, by viewing the **Virtual Data Center Status**.
* When the resources are successfully deployed, the components that are described in [Technical specifications for {{site.data.keyword.vm-shared}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview#shared_overview-specs) are installed on your VMware® virtual platform.
* When the resources are ready to use, the status of the virtual data center changes to **Available**.

## What to do next
{: #shared_ordering-next}

View the virtual data center that you ordered and then set the **admin** password for the VMware Cloud Director Management console. For more information, see [Viewing and managing virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary).

## Related links
{: #shared_ordering-related}

* [Operating {{site.data.keyword.vm-shared}}](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [VMware Cloud Director](https://www.vmware.com/products/cloud-infrastructure/cloud-director){: external}
