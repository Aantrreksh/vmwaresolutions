---

copyright:

  years:  2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for deploying Tanzu on VMware Cloud Foundation standard architecture
{: #arch-pattern-vcf-tanzu-std}

This architecture pattern explains how to deploy VMware Tanzu on {{site.data.keyword.vcf-vpc}} standard architecture deployment in {{site.data.keyword.vpc_short}}. Tanzu is a modular, cloud-native application platform that accelerates development, delivery, and operations across multiple clouds. With Tanzu, you can deploy containers on a Kubernetes-based platform that is integrated with VMware vSphere® and VMware NSX®.

An overview of this architecture pattern is shown in the following diagram.

![Tanzu on VMware Cloud Foundation standard architecture](../../images/vcf-arch-tanzu-std.svg "Tanzu on VMware Cloud Foundation standard architecture."){: caption="Figure 1. Tanzu on VMware Cloud Foundation standard architecture" caption-side="bottom"}

Tanzu can be deployed only on the VMware Cloud Foundation standard architecture.
{: important}

## Deploying Tanzu on VMware Cloud Foundation standard architecture deployment
{: #arch-pattern-vcf-tanzu-std-deploy}

The following diagram represents high-level deployment steps for Tanzu implementation. In this architecture pattern, Tanzu will be deployed into NSX overlay at the VI workload domain.

![Deploying Tanzu on VMware Cloud Foundation standard architecture](../../images/vcf-arch-tanzu-std-steps.svg "Deploying Tanzu on VMware Cloud Foundation standard architecture."){: caption="Figure 2. Deploying Tanzu on VMware Cloud Foundation standard architecture" caption-side="bottom"}

This architecture pattern deployment is summarized as follows:

1. Design IP addressing for the Tanzu networks on the VI workload domain's NSX overlay. Create VPC (Virtula Private Cloud) routes for routable Tanzu networks with VI workload Tier 0 HA VIP as the next-hop for these networks.
1. Deploy Tanzu on VI workload domain following the VMware Cloud Foundation and Tanzu documentation.
1. Add DNS records to DNS Service as needed.

## Considerations for deploying Tanzu on VMware Cloud Foundation standard architecture
{: #arch-pattern-vcf-tanzu-std-considerations}

When you design or deploy this architecture pattern, not that Tanzu can only be deployed on the VMware Cloud Foundation standard architecture.
{: important}

## Related links
{: #arch-pattern-vcf-tanzu-std-links}

* [VPC network design](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-vpc-deployment)
* [Developer Ready Infrastructure for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/vcf-developer-ready-infrastructure-v1/GUID-641F8C25-CA4E-4F27-B467-484C849C7332.html){: external}
* [VMware Cloud Foundation with VMware Tanzu](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-9BEED8EB-0DD7-4AC1-A9ED-216EDEA97D6C.html){: external}
