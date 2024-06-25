---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-12"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.redhat_openshift_notm}} NSX DLR configuration
{: #openshift-runbook-runbook-nsxdlr-intro}

The NSX distributed logical router is used to support the {{site.data.keyword.redhat_openshift_full}} 4.7 environment. To use this information, you must understand how to create these components and add the configuration.

Review [Add a Distributed Logical Router](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.4/com.vmware.nsx.admin.doc/GUID-A20103B0-ABA1-4884-8EC3-287874E23181.html){: external}. PowerNSX commands are provided if you would want to use this method.

## NSX DLR
{: #openshift-runbook-runbook-nsxdlr-config}

The NSX distributed logical router runs as a kernel module in the hypervisor of each host and is optimized for East-West routing. Optionally, a DLR Control VM can be installed. The DLR Control VM is needed to peer with NSX Edges and NSX controllers for dynamic routing (OSPF or BGP) updates. In this deployment, static routing is used. However, DLR Control VMs are deployed, in case you require to use a routing protocol.

The NSX DLR Control VMs are configured as an active and passive pair of appliances. During the configuration process, the DLR control VM is deployed in the compact size and the NSX DLR is connected to the {{site.data.keyword.redhat_openshift_notm}} Edge.

| Component | Configuration |
|-----------|---------------|
| CPU       | 1 vCPU        |
| RAM       | 1 GB          |
| Disk      | 4.5 GB VMDK resident on shared storage with 4 GB swap |
{: caption="Table 1. NSX DLR deployment" caption-side="bottom"}

Since the NSX DLR Control VMs are configured as active-passive, you must create vSphere Distributed Resource Scheduler (DRS) anti-affinity rules. The rules ensure that NSX Edges do not run on the same host as their respective peer appliance.

| Field     | Value         |
|-----------|---------------|
| Name      | `OpenShift-DLR` |
| Type      | Separate virtual machines |
| Members   | `OpenShift-DLR-0` \n `OpenShift-DLR-1` |
{: caption="Table 2. NSX DLR anti-affinity rules" caption-side="bottom"}

## NSX DLR interfaces
{: #openshift-runbook-runbook-nsxdlr-interfaces}

The NSX DLR is deployed with a transit network between the {{site.data.keyword.redhat_openshift_notm}} NSX Edge and the {{site.data.keyword.redhat_openshift_notm}} Logical switch. The Edge is defined as an uplink interface and the Logical switch is defined as an internal interface.

| Interface name| Interface type | IP addresses | Port group or logical switch |
| --- | ---| --- | --- |
| OpenShift-LS | Internal | `192.168.133.1` | OpenShift-LS |
| OpenShift-Transit | Uplink | `192.168.100.2/24` | OpenShift-Transit  |
{: caption="Table 3. Configuration for NSX DLR - interfaces" caption-side="bottom"}

## NSX DLR firewall
{: #openshift-runbook-runbook-nsxdlr-firewall}

The DLR firewall is configured open.

| Firewall rule | Source | Destination | Service | Action |
| --- | --- | --- | --- | --- |
| Default | Any | Any | Any | Accept |
{: caption="Table 4. Configuration for NSX DLR - NSX firewalls" caption-side="bottom"}

## NSX DLR routes
{: #openshift-runbook-runbook-nsxdlr-routes}

On the Edge, the default route is configured to be to the transit network connection to the {{site.data.keyword.redhat_openshift_notm}} Edge.

### Global configuration
{: #openshift-runbook-runbook-nsxdlr-global-config}

| Global configuration | vNIC | Gateway IP address |
| --- | --- | --- |
| Default Gateway | Transit-Uplink | 192.168.100.1 |
{: caption="Table 5. Configuration for NSX Edge - global configuration" caption-side="bottom"}

## NSX DHCP relay
{: #openshift-runbook-runbook-nsxdlr-dhcprelay}

For the {{site.data.keyword.redhat_openshift_notm}} 4.7 environment, the connection to the DHCP Service runs on the {{site.data.keyword.redhat_openshift_notm}} Edge.

| DCHP relay | Value |
| :--- | --- |
| IP address  | 192.168.101.1 |
{: caption="Table 6. Configuration for NSX Edge - DHCP relay" caption-side="bottom"}

| DCHP relay | Value |
| :--- | --- |
| Name  | OpenShift-LS |
| Gateway IP | 192.168.133.1 |
{: caption="Table 7. Configuration for NSX Edge - DHCP relay agent" caption-side="bottom"}

## PowerNSX commands
{: #openshift-runbook-runbook-nsxdlr-powernsx}

Review the following example PowerNSX commands that you can use to automate the provisioning and configuration of the NSX DLR.

Use the following table to document the parameters that you need for your deployment. Examples are shown that match the deployment described previously.

| Parameters | Example | Your deployment |
| --- | --- | --- |
| vCenter Server IP address | | |
| vCenter Server user | | |
| vCenter Server password | | |
| Transit Logical Switch | `OpenShift-Transit` | |
| OpenShift Logical Switch | `OpenShift-LS` | |
| Uplink IP address | `192.168.100.2` | |
| Internal IP address | `192.168.133.1` | |
| DLR name | OpenShift-DLR | |
| vCenter Server instance cluster | `cluster1` | |
| vCenter Server instance datastore | `vsanDatastore` | |
{: caption="Table 8. PowerNSX DLR parameters" caption-side="bottom"}

```text
# Connect to NSX Manager
Connect-NsxServer -vCenterServer <IP_Address> -User <UserName> -Password '<Password>'

# Create DLR interface specifications and then create DLR
$uplinkLif = New-NsxLogicalRouterInterfaceSpec -Name ToESG -Type uplink -ConnectedTo (Get-NsxLogicalSwitch OpenShift-Transit) -PrimaryAddress 192.168.100.2 -SubnetPrefixLength 24
$internalLif = New-NsxLogicalRouterInterfaceSpec -Name ToLS -Type internal -ConnectedTo (Get-NsxLogicalSwitch OpenShift-LS) -PrimaryAddress 192.168.133.1 -SubnetPrefixLength 24
$haLif = New-NsxLogicalRouterInterfaceSpec -Name ToHA -Type internal -ConnectedTo (Get-NsxLogicalSwitch OpenShift-HA)
New-NsxLogicalRouter -Name OpenShift-DLR -ManagementPortGroup (Get-NsxLogicalSwitch OpenShift-HA) -Interface $uplinkLif,$internalLif,$haLif -Cluster (Get-Cluster cluster1) -EnableHA -Datastore (Get-Datastore vsanDatastore)

# Configure the default gateway on the DLR to be the ESG
$uplinkVnic = Get-NsxLogicalRouter OpenShift-DLR | Get-NsxLogicalRouterInterface "ToESG"
$uplinkVnicId = $uplinkVnic.index
Get-NsxLogicalRouter OpenShift-DLR | Get-NsxLogicalRouterRouting | Set-NsxLogicalRouterRouting -DefaultGatewayVnic $uplinkVnicId -DefaultGatewayAddress 192.168.100.1 -Confirm:$false

# Configure the default firewall rule on the DLR to "allow"
$dlr = Get-NsxLogicalRouter OpenShift-DLR
$dlr.features.firewall.defaultpolicy.action = "Accept"
$dlr | Set-NsxLogicalRouter -Confirm:$false

# Configure DHCP relay on DLR
$dlrID = (Get-NsxLogicalRouter -Name "OpenShift-DLR").Id
$internalLifVnicId = (Get-NsxLogicalRouter OpenShift-DLR | Get-NsxLogicalRouterInterface "ToLS").index
$uri = "/api/4.0/edges/$($dlrID)/dhcp/config/relay"
$xmlPayload = "
  <relay>
  <relayServer>
    <ipAddress>192.168.100.1</ipAddress>
  </relayServer>
  <relayAgents>
    <relayAgent>
      <vnicIndex>$($internalLifVnicId)</vnicIndex>
      <giAddress>192.168.133.1</giAddress>
    </relayAgent>
  </relayAgents>
 </relay>"

$null = invoke-nsxwebrequest -method "put" -uri $uri -body $xmlPayload -connection $nsxConnection

# Disconnect
Disconnect-NsxServer
```
{: pre}

## Related links
{: #vcs-openshift-runbook-nsxdlr-related}

* [{{site.data.keyword.redhat_openshift_notm}} Bastion node setup](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-bastion-intro)
* [{{site.data.keyword.redhat_openshift_notm}} 4.14 user provider infrastructure installation](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-install-intro)
