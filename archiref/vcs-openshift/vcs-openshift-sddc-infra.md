---

copyright:

  years: 2016, 2024

lastupdated: "2024-06-13"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloud_notm}} networking and infrastructure
{: #vcs-openshift-sddc-infra}

## Physical structure
{: #vcs-openshift-sddc-infra-phys-struct}

The physical infrastructure required to deploy a {{site.data.keyword.redhat_openshift_full}} production instance onto a {{site.data.keyword.vcf-auto}} cluster requires the following minimum specification.

| Item | NFS deployment | vSAN deployment |
|:---- |:-------------- |:--------------- |
| Number of servers | 3 | 4 |
| CPU | 28 Cores 2.2 GHz | 28 Cores 2.2 GHz |
| Memory (GB) | 384 | 384 |
| Storage |2,000 GB 2 IOPS/GB Management </br>2,000 GB 4 IOPS/GB Workload </br>4,000 GB 4 IOPS/GB | Min 960-GB SSD x2 |
{: caption="Table 1. {{site.data.keyword.vcf-classic-short}} specification for Red Hat OpenShift" caption-side="bottom"}

In addition to the {{site.data.keyword.redhat_openshift_notm}} hardware requirements, you must create persistent volumes in the {{site.data.keyword.redhat_openshift_notm}} environment to store images from the container register or customer workloads.

## Virtual structure
{: #vcs-openshift-sddc-infra-virtual-struct}

![Physical structure](../../images/openshift-networking41.svg){: caption="Figure 1. Physical structure" caption-side="bottom"}

Within the {{site.data.keyword.vcf-auto-short}} instance, the {{site.data.keyword.redhat_openshift_notm}} instance is deployed with a dedicated NSX® Edge Services Gateway (ESG) and Distributed Logical Router (DLR). The {{site.data.keyword.redhat_openshift_notm}} installation is loaded into the VXLAN subnet that is defined in the previous components.

The ESG is configured with a source NAT rule (SNAT) to allow outbound traffic, which enables internet connectivity to download the {{site.data.keyword.redhat_openshift_notm}} prerequisites and to connect to GitHub and {{site.data.keyword.redhat_full}}. Alternatively, you can use a web-proxy for internet connectivity. The ESG is also configured to provide access to DNS and NTP services within the {{site.data.keyword.cloud}} environment.

The ESG is also configured to use the load balancer capability, thus reducing the need for HAProxy nodes. The load balancers are configured for the apps wildcard DNS URL and the API / API-INT DNS Records. The apps DNS record load balancers to the worker nodes provisioned, while the api and api-int DNS records are load balanced against the control-plane nodes.

{{site.data.keyword.redhat_openshift_notm}} 4.1 installation on the VMware platform requires a capability to download their ignition files to install and configure the RHCOS bootstrap / control-plane and worker nodes. The ESG is configured to provide DHCP and DHCP relay services for the {{site.data.keyword.redhat_openshift_notm}} logical switch / VXLAN defined.

## NSX Edge specifications
{: #vcs-openshift-sddc-infra-nsx-edge-spec}

The first component that is configured within the {{site.data.keyword.vcf-auto-short}} with {{site.data.keyword.redhat_openshift_notm}} is a pair of NSX Edge virtual machines. The NSX Edge virtual machines are configured as an active-passive pair of X-Large NSX Edge devices.

The Quad-Large NSX Edge was chosen and as part of the configuration process, the NSX Edge is connected to the {{site.data.keyword.cloud_notm}} public and private VLAN.

| Component | Configuration |
|:--------- |:------------- |
| CPU       | 6 vCPU        |
| RAM       | 8 GB          |
| Disk      | 4.5 GB VMDK resident on shared storage with 4 GB swap |
{: caption="Table 2. NSX Edge specifications" caption-side="bottom"}

Because the NSX Edges are configured as active/passive in either the internal or dedicated deployment, vSphere® Distributed Resource Scheduler (DRS) anti-affinity rules must be created by the user to ensure that NSX Edges do not run on the same host as their respective peer appliance.

| Field   | Value         |
|:------- |:------------- |
| Name    | NSX Edge {{site.data.keyword.redhat_openshift_notm}} |
| Type    | Separate VMs |
| Members | `openshift-edge-0` </br>`openshift-edge-1` |
{: caption="Table 3. vSphere Distributed Resource Scheduler rules" caption-side="bottom"}

## NSX Load Balancer specifications
{: #vcs-openshift-sddc-infra-nsx-load-spec}

Within the {{site.data.keyword.redhat_openshift_notm}} environment, two load balancers for accessing the control plane nodes and the worker nodes are required. The NSX Edge is enabled to use load balancing and is configured with application profiles that use a certificate for inbound connection from the source. The NSX Edge is also configured with load-balancing pools to point to the {{site.data.keyword.redhat_openshift_notm}} Primaries and {{site.data.keyword.redhat_openshift_notm}} Workers. Additionally, a virtual server is created with a virtual IP address (vIP) on the private interface with rules that connect the pools with vIP.

| Description | Port number | Algorithm  | Monitor | Members | Protocol | IP subnet |
|:----------- |:----------- |:---------- |:------- |:------- |:-------- |:--------- |
| Application load balancer | 80 | ROUND-ROBIN | default_tcp_monitor | Worker nodes | TCP | {{site.data.keyword.cloud_notm}} 10.x |
| Application load balancer | 443 | ROUND-ROBIN | default_tcp_monitor | Worker nodes | TCP | {{site.data.keyword.cloud_notm}} 10.x |
| API and API-INT load balancer | 6443 | ROUND-ROBIN | default_tcp_monitor | Bootstrap and primary nodes | TCP | {{site.data.keyword.cloud_notm}} 10.x |
| API and API-INT load balancer | 22623 | ROUND-ROBIN | default_tcp_monitor | Bootstrap and primary nodes | TCP | {{site.data.keyword.cloud_notm}} 10.x |
{: caption="Table 4. NSX load balancer specifications" caption-side="bottom"}

## Red Hat OpenShift specifications
{: #vcs-openshift-sddc-infra-redhat-spec}

The following tables show the specifications of the management node, control plane node, and worker node.

| Host description | vCPU  | Memory (GB) | Disk (GB) | OS |
|:---------------- |:----- |:----------- |:--------- |:-- |
| `Management0` | 2 | 8 | 50 | {{site.data.keyword.redhat_notm}} Enterprise Linux® 8.0 |
{: class="simple-tab-table"}
{: caption="Table 5. Management node specifications" caption-side="bottom"}
{: #table1}
{: tab-title="Management node"}
{: tab-group="rhos-specs"}

| Host description | vCPU  | Memory (GB) | Disk (GB) | OS | Hostname |
|:---------------- |:----- |:----------- |:--------- |:-- |:--------- |
| Control-plane0 | 4 | 8 | 60 | {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS |
| Control-plane1 | 4 | 8 | 60 | {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS |
| Control-plane2 | 4 | 8 | 60 | {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS |
{: class="simple-tab-table"}
{: caption="Table 5. Control plane node specifications" caption-side="bottom"}
{: #table2}
{: tab-title="Control plane node"}
{: tab-group="rhos-specs"}

| Host description | vCPU  | Memory (GB) | Disk (GB) | OS | Hostname |
|:---------------- |:----- |:----------- |:--------- |:-- |:--------- |
| Worker0 | 16 | 32 | 200 | {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS |
| Worker1 | 16 | 32 | 200 | {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS |
| Worker2 | 16 | 32 | 200 | {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS |
{: caption="Table 5. Worker node specifications" caption-side="bottom"}
{: #table3}
{: tab-title="Worker node"}
{: tab-group="rhos-specs"}
{: class="simple-tab-table"}

## Related links
{: #vcs-openshift-sddc-infra-related}

* [{{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-intro)
* [System context for {{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-syscontext)
* [{{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-redhat-arch)
* [{{site.data.keyword.vmwaresolutions_short}} SDDC architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-arch)
