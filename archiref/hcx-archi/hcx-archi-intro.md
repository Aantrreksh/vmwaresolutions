---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware HCX introduction
{: #hcx-archi-intro}

The VMware® HCX™ service enables creating a seamless connection between {{site.data.keyword.vmwaresolutions_full}} instances and an on-premises VMware virtualized data center.

The {{site.data.keyword.vmwaresolutions_short}} includes fully automated, rapid deployments of {{site.data.keyword.vcf-auto}} in the {{site.data.keyword.cloud_notm}}. These offerings complement the on-premises infrastructure and allow existing and future workloads to run in the {{site.data.keyword.cloud_notm}} without conversion by using the same tools, skills, and processes they use on-premises.

The VMware HCX service takes this hybridity to the next step, blending instances of {{site.data.keyword.vcf-auto-short}} with existing on-premises virtualized data centers. It enables the creation of seamless network extensions and bidirectional migration of workloads.

The VMware HCX components are deployed as virtual machines (VMs) in the {{site.data.keyword.cloud_notm}} VMware target site. They allow a connection with the VMware HCX components that are installed in the peer on-premises source site.

![{{site.data.keyword.vcf-auto-short}} – Hybrid Cloud services](../../images/ibmcloud-hcx-overview.svg "{{site.data.keyword.vcf-auto-short}} – HCX overview"){: caption="Figure 1. {{site.data.keyword.vcf-auto-short}} - HCX overview" caption-side="bottom"}

This connection creates a loosely coupled interconnectivity between on-premises and {{site.data.keyword.cloud_notm}} and enables capabilities, such as:
* Simple interconnectivity – logical network connections are established easily over any physical connection such as public internet, private VPN, or direct link.
* Layer 2 extension – on-premises networks are extended into the cloud. These networks include on-premises subnets and IP addressing.
* Encryption – network traffic is securely encrypted between the two sides.
* Optimized network – selects the best connection and efficiently floods the connection so that network traffic is moved as fast as possible.
* Data deduplication – as much as 50% reduction in network traffic can be achieved
* vMotion migration - a single running system can be moved between HCX enabled sites by using the VMware vMotion protocol with no service interruption.
* Bulk migration - multiple systems can be moved in parallel using VMware vSphere® Replication protocol between HCX enabled sites.
* Scheduled migration – any number of VMs can be replicated to the destination site and then activated on that site at a designated time. The replication replaces the systems that are running on the originating site.
* Migration of security policies – if NSX is used on-premises, any security policies or firewalls are moved along with the workload.

## Related links
{: #hcx-archi-intro-related}

* [Glossary of HCX components and terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-components)
* [HCX Client deployment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-client-deployment)
* [HCX on-premises Service Mesh](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-mesh-deployment)
* [VMware Hybrid Cloud migrations](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-migrations)
* [Monitoring parameters and components](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-monitoring)
* [HCX troubleshooting](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-troubleshooting)
