---

copyright:

  years:  2019, 2023

lastupdated: "2023-09-25"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Glossary of vSRX terminology
{: #vcsvsrx-components}

## Interface names
{: #vcsvsrx-components-interface}

Review the following interface names.

`ae` - Aggregated Ethernet interface. This interface is a virtual aggregated link and has a different naming format from most PICs. For more information, see [Aggregated Ethernet interfaces overview](https://www.juniper.net/documentation/en_US/junos/topics/topic-map/aggregated-ethernet-interfaces-lacp-configuring.html#id-aggregated-ethernet-interfaces-overview){: external}.

`fxp` - Management and internal Ethernet interfaces. You can use the `show chassis hardware` command to display hardware information about the router, including its Routing Engine model. To determine which management interface is supported on your router and Routing Engine combination, see [Understanding management Ethernet interfaces](https://www.juniper.net/documentation/en_US/junos/topics/concept/interfaces-understanding-management-ethernet-interfaces.html){: external}.

`ge` - Gigabit Ethernet interface.

      `user@host> show configuration interfaces`

      or

      `user@host> show configuration interfaces ge-4/0/0`

`gr` - Generic routing encapsulation (GRE) tunnel interface.

`gre` - Internally generated interface that is configurable only as the control channel for Generalized MPLS (GMPLS). For more information, see the [MPLS applications user guide](https://www.juniper.net/documentation/us/en/software/junos/mpls/index.html){: external}.

You can configure `gre` interfaces (gre-x/y/z) only for GMPLS control channels. `gre` interfaces are not supported or configurable for other applications.
{: note}

`lo` - Loopback interface. The Junos OS automatically configures one loopback interface (lo0). The logical interface lo0.16383 is a non-configurable interface for router control traffic.

`reth` - redundant Ethernet interface is a pseudo-interface that includes a physical interface from each node of a cluster. A `reth` interface of the active node is responsible for passing the traffic in a chassis cluster setup.  

A redundant Ethernet interface inherits its failover properties from the redundancy group x that it belongs to. A redundant Ethernet interface remains active if its primary child interface is available or active. For example, if `reth0` is associated with redundancy group 1 and redundancy group 1 is active on node 0, then `reth0` is up if the node 0 child of `reth0` is up.

`st0` - Secure Tunnel interface, which is used for routing traffic in VPNs. For every new VPN destination, use a different `st0`. Don't use `st1`, `st2`, and so on.

For more information, see [Interface naming overview](https://www.juniper.net/documentation/en_US/junos/topics/concept/interfaces-interface-naming-overview.html){: external}.

## Related links
{: #vcsvsrx-components-related}

* [Getting Started with Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started)
* [Juniper Networks vSRX deployment guide for VMware](https://www.juniper.net/documentation/en_US/vsrx/information-products/pathway-pages/security-vsrx-vmware-guide-pwp.html){: external}
* [Juniper Networks requirements for vSRX on VMware](https://www.juniper.net/documentation/en_US/vsrx/topics/reference/general/security-vsrx-vmware-system-requirement.html){: external}
* [Juniper Networks vSRX installation with vSphere Web Client](https://www.juniper.net/documentation/en_US/vsrx/topics/task/installation/security-vsrx-vsphere-client-installing.html){: external}
* [Juniper Networks configuring a vSRX Chassis Cluster in Junos OS](https://www.juniper.net/documentation/en_US/vsrx/topics/task/multi-task/security-vsrx-chassis-cluster-configuring.html){: external}
* [Configure ECMP on VMware NSX](https://letsv4real.com/2016/09/23/configure-ecmp-on-vmware-nsx/){: external}
