---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-13"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# vSRX example configuration
{: #vcsvsrx-default-config}

The following configuration is provided as a reference and is not intended for use in your vSRX cluster.

```JUNOS
set version 18.4R1.8;

system {

    login {

        user pokeyjo {
            uid 2000;
            class super-user;
            authentication {
                encrypted-password}
        }
    }

    root-authentication {
        encrypted-password}

    services {
        ssh;
        web-management {
            http {
                interface [ fxp0.0 ge-0/0/0.0 ];
            }
        }
    }

    syslog {
        user * {
            any emergency;
        }
        file messages {
            any any;
            authorization info;
        }
        file interactive-commands {
            interactive-commands any;
        }
    }
}

security {

    screen {
        ids-option untrust-screen {
            icmp {
                ping-death;
            }
            ip {
                source-route-option;
                tear-drop;
            }
            tcp {
                syn-flood {
                    alarm-threshold 1024;
                    attack-threshold 200;
                    source-threshold 1024;
                    destination-threshold 2048;
                    timeout 20;
                }
                land;
            }
        }
    }

    policies {
        from-zone trust to-zone trust {
            policy default-permit {
                match {
                    source-address any;
                    destination-address any;
                    application any;
                }
                then {
                    permit;
                }
            }
        }
        from-zone trust to-zone untrust {
            policy default-permit {
                match {
                    source-address any;
                    destination-address any;
                    application any;
                }
                then {
                    permit;
                }
            }
        }
    }

    zones {
        security-zone trust {
            tcp-rst;
            host-inbound-traffic {
                system-services {
                    all;
                }
            }
            interfaces {
                ge-0/0/0.0;
                ge-0/0/1.0;
            }
        }
        security-zone untrust {
            screen untrust-screen;
            interfaces {
                ge-0/0/2.0;
            }
        }
    }
}

interfaces {

    ge-0/0/0 {
        unit 0 {
            family inet {
                address 10.135.70.22/26;
            }
        }
    }

    ge-0/0/1 {
        unit 0 {
            family inet {
                address 10.134.217.140/26;
            }
        }
    }

    ge-0/0/2 {
        unit 0 {
            family inet {
                address 169.50.51.92/29;
            }
        }
    }

    ge-0/0/3 {
        unit 0;
    }

    fxp0 {
        unit 0;
    }

}

routing-options {

    static {
        route 10.0.0.0/8 next-hop 10.135.70.1;
        route 0.0.0.0/0 next-hop 169.50.51.89;
    }

}
```

## Set commands
{: #vcsvsrx-default-config-set-cmd}

```set version 18.4R1.8

set system login user pokeyjo uid 2000

set system login user pokeyjo class super-user

set system login user pokeyjo authentication encrypted-password
"removed for security"

set system root-authentication encrypted-password
"removed for security"

set system services ssh

set system services web-management http interface fxp0.0

set system services web-management http interface ge-0/0/0.0

set system syslog user * any emergency

set system syslog file messages any any

set system syslog file messages authorization info

set system syslog file interactive-commands interactive-commands any

set security screen ids-option untrust-screen icmp ping-death

set security screen ids-option untrust-screen ip source-route-option

set security screen ids-option untrust-screen ip tear-drop

set security screen ids-option untrust-screen tcp syn-flood
alarm-threshold 1024

set security screen ids-option untrust-screen tcp syn-flood
attack-threshold 200

set security screen ids-option untrust-screen tcp syn-flood
source-threshold 1024

set security screen ids-option untrust-screen tcp syn-flood
destination-threshold 2048

set security screen ids-option untrust-screen tcp syn-flood queue-size
2000

set security screen ids-option untrust-screen tcp syn-flood timeout 20

set security screen ids-option untrust-screen tcp land

set security policies from-zone trust to-zone trust policy
default-permit match source-address any

set security policies from-zone trust to-zone trust policy
default-permit match destination-address any

set security policies from-zone trust to-zone trust policy
default-permit match application any

set security policies from-zone trust to-zone trust policy
default-permit then permit

set security policies from-zone trust to-zone untrust policy
default-permit match source-address any

set security policies from-zone trust to-zone untrust policy
default-permit match destination-address any

set security policies from-zone trust to-zone untrust policy
default-permit match application any

set security policies from-zone trust to-zone untrust policy
default-permit then permit

set security zones security-zone trust tcp-rst

set security zones security-zone trust host-inbound-traffic
system-services all

set security zones security-zone trust interfaces ge-0/0/0.0

set security zones security-zone trust interfaces ge-0/0/1.0

set security zones security-zone untrust screen untrust-screen

set security zones security-zone untrust interfaces ge-0/0/2.0

set interfaces ge-0/0/0 unit 0 family inet address 10.135.70.22/26

set interfaces ge-0/0/1 unit 0 family inet address 10.134.217.140/26

set interfaces ge-0/0/2 unit 0 family inet address 169.50.51.92/29

set interfaces ge-0/0/3 unit 0

set interfaces fxp0 unit 0

set routing-options static route 10.0.0.0/8 next-hop 10.135.70.1

set routing-options static route 0.0.0.0/0 next-hop 169.50.51.89
```

## Related links
{: #vcsvsrx-default-config-related}

* [Getting started with {{site.data.keyword.cloud_notm}} Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started)
* [Understand vSRX Virtual Firewall with VMware](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/concept/security-vsrx-vmware-overview.html){: external}
* [Requirements for vSRX Virtual Firewall on VMware](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/concept/security-vsrx-vmware-system-requirement.html){: external}
* [Install vSRX Virtual Firewall with VMware vSphere Web Client](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/task/security-vsrx-vsphere-client-installing.html){: external}
* [Configure a vSRX Virtual Firewall Chassis Cluster in Junos OS](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-hyper-v/topics/task/security-vsrx-chassis-cluster-configuring.html){: external}
* [Configure ECMP on VMware NSX](https://letsv4real.com/2016/09/23/configure-ecmp-on-vmware-nsx/){: external}
