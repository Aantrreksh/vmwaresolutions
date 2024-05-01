---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Step 1 - Initial planning and prerequisites
{: #caveonix-step1}

Each Caveonix RiskForesight™ application component is loosely coupled, but centrally managed. Therefore, they can be deployed in an all-in-one virtual machine deployment pattern or the application components can be “scaled-out” and deployed on multiple VMs for higher availability, performance, and capacity.

Deployment patterns are based on both availability requirements and sizing for data retention. RiskForesight deployment nodes can be characterized as:
* Base VMs – The base VMs host the application components that do not scale due to data retention. These components are; RiskForesight UI, RiskForesight App, RiskForesight Plugins, Central Collector, Remote Collector, Index Datastore, Messaging Datastore, and Relational Datastore.
* Scale-out VMs – The scale-out VMs (the database and the data index) scale according to the number of assets and the required data retention. These requirements might create demand for more scale-out hard disk space and more scale-out VMs.

Review the three Caveonix RiskForesight deployment models:
* All-in-one – An automated deployment and configuration of one VM that hosts all the application components:
   * All application components installed on one VM.
   * Remote Collectors can be installed on separate VMs.
   *  Small deployments – up to 100 assets with 7 - 30 days of indexing.
* Partial Distributed – After the automated deployment is completed, you can manually scale out by increasing RAM and disk in the initial VM and add three scale-out VM.
   * UI, App, Plugins, Central Collector, Remote Collector, Index Datastore, Messaging Datastore, and Relational Datastore deployed on one VM.
   * Remote Collectors installed on separate VMs.
   * Index Data Nodes deployed on separate VMs.
   * Small-to-medium deployments – up to 500 assets with 30 days of indexing.
* Fully Distributed - Add more base VMs and scale-out VMs according to the number of assets and data retention requirements:
   * Application components distributed onto separate VMs to facilitate scaling.
   * Required deployment pattern as number of assets increases in the range 500 - 100000.
   * Remote Collectors installed on separate VMs.
   * UI on multiple VMs.
   * App and Plugins on multiple VMs.
   * Central Collector configured in a Cluster.
   * Relational datastore that is deployed in a primary or secondary model.
   * Messaging Datastore deployed in a cluster.
   * Index datastore that is deployed with primary data nodes.
   * More data nodes that are used for scaling out as number of assets increases.

All components must have an FQDN and registered in DNS before any VM deployment. This step is completed by the {{site.data.keyword.vmwaresolutions_full}} automation for the initial all-in-one deployment, but is your responsibility when you scale the deployment.
