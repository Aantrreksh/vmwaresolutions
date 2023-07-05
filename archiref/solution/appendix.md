---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-12"

keywords: nsx editions, vsan editions, nsx edition comparison, vsan edition comparison

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Comparison chart for VMware NSX-T, NSX-V, and vSAN
{: #solution-appendix}

## NSX-T edition comparison
{: #solution-appendix-nsx-editions}

The design has multiple components that require licenses. This information captures the minimum licenses that are required for the environment to operate correctly.

| Component | Purpose | License |
|:--------- |:------- |:------- |
| VMware vSphere® | Compute virtualization | vSphere 7.0 Enterprise Plus |
| VMware vCenter Server® | Infrastructure management | vCenter Server 7.0 Standard |
| VMware NSX® | Network virtualization | NSX DC Standard Edition |
| VMware vSAN™ | Storage virtualization | vSAN 7.0 Advanced |
{: caption="Table 1. NSX-T license requirements" caption-side="bottom"}

NSX-T Data Center (DC) SP license editions provide the following features.

| NSX-T feature | NSX DC SP Base | NSX DC SP Professional | NSX DC SP Advanced | NSX DC SP Enterprise Plus |
|:--------------|:---------------|:------------------------|:------------------|:-----------------------------------|
| Distributed switching and routing | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| NSX gateway firewall (stateful) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| NSX gateway NAT | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Software L2 bridging to physical environment | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Dynamic routing with ECMP (Active-Active) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Integration with Cloud Management platforms | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| IPv6 with static routing and static IPv6 allocation | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| VPN - L3 (IPsec) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| VPN - L3 (SSL) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Load balancing (NSX Advanced LB for NSX-T) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| VPN - L2 (L2VPN) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Distributed firewalling for VMs and workloads running on bare metal | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Integration with Distributed Firewall (Active Directory, VMware AirWatch, Endpoint Protection and Third-Party Service Insertion) | | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Container networking and security | | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Multi-vCenter networking and security | | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| IPv6 with Dynamic Routing, Dynamic IPv6 Allocation and Services | | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Context-aware Micro-Segmentation (L7 Application Identification, RDSH, Protocol Analyzer) | | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Distributed FQDN allowlisting | | | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| VRF |  | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Federation | | | | ![Available](../../../icons/checkmark-icon.svg) |
| VM-to-VM traffic flow analysis | | | | ![Available](../../../icons/checkmark-icon.svg) |
| Firewall visibility | | | | ![Available](../../../icons/checkmark-icon.svg) |
| Automated security policy | | | | ![Available](../../../icons/checkmark-icon.svg) |
| Rule and group recommendation analytics | | | | ![Available](../../../icons/checkmark-icon.svg) |
| VMware Aria Operations™ for Networks Advanced | | | | ![Available](../../../icons/checkmark-icon.svg) |
| VMware HCX Advanced | | | | ![Available](../../../icons/checkmark-icon.svg) |
| VMware Aria Operations™ for Logs for NSX | | | | |
{: caption="Table 2. NSX-T edition comparison chart" caption-side="bottom"}

## NSX-V edition comparison
{: #solution-appendix-nsxv-editions}

The design has multiple components that require licenses. This information captures the minimum licenses that are required for the environment to operate correctly.

| Component | Purpose | License |
|:--------- |:------- |:------- |
| VMware vSphere | Compute virtualization | vSphere 6.7 Enterprise Plus |
| VMware vCenter Server | Infrastructure management | vCenter Server 6.7 Standard |
| VMware NSX | Network virtualization | NSX Base for Service Providers 6.4 |
| VMware vSAN | Storage virtualization | vSAN 6.6 Advanced |
{: caption="Table 3. NSX-V license requirements" caption-side="bottom"}

NSX Base for Service Providers edition is only available for service providers through the VMware vCloud Air Network (vCAN). The features in this edition can be found in the following table.
{: note}

| NSX-V feature | Base | Advanced | Enterprise |
|:------------- |:---- |:-------- |:---------- |
| Distributed switching and routing             | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| NSX Edge firewall                             | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| NAT                                           | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| NSX Edge load balancing                       | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| VPN (IPsec)                                   | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| VPN (SSL)                                     | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| API-driven automation                         | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Integration with VMware Aria and OpenStack[^OpenStack]  | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Automation of security policies with VMware Aria |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| SW L2 bridging to physical environment        |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Dynamic routing with ECMP (active-active)     |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Distributed firewalling                       |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Integration with Active Directory             |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Server activity monitoring                    |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Service insertion (third-party integration)     |      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Distributed load balancing                    |      |          | ![Available](../../../icons/checkmark-icon.svg) |
| Cross vCenter NSX                             |      |          | ![Available](../../../icons/checkmark-icon.svg) |
| Multisite NSX optimizations                  |      |          | ![Available](../../../icons/checkmark-icon.svg) |
| Remote Gateway                                |      |          | ![Available](../../../icons/checkmark-icon.svg) |
| Integration with HW VTEPs                     |      |          | ![Available](../../../icons/checkmark-icon.svg) |
| VMware Aria Operations for Logs for NSX | | | | |
{: caption="Table 4. NSX-V edition comparison chart" caption-side="bottom"}

[^OpenStack]: L2, L3 & NSX Edge integration only. No consumption of security groups.

## vSAN edition comparison
{: #solution-appendix-vsan-editions}

The following table lists the available features for the vSAN Advanced and Enterprise editions that the solution supports.

| vSAN feature | Advanced | Enterprise |
|:------------ |:-------- |:---------- |
| Storage policy-based management                 | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Flash read/write caching                        | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Distributed RAID                                | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Virtual Distributed Switch                      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Rack awareness                                  | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| vSphere replication                             | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Software checksum                               | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| All-Flash hardware                              | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| iSCSI target service                            | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| IOPS limit                                      | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Deduplication and compression                   | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| RAID-5/6 erasure coding                         | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Data at rest encryption                         |          | ![Available](../../../icons/checkmark-icon.svg) |
| Stretched cluster with local failure protection |          | ![Available](../../../icons/checkmark-icon.svg) |
{: caption="Table 5. vSAN edition comparison chart" caption-side="bottom"}

## Related links
{: #solution-appendix-related}

* [Overview of VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-solution_overview)
* [Design overview](/docs/vmwaresolutions?topic=vmwaresolutions-design_overview)
* [Backing up components](/docs/vmwaresolutions?topic=vmwaresolutions-solution_backingup)
