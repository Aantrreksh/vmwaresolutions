---

copyright:

  years:  2020, 2024

lastupdated: "2024-06-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Bare metal hosts
{: #vrw-baremetal}

The {{site.data.keyword.cloud}} for VMware® Regulated Workloads is built upon multiple clusters of bare metal hosts with VMware ESXi™ as the hypervisor.

![{{site.data.keyword.rw}} infrastructure overview](../../images/vrw-v2-overview.svg "{{site.data.keyword.rw}} infrastructure overview"){: caption="{{site.data.keyword.rw}} infrastructure overview" caption-side="bottom"}

## Management cluster
{: #vrw-baremetal-management}

The management cluster is formed of four bare metal hosts. Configuring the cluster with four hosts is the mandatory, minimum requirement where vSAN™ is the storage platform. These hosts are sized to meet the requirements of the management applications. No nonmanagement workloads are run in the management cluster.

## Gateway cluster
{: #vrw-baremetal-edge}

The gateway cluster requires only two bare metal hosts. vSAN is not an available storage option. Shared storage is not required since use of the local datastore is preferred. The hosts are sized to support the requirements of the virtual router or gateway appliance that is deployed to the individual hosts.

## Workload cluster
{: #vrw-baremetal-workload}

The workload cluster uses vSAN for storage and thus a minimum of four bare metal hosts with ESXi as the hypervisor are required. More hosts are added as necessary to scale horizontally to deliver the required compute, memory, and storage required by the hosted applications.

The deployment of more workload clusters is supported to supply dedicated resources for an application or business unit.

## Physical host connections
{: #vrw-baremetal-phys-connect}

Each physical host in this design has two redundant pairs of 10 Gbps Ethernet connections into each {{site.data.keyword.cloud_notm}} Top of Rack (ToR) switch (public and private). The adapters are set up as individual connections (unbonded) for a total of 4 x 10 Gbps connections. This design allows networking interface card (NIC) connections to work independently from each other.

Removing physical network connectivity to the public or private network for the bare metal servers that are used within the vCenter Server offering is not possible. When a {{site.data.keyword.rw}} instance is deployed with the private only network option, the physical ports on the internal NIC of the bare metal hosts are disabled and the ToR switch ports are administratively down. There is no support for unplugging the cables.

![Physical host connections](../../images/vrw-v2-baremetal.svg "Physical host connections"){: caption="Physical host connections" caption-side="bottom"}

To prevent undesired access, the SaaS provider must change the IPMI password and not update it in the VMware Solutions console. The insertion of filters to prevent network access to the IPMI from non-SaaS provider-controlled subnets is recommended.

## Related links
{: #vrw-baremetal-related}

* [{{site.data.keyword.cloud_notm}} compliance programs](https://www.ibm.com/cloud/compliance)
