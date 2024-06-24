---

copyright:

  years:  2020, 2022

lastupdated: "2022-08-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware HCX component-level target architecture with NSX-T deployments
{: #hcx-archi-target-t}

Review the architecture of each VMware® HCX™ component that is deployed within the {{site.data.keyword.cloud}} environment with NSX-T™.

## NSX-T Services Edge Tier 0 Gateway
{: #hcx-archi-target-t-nsx-edge}

The components that are configured first within the {{site.data.keyword.cloud_notm}} are the existing NSX-T virtual machines (VMs). These VMs provide public connectivity for the HCX Cloud Virtual appliance.

The services edge is configure with Destination NAT (DNAT) rule and related firewall rules to allow connectivity to HCX Cloud through the Internet. Also, Source NAT (SNAT) is used for lisence registration and services update.


## HCX Manager
{: #hcx-archi-target-t-hcxm}

The HCX Manager component is the first appliance that is deployed after the NSX-T services T0 are configured on the target. This appliance is used as the main interface into the cloud environment for the source components.

HCX Manager provides an abstracted networking user interface that can be used to add, edit, and delete networks, and to design and configure routing without direct use of NSX. As a result of the vCenter and NSX integration, the HCX Manager appliance is assigned a private portable IP address on the management VLAN.

| Component | Configuration |
|-----------|---------------|
| CPU       | 4 vCPU        |
| RAM       | 12 GB         |
| Disk      | 60 GB VMDK resident on shared storage |
{: caption="Table 1. HCX Manager" caption-side="bottom"}

Additionally, it is configured to access vCenter and NSX with a specific user.

## HCX-IX Interconnect Appliance
{: #hcx-archi-target-t-hcx-ix}

A virtual appliance is deployed after a connection is established from the source to the target cloud. This appliance is the HCX-IX Interconnect Appliance (CGW) and is used to maintain a secure channel between vSphere environment that is designated as the source and the {{site.data.keyword.cloud_notm}}. The following table shows the sizing specification of the CGW appliance that is deployed within the {{site.data.keyword.cloud_notm}}.

| Component | Configuration |
|-----------|---------------|
| CPU       | 8 vCPU        |
| RAM       | 3 GB          |
| Disk      | 2 GB VMDK resident on shared storage |
{: caption="Table 2. HCX-IX Interconnect Appliance deployment" caption-side="bottom"}

This HCX-IX Interconnect Appliance is deployed and configured to be on the management VLAN (Private Portable Subnet) and the vMotion VLAN (Private Portable Subnet) of the {{site.data.keyword.vmwaresolutions_short}} deployment.

Additionally, another interface is configured on the Public VLAN (Public Portable) for connections that are made over the public internet. Public access is not required if a direct private connection is in place. The last connection that is associated with the HCX-IX Interconnect Appliance is a logical switch that is created and configured upon site pairing.

This logical switch is a private, non-routable network that is used as a communication channel between the HCX-IX Interconnect Appliance and HCX WAN Optimizer.

## WAN Optimizer
{: #hcx-archi-target-t-hcx-wo}

The second component that is deployed is the WAN Optimization appliance. While the WAN Optimization appliance is optional, it performs WAN conditioning to reduce effects of latency. It also incorporates Forward Error Correction to negate packet loss scenarios, and deduplication of redundant traffic patterns.

Altogether, these reduce bandwidth use and ensure the best use of available network capacity to expedite data transfer to and from the {{site.data.keyword.cloud_notm}}. The WAN Optimizer is disk intensive and requires sufficient amount of IOPS to function properly. As a result, the WAN optimizer is located on the vSAN storage, if present, or on the endurance storage with 2,000 IOPS.

The following table shows the sizing specification for the HCX WAN Optimization appliance.

| Component | Configuration |
|-----------|---------------|
| CPU       | 8 vCPU        |
| RAM       | 14 GB         |
| Disk      | 100 GB VMDK resident on shared storage / 5000 IOPS |
{: caption="Table 3. HCX WAN Optimizer appliance sizing" caption-side="bottom"}

Unlike the HCX-IX Interconnect Appliance, the WAN Optimization appliance is only attached to a logical switch to enable communication between itself and the HCX-IX Interconnect Appliance. This appliance is required if WAN optimization is in use within the source environment.

## HCX Network Extension Virtual Appliance
{: #hcx-archi-target-t-hcx-ne}

The third component is known as the HCX Network Extension Virtual Appliance and is part of the Network Extension Services. The HCX-NE is the VM that allows the extension of on-premises datacenter networks to the {{site.data.keyword.cloud_notm}}. The HCX-NE stretches on-premises VLANs or VXLANs. Each HCX-NE can stretch up to 4096 VLANs. Each HCX-NE, when paired with its on-premises partner can provide up to 1 Gbps per “flow” and up to an aggregate of 4 Gbps per VLAN (or VXLAN). Deployment of more HCX-NE appliances is supported if more network throughputs are required.

As part of this design, the HCX-NE appliance is deployed so that a customer can stretch multiple VLANs and VLXANs into the {{site.data.keyword.cloud_notm}} over the Internet or through the private network by using Direct-Link.

The sizing specification of the HCX-NE appliance on the {{site.data.keyword.cloud_notm}} is listed in the following table.

| Component | Configuration |
|-----------|---------------|
| CPU       | 8 vCPU        |
| RAM       | 3 GB          |
| Disk      | 2 GB VMDK on shared storage |
{: caption="Table 4. HCX-NE appliance sizing" caption-side="bottom"}

The HCX-NE appliance is deployed on the management VLAN and on the public VLAN. The public interface is used for application traffic that bound for the source of the extended network. More connections such as the extended networks, are created and attached to the HCX-NE appliance after the source administrator initiates the network extension into the {{site.data.keyword.cloud_notm}}.

## Related links
{: #hcx-archi-target-t-related}

* [Source architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-port-req)
