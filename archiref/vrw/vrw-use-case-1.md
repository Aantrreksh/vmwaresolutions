---

copyright:

  years:  2020, 2024

lastupdated: "2024-06-04"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Use case 1
{: #vrw-use-case-1}

{{site.data.keyword.cloud}} for VMware® Regulated Workloads delivers a virtualized platform for users in a highly regulated industry who require a platform that is designed to support compliance with industry security standards or governmental regulations.

Typical hyper-converged virtual infrastructure designs include management, edge services, and compute all on the same cluster. This approach might blur the lines between the virtualization administrator, typically responsible for the compute and storage infrastructure, the network administrator, and the security administrator.

The {{site.data.keyword.rw}} architecture restores the strict separation of duties that are usually enforced in an on-premises environment.

The {{site.data.keyword.rw}} architecture spreads the delivery of necessary services across purpose-built regions.

The management region allows the virtualization administrator to manage the entire compute and storage infrastructure. Through the adoption of NSX™ as the SDN provider for the workloads, it removes the network and security administration duties from the scope of the virtualization administrator role. NSX, unlike NSX for vSphere, is not reliant upon a vCenter to manage the SDN network objects, traffic flows, and security configurations. Divorcing the network control plane from the vCenter means it is no longer possible for the virtualization administrator to view or change anything that impacts the network.
The network and security administrators use the NSX dedicated management portal to configure the network and the required security policies.

The edge services region is strictly limited to the protection of the management region and the vSphere components that deliver compute and storage resources to the workload region. The security administrator, who has the responsibility of managing the SDN security, might also serve as the administrator of the gateway VMs that run on the gateway cluster. Or, to isolate a single administrator's scope of influence, the responsibility might be assigned to an administrator who has access only to the edge gateway and no access to manage SDN security.

The workload region is managed by one or more administrators that are only responsible for the management of the application VMs deployed upon the workload clusters. One approach where multiple administrators are useful is the case where a user wants to isolate administrative tasks on a per business unit basis or other compliance requirements.

Three distinct regions: the management region, the edge services region, and the workload region, design the zero trust security model into the {{site.data.keyword.rw}}. Taking advantage of this design through audited and enforced separation of duties at every possible opportunity, assists users to comply with industry standards or government regulations, making the {{site.data.keyword.rw}} that are uniquely suited to host applications for clients in highly regulated industries.

## Related links
{: #vrw-use-case-1-related}

* [{{site.data.keyword.cloud_notm}} compliance programs](https://www.ibm.com/cloud/compliance)
