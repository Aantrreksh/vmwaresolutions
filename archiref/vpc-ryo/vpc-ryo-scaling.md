---

copyright:

  years:  2022, 2024

lastupdated: "2024-03-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Scaling capacity
{: #vpc-ryo-scaling}

After initial deployment, you can scale out the compute capacity on demand. The design supports the following scale-out paths:

* Addition of new hosts to an existing cluster in the same Zone.
* Addition of new clusters in the same Zone.
* Addition of a new deployment in a new Zone in the same or different Region.

## Adding ESXi hosts into existing clusters
{: #vpc-ryo-scaling-hosts}

You can scale out an existing cluster by ordering hosts. You must add manually the hosts to your cluster and provision the required VLAN interfaces to the hosts for VMkernel adapters.

## Adding new clusters
{: #vpc-ryo-scaling-clusters}

You can also scale out the compute capacity by ordering new hosts and creating a new cluster. You must add manually the hosts to create the cluster and provision the required VLAN interfaces to the hosts for VMkernel adapters.

This method allows achieving the following tasks:

* Creating an additional, separate cluster in the environment.
* Separating management workloads from application workloads physically and logically.
* Separating workloads based on other characteristics, for example, Microsoft® SQL database cluster.
* Deploying applications in highly available topologies.

## Adding more sites
{: #vpc-ryo-scaling-sites}

You can use other multizone regions and {{site.data.keyword.cloud}} worldwide data center presence to allow for various cross-geographies use cases to be deployed.

This method allows achieving the following tasks:

* Creating an additional, geographically separated deployment for Disaster Recovery use cases.
* Creating an additional, geographically separated deployment for closer proximity to users.
* Creating an additional, geographically separated deployment for Regulatory or Compliance reasons of your business and workloads.

## Related links
{: #vpc-ryo-scaling-links}

* [{{site.data.keyword.vpc_short}} getting started](/docs/vpc?topic=vpc-getting-started)
* [{{site.data.keyword.vpc_short}} Bare Metal Servers](/docs/vpc?topic=vpc-planning-for-bare-metal-servers)
* [{{site.data.keyword.vpc_short}} RYO VMware reference architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-ryo-arch-overview)
* [{{site.data.keyword.dl_full_notm}} overview](/docs/dl?topic=dl-get-started-with-ibm-cloud-dl)
* [{{site.data.keyword.tg_full_notm}} overview](/docs/transit-gateway?topic=transit-gateway-getting-started)
* [{{site.data.keyword.vpc_short}} VPN overview](/docs/vpc?topic=vpc-vpn-overview)
* [VPC IaaS endpoints](/docs/vpc?topic=vpc-service-endpoints-for-vpc#infrastructure-as-a-service-iaas-endpoints)
