---

copyright:

  years:  2020, 2023

lastupdated: "2023-06-20"

keywords: monitor, default dashboard, custom dashboard, virtual data center, platform metrics, monitoring

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Visualizing your virtual data center environment with IBM Cloud Monitoring
{: #shared-monitor}

VMware Shared provides an integration with {{site.data.keyword.mon_full}}, which allows you to use a dashboard, provided by VMware Shared to view metrics for your virtual data centers. Alternatively, you can create your own dashboard to visualize performance, volume of usage, and to define alerts to monitor your environment.

Use {{site.data.keyword.mon_short}} dashboards to complete the following tasks.

* Explore and easily visualize your environment.
* Accelerate a diagnosis and a resolution for performance incidents.
* Control cost of monitoring infrastructure.
* Mitigate impact of abnormal situations with proactive notifications.

For more information about the benefits of using {{site.data.keyword.mon_short}}, see the *Features* section in [Monitoring getting started tutorial](/docs/monitoring?topic=monitoring-getting-started#getting-started-features).

## Provisioning an IBM Cloud Monitoring instance
{: #shared-monitor-create-instance}

Before you can view platform metrics for your virtual data center, you must order a {{site.data.keyword.mon_short}} instance.

Review the following requirements for your instance order.

* Order the instance with the Graduated Tier plan, not the Lite plan.
* The instance must be within the same region as your virtual data center instance.
* You must enable the automatic collection of platform metrics.

Order the {{site.data.keyword.mon_short}} instance.

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > VMware Shared** from the left navigation pane.
2. In the **VMware Shared** table, select the instance for which you want to collect platform metrics.
3. From the instance details page, click the **Actions** menu and click **Add monitoring**.
4. On the {{site.data.keyword.mon_short}} provisioning page, complete the steps in [Provisioning an instance](/docs/monitoring?topic=monitoring-provision) to order a {{site.data.keyword.mon_short}} instance and enable the automatic platform metrics collection.

## Viewing platform metrics for your virtual data center
{: #shared-monitor-view-metrics}

After you order your {{site.data.keyword.mon_short}} instance, you can view the platform metrics in the {{site.data.keyword.mon_short}} console.

1. In the **VMware Shared** table, select the virtual data center for which you want to view platform metrics.
2. From the virtual data center details page, click the **Actions** menu and click **Monitoring**. The {{site.data.keyword.mon_short}} dashboard displays the metrics for the associated instance.

## VMware Shared metrics
{: #shared-monitor-metrics}

VMware Shared provides the following metrics for the default dashboard:
* vCPU usage
* vCPU allocation
* Memory usage
* Memory allocation
* Storage usage

Metrics updates can be delayed by up to 60 minutes.
{: note}

## Customizing your VMware Shared dashboard
{: #shared-monitor-view-customize}

You can optionally customize your dashboard.

1. In the {{site.data.keyword.mon_short}} console, click **Dashboards** from the left navigation pane.
2. Click the **IBM** menu and click **VMware Shared**.
3. Customize your dashboard. For more information, see [Dashboards](/docs/monitoring?topic=monitoring-monitoring#monitoring_dashboards).

## Related links
{: #shared-monitor-related}

* [{{site.data.keyword.cloud_notm}} Monitoring getting started tutorial](/docs/monitoring?topic=monitoring-getting-started)
