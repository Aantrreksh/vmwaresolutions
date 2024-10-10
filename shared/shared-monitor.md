---

copyright:

  years:  2020, 2024

lastupdated: "2024-04-26"

keywords: monitor, default dashboard, custom dashboard, virtual data center, platform metrics, monitoring

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Visualizing your virtual data center environment with {{site.data.keyword.mon_full_notm}}
{: #shared-monitor}

{{site.data.content.shared-deprecated-note}}

{{site.data.keyword.vm-shared}} provides an integration with {{site.data.keyword.mon_full}}, which allows you to use a dashboard, provided by {{site.data.keyword.vm-shared}} to view metrics for your virtual data centers. Alternatively, you can create your own dashboard to visualize performance, volume of usage, and to define alerts to monitor your environment.

Use {{site.data.keyword.mon_short}} dashboards to complete the following tasks.

* Explore and easily visualize your environment.
* Accelerate a diagnosis and a resolution for performance incidents.
* Control cost of monitoring infrastructure.
* Mitigate impact of abnormal situations with proactive notifications.

For more information about the benefits of using {{site.data.keyword.mon_short}}, see [Getting started with {{site.data.keyword.mon_full_notm}}](/docs/monitoring?topic=monitoring-getting-started).

## Provisioning an {{site.data.keyword.mon_full_notm}} instance
{: #shared-monitor-create-instance}

Before you can view platform metrics for your virtual data center, you must order a {{site.data.keyword.mon_short}} instance.

Review the following requirements for your instance order.

* Order the instance with the Graduated Tier plan, not the Lite plan.
* The instance must be within the same region as your virtual data center instance.
* You must enable the automatic collection of platform metrics.

To order the {{site.data.keyword.mon_short}} instance:

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > {{site.data.keyword.vm-shared}}** from the left navigation pane.
2. In the **{{site.data.keyword.vm-shared}}** table, select the instance for which you want to collect platform metrics.
3. From the instance details page, click the **Actions** menu and click **Add monitoring**.
4. On the {{site.data.keyword.mon_short}} provisioning page, complete the steps in [Provisioning an instance](/docs/monitoring?topic=monitoring-provision) to order a {{site.data.keyword.mon_short}} instance and enable the automatic platform metrics collection.

## Viewing platform metrics for your virtual data center
{: #shared-monitor-view-metrics}

After you order your {{site.data.keyword.mon_short}} instance, you can view the platform metrics in the {{site.data.keyword.mon_short}} console.

1. In the **{{site.data.keyword.vm-shared}}** table, select the virtual data center for which you want to view platform metrics.
2. From the virtual data center details page, click the **Actions** menu and click **Monitoring**. The {{site.data.keyword.mon_short}} dashboard displays the metrics for the associated instance.

## {{site.data.keyword.vm-shared}} metrics
{: #shared-monitor-metrics}

{{site.data.keyword.vm-shared}} provides the following metrics for the default dashboard:
* vCPU usage
* vCPU allocation
* Memory usage
* Memory allocation
* Storage usage

Metrics updates can be delayed by up to 60 minutes.
{: note}

### VMware virtual data center vCPU usage
{: #shared-monitor-metrics-vcpu-usage}

The following table displays the total usage of the virtual data center vCPU.

| Metadata | Description |
|:-------- |:----------- |
| `Metric Name` | `ibm_vmwaresolutions_vdc_vcpu_usage` |
| `Metric Type` | `gauge` |
| `Unit` | `none` |
| `Segment By` | `Service instance ID` |
{: caption="Virtual data center vCPU usage" caption-side="bottom"}

### VMware virtual data center vCPU allocation
{: #shared-monitor-metrics-vcpu-allocation}

The following table displays the total allocation of the virtual data center vCPU.

| Metadata | Description |
|:-------- |:----------- |
| `Metric Name` | `ibm_vmwaresolutions_vdc_vcpu_allocation` |
| `Metric Type` | `gauge` |
| `Unit` | `none` |
| `Segment By` | `Service instance ID` |
{: caption="Virtual data center vCPU allocation" caption-side="bottom"}

### VMware virtual data center memory usage
{: #shared-monitor-metrics-memory-usage}

The following table displays the total usage of the virtual data center memory.

| Metadata | Description |
|:-------- |:----------- |
| `Metric Name` | `ibm_vmwaresolutions_vdc_memory_usage` |
| `Metric Type` | `gauge` |
| `Unit` | `byte` |
| `Segment By` | `Service instance ID` |
{: caption="Virtual data center memory usage" caption-side="bottom"}

### VMware virtual data center memory allocation
{: #shared-monitor-metrics-memory-allocation}

The following table displays the total allocation of the virtual data center memory.

| Metadata | Description |
|:-------- |:----------- |
| `Metric Name` | `ibm_vmwaresolutions_vdc_memory_allocation`|
| `Metric Type` | `gauge` |
| `Unit` | `byte` |
| `Segment By` | `Service instance ID` |
{: caption="Virtual data center memory allocation" caption-side="bottom"}

### VMware virtual data center storage usage
{: #shared-monitor-metrics-storage-usage}

The following table displays the total usage of the virtual data center storage.

| Metadata | Description |
|:-------- |:----------- |
| `Metric Name` | `ibm_vmwaresolutions_vdc_storage_usage`|
| `Metric Type` | `gauge` |
| `Unit` | `byte` |
| `Segment By` | `Service instance ID` |
{: caption="Virtual data center storage usage" caption-side="bottom"}

## Customizing your {{site.data.keyword.vm-shared}} dashboard
{: #shared-monitor-view-customize}

To customize your dashboard:

1. In the {{site.data.keyword.mon_short}} console, click **Dashboards** from the left navigation pane.
2. Click the **IBM** menu and click **VMware Solutions Shared**.
3. Customize your dashboard. For more information, see [Dashboards](/docs/monitoring?topic=monitoring-monitoring#monitoring_dashboards).
