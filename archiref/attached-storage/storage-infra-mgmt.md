---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Attached storage infrastructure management
{: #storage-infra-mgmt}

Infrastructure management refers to the VMware® components that manage the VMware vSphere ESXi infrastructure.

For more information about the components, see [Virtual infrastructure design](/docs/vmwaresolutions?topic=vmwaresolutions-design_virtualinfrastructure).

## Virtual networking design
{: #storage-infra-mgmt-visual-net-design}

The network virtualization that is used in this design uses the existing vSphere Distributed Switch (vDS) associated with the private network and specified in [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview).

## vSphere Distributed Switch
{: #storage-infra-mgmt-vsphere-ds}

Another VLAN is created within the vCenter Server instance and used to attach the NFS mount point to the ESXi hosts in the existing cluster. The vCenter Server instance has a vSphere Distributed Switch that is associated with the private network. Therefore, another port group is created and tagged with the additional VLAN number since this additional VLAN isn't native.

The following table describes the default settings of the new port group.

Don't change these default settings.
{: important}

| Port Group Name | SDDC-DPG-NFS |
|:--------------- |:------------ |
| Port binding | Static |
| VLAN type | Private VLAN B |
| Load balancing | Route base on originating virtual port |
| Active Uplinks | `uplink1` `uplink2` |
{: caption="Table 1. NFS port group summary" caption-side="bottom"}

In addition to the vDS port group that is created for NFS storage traffic, a VMkernel port is created on each vSphere ESXi host during the deployment. The VMkernel port is assigned to the `SDDC-DPG-NFS` port group. The VMkernel port is also assigned to an IP address from the private portable subnet that is associated with the attached storage VLAN (private VLAN B). The port MTU is set to 9000 to support jumbo frames.

![Private vDS Port groups and uplinks](../../images/private_vds_portgroups_and_uplinks.svg "Private vDS Port groups and uplinks"){: caption="Figure 1. Private vDS Port groups and uplinks" caption-side="bottom"}

### vSphere host static routing
{: #storage-infra-mgmt-vsphere-routing}

Although the vDS is configured with a new port group and a VMkernel port is assigned to the port group, the solution creates a static route on each vSphere ESXi host in the deployment so that all NFS traffic traverses the VLAN and subnet for NFS. The static route is created in `/etc/rc.local.d/local.sh` so that it persists across host restarts.

## Related links
{: #storage-infra-mgmt-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
