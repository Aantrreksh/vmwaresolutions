---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture pattern for single site vCenter Server deployment topologies 
{: #arch-pattern-deployment-single-site}

{{site.data.keyword.vcf-auto}} instances offer a standard initial topology with a single management or converged cluster. It includes a vCenter, three VMware NSX™ managers, and an Active Directory™ deployment. They run either on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or on two VMware virtual machines (VMs) in a high availability deployment. The initial deployment also includes a standard NSX topology.

You have several options to expand the capacity for the deployment by provisioning new hosts on the initial cluster or by adding new clusters. This pattern provides a few examples on how to expand and customize the initial deployment for a few use cases to fit your needs.

To customize the NSX topologies, see [the architecture pattern for single site NSX topologies](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-single-site).
{: note}

## Single-site vCenter Server deployment
{: #arch-pattern-deployment-single-site-vcs-depl}

Single-site deployment is the most common use case and network deployment pattern. This pattern uses a single [{{site.data.keyword.vcf-auto-short}} instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview). It is also highly scalable and easier to manage and expand.

The following diagram shows an example of a customer deployment by using the standard topology. You can add more hosts or new clusters to scale the solution.

![Single-site deployment topology](../../images/arch-pattern-s-s-1.svg "Single-site deployment topology."){: caption="Single-site deployment topology" caption-side="bottom"}

1. The vCenter Server automation deploys an initial vSphere cluster, which includes a vCenter, three NSX managers, and an Active Directory deployment. They run either on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment. The initial vSphere cluster is deployed on the initial {{site.data.keyword.cloud_notm}} data center location. This vSphere cluster also hosts NSX edge transport node VMs for services and workload NSX edge clusters. The workload NSX edge cluster is purpose for your workloads, while the services NSX edge cluster is used by optional add-on services. You can expand the capacity of this vSphere cluster by ordering new hosts through {{site.data.keyword.vmwaresolutions_short}} portal. 
2. If you select an optional gateway cluster, the vCenter Server automates two ESXi hosts by using {{site.data.keyword.cloud_notm}} bare metal server and forms a new vSphere cluster in your deployment. These ESXi hosts can be used to host, for example, Juniper vSRX virtual router and firewall appliances. This cluster hosts also behave such as [{{site.data.keyword.cloud_notm}} gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-about), which allows you to assign and route VLANs through the router or firewall that is hosted on the cluster.
3. You can add new vSphere clusters to increase the compute capacity for your workloads. You can add vSphere clusters with different host specifications, and define how to functionally position these clusters and what workloads are run on each cluster.
4. You can add NFS based {{site.data.keyword.filestorage_full_notm}} to your clusters. You can add one or more file shares and configure them individually by selecting the performance (IOPS) and size (GB) for each.
5. You can also use vSAN™ with your vSphere clusters. When you are using vSAN, due to the nature of dedicated local storage, you must select the vSAN option when you order the cluster.
6. The hosts in the specific data center or POD are attached to VLANs and subnets that are local to that {{site.data.keyword.cloud_notm}} data center or POD. These VLANs and subnets cannot be extended or moved to other {{site.data.keyword.cloud_notm}} data centers. However, these subnets can communicate with subnets that are provisioned to another {{site.data.keyword.cloud_notm}} center over {{site.data.keyword.cloud_notm}} private network. 

## Extending a single-site vCenter Server deployment to another data center
{: #arch-pattern-deployment-single-site-extend}

Single-site deployment can be expanded to another {{site.data.keyword.cloud_notm}} data center by provisioning new clusters on a different {{site.data.keyword.cloud_notm}} data center location.

The following diagram shows an example of a customer deployment by using this deployment topology.

![Extended single-site deployment topology](../../images/arch-pattern-s-s-2.svg "Extended single-site deployment topology."){: caption="Extended single-site deployment topology" caption-side="bottom"}

1. The vCenter Server automation deploys an initial vSphere cluster, which includes a vCenter, three NSX managers, and an Active Directory deployment. They run either on a single {{site.data.keyword.cloud_notm}} Classic Virtual Server Instance or two VMware VMs in a high availability deployment. The initial vSphere cluster is deployed on the initial {{site.data.keyword.cloud_notm}} data center location. These management workloads are not moved from their original location.
2. You can add new vSphere clusters to increase the compute capacity for your workloads in a different {{site.data.keyword.cloud_notm}} data center location. By default, your workloads can communicate by using NSX overlay segments and you can connect them to the physical network through the initial location. If you want to use the physical connectivity through the new location to access {{site.data.keyword.cloud_notm}} private or public networks, you must [manually customize the NSX topology](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-single-site).
3. If you select an optional gateway cluster on this new location, the vCenter Server automates two ESXi hosts by using {{site.data.keyword.cloud_notm}} bare metal server and forms a new vSphere cluster in your deployment. These ESXi hosts can be used to host, for example, Juniper vSRX and they also behave such as [{{site.data.keyword.cloud_notm}} gateway appliance](/docs/gateway-appliance?topic=gateway-appliance-about).
4. You can add more vSphere clusters on this secondary location. You can add vSphere clusters with different host specifications, and define how to functionally position these clusters and what workloads are run on each cluster.
5. You can add NFS based {{site.data.keyword.filestorage_full_notm}} to your clusters in the new data center location. These NFS shares are local to the data center, and they cannot be accessed from the initial data center.
6. You can also use vSAN with your vSphere clusters in the new data center location. When you are using vSAN, due to the nature of dedicated local storage, you must select the vSAN option when you order the cluster. This deployment pattern does not offer stretched vSAN clusters.
7. The hosts in the new data center (or POD) are attached to VLANs and subnets that are local to that {{site.data.keyword.cloud_notm}} data center or POD. These VLANs and subnets cannot be extended or moved to other {{site.data.keyword.cloud_notm}} data centers. However, these subnets can communicate with subnets that are provisioned to another {{site.data.keyword.cloud_notm}} data center over {{site.data.keyword.cloud_notm}} private network. 

If you deploy clusters or hosts in another POD of the same {{site.data.keyword.cloud_notm}} data center, you must use the same backend NFS storage. The storage is assigned for each cluster separately.
{: note}

## Considerations for single site vCenter Server deployment topologies 
{: #arch-pattern-deployment-single-site-considerations}

When you are designing or deploying this architecture pattern, take the following information into consideration:

* You have several options to expand the capacity for the deployment, for example by provisioning new hosts on the initial cluster or by adding new clusters. 
* This pattern provides a few examples of how to expand and customize the initial deployment for a few use cases to fit your needs, but note that these are just examples. 
* Note any VMware limitations.

To customize the NSX overlay topologies, see [the architecture pattern for single site NSX topologies](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-single-site).
{: note}

## Related links
{: #arch-pattern-deployment-single-site-links}

* [vCenter Server overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [Architecture pattern for single site NSX topologies](/docs/vmwaresolutions?topic=vmwaresolutions-arch-pattern-overlays-single-site)
