---

copyright:

  years:  2020, 2024

lastupdated: "2024-07-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Operations management
{: #vrw-operations}

{{site.data.keyword.cloud}} for VMware® Regulated Workloads is delivered as a clean environment. Extensive work was done to identify and remediate common errors and warnings that are often found in a typical vSphere deployment. IBM and VMware® best practices, which are combined with standard and customized templates for VMware Aria® Operations™, ensure that all {{site.data.keyword.rw}} configurations are deployed as clean as possible, ready for onboarding. Caveonix RiskForesight is used to scan the environment for compliance with industry and government standards such as NIST, PCI, and more. RiskForesight is continually monitoring the {{site.data.keyword.rw}} for adherence to compliance standards. RiskForesight provides on-demand compliance posture reporting and at-a-glance compliance status.
The operational tools support the customer in compliance with current standards and assist them in rapidly responding to a changing compliance landscape.

![{{site.data.keyword.rw}} operational tools overview](../../images/vrw-v2-opstools.svg "{{site.data.keyword.rw}} operational tools overview"){: caption="Figure 1. {{site.data.keyword.rw}} operational tools overview" caption-side="bottom"}

## Management cluster
{: #vrw-operations-management}

All operational tools are deployed into the management cluster. The {{site.data.keyword.rw}} depends upon multiple layers of tools to deliver comprehensive insight into the operation, security, and compliance of all layers of the platform. Customers that use {{site.data.keyword.rw}} can extend the use of the operational tools to monitor the VMs supporting their applications.

### Caveonix RiskForesight
{: #vrw-operations-management-riskforesight}

[Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-caveonix) provides a comprehensive cloud workload protection platform for {{site.data.keyword.rw}}. This platform delivers a common Risk Management Control Plane (RMCP) for continuous and proactive protection of management and edge workloads.

### VMware Aria Operations
{: #vrw-operations-management-vrops}

[VMware Aria Operations](https://www.vmware.com/products/cloud-infrastructure/aria-operations){: external} delivers self-driving IT operations management from apps to infrastructure to optimize, plan, and scale hybrid cloud and HCI deployments while unifying multicloud monitoring. Powered by AI/ML, VMware Aria Operations helps IT run production operations hands-off and hassle-free with a unified operations platform. This platform delivers continuous performance optimization, efficient capacity management, proactive planning, intelligent remediation, and integrated compliance.

### VMware Aria Operations for Logs
{: #vrw-operations-management-vrli}

[VMware Aria Operations for Logs](https://www.vmware.com/products/cloud-infrastructure/aria-operations-for-logs){: external} delivers heterogeneous and highly scalable log management with intuitive, actionable dashboards, sophisticated analytics, and broad third-party extensibility. It provides deep operational visibility and faster troubleshooting across physical, virtual, and cloud environments.

All systems that generate logs are configured to send their logs to VMware Aria Operations™ for Logs. Centralized collection of all logging enables a comprehensive view of all aspects of the {{site.data.keyword.rw}} operation.VMware Aria Operations for Logs is also capable of forwarding logs to security scanning services such as IBM QRadar.

![VMware Aria Operations for Logs integration](../../images/vrw-v2-operations-logs-flow.svg "VMware Aria Operations for Logs integration"){: caption="Figure 2. VMware Aria Operations for Logs integration" caption-side="bottom"}

### VMware Aria Operations for Networks
{: #vrw-operations-management-vrni}

[VMware Aria Operations for Networks](https://www.vmware.com/products/cloud-infrastructure/aria-operations-for-networks){: external} helps you build an optimized, highly available, and secure network infrastructure across hybrid and multicloud environments. It provides network visibility and analytics to accelerate micro-segmentation security, minimize risk during application migration, optimize network performance and confidently manage and scale NSX deployments.

VMware Aria Operations™ for Networks monitors network components and management traffic throughout the entire {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads instance. The monitoring scope includes insight into the operation of the NSX™ overlay network. VMware Aria Operations for Networks is also used to help optimizing performance by eliminating network bottlenecks. VMware Aria Operations for Networks is an optional component that requires manual installation.

## Gateway cluster
{: #vrw-operations-edge}

No operational tools are deployed to the gateway cluster. The gateway cluster is monitored and managed by using the tools that are deployed on the management cluster. All components of the gateway cluster are configured to deliver their log files to VMware Aria Operations for Logs, inclusive of the virtual gateway syslog facilities. If the physical FortiGate is deployed instead of the gateway cluster, its syslog facility must send logs to VMware Aria Operations for Logs.

## Workload cluster
{: #vrw-operations-workload}

No operational tools are deployed to the workload cluster. The workload cluster is monitored and managed by using the tools that are deployed on the management cluster. All platform components that are deployed in the workload cluster are configured to deliver their log files to VMware Aria Operations for Logs.

## Related links
{: #vrw-operations-related}

* [{{site.data.keyword.cloud_notm}} compliance programs](https://www.ibm.com/cloud/compliance)
* [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)
* [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
