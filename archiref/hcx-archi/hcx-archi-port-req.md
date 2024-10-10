---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Port access requirements for VMware HCX
{: #hcx-archi-port-req}

VMware® HCX™ must traverse the public internet and private lines, and connect to data center components, such as networks, switches, and port groups.

The following table lists ports that must be opened so that Hybrid Cloud Services virtual appliances can install successfully. Both the vSphere environment and the {{site.data.keyword.cloud}} environment must allow Network Time Protocol (NTP) clock synchronization among vSphere on-premises devices and the {{site.data.keyword.cloud_notm}} devices. UDP port 123 must be accessible to Hybrid Cloud Services virtual appliances and networks. Installed NTP Servers can be specified when the Hybrid Cloud Services Appliance is installed.

| Source | Target       | Port | Protocol | Purpose         | Services |
|--------|--------------|------|----------|-----------------|----------|
| HCX    | Customer DNS | 53   | TCP/UDP  | Name resolution | DNS      |
| HCX    | NSX LB in {{site.data.keyword.cloud_notm}} | 443 | TCP | Registration service | HTTPS |
| HCX    | vCenter in {{site.data.keyword.cloud_notm}} | 443 | TCP | HCX REST service | HTTPS |
| HCX    | PSC in {{site.data.keyword.cloud_notm}} | 443 | TCP | HCX REST service | HTTPS |
| HCX    | connect.hcx.vmware.com | 443 | TCP | Registration service | HTTPS |
| Web Browser | HCX | 9443 | TCP | HCX Virtual Appliance Management Interface for HCX system configuration | HTTPS |
| Admin network | HCX | 22 | SSH | Administrator SSH access to Hybrid Cloud Services | SSH |
| HCX | ESXi Hosts | 902 | TCP | Send management and provisioning instructions from HCX to ESXi Hosts in {{site.data.keyword.cloud_notm}}. | Internal |
| HCX | vCenter SSO Server | 7444 | TCP | vSphere Lookup Service |  |
| HCX | NTP Servers | 123 | UDP | Time synchronization | |
| HCX | Syslog |   | User-configured | Connection between HCX (the client) and the Syslog server. Values for the Syslog port and protocol are specified in the vSphere Web Client. For example, port 514 for UDP protocol. | |
| HCX | HCX-IX | 8123 | TCP | Send host-based replication service instructions to the HCX-IX. | HTTP |
| HCX | HCX-IX | 9443 | TCP | Send management instructions to the local HCX-IX by using the REST API. | HTTP</br>HTTPS |
| HCX-IX | HCX-NE | 443 | TCP | Send management instructions from HCX-IX to HCX-NE when HCX-NE uses the same path as the HCX-IX. | HTTP</br>HTTPS |
| HCX-IX | HCX-NE | 8443 | TCP | Bidirectional management instructions from HCX-IX to HCX-NE, when HCX-NE uses an alternative data path. | HTTP</br>HTTPS |
| HCX-NE | HCX-NE (remote) | 443 | TCP | Bidirectional management instructions from HCX-IX to HCX-NE, when HCX-NE uses an alternative data path. | HTTP</br>HTTPS |
| HCX-IX | ESXi hosts | 80, 902  | TCP | Management and OVF deployment | Internal |
| ESXi Hosts | HCX-IX | 31031, 44046 | TCP | Internal host-based replication traffic | Internal |
| HCX-IX | ESXi hosts | 8000  | TCP | vMotion (zero downtime migration) |  |
| HCX-IX (local) | HCX-IX</br>(remote) | 4500  | UDP | Internet Key Exchange (IKEv2) to encapsulate workloads for the bidirectional tunnel | IPsec |
| HCX-IX (local) | HCX-IX</br>(remote) | 500  | UDP | Internet Key Exchange (ISAKMP) for the bidirectional tunnel | IPsec |
{: caption="Port access requirements" caption-side="bottom"}

## Related links
{: #hcx-archi-port-req-related}

* [VMware HCX ports and protocols](https://ports.esp.vmware.com/home/VMware-HCX){: external}
