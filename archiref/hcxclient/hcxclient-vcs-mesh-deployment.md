---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# HCX on-premises Service Mesh
{: #hcxclient-vcs-mesh-deployment}

Review the following steps to configure the VMware HCX™ Client instance.

## Site pairing the VMware Solutions environment
{: #hcxclient-vcs-mesh-deployment-sitepair}

1. Log in to the VMware vSphere® Web Client.
2. From the **Home** menu, select the **HCX** option.
3. Under **Infrastructure**, **InterConnect**, click **Add Site Pairing**.
   1. Set the Site URL to the HCX Cloud Manager URL, for example, `https://x.x.x.x.x`.
   2. Set the username and password to the HCX Manager Admin Details: `admin / password`.

      The previous details can be obtained from the {{site.data.keyword.vmwaresolutions_full}} console, under **Services**, **HCX** for the {{site.data.keyword.vcf-auto}} instance.

4. Click **Connect**.

### Results
{: #hcxclient-vcs-mesh-deployment-sitepair-results}

The Site Pairing is registered and displayed on the user interface.

## Creating HCX on-premises profiles
{: #hcxclient-vcs-mesh-deployment-profiles}

### Creating on-premises Service Mesh network profiles
{: #hcxclient-vcs-mesh-deployment-profiles-network}

1. Log in to the vSphere Web Client.
2. From the **Home** menu, select the **HCX** option.
3. Under **Infrastructure**, click **InterConnect**.
4. Under **Multi-Site Service Mesh**, click **Network Profiles**.
5. From **Create Network Profile**:
   1. Select Distributed Port Group, for example, External.
   2. Provide IP address ranges for **External IPs**, **External Subnet Prefix Length**, **External Gateway**, and **DNS Details**.
   3. Set MTU to 1500.
   4. Click **Create**.
6. Repeat the previous steps for Management and vMotion Networks. Set the MTU value to 9000.

#### Results
{: #hcxclient-vcs-mesh-deployment-profiles-network-results}

| Network Name | MTU |
| -----| ----|
| External | 1500 |
| Management | 9000 |
| vMotion | 9000 |
{: caption="Table 1. Results" caption-side="bottom"}

### Creating on-premises Service Mesh compute profiles
{: #hcxclient-vcs-mesh-deployment-profiles-compute}

1. Log in to the vSphere Web Client.
2. From the **Home** menu, select the **HCX** option.
3. Under **Infrastructure**, click **InterConnect**.
4. Under **Multi-Site Service Mesh**, click **Compute Profiles**.
5. From **Create Compute Profile**:
   1. Provide Compute Profile Name.
   2. Select All Services to be enabled, click **Continue**.
   3. Select the Cluster, click **Continue**.
   4. Select the Datastore, click **Continue**.
   5. Select Network Profile for Management, click **Continue**.
   6. Select **Network Profile for External/Uplink**, click **Continue**.
   7. Select Network Profile for vMotion, click **Continue**.
   8. Select Network Profile for vSphere Replication (Management), click **Continue**.
   9. Select Distribute Switch for extension, for example, Private-Switch, click **Finish**.

#### Results
{: #hcxclient-vcs-mesh-deployment-profiles-compute-results}

A compute profile for the cluster and storage combination is created and is available with the Service Mesh creation.

## HCX on-premises Service Mesh
{: #hcxclient-vcs-mesh-deployment-servicemesh}

## Creating on-premises Service Mesh
{: #hcxclient-vcs-mesh-deployment-servicemesh-creation}

1. Log in to the vSphere Web Client.
2. From the **Home** menu, select the **HCX** option.
3. Under **Infrastructure**, click **InterConnect**.
4. Under **Multi-Site Service Mesh**, click **Service Mesh**.
5. From **Create Service Mesh**:
   1. Select sites: on-premises and vCloud Organization, click **Continue**.
   2. Select Source Compute Profile.
   3. Select Remote Compute Profile. For example, CloudCompute.
   4. Select All Services, click **Continue**.
   5. Click **Continue**, on page Advanced Configuration - Override Uplink Network profiles (Optional)
   6. Click **Continue**.
   7. Click **Continue**, leave default on page Advanced Configuration - Configure WAN Optimization Service Bandwidth Limit.
   8. Provide Service Name, click **Finish**.
6. Watch the task list for Service Mesh creation. After successful completion, the on-premises location has three HCX appliances and the cloud location has three HCX appliances.

### Results
{: #hcxclient-vcs-mesh-deployment-servicemesh-results}

An HCX Service Mesh is the effective HCX services configuration for a source and destination site. A Service Mesh can be added to a connected Site Pair with a valid Compute Profile created on both sites.

Adding a Service Mesh initiates the deployment of HCX Interconnect virtual appliances on both of the sites. An interconnect Service Mesh is always created at the source site.

## Network stretching
{: #hcxclient-vcs-mesh-deployment-network-stretching}

To stretch a network (VLAN or VXLAN) with HCX, complete the following steps from the client-side vCenter web user interface.
1. Log in to the vSphere Web Client.
2. From the **Home** menu, select the **HCX** option.
3. In the left menu, under **Services**, click **Network Extension**.
4. Click **Extend Network**:
   1. Select the network to be extended.
   2. Type the current default gateway and subnet mask in CIDR format.
   3. Scroll down and click **Stretch** to begin the network stretch workflow.

Network progress is monitored in the vCenter client tasks pane.

## Concepts and best practices for network stretching
{: #hcxclient-vcs-mesh-deployment-stretching-best-practices-network}

The glue that bridges the client-side network to the cloud side VXLAN is a sophisticated multitunnel VPN that consists of proprietary HCX technology. It is not based on NSX, but does work with NSX and extend its capability. This process is controlled by the client-side vCenter web user interface and automates the deployment and starting of both endpoints on the client and cloud side. Selecting the network to stretched is done individually or in batch.

Additionally, as part of the network stretching workflow, NSX on the cloud side is authorized to build a VXLAN. The VXLAN is then connected to an interface created on the specified cloud side L3 device (DLR or ESG left in an unconnected state) and the cloud side Network Extension appliance.

Typically, when you migrate a particular application, all the networks in use by the applicable virtual machines (VMs) must get stretched across the {{site.data.keyword.cloud}} instance.

Why typically and not always? It can be advantageous to disconnect certain traffic from the client side after the VM is migrated. For example, VM guest backup clients, which might cause high-bandwidth use when moved to the cloud. The in-guest backup client is not required when the VM is migrated as it is automatically picked up by a more modern block level backup on the cloud side.

The client’s backup network adapter is not being accessed because it would mean accessing each VM to shut off the in-guest client backup schedule. Therefore, if a backup network is used, the backup might fail. This situation is temporary until all the VMs can be reached post migration to disable the in-guest backup client.

Bandwidth of a single network extension is theoretically 4 Gbps. However, this value can be the limit for all stretched networks within a single network extension pair and is not achievable by a single stretched network. A single stretched network can achieve ~1 Gbps if enough underlay bandwidth is allotted and the latency is low (<~10 ms).

### Proximity Routing option
{: #hcxclient-vcs-mesh-deployment-stretching-prox-routing}

Without any type of route optimization, extended networks route back to the client side for any L3 access. This trombone-ing introduces an inefficient traffic pattern as packets need to travel back and forth between client (source) and cloud. This situation exists even for cases where both the source and destination VMs are in the cloud. The Proximity Routing feature of HCX was designed to address this issue and local egress of traffic.

## Related links
{: #hcxclient-vcs-mesh-deployment-deployment-related}

* [Glossary of HCX components and terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-components)
* [Preparing the installation environment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-planning-prep-install)
* [HCX Client deployment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-client-deployment)
* [Monitoring parameters and components](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-monitoring)
* [HCX troubleshooting](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-troubleshooting)
