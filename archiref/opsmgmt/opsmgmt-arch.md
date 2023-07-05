---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-12"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Operations management architecture overview
{: #opsmgmt-arch}

The architecture of the products in the operations management layer provides centralized monitoring with logging data from {{site.data.keyword.vmwaresolutions_full}}. The operations management layer monitors in real time, the physical infrastructure, virtual infrastructure, and optionally the client’s compute workloads.

At a high level, the following information is collected:
* Topology data, such as physical and virtual compute, networking, and storage objects.
* Monitoring data, such as:
   * Metrics - structured data such as performance and capacity
   * Logs - unstructured data such as system events

## Operation management flows
{: #opsmgmt-arch-flows}

The following diagram shows the key interaction and integration of the operations management tools.

![Management flows diagram](../../images/opsmgmt-mgmtflows.svg "Management flows diagram"){: caption="Figure 1. Operational tools management flow" caption-side="bottom"}

The {{site.data.keyword.vmwaresolutions_short}} operations management consists of the following steps:
* Monitoring - VMware Aria® Operations™ Manager tracks and analyzes the operation of multiple objects in the {{site.data.keyword.vmwaresolutions_short}} architecture by using analytic algorithms. These algorithms help VMware Aria Operations learn and predict the behavior of these objects. System administrators access this information by using views, reports, and dashboards.

    When an issue occurs in the environment VMware Aria Operations generates alerts of three impact types:
    * Health alerts - indicate issues that affect the health of the environment and require immediate attention.
    * Risk alerts - indicate issues that are not immediate threats but need to be addressed soon.
    * Efficiency alerts - information to improve performance or reclaim resources.

    VMware Aria Operations Alerts are events that occur on the monitored objects when data analysis indicates deviations from normal metric values, or when an issue occurs with one of the monitored components. VMware Aria Operations alerts are assigned one of these categories:
    * Critical - must be acted upon immediately.
    * Immediate - must be acted on as soon as possible.
    * Warning - must be checked when time allows.

* Logging - VMware Aria Operations™ for Logs provides real-time log management and log analysis with machine learning-based intelligent grouping, high performance searching, and troubleshooting across the physical and virtual objects in the {{site.data.keyword.vmwaresolutions_short}} architecture. VMware Aria Operations for Logs collects data from vSphere hosts by using the `syslog` protocol. It also collects events, tasks, and alarm data for other VMware products, like vCenter Server. It integrates with VMware Aria Operations to send notification events and enable launch-in-context. Other objects in the {{site.data.keyword.vmwaresolutions_short}} architecture that can send `syslog` data are pointed to VMware Aria Operations for Logs. Optionally, the client can configure any system that can send syslog data to forward this data to VMware Aria Operations for Logs.

* Network Health - VMware Aria Operations™ for Networks is an analytics tool that is focused on proactively enabling:
   * Network health and performance monitoring.
   * End-to-end troubleshooting.
   * 360° visibility and analytics.
   * Micro-segmentation-based compliance management.

* Patching and Upgrading - vSphere Update Manager (VUM) provides centralized, automated patch and version management for VMware vSphere hosts and virtual machines (VMs) (not OS and apps).

## Operation management networking
{: #opsmgmt-arch-network}

The following diagram shows the network overview.

![Network diagram](../../images/opsmgmt-network.svg "Network diagram"){: caption="Figure 2. Operational tools networking" caption-side="bottom"}

* A tooling private portable subnet is provisioned to provide {{site.data.keyword.cloud_notm}} IP address space that is used for the initial provisioning of the tooling VMs. After provisioning, it becomes the responsibility of the client to manage the IP address space for scale-out of the tooling. VMs on this subnet require access to the components hosted on the Management and Internal Management subnets.
* Tooling VXLAN subnet is used to provide BYOIP IP address space that is used for the initial provisioning of the tooling VMs but then becomes the responsibility of the client to manage the IP address space for scale-out of the tooling. VMs on this subnet require access to the components hosted on the Overlay subnets. The ESG provides NAT between the {{site.data.keyword.cloud_notm}} and BYOIP address spaces.
* The VMware Aria Operations Remote Collectors are deployed by the client if they would like to take advantage of the VMware Aria Operations to monitor their compute VMs.
* The VMware Aria Operations for Logs Forwarders relay log messages from overlay components to the VMware Aria Operations for Logs cluster. The client can also configure their compute VMs to uses these forwarders, if required.
* VMware Update Manager (VUM) provides updating of vSphere hosts and VM hardware and tools. VUM uses the Proxy to gain access to the internet repositories.

VMware Aria Operations collects data from objects in the environment. Each piece of data that is collected is called a metric observation or value. VMware Aria Operations uses the vCenter adapter to collect raw metrics from vCenter. In addition to the metrics it collects, VMware Aria Operations calculates capacity metrics, badge metrics, and metrics to monitor the health of your system. Alert definitions are a combination of symptoms and recommendations that identify problem areas and generate alerts on which you act for those areas.

## Monitored components
{: #opsmgmt-arch-components}

### Monitoring of vCenter
{: #opsmgmt-arch-components-vcenter}

The monitoring of vCenter is accomplished with VMware Aria Operations and the VMware SDDC Health Management Pack. VMware Aria Operations for Logs collects the log data from vCenter and the Content Pack for vSphere adds specific understanding to the logs and in turn sends alerts to VMware Aria Operations.

The VMware SDDC Health Management Pack monitors the SDDC Management stack and provides badges for health and alerts related to configuration and compliance of SDDC product components that include vCenter.

### Monitoring of vSphere hosts
{: #opsmgmt-arch-components-hosts}

Monitoring of the vSphere hosts is accomplished with VMware Aria Operations through vCenter and the collection of logs through VMware Aria Operations for Logs.

### Monitoring of vSAN
{: #opsmgmt-arch-components-vsan}

To monitor vSAN, VMware Aria Operations, and VMware Aria Operations for Logs are used. In vCenter, you can use an extra set of vSAN Health Checks. Installation of the Management Pack for vSAN provides more dashboards to aid with the monitoring of vSAN.

VMware Aria Operations generates an alert if a problem occurs in the SDDC product components in the storage area network that the VMware vSAN adapter is monitoring. An alert that is related to configuration compliance and health is passed through VMware SDDC Health Solution management pack from VMware vSAN Management Pack. vSAN is monitored with the VMware Aria Operations vSAN Management Pack through the vCentre appliance by using a vSAN adapter. The default collection interval is five minutes and the vSAN adapter also collects Health Check Service and Performance Service metrics from vSphere objects. The Health Check Service interval is configured in the vSphere interface and is 60 minutes by default.

To ensure that the vSAN adapter can collect all performance data, the vSAN performance service must be enabled in vSphere.

### Monitoring of NSX for vSphere
{: #opsmgmt-arch-components-nsxv}

To monitor NSX, the following tools are implemented:
* VMware Aria Operations Manager
* VMware Aria Operations for Logs
* VMware Aria Operations for Networks

This enables system administrators to monitor, manage, and troubleshoot VMware NSX. The VMware Aria Operations Management Pack for VMware NSX provides visibility into the network topology. NSX dashboards provide a quick overview of the NSX environment and the health of its components. Correlation between NSX objects and vSphere objects enables easier troubleshooting.

VMware Aria Operations uses the management pack to poll VMware NSX for configuration, performance, and support data. On behalf of VMware Aria Operations, the Management Pack converts the polling requests into REST API calls to retrieve the required data from NSX Manager.

The NSX components need to be configured to send syslog to VMware Aria Operations for Logs.

* NSX Manager - [Specify a Syslog Server](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.2/com.vmware.nsx-cross-vcenter-install.doc/GUID-EA70974C-07F8-469D-8A9D-0ED54F0C8F34.html){: external}.
* NSX Controllers - [Configuring syslog server for VMware NSX for vSphere 6.x controllers](https://kb.vmware.com/s/article/2092228){: external}.
* NSX Edge - [Configure Remote Syslog Servers](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.2/com.vmware.nsx.admin.doc/GUID-9C25E097-E2CC-461A-9DA6-E8118D16EE62.html){: external}.
* Firewall - You must configure the remote syslog server for each cluster that where the firewall is enabled. The remote syslog server is specified in the `Syslog.global.logHost` attribute.

NSX Flow Monitoring can be used in NSX Manager to determine which flows are approved and which flows are blocked. If required, then port mirroring can be configured for a vSphere Distributed Switch.

### Monitoring of NSX-T
{: #opsmgmt-arch-components-nsxt}

To monitor NSX-T™, the following tools are implemented:

* VMware Aria Operations Manager
* VMware Aria Operations for Logs

The VMware SDDC Health Management Pack monitors the following components:
* Logical Switches - Monitors admin state of the logical switches.
* Controller Cluster - Monitors the deployed cluster node count for HA and maintains quorum.
* Controller Nodes - Monitors node connectivity with controller cluster and manager node.
* Edge Nodes - Monitors edge node running state and its connectivity with controller cluster and manager nodes.
* NSX-T Management Services.
* T0 Router Service - Monitors static route, NAT, BGP, BFD, and route redistribution services.
* T1 Router Service - Monitors static route, NAT, and route advertisement services.

### Monitoring of VMware Aria Operations Manager
{: #opsmgmt-arch-components-vrops}

The VMware SDDC Health Management Pack has Alert definitions for the following events:
* Current sizing of the VMware Aria Operations Manager nodes are not sufficient for given load.
* Cluster node configuration does not follow the VMware Aria Operations Manager sizing guideline.
* Current sizing of the Remote Collector is not sufficient for given load.
* Remote Collector configuration does not follow the VMware Aria Operations Manager sizing guideline.
* VMware Aria Operations Cluster has exceeded the recommended number of analytic nodes.

### Monitoring of VMware Aria Operations for Logs
{: #opsmgmt-arch-components-vrli}

VMware Aria Operations for Logs supports alerts that trigger notifications about its health and generates notifications when an important system event occurs, for example, when the disk space is almost exhausted and VMware Aria Operations for Logs must start deleting or archiving old log files.

## System requirements
{: #opsmgmt-arch-requirements}

The design uses the following quantity and size of appliances:

| | VMware Aria Operations | VMware Aria Operations for Logs | VMware Aria Operations for Networks | Proxy |
|:-- |:-- |:---- |:---- |:----- |
| VM Qty | 4 | 4 | 1+1 | 1 |
| vCPU | 8 | 8 | 4 + 8 | 4 |
| RAM (GB) | 32 | 16 | 12 + 32 | 0.5 |
| Disk (GB) | 254 | 1,042 | 158 + 1000 | 80 |
{: caption="Table 1. Operation tooling summary system requirements" caption-side="bottom"}

## Software versions
{: #opsmgmt-arch-versions}

| Product name | Version |
|:------------ |:------- |
| VMware Aria Operations Manager Advanced or higher | 7.0 |
| VMware Aria Operations Management Pack for NSX for vSphere | 3.5.2 |
| VMware Aria Operations Management Pack for Storage Devices | 7.0.0 |
| VMware Aria Operations Management Pack for Site Recovery Manager | 8.1.1 |
| VMware Aria Operations for Logs | 4.7 |
| VMware Aria Operations for Logs Content Pack for NSX for vSphere | 3.8 |
{: caption="Table 2. Operational tooling software versions" caption-side="bottom"}
