---

copyright:

  years:  2019, 2023

lastupdated: "2023-09-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Juniper Networks vSRX deployment and operation with vCenter Server on {{site.data.keyword.cloud_notm}}
{: #vcsvsrx-intro}

This information is intended for the deployment and operations of a high availability vSRX cluster as the gateway for the VMware vCenter Server®. The guide follows best practices as currently accepted and understood.

Currently, the vSRX is only available as an {{site.data.keyword.cloud}} infrastructure offering. Orders are placed from the [{{site.data.keyword.cloud_notm}} infrastructure customer portal](https://control.softlayer.com/network/gatewayappliances), Networking, Gateway Appliances section.

Initial deployment consists of two bare metal hosts with KVM as the hypervisor and a single vSRX node as the only workload on each host. These items form the high-availability vSRX cluster.

The vSRX cluster must be ordered as noted previously, so the gateway role is assigned to the cluster.

## Related links
{: #vcsvsrx-intro-related}

* [Getting Started with {{site.data.keyword.cloud_notm}} Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started)
* [Juniper Networks vSRX Deployment Guide for VMware](https://www.juniper.net/documentation/en_US/vsrx/information-products/pathway-pages/security-vsrx-vmware-guide-pwp.html){: external}
* [Juniper Networks Requirements for vSRX on VMware](https://www.juniper.net/documentation/en_US/vsrx/topics/reference/general/security-vsrx-vmware-system-requirement.html){: external}
* [Juniper Networks vSRX installation with vSphere Web Client](https://www.juniper.net/documentation/en_US/vsrx/topics/task/installation/security-vsrx-vsphere-client-installing.html){: external}
* [Juniper Networks configuring a vSRX Chassis Cluster in Junos OS](https://www.juniper.net/documentation/en_US/vsrx/topics/task/multi-task/security-vsrx-chassis-cluster-configuring.html){: external}
* [Configure ECMP on VMware NSX](https://letsv4real.com/2016/09/23/configure-ecmp-on-vmware-nsx/){: external}
