---

copyright:

  years:  2016, 2024

lastupdated: "2024-10-09"

keywords: automated instances bom, bill materials vcf classic, vcf bom

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# BOM for {{site.data.keyword.vcf-auto-short}}
{: #vc_bom}

Review the Bill of Materials (BOM) information for {{site.data.keyword.vcf-auto}} instances.

## VLANs BOM for Automated instances
{: #vc_bom-vlans}

The following table details the BOM information for the {{site.data.keyword.vcf-auto-short}} VLANs.

| VLAN | Type | Details |
|:---- |:---- |:------- |
| VLAN1 | Public, Primary | Assigned to physical VMware ESXi™ servers for public network access. The servers are assigned a public IP address but this IP address is not configured on the servers, so they are not directly accessible on the public network. Instead, the public VLAN is intended to provide public internet access for other components, such as VMware NSX Edge™ Services Gateways (ESGs). |
| VLAN2 | Private A, Primary | Assigned by {{site.data.keyword.cloud}} to physical ESXi servers. Used by the management interface for VMware vSphere® management traffic. \n Assigned to VMs (virtual machines) that function as management components. \n For NSX-T™ instances with vSphere 6.7, used by some VMware NSX TEP (Geneve Tunnel Endpoint). |
| VLAN3 | Private B, Portable | Assigned to VMware vSAN™, if used. \n Assigned to VMware NFS, if used. \n Assigned to VMware vSphere® vMotion. \n For NSX-T™ instances with vSphere 6.7, used by VMware NSX TEP. For vSphere 7, all NSX VTEPs are put in VLAN2. |
{: caption="Table 1. BOM for the VLANs in Automated instances" caption-side="bottom"}

## Software BOM for Automated instances
{: #vc_bom-software}

The following table details the BOM information for {{site.data.keyword.vcf-auto-short}} software components.

| Manufacturer | Component | Version |
|:------------ |:--------- |:------- |
| VMware® by Broadcom | vSphere ESXi | ESXi 8.0 Update 2b (build 23305546)[^esxi80] or \n ESXi 7.0 Update 3q (build 23794027)[^esxi70] or \n ESXi 6.7 (202403001)[^esxi67] |
| VMware by Broadcom | Distributed vSwitch | 8.0.0[^vcs-vsphere800] or 7.0.0[^vcs-vsphere700] or 6.6.0[^vcs-vsphere660] |
| VMware by Broadcom | vCenter Server Appliance | 8.0 Update 3b (24262322) or \n 7.0 Update 3s (24201990) |
| VMware by Broadcom | vSAN[^vsan] | 7.0 Update 3l (21424296) |
| VMware by Broadcom | NSX for vSphere[^nsxt] | 4.1.2.4 (23786733) |
| VMware by Broadcom | NSX-V for vSphere[^nsxv] | 6.4.13 (19307994) |
| Microsoft® | Windows® Server Standard edition | 2019 |
| Microsoft | Active Directory™ domain functional level | 2016 (WinThreshold)[^domain] |
{: caption="Table 2. BOM for the software components in Automated instances" caption-side="bottom"}


[^esxi80]: Applicable to vSphere 8

[^esxi70]: Applicable to vSphere 7

[^esxi67]: Applicable to existing vSphere 6.7 hosts

[^vcs-vsphere800]: Applicable to vSphere 8

[^vcs-vsphere700]: Applicable to vSphere 7

[^vcs-vsphere660]: Applicable to existing vSphere 6.7 hosts

[^vsan]: VMware vSAN is an optional component

[^nsxt]: Applicable to NSX-T instances

[^nsxv]: Applicable to existing NSX-V instances

[^domain]: The domain functional level is set to 2016 for compatibility with an earlier version. For more information, see [Domain controllers](/docs/vmwaresolutions?topic=vmwaresolutions-adds-infra-domain#adds-infra-domain-controllers).

## Advanced configuration settings for ESXi servers
{: #vc_bom-esxi-server-advance-config}

Review the following table for an overview of the advanced configuration settings that are applied to ESXi servers.

| Configuration setting | Value |
|:--------------------- |:----- |
| Maximum of Volumes[^maxvol] | Both **/NFS/MaxVolumes** and **/NFS41/MaxVolumes** = 256 |
| Heartbeat Maximum Failures | **/NFS/HeartbeatMaxFailures** = 10 |
| Heartbeat Frequency | **/NFS/HeartbeatFrequency** = 12 |
| Heartbeat Timeout | **/NFS/HeartbeatTimeout** = 5 |
| Maximum Queue Depth | **/NFS/MaxQueueDepth** = 64 |
| Queue Full Sample Size | **/Disk/QFullSampleSize** = 32 |
| Queue Full Threshold | **/Disk/QFullThreshold** = 8 |
| TCP/IP Heap Size | **/Net/TcpipHeapSize** = 32 |
| TCP/IP Heap Maximum | **/Net/TcpipHeapMax** = 1536 |
{: caption="Table 3. ESXi servers advanced configuration settings for Automated instances and clusters" caption-side="bottom"}

[^maxvol]: This setting is required for IBM Spectrum® Protect Plus because this service might use more than the default number of NFS mounts on the ESXi server.

Review the following table for an overview of the advanced configuration settings that are applied to ESXi servers. ESXi servers join Active Directory domain for authentication. Also, the ESXi shell service is stopped.

| Configuration setting | Value |
|:--------------------- |:----- |
| Block guest sourced BPDU frames | **/Net/BlockGuestBPDU** = 1 |
| Duration, in seconds, to lock out a user's account after it exceeds the maximum allowed failed login attempts. | **Security.AccountUnlockTime** = 1800 |
| Maximum allowed failed login attempts before a user's account is locked out. Zero disables locking of account. | **Security.AccountLockFailures** = 6 |
{: caption="Table 4. ESXi servers advanced configuration settings for Automated instances and clusters" caption-side="bottom"}

## NSX and port group configuration settings
{: #vc_bom-nsx-port-group-config}

Review the following table for an overview of the VMware NSX and port group configuration settings for Automated instances.

| Configuration setting | Value |
|:--------------------- |:----- |
| NSX VXLAN cluster-teaming policy |Load Balance - SRCID |
| NSX VXLAN cluster VTEP | 2 |
| Segment ID pool for primary instance | 6000 - 7999 |
| Segment ID pool for subsequent secondary instance or instances | Previous end range in the multisite configuration + 1 to the previous end range in the multisite configuration + 2000 |
| Port group SDDC-DPortGroup-vSAN (if applicable) | **Active uplinks** set to **uplink2** and **Standby uplinks** set to **uplink1** |
| Port group SDDC-DPortGroup-Mgmt | **Port binding** set to **Static binding** and **Load balancing** set to **Route based on physical NIC load** |
| Port group SDDC-DPortGroup-External | **Port binding** set to **Static binding** |
{: caption="Table 5. NSX and port group configuration settings for Automated instances" caption-side="bottom"}

Security policies for promiscuous mode, MAC address changes, and forged transmits are accepted on distributed port groups.

## Network MTU configuration settings
{: #vc_bom-network-mtu-config}

The vSphere cluster uses two vSphere Distributed Switches (vDS), one for public network connectivity and the other one for private network connectivity.

The private network connections are configured to use Jumbo Frames MTU (Maximum Transmission Unit) with the size of 9000, which improves performance for large data transfers such as storage and VMware vMotion. This value is the maximum MTU allowed within VMware and by {{site.data.keyword.cloud_notm}}.

The public network connections use a standard Ethernet MTU of 1500, which must be maintained. Any changes might cause packet fragmentation over the internet.

Review the following table for an overview of the Network MTU configuration settings that are applied to the public and private Distributed Virtual Switch (DVS).

| Configuration setting | Value |
|:--------------------- |:----- |
| Public switch | 1500 (default) |
| Private switch | 9000 (Jumbo Frames) |
{: caption="Table 6. MTU configuration settings for Automated instances and clusters" caption-side="bottom"}

### Updating the public switch MTU setting
{: #vc_bom-procedure-update-public-switch-mtu-setting}

To update the MTU setting for the public switch, complete the following steps in the VMware vSphere Web Client:
1. Right-click the vDS and click **Edit Settings**.
2. On the **Properties** tab, select the **Advanced** option.
3. Ensure that the **Maximum MTU** value is set to 1500.

   When the MTU size in a vDS is changed, the attached uplinks (physical NICs) are brought down and up again. As a result, a brief outage occurs for the VMs that are using the uplink. Therefore, plan the MTU setting update during scheduled downtime.
   {: note}

## Distributed switch allocation
{: #vc_bom-network-dswitch-allocation}

The allocation of distributed switches varies if you have existing instances and clusters. Review the following considerations for switch creation when you create a cluster:

* If one or more existing clusters are in the same pod that uses distributed switches that are named `SDDC-DSwitch-Private` and `SDDC-DSwitch-Public`, your new cluster uses the same switches as the existing cluster.
* If one or more existing clusters are in the same pod, and the pod uses distributed switches that are named by using the same name as the pod (rather than named by using the same name as the cluster), your new cluster uses the same switches as the existing cluster.
* If no existing cluster is in the same pod, or all clusters in that pod distribute switches that are named by using the same name as the cluster rather than the pod, then your new cluster is configured with the new switch whose name is based only on the pod.
* For vSphere 7, each cluster has its own-distributed switch pair that is named `<instance_name>-<cluster_name>-public` and `<instance_name>-<cluster_name>-private`.

## EVC mode settings
{: #vc_bom-evc-mode-settings}

Review the following table for an overview of the EVC (Enhanced VMware vMotion Compatibility) mode settings for Automated instances and the differences between vSphere versions.

| Bare metal server CPU model | vSphere 6.7[^evc-vsphere67] | vSphere 7.0 |
|:--------------------------- |:--------------------------- |:----------- |
| Skylake | EVC is set to Intel® **Broadwell** Generation. | Skylake is not supported. |
| Cascade Lake | For the management cluster, EVC is not set. For all other clusters, EVC is set to Intel **Skylake** Generation. | EVC is set to Intel **Cascade Lake** Generation. |
{: caption="Table 7. EVC mode settings for Automated instances and clusters" caption-side="bottom"}

[^evc-vsphere67]: Existing vSphere 6.7 clusters only

## Active Directory Certificate Services
{: #vc_bom-ad-certificate-services}

* For instances deployed on or after 1 April 2024, Active Directory Certificate Services are installed and configured only on the first domain controller in a domain.
* For instances deployed before 1 April 2024, the Certificate Services are installed on every domain controller. However, you can simplify your topology to a single instance of Certificate Services without impacting the {{site.data.keyword.cloud_notm}} automation.

## Related links
{: #vc_bom-related}

* [Build numbers and versions of VMware ESXi and ESX (2143832)](https://knowledge.broadcom.com/external/article?legacyId=2143832){: external}
* [Build numbers and versions of VMware vCenter Server (2143838)](https://knowledge.broadcom.com/external/article?legacyId=2143838){: external}
* [Enabling Jumbo Frames on virtual switches](https://knowledge.broadcom.com/external/article?legacyId=1038827){: external}
* [{{site.data.keyword.vmwaresolutions_short}} Protection data sheet](https://www.ibm.com/software/reports/compatibility/clarity-reports/report/html/softwareReqsForProduct?deliverableId=236C87407E7411E6BA51E79BE9476040){: external}
* [{{site.data.keyword.vcf-auto-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [Planning for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_planning)
