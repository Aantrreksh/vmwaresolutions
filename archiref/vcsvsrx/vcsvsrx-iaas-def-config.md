---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-13"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

#  The {{site.data.keyword.cloud_notm}} IaaS vSRX default configuration
{: #vcsvsrx-iaas-def-config}

The following configuration is provided as a reference and is not intended for use in your vSRX cluster.

```JUNOS
set version 18.4R1.8
set groups node0 system host-name edge01-vSRX-Node0
set groups node1 system host-name edge01-vSRX-Node1
set apply-groups "${node}"
set system login class security permissions security-control
set system login class security permissions view-configuration
set system login user vSRX_USER uid 2000
set system login user vSRX_USER class super-user
set system login user vSRX_USER authentication encrypted-password "Secret"
set system root-authentication encrypted-password "Secret"
set system services ssh
set system services netconf ssh port 830
set system services web-management http interface fxp0.0
set system services web-management https port 8443
set system services web-management https system-generated-certificate
set system services web-management https interface fxp0.0
set system services web-management https interface reth0.0
set system services web-management https interface reth1.0
set system services web-management session session-limit 100
set system name-server 10.134.217.115
set system syslog user * any emergency
set system syslog file messages any any
set system syslog file messages authorization info
set system syslog file interactive-commands interactive-commands any
set system ntp server 10.134.217.115
set chassis cluster reth-count 4
set chassis cluster redundancy-group 0 node 0 priority 100
set chassis cluster redundancy-group 0 node 1 priority 1
set chassis cluster redundancy-group 1 node 1 priority 1
set chassis cluster redundancy-group 1 node 0 priority 100
set chassis cluster redundancy-group 1 preempt
set security log mode stream
set security log report
set security address-book global address SL1 10.0.64.0/19
set security address-book global address SL2 10.1.128.0/19
set security address-book global address SL3 10.0.86.0/24
set security address-book global address SL4 10.2.128.0/20
set security address-book global address SL5 10.1.176.0/20
set security address-book global address SL6 10.1.64.0/19
set security address-book global address SL7 10.1.96.0/19
set security address-book global address SL8 10.1.192.0/20
set security address-book global address SL9 10.1.160.0/20
set security address-book global address SL10 10.2.32.0/20
set security address-book global address SL11 10.2.64.0/20
set security address-book global address SL12 10.2.112.0/20
set security address-book global address SL13 10.2.160.0/20
set security address-book global address SL14 10.1.208.0/20
set security address-book global address SL15 10.2.80.0/20
set security address-book global address SL16 10.2.144.0/20
set security address-book global address SL17 10.2.48.0/20
set security address-book global address SL18 10.2.176.0/20
set security address-book global address SL19 10.3.64.0/20
set security address-book global address SL20 10.3.80.0/20
set security address-book global address SL_PRIV_MGMT 10.135.70.22/32
set security address-book global address SL_PUB_MGMT 169.50.51.92/32
set security address-book global address-set SERVICE address SL1
set security address-book global address-set SERVICE address SL2
set security address-book global address-set SERVICE address SL3
set security address-book global address-set SERVICE address SL4
set security address-book global address-set SERVICE address SL5
set security address-book global address-set SERVICE address SL6
set security address-book global address-set SERVICE address SL7
set security address-book global address-set SERVICE address SL8
set security address-book global address-set SERVICE address SL9
set security address-book global address-set SERVICE address SL10
set security address-book global address-set SERVICE address SL11
set security address-book global address-set SERVICE address SL12
set security address-book global address-set SERVICE address SL13
set security address-book global address-set SERVICE address SL14
set security address-book global address-set SERVICE address SL15
set security address-book global address-set SERVICE address SL16
set security address-book global address-set SERVICE address SL17
set security address-book global address-set SERVICE address SL18
set security address-book global address-set SERVICE address SL19
set security address-book global address-set SERVICE address SL20
set security screen ids-option untrust-screen icmp ping-death
set security screen ids-option untrust-screen ip source-route-option
set security screen ids-option untrust-screen ip tear-drop
set security screen ids-option untrust-screen tcp syn-flood alarm-threshold 1024
set security screen ids-option untrust-screen tcp syn-flood attack-threshold 200
set security screen ids-option untrust-screen tcp syn-flood source-threshold 1024
set security screen ids-option untrust-screen tcp syn-flood destination-threshold 2048
set security screen ids-option untrust-screen tcp syn-flood queue-size 2000
set security screen ids-option untrust-screen tcp syn-flood timeout 20
set security screen ids-option untrust-screen tcp land
set security policies from-zone trust to-zone trust policy default-permit match source-address any
set security policies from-zone trust to-zone trust policy default-permit match destination-address any
set security policies from-zone trust to-zone trust policy default-permit match application any
set security policies from-zone trust to-zone trust policy default-permit then permit
set security policies from-zone trust to-zone untrust policy default-permit match source-address any
set security policies from-zone trust to-zone untrust policy default-permit match destination-address any
set security policies from-zone trust to-zone untrust policy default-permit match application any
set security policies from-zone trust to-zone untrust policy default-permit then permit
set security zones security-zone trust tcp-rst
set security zones security-zone trust interfaces reth0.0 host-inbound-traffic system-services all
set security zones security-zone untrust screen untrust-screen
set security zones security-zone untrust interfaces reth1.0 host-inbound-traffic system-services all
set interfaces ge-0/0/1 gigether-options redundant-parent reth0
set interfaces ge-0/0/2 gigether-options redundant-parent reth2
set interfaces ge-0/0/3 gigether-options redundant-parent reth1
set interfaces ge-0/0/4 gigether-options redundant-parent reth3
set interfaces ge-7/0/1 gigether-options redundant-parent reth0
set interfaces ge-7/0/2 gigether-options redundant-parent reth2
set interfaces ge-7/0/3 gigether-options redundant-parent reth1
set interfaces ge-7/0/4 gigether-options redundant-parent reth3
set interfaces fab0 fabric-options member-interfaces ge-0/0/0
set interfaces fab1 fabric-options member-interfaces ge-7/0/0
set interfaces fxp0 unit 0 family inet address 10.135.70.20/26
set interfaces lo0 unit 0 family inet address 127.0.0.1/32
set interfaces reth0 mtu 9000
set interfaces reth0 redundant-ether-options redundancy-group 1
set interfaces reth0 unit 0 description "SL Private VLAN interface"
set interfaces reth0 unit 0 family inet address 10.135.70.22/26
set interfaces reth1 redundant-ether-options redundancy-group 1
set interfaces reth1 unit 0 description "SL Public VLAN interface"
set interfaces reth1 unit 0 family inet address 169.50.51.92/29
set interfaces reth1 unit 0 family inet6 address 2a03:8180:1201:0129:0000:0000:0000:0005/64
set routing-options static route 0.0.0.0/0 next-hop 10.135.70.1
```
