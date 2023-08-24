---

copyright:

  years:  2020, 2023

lastupdated: "2023-07-17"

keywords: VLAN ports, vmware solutions ports, ports usage vmware solutions

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VLANs and subnets in VMware Solutions
{: #vmwaresol_ports-vlans-subnets}

The following table provides information about the subnets that are used in each VLAN. You can either order new VLANs or subnets for VMware vCenter Server® or you can select existing VLANs. You can define your firewall rules based on the subnets and ports that the network traffic goes through.

It is not recommended to put a firewall on a secondary private VLAN that has storage and vSphere® vMotion® traffic.
{: note}

| Public VLAN | Private VLAN | Secondary private VLAN |
|:------------|:-------------|:-----------------------|
| Primary subnet \n \n Portable subnets \n - Management edge gateway public \n - Customer edge gateway public | Primary subnet \n \n Portable subnets \n - Infrastructure VMs (vCenter, NSX managers, NSX edges, \n Active Directory VMs, IBM CloudDriver automation VSI) \n - NSX host tunnel endpoint (TEP) traffic (NSX-T™)[^hosttep-v7] \n - VMware NSX® Host TEP (NSX-V) \n - Customer edge gateway private | Portable subnets \n - vSAN™ traffic \n - Shared storage traffic \n - vMotion traffic  \n - NSX host TEP traffic (NSX-T)[^hosttep-v67] \n - NSX edge TEP traffic (NSX-T) \n - Customer edge TEP traffic (NSX-T) |
{: caption="Table 1. Subnets for public, private, and secondary private VLANs" caption-side="bottom"}

[^hosttep-v7]: For NSX-T instances with vSphere 7

[^hosttep-v67]: For existing instances with vSphere 6.7

## Related links
{: #vmwaresol_ports--vlans-subnets-related}

* [Ports that are used for deployment and Day 2 operations](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-deploy-day2ops)

