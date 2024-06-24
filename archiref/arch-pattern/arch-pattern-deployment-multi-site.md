---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-03"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for multisite vCenter Server deployment topologies
{: #arch-pattern-deployment-multi-site}

{{site.data.keyword.vcf-auto}} instances offer a standard initial topology with a single management or converged cluster, which includes a vCenter, three VMware NSX™ managers, and an Active Directory™ deployment. These deployments run either on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or on two VMware virtual machines (VMs) in a high availability deployment. The initial deployment also includes a standard NSX topology.

You have several options to expand the capacity for the deployment by provisioning new hosts on the initial cluster or by adding new clusters. This pattern provides a few examples on how to expand and customize the initial deployment for a few use cases to fit your needs.

To customize the NSX topologies, see [the architecture pattern for multisite NSX topologies](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-multi-site).
{: note}

## Multisite vCenter Server deployment
{: #arch-pattern-deployment-multi-site-base}

The multisite deployment is a common use case and network deployment pattern. This topology is highly scalable and it is easy to manage and expand. The multisite deployment pattern is based on the [vCenter Server multisite deployment option](/docs/vmwaresolutions?topic=vmwaresolutions-vc_multisite).

The following diagram shows an example of a customer deployment by using this topology. You can add more hosts or new clusters to scale the solution.

![Multisite deployment topology](../../images/arch-pattern-m-s.svg "Multisite deployment topology."){: caption="Figure 1. Multisite deployment topology" caption-side="bottom"}

1. The vCenter Server automation deploys an initial vSphere cluster on the primary instance, which includes a vCenter, three NSX managers, and an Active Directory deployment. They run either on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment. This instance includes a vCenter, three NSX managers, an Active Directory deployment with either running on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment and two NSX edge clusters, one for services and one for workloads.
2. The initial {{site.data.keyword.vcf-auto-short}} instance can include several vSphere clusters (refer to single site deployment). They are typically deployed in the initial {{site.data.keyword.cloud_notm}} data center location.
3. You can provision a secondary {{site.data.keyword.vcf-auto-short}} instance after the primary that is deployed. This option deploys automatically a secondary {{site.data.keyword.vcf-auto-short}} instance in the new {{site.data.keyword.cloud_notm}} data center location. This instance is then linked to the initial primary vCenter Server single site deployed on step 1. You can create multiple secondary instances. As the primary, this instance includes a vCenter, three NSX managers, an Active Directory deployment with either running on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment and two NSX edge clusters, one for services and one for workloads. The second site is under the same SSO and root domain as the primary.
4. As the primary, also the secondary {{site.data.keyword.vcf-auto-short}} instance can include several vSphere clusters. They are typically deployed in the same {{site.data.keyword.cloud_notm}} data center location as the secondary.
5. You can add NFS based {{site.data.keyword.filestorage_full_notm}} to your clusters. You can add one or more file shares and configure them individually by selecting the performance (IOPS) and size (GB) for each. Each data center and each instance uses its own storage.
6. You can also use vSAN with your vSphere clusters. When you use vSAN, due to the nature of dedicated local storage, you must select vSAN option when ordering the cluster. Each instance uses its own storage.
7. Both primary and secondary instance have their own NSX managers and their own NSX topologies. Each instance has a workload edge cluster, which consists of two edge transport nodes for your usage.
8. The hosts and NSX Tier-0 Gateways in the specific data center or POD are attached to VLANs and subnets that are local to that {{site.data.keyword.cloud_notm}} data center or POD. These VLANs and subnets cannot be extended or moved to other {{site.data.keyword.cloud_notm}} data centers. However, these subnets can communicate with subnets that are provisioned to another {{site.data.keyword.cloud_notm}} data center over {{site.data.keyword.cloud_notm}} private network.
9. If you select an optional gateway cluster, the vCenter Server automates two ESXi hosts by using {{site.data.keyword.cloud_notm}} bare metal servers and forms a new vSphere cluster in your deployment. This can be done on each instance separately.

## Dual-site vCenter Server deployment
{: #arch-pattern-deployment-dual-site-base}

The dual-site deployment is typically suitable for the production and disaster recovery use cases. This deployment pattern is based on two [vCenter Server as a single site instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview), where each instance is deployed separately and they do not have any common management. This pattern is highly scalable and each instance is managed and expand separately. Integration between these environments is typically at network level and in disaster recovery use cases, third-party products are typically used to replicate data and VMs.

The following diagram shows an example of a customer deployment by using this topology. 

![Dual-site deployment topology](../../images/arch-pattern-d-s.svg "Dual-site deployment topology."){: caption="Figure 2. Dual-site deployment topology" caption-side="bottom"}

1. The vCenter Server automation deploys instance A and its management or converged cluster, which includes a vCenter, three NSX managers, and an Active Directory deployment. They run either on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment. This instance includes a vCenter, three NSX managers, an Active Directory deployment with either running on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment and two NSX edge clusters, one for services and one for workloads.
2. You can provision another {{site.data.keyword.vcf-auto-short}} instance, instance B, at the same time or later than the instance A. By using this option, the automation deploys a new {{site.data.keyword.vcf-auto-short}} instance in the new {{site.data.keyword.cloud_notm}} data center location. As the instance A, this instance includes a vCenter, three NSX managers, an Active Directory deployment with either running on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment and two NSX edge clusters, one for services and one for workloads.
3. Both {{site.data.keyword.vcf-auto-short}} instances can include several vSphere clusters (refer to single site deployment). 
4. If you select an optional gateway cluster, the vCenter Server automates two ESXi hosts by using {{site.data.keyword.cloud_notm}} bare metal servers and forms a new vSphere cluster in your deployment. This can be done on each instance separately.
5. Each instance has its own storage, which can be NFS based {{site.data.keyword.filestorage_full_notm}} or vSAN. You can add one or more NFS file shares and configure them individually by selecting the performance (IOPS) and size (GB) for each. When you use vSAN, due to the nature of dedicated local storage, you must select vSAN option when ordering the cluster.
6. Both instances have their own NSX managers and their own NSX topologies. Each instance has a workload edge cluster, which consists of two edge transport nodes for your usage.
7. The hosts and NSX Tier-0 Gateways in the specific data center or POD are attached to VLANs and subnets that are local to that {{site.data.keyword.cloud_notm}} data center or POD. These VLANs and subnets cannot be extended or moved to other {{site.data.keyword.cloud_notm}} data centers. However, these subnets can communicate with subnets that are provisioned to another {{site.data.keyword.cloud_notm}} data center over {{site.data.keyword.cloud_notm}} private network.

## Considerations for multisite vCenter Server deployment topologies 
{: #arch-pattern-deployment-multi-site-considerations}

When you design or deploy this architecture pattern, consider the following steps:

* You have several options to expand the capacity for the deployment, for example by provisioning new hosts on the initial cluster or by adding new clusters. 
* This pattern provides a few examples of how to expand and customize the initial deployment for a few use cases to fit your needs, but note that these are just examples. 
* You must note VMware limitations. 

To customize the NSX overlay topologies, see [the architecture pattern for multisite NSX topologies](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-multi-site).
{: note}

## Related links
{: #arch-pattern-deployment-multi-site-links}

* [vCenter Server overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [Architecture pattern for multisite NSX topologies](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-multi-site)
* [Multisite configuration for {{site.data.keyword.vcf-auto-short}} instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_multisite)

