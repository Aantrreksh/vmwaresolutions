---

copyright:

  years: 2020, 2024

lastupdated: "2024-04-02"

keywords: vmware solutions shared, price for shared, pricing plan

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware Shared pricing
{: #shared_pricing}

{{site.data.content.shared-deprecated-note}}

{{site.data.keyword.vmwaresolutions_full}} Shared offers two pricing plans for creating VMware® virtual data centers. Virtual data centers incur charges for the following virtual data center resource usages:

* Storage allocations with tiered pricing based on storage performance
* Virtual CPU (vCPU) usage
* Virtual memory usage
* Egress on public networking
* Commercial operating system licenses used
* Third-party VMware services

| Plans | Description |
|:----- |:----------- |
| VMware Shared On-demand | - The vCPU and RAM virtual data center are allocated based on the demand. Resources are not preallocated. If you have a large regional demand, delays in availability can occur. \n - The limits that are established for the amount of vCPU and RAM are maximums. \n - vCPU and RAM resource limits can be increased and decreased later as required. \n - The price is calculated hourly and it is based on the resource usage in the virtual data center. \n - The amount of storage that can be allocated and used in the virtual data center is unlimited. Charges are hourly based on GB of allocated storage. \n - The amount of inbound and outbound public networking is unlimited. Public outbound bandwidth is charged per GB. |
| VMware Shared Reserved | - The vCPU and RAM virtual data center reservations are pre-allocated and their availability is guaranteed. \n - vCPU and RAM resources can be increased and decreased later as required. \n - The amount of storage that can be allocated and used in the virtual data center is unlimited. Charges are hourly based on GB of allocated storage. \n - The amount of inbound and outbound public networking is unlimited. Public outbound bandwidth is charged per GB. |
{: caption="Table 1. Pricing plans" caption-side="bottom"}

## Price breakdown
{: #shared_pricing-cost}

### Usage
{: #shared_pricing-term-usage}

Metering is for the full potential size of the resource for the time period that the resource is used.

For example, a single-zone on-demand virtual data center is created with a resource limit of 100 vCPU and 800 GB RAM. The data center has no VMs running on it, so you do not receive a charge for the vCPU and RAM. If an 8 vCPU with 8 GB virtual machine (VM) is started, metering is calculated for the size of that VM. If the VM uses fewer resources than the ones assigned to it, metering is applicable to the full size of the VM.

### Allocation
{: #shared_pricing-term-alloc}

Metering is applicable to the full potential size of the resource for the life of the resource.

For example, a single zone reserved virtual data center is created with a resource allocation of 100 vCPU and 800 GB RAM and no VMs are created or running on it. Metering is applicable to 100 vCPU and 800 GB RAM.

### Monthly peak metric usage
{: #shared_pricing-term-mon-peak}

The maximum value of the metric used over a full month.

For example, a single zone reserved virtual data center is created with 100 vCPU and 800 GB RAM. Later in the month, the data center is reduced to 50 vCPU and 400 GB RAM. The monthly peak usage is 100 vCPU and 800 GB RAM.

### Hourly peak metric usage
{: #shared_pricing-term-hour-peak}

The maximum value of the metric used over an hour. For example, if 100 vCPU is used for a minute of the hour with 0 vCPU used for the other 59 mins, the hourly peak metric usage is 100 vCPU.

## VMware Shared on-demand billing plan
{: #shared_pricing-cost-ondemand}

VMware Shared on-demand virtual data center resources are allocated as needed. Pricing is hourly based on the resource usage in the virtual data center. The following metrics are part of this plan.

The standard storage policy pricing is the same as the 4-IOPS/GB storage policy. The number of IOPS/GB for the standard storage policy is not guaranteed.

Storage policy availability can vary by region and deployment topology. On the VMware Shared order page, select the [**About** tab](https://cloud.ibm.com/infrastructure/vmware-solutions/console/ordernew/vdc) to view available storage policy offerings.
{: note}

| Metric                                   | Frequency | Description |
|:-----------------------------------------|:----------|:------------|
| MAX_BASE_COST | Monthly | Virtual data center price, which includes the edge gateway with five IP addresses. |
| TOTAL_VCPU_HOURS | Hourly | The peak vCPU **usage** over the period of an hour. |
| TOTAL_RAM_GB_HOURS | Hourly | The peak memory **usage** over the period of an hour. |
| TOTAL_EGRESS_GB | Usage | The **total** outbound public traffic is charged per GB transferred over the period of an hour. This value includes public outbound traffic. |
{: class="simple-tab-table"}
{: caption="Table 2. VMware Shared Solutions On-demand billing plan - General metrics" caption-side="bottom"}
{: #table1}
{: tab-title="General metrics"}
{: tab-group="on-demand-metrics"}

| Metric                                   | Frequency | Description |
|:-----------------------------------------|:----------|:------------|
| TOTAL_STORAGE_POINT_TWO_FIVE_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 0.25 IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_TWO_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 2-IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_FOUR_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 4-IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_TEN_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 10 IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_VSAN_GB_HOURS | Hourly | The peak storage **allocation** over the period of an hour. |
{: caption="Table 2. VMware Shared Solutions On-demand billing plan - Storage metrics" caption-side="bottom"}
{: #table2}
{: tab-title="Storage metrics"}
{: tab-group="on-demand-metrics"}
{: class="simple-tab-table"}

| Metric                                   | Frequency | Description |
|:-----------------------------------------|:------------|:------------|
| MAX_WINDOWS_LICENSES | Hourly | The peak number of Windows® license **usage** based on Windows VM vCPU size. For example, if you have two Windows VMs, one VM with 16 vCPU and one VM with 8 vCPU, the usage is 24 vCPU of Windows license usage. |
| TOTAL_RHEL_SMALL_LICENSES | Hourly | The peak number of RHEL license usage based on VM vCPU size. One license is charged per vCPU. Small RHEL VMs are 8 vCPUs or smaller. |
| TOTAL_RHEL_MID_LICENSES | Hourly | The peak number of RHEL license usage based on VM vCPU size. One license is charged per vCPU. Mid RHEL VMs are between 9 and 127 vCPUs. |
| TOTAL_RHEL_LARGE_LICENSES | Hourly | The peak number of RHEL license usage based on VM vCPU size. One license is charged per vCPU. Large RHEL VMs are larger than 127 vCPUs. |
{: caption="Table 2. VMware Shared Solutions On-demand billing plan - Operating system metrics" caption-side="bottom"}
{: #table3}
{: tab-title="Operating system metrics"}
{: tab-group="on-demand-metrics"}
{: class="simple-tab-table"}

## VMware Shared Solutions Reserved billing plan
{: #shared_pricing-cost-reserved}

VMware Shared Solutions Reserved virtual data center resources are preallocated and guaranteed. Pricing is monthly based on the allocation size of the virtual data center.

The standard storage policy pricing is the same as the 4-IOPS/GB storage policy. The number of IOPS/GB for the standard storage policy is not guaranteed.

Storage policy availability can vary by region and deployment topology. On the VMware Shared order page, select the [**About** tab](https://cloud.ibm.com/infrastructure/vmware-solutions/console/ordernew/vdc) to view available storage policy offerings.
{: note}

| Metric                                   | Frequency | Description |
|:-----------------------------------------|:----------|:------------|
| MAX_VCPU | Monthly | The peak vCPU **allocation** for the virtual data center over the period of one month. The peak vCPU metric is determined by the largest vCPU reservation value that is selected by the customer over a one month period. |
| MAX_RAM_GB | Monthly | The peak memory **allocation** for the virtual data center over the period of one month. The peak vCPU metric is determined by the largest memory reservation value that is selected by the customer over a one month period. |
| TOTAL_EGRESS_GB  | Usage | The **total** outbound public traffic is charged per GB transferred over the period of one month. This value includes the outbound traffic through the virtual data center NSX edge to the public internet. |
{: class="simple-tab-table"}
{: caption="Table 3. VMware Shared Solutions Reserved billing plan - General metrics" caption-side="bottom"}
{: #reservedbilling-table1}
{: tab-title="General metrics"}
{: tab-group="res-billing-metrics"}

| Metric                                   | Frequency | Description |
|:-----------------------------------------|:----------|:------------|
| TOTAL_STORAGE_POINT_TWO_FIVE_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 0.25 IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_TWO_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 2-IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_FOUR_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 4-IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_TEN_IOPS_GB_HOURS | Hourly | The peak storage **allocation** at the 10 IOPS/GB tier over the period of an hour. |
| TOTAL_STORAGE_VSAN_GB_HOURS | Hourly | The peak storage **allocation** over the period of an hour. |
{: caption="Table 3. VMware Shared Solutions Reserved billing plan - Storage metrics" caption-side="bottom"}
{: #reservedbilling-table2}
{: tab-title="Storage metrics"}
{: tab-group="res-billing-metrics"}
{: class="simple-tab-table"}

| Metric                                   | Frequency | Description |
|:-----------------------------------------|:------------|:------------|
| MAX_WINDOWS_LICENSES | Hourly | The peak number of Windows® license **usage** based on Windows VM vCPU size. For example, if you have two Windows VMs, one VM with 16 vCPU and one VM with 8 vCPU, the usage is 24 vCPU of Windows license usage. |
| TOTAL_RHEL_SMALL_LICENSES | Hourly | The peak number of RHEL license usage based on VM vCPU size. One license is charged per vCPU. Small RHEL VMs are 8 vCPUs or smaller. |
| TOTAL_RHEL_MID_LICENSES | Hourly | The peak number of RHEL license usage based on VM vCPU size. One license is charged per vCPU. Mid RHEL VMs are between 9 and 127 vCPUs. |
| TOTAL_RHEL_LARGE_LICENSES | Hourly | The peak number of RHEL license usage based on VM vCPU size. One license is charged per vCPU. Large RHEL VMs are larger than 127 vCPUs. |
{: caption="Table 3. VMware Shared Solutions Reserved billing plan - Operating system metrics" caption-side="bottom"}
{: #reservedbilling-table3}
{: tab-title="Operating system metrics"}
{: tab-group="res-billing-metrics"}
{: class="simple-tab-table"}

## Private network endpoint billing plan
{: #shared_pricing-private-network-endpoints}

Private network endpoint usage incurs charges as part of the on-demand or reserved virtual data center plan. On the **VMware Shared** order page, select the [**About** tab](https://cloud.ibm.com/infrastructure/vmware-solutions/console/ordernew/vdc) to view the pricing plan details.

| Metric                                   | Frequency   | Description |
|:-----------------------------------------|:------------|:------------|
| MAX_PRIVATE_NETWORK_ONE_G_COST | Monthly | Charge for private network endpoint at 1 GB uplink over a period of one month. |
| MAX_PRIVATE_NETWORK_TEN_G_COST | Monthly | Charge for private network endpoint at 10 GB uplink over a period of one month. |
{: caption="Table 4. Billing plan for private network endpoints" caption-side="bottom"}

## Licenses and fees for Veeam Availability Suite and Zerto
{: #shared_pricing-services}

Veeam® and Zerto usage incurs the following on-demand charges. You can view the charges on the **{{site.data.keyword.cloud_notm}} billing and usage** view along with the usage and charges from all other {{site.data.keyword.cloud_notm}} services.

In the **{{site.data.keyword.cloud_notm}} Usage** view, locate the **VMware Solutions** service type. Locate the **Organization** plan to find the Veeam and Zerto usage across all virtual data centers in that organization. The virtual data center usage is located in a separate plan for either VMware Shared on-demand or VMware Shared Reserved.

| Metric                                   | Frequency   | Description |
|:-----------------------------------------|:------------|:------------|
| MAX_VEEAM_LICENSES | Monthly | Veeam license charge for every VM under backup. The monthly charge is for the highest number of VMs under backup at any time period in the month. |
| TOTAL_VEEAM_BLOCK_STORAGE_GB_HOURS | Hourly | Charge per GB of block storage used for all backups. |
| TOTAL_VEEAM_OBJECT_STORAGE_GB_HOURS | Hourly | Charge per GB of object storage used for all backups. |
{: caption="Table 5. Licenses and fees for Veeam" caption-side="bottom"}
{: class="simple-tab-table"}
{: #service-table1}
{: tab-title="Veeam"}
{: tab-group="service-billing-metrics"}

| Metric                                   | Frequency   | Description |
|:-----------------------------------------|:------------|:------------|
| TOTAL_ZERTO_LICENSE_HOURS | Hourly | Zerto license charge for every VM replicated. The hourly charge is for the highest number of VMs replicated to a virtual data center at any time period in the hour. |
| TOTAL_ZERTO_CLOUD_CONNECTOR_HOURS | Hourly | Charge for every virtual data center. One Zerto Cloud Connector per virtual data center. |
{: caption="Table 5. Licenses and fees for Zerto" caption-side="bottom"}
{: #service-table2}
{: tab-title="Zerto"}
{: tab-group="service-billing-metrics"}
{: class="simple-tab-table"}

No additional Veeam or Zerto usage charges for VMware Shared are incurred.
{: note}

For the Veeam service, initially, all backups go to the {{site.data.keyword.blockstorageshort}} that is closest to their VM workloads. Backups that are a part of an inactive backup chain are immediately moved to Cloud Object Storage. The restore speed for these inactive backups might be impacted.

You can change how fast the inactive backup chains are moved to Cloud Object Storage by opening an {{site.data.keyword.vmwaresolutions_short}} service ticket.

## Related links
{: #shared_pricing-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Requirements and planning for VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_planning)
* [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [Viewing and managing virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary)
* [Resizing virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_resize)
* [Operating VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide)
* [Managing Veeam for VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_veeam)
* [Managing Zerto for VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-portal)
* [VMware Cloud Director](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/VMware-Cloud-Director-Tenant-Portal-Guide/GUID-74C9E10D-9197-43B0-B469-126FFBCB5121.html){: external}
* [Troubleshooting NSX Edge](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.4/com.vmware.nsx.troubleshooting.doc/GUID-E6CD6FAA-3DA7-4AD7-9577-EE121AA7E1E6.html){: external}
