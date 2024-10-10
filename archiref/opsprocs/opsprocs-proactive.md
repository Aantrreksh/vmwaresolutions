---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-12"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Proactive tasks
{: #opsprocs-proactive}

The goal of these proactive checks is to enable system administrators to maintain their {{site.data.keyword.vcf-auto}} instance in a healthy state. When carried out daily, it prevents many common issues that are related to usage, capacity and performance issues, from impacting your workloads. These proactive checks can be classified into the following structure.

* Health - Checks that indicate issues that are currently affecting the health of your environment and require immediate attention to minimize impact that is, hardware failures.
* Risk - Checks that indicate issues that are not immediate threats but must be addressed soon. For example, capacity issues.
* Efficiency - Checks that indicate areas to improve performance or reclaim resources. For example, right-sizing virtual machines (VMs) and clusters.

Many of these proactive tasks can be made much simpler with the Operations Management on {{site.data.keyword.cloud}} and reduce the management time.

It is important to understand your "baseline". This baseline reflects normal operations in your environment. All clients have a different baseline that is determined by their standard practices, the workloads that run on the {{site.data.keyword.vcf-auto-short}} instance, and more. These proactive checks are then comparing the recent capacity/performance/utilization against this baseline. These proactive usage checks are answering the following four questions.

1. Am I over-utilized now?
2. Will I run out of capacity soon?
3. Is my cluster under-sized for expected peak usage periods?
4. Can I reclaim unused resources from my virtual infrastructure?

## Guidelines
{: #opsprocs-proactive-guidelines}

The following guidelines assist you in being proactive and maintaining a stable environment:
* Plan your VM deployments by allocating enough resources for all the VMs you plan to run. Don't forget to allow resources for vSphere ESXi™ itself.
* Size your VMs correctly and allocate to each VM only as much virtual resources as that VM needs. Provisioning a VM with more resources than it needs might reduce the performance of that VM and of others on the same host.
* In general, 80% host CPU usage is a reasonable ceiling and 90% is a warning that the CPUs are approaching an overloaded condition. If your hosts are approaching 80% CPU usage, provision more hosts.
* In general, 80% host RAM usage is a reasonable ceiling and 90% is a warning that the hosts are fully used. If your hosts are approaching 80% RAM usage, provision more hosts.
* It is important not to under-allocate memory, so allocate enough memory to hold the working set of the applications you plan to run in the VMs, to minimize thrashing. Thrashing can dramatically impact application performance. However, avoid substantially over-allocating memory as well.
* Use resource settings, reservation, shares, and limits, only if needed in your environment. If you expect frequent changes to the total available resources, use shares, not reservation, to allocate resources fairly across VMs. Shares take effect only when resource contention exists.
* If you do need to use reservations, configure them to specify the minimum acceptable amount of CPU or memory, not the amount you would like to have available.
* Use resource pools for delegated resource management and to fully isolate a resource pool, make the resource pool type Fixed, and use Reservation and Limit.
* Group VMs for a multitier service into a resource pool, which allows resources to be assigned for the service as a whole. Carefully select the resource settings (that is, reservations, shares, and limits) for your VMs. Setting reservations too high can leave few unreserved resources in the cluster, thus limiting the options that DRS must balance load.
* Setting limits too low might keep VMs from using extra resources available in the cluster to improve their performance.
* Run your clusters at no more than 80% usage to allow remediation of hosts by using VMware Update Manager. Cluster remediation is most likely to succeed when the cluster is running at a maximum of 80% usage.
* Thin provisioning of storage increases the management workload of maintaining your environment as you need to be careful in your capacity management process.
*  Analyze your VM growth and understand how your infrastructure is getting used up to support this growth, order more capacity to facilitate this growth.
* Use usable capacity, which considers HA and buffers and not total available capacity.
* Ensure that you are running the current version of the BIOS available for your system.
* Ensure that you are running the current VMware updates to your installed products, including VM hardware and VM tools.

## List of tasks
{: #opsprocs-proactive-tasks}

| Title | Description |
|:----- |:----------- |
| Health | Using vCenter, check the health of all hosts and VM objects. Methodically step through the clusters, hosts, datastores, VMs, and networks that look for alarms.  |
| Alarm and notification check | Review to confirm that there are not any active alarms in vCenter for which you are not aware of. By default, vCenter has a number of alarms that are defined when installed. These alarms might alert you to issues. However, by default, these alarms deliver a warning or alert only in the VMware vSphere® Web Client. They can be configured to a notification such as an email. As you check the health of the hosts and VM objects, review the alarms, decide whether a notification is needed, and configure as required. You need to be notified for only the most important or critical issues. Consider the following case: do I want to be notified of this issue at 2 AM or can it wait until normal working hours? Too many notifications are considered as "noise" and human nature is to ignore all alarms. |
| Cluster CPU and memory capacity and utilization check | Review the capacity and utilization metrics for the cluster's CPU and memory. Use vCenter to navigate to each cluster in turn and selecting Monitor, then Performance. Review the graphs and statistics to ensure that your cluster has enough resources to satisfy demand. You must base demand on maintaining enough capacity for VMs to burst when needed, a vSphere ESXi host to fail, and for VMs to be added according to your known service requests. |
| Datastore capacity and utilization check | Review the capacity and utilization metrics for the datastores. Use vCenter to navigate to each datastore in turn and selecting Monitor, Performance, Space. Review the graphs and statistics to ensure that your datastore has enough space to satisfy demand. Demand should be based on maintaining enough capacity for a vSphere ESXi host to fail (for a vSAN™ cluster) and for VMs to be added according to your known service requests. |
| Datastore performance check | Review the performance metrics for the datastores. Use vCenter to navigate to each datastore in turn and selecting: Monitor, Performance, Performance, Real-time. Review the graphs and statistics to ensure that your datastore performance baseline is expected and that any changes can be accounted for. Investigate any abnormalities. |
| Bare metal server firmware | Best practices recommend installing the most recent firmware updates for your bare metal server hosts. Check for firmware updates on the bare metal server hosts by using the Update Firmware option in the {{site.data.keyword.cloud_notm}} portal. On the page that is displayed, review the current and update version for system board and hard disk drives and see whether updates are available. If they are, plan to update the firmware in your next maintenance window. For more information, see [FAQs: Bare metal servers](/docs/virtual-servers?topic=virtual-servers-bm-faq). |
| vSphere ESXi patching | For more information about checking for the availability of vSphere ESXi patches, see [Creating baselines and attaching to inventory objects](/docs/vmwaresolutions?topic=vmwaresolutions-vum-baselines#vum-baselines). |
| VM hardware updates | For more information about checking for the availability of VM hardware updates, see [Creating baselines and attaching to inventory objects](/docs/vmwaresolutions?topic=vmwaresolutions-vum-baselines#vum-baselines). |
| VM Tools updates | For more information, see [Creating baselines and attaching to inventory objects](/docs/vmwaresolutions?topic=vmwaresolutions-vum-baselines#vum-baselines). |
| vSphere vSAN patching | For more information about checking for the availability of vSphere vSAN patches and the patch process, see [Updating vSAN clusters](/docs/vmwaresolutions?topic=vmwaresolutions-vum-updating-vsan#vum-updating-vsan). |
| VMware vCenter® patching | For more information about checking for the availability of vCenter patches and applying the update, see [VCSA update and SSO-linked vCenters](/docs/vmwaresolutions?topic=vmwaresolutions-vum-updating-vcsa#vum-updating-vcsa). |
| Updating NSX | For more information about checking for the availability of NSX patches and applying the upgrades, see [NSX patching](/docs/vmwaresolutions?topic=vmwaresolutions-vum-updating-nsx#vum-updating-nsx). |
| Check for VMs without VM Tools | It is good practice to install VM Tools as this allows greater interaction with the OS, that is, graceful power down of the VM. You can use vCenter to check which VMs do not have VM Tools that are installed. Go to the cluster, select **Related Objects**, **VMs**, and in the table enable the columns for **VM Tools running** and **VM Tools version**. Review the list and install VM Tools if needed. |
| VMs with snapshots | For more information about best practices when you work with snapshots, see [Best practices for using snapshots in the vSphere environment (1025279)](https://knowledge.broadcom.com/external/article?legacyId=1025279){: external}. It is important to identify the existence of VMs with snapshots as using a single snapshot for more than 72 hours creates a snapshot file that continues to grow in size and can cause the snapshot storage location to run out of space and impact the system performance. To review VMs with snapshots, connect to vCenter by using the Web Client, select the vCenter and go to the Related Objects tab. Right-click on the column titles and go to the Show/Hide Columns list. From the list of columns, choose the **Needs Consolidation** option. This column shows a summary of all the VMs that are currently running. |
| AD/DNS OS patching | The Microsoft® Active Directory™ (AD) / Domain Name Server (DNS) is automatically set up to download the updates only. For more information, see [More limitations and considerations](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_limitations#trbl_limitations) for further updating advice. |
| Check storage latency | Check storage latency to understand any changes for the vSphere ESXi hosts to access the datastores. Too high a latency causes applications that are hosted in the VMs to slow down. In vCenter, go to the Performance tab. On each of the datastores, review the average write latency per VM. |
| Review VMs with virtual devices | Virtual devices such as CD or diskette drives create an overhead, therefore, remove any devices that are not needed for a VM. |
| vSAN capacity advice | When any capacity device in your cluster reaches 80% full, vSAN automatically rebalances the cluster until the space available on all capacity devices is lower than the threshold. The following operations can cause disk capacity to reach 80% and initiate cluster rebalancing: hardware failures, vSAN hosts are placed in maintenance mode with the Evacuate all data option, or vSAN hosts are placed in maintenance mode with Ensure data accessibility when objects assigned PFTT=0 reside on the host. To provide enough space for maintenance and reprotection, and to minimize automatic rebalancing of events in the vSAN cluster, consider keeping 30% capacity available always. |
| Cluster utilization check | Using vCenter, review each cluster and identify which clusters are at 50% or greater utilization for CPU and RAM. 50% is chosen as a warning level to focus attention on potential expansion of this cluster with more hosts or clusters. The difference between 50% utilization and a maximum of 80 - 90% is your room for more VMs due to service requests. At the 50% limit, you should be looking at the near-future requests and forecasting when more resources need to be added. |
| Cluster consolidation review | Using vCenter, review each cluster and identify which clusters are at 30% or less utilization for CPU and RAM. 30% is chosen as a warning level to focus attention on potential right-sizing of this cluster by removing hosts or removing this cluster and moving VMs to another cluster. |
| Right-size over-sized VMs | Use a simple approach to right-size oversized VMs: identify, profile and tune, and monitor demand trends. Using vCenter identify large VMs that have the potential for right-sizing. Navigate to Monitor, Performance, and profile the average CPU and RAM demand profile of the workload over time and adjust the virtual resources. Finally, continue to monitor the workloads to see that the performance is acceptable. Ideally, consumed memory for the VM should be close to the memory used by the guest OS, plus overhead for running the VM.|
| Right-size under-sized VMs | Use a simple approach to right-size under-sized VMs. First, identify then profile and tune, and then monitor demand trends. Identify small VMs that need right-sizing. Profile the average CPU and RAM demand profile of the workload over time and adjust the virtual resources. Finally, continue to monitor the workloads to see that the performance is acceptable. Ideally, consumed memory for the VM should be close to the memory used by the guest OS, plus overhead for running the VM.|
| Check VM hardware device compatibility | Using the VMware hardware compatibility online resource, check that your VMs' hardware resources such as network and storage devices, are supported for that OS. If they are not supported, change to a supported device to improve reliability and performance.  |
{: caption="Proactive tasks" caption-side="bottom"}

## Related links
{: #opsprocs-proactive-links}

* [Operations Management on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-intro)
