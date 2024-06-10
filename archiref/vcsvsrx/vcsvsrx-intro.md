---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Juniper Networks vSRX deployment and operation with {{site.data.keyword.vcf-auto}}
{: #vcsvsrx-intro}

This information is intended for the deployment and operations of a high availability vSRX cluster as the gateway for the {{site.data.keyword.vcf-auto-short}}. The guide follows best practices as currently accepted and understood.

Currently, the vSRX is only available as an {{site.data.keyword.cloud}} infrastructure offering. Orders are placed from the [{{site.data.keyword.cloud_notm}} infrastructure customer portal](https://control.softlayer.com/network/gatewayappliances), Networking, Gateway Appliances section.

Initial deployment consists of two bare metal hosts with KVM as the hypervisor and a single vSRX node as the only workload on each host. These items form the high-availability vSRX cluster.

The vSRX cluster must be ordered as noted previously, so the gateway role is assigned to the cluster.

## Related links
{: #vcsvsrx-intro-related}

* [Getting Started with {{site.data.keyword.cloud_notm}} Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started)
* [Understand vSRX Virtual Firewall with VMware](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/concept/security-vsrx-vmware-overview.html){: external}
* [Requirements for vSRX Virtual Firewall on VMware](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/concept/security-vsrx-vmware-system-requirement.html){: external}
* [Install vSRX Virtual Firewall with VMware vSphere Web Client](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/task/security-vsrx-vsphere-client-installing.html){: external}
* [Configure a vSRX Virtual Firewall Chassis Cluster in Junos OS](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-hyper-v/topics/task/security-vsrx-chassis-cluster-configuring.html){: external}
* [Configure ECMP on VMware NSX](https://letsv4real.com/2016/09/23/configure-ecmp-on-vmware-nsx/){: external}
