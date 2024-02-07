---

copyright:

  years:  2019, 2024

lastupdated: "2024-01-12"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware Solutions DNS configuration
{: #openshift-runbook-runbook-dns-intro}

## Collecting Active Directory credentials
{: #openshift-runbook-runbook-dns-creds}

1. Log in to [{{site.data.keyword.cloud}}](https://cloud.ibm.com/login){: external}.
2. From left menu, select **VMware**.
3. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources** > **vCenter Server** from the left navigation pane.
4. Select your deployed instance.
5. Click the **Access information** tab and collect the AD/DNS IP and remote desktop credentials.
6. From a jump server or by using SSL VPN, remote desktop to the AD/DNS server.

## Creating DNS records
{: #openshift-runbook-runbook-dns-records}

1. Based on the following example, create a table to record your values.
2. Update the following PowerShell commands with your values.
3. From the Windows® RDP Session, open a PowerShell command window.
4. Run commands to create the DNS artifacts.
   - Reverse Lookup Zones
   - Create DNS A Records, with PTR
   - Create DNS Service record for `etcd`
   - Create DNS SRV record for `etcd`

### Notes about DNS records
{: #openshift-runbook-runbook-dns-records-notes}

* The `Add-DnsServerPrimaryZone-networkid` cmdlet creates only classful reverse lookup zones. Therefore, if you specify a prefix longer than `/24`, then the cmdlet creates a `/32` reverse lookup zone. Therefore, as a workaround in the script use `/24` instead of a `/26`. You also need to modify the private portable subnet to match classful `/24` network in the commands.
* Do not create CNAME entries because the {{site.data.keyword.redhat_openshift_full}} certificates are keyed to the DNS returning the IP address only and not a referral to the base hostname.
   Use the following format for DNS naming standards:
   `HostName.ClusterName.SubDomain.DomainName`
   - **HostName** - Name of the virtual machine or host, for example, `control-plane-0`
   - **ClusterName** - {{site.data.keyword.redhat_openshift_notm}} cluster name, for example, `ocp`
   - **SubDomain** - Subdomain of the {{site.data.keyword.vmwaresolutions_short}} deployment, for example, `dallas`
   - **DomainName** - Domain name of the {{site.data.keyword.vmwaresolutions_short}} Deployment, for example, `ibm.local`

For example, the FQDN would be, *control-plane-0.ocp.dallas.ibm.local*.

The following table is for an example deployment. Use your own values.

| DNS Description | DNS Example Name | DNS Example IP address |
| --- | --- | --- |
| DNS Reverse Lookup for {{site.data.keyword.redhat_openshift_notm}} VXLAN  | `192.168.133.0/24` | |
| DNS Reverse Lookup for {{site.data.keyword.redhat_openshift_notm}} {{site.data.keyword.cloud_notm}} Subnet  | `10.208.242.128/26` | |
| Bastion Host | bastion.ocp.dallas.ibm.local | 192.168.133.8 |
| bootstrap-0 Host | bootstrap-0.ocp.dallas.ibm.local | 192.168.133.9 |
| control-plane-0 Host | control-plane-0.ocp.dallas.ibm.local | 192.168.133.10 |
| control-plane-1 Host | control-plane-1.ocp.dallas.ibm.local | 192.168.133.11 |
| control-plane-2 Host | control-plane-2.ocp.dallas.ibm.local | 192.168.133.12 |
| compute-0 Host | compute-0.ocp.dallas.ibm.local | 192.168.133.13 |
| compute-1 Host | compute-1.ocp.dallas.ibm.local | 192.168.133.14 |
| compute-2 Host | compute-2.ocp.dallas.ibm.local | 192.168.133.15 |
| Application wildcard DNS (Load Balancer) | *.apps.ocp.dallas.ibm.local | 10.208.242.131 |
| Kubernetes API URL (Load Balancer) | api.ocp.dallas.ibm.local | 10.208.242.132 |
| Kubernetes API-INT (Internal) URL (Load Balancer) | api-int.ocp.dallas.ibm.local | 10.208.242.132 |
| etcd Node0 | etcd-0.ocp.dallas.ibm.local | 192.168.133.10 |
| etcd Node1 | etcd-1.ocp.dallas.ibm.local | 192.168.133.11 |
| etcd Node2 | etcd-2.ocp.dallas.ibm.local | 192.168.133.12 |
| etcd Service Record Node 0 | _etcd-server-ssl._tcp.ocp.dallas.ibm.local | 192.168.133.10 |
| etcd Service Record Node 1 | _etcd-server-ssl._tcp.ocp.dallas.ibm.local | 192.168.133.11 |
| etcd Service Record Node 2 | _etcd-server-ssl._tcp.ocp.dallas.ibm.local | 192.168.133.12 |
{: caption="Table 1. DNS records for OpenShift implementation" caption-side="bottom"}

## DNS commands
{: #openshift-runbook-runbook-dns-commands}

```powershell
# Create Reverse Lookup Zones
Add-DnsServerPrimaryZone -networkid "192.168.133.0/24" -replicationscope forest
Add-DnsServerPrimaryZone -networkid "10.208.242.0/24" -replicationscope forest

# Create DNS A Records, with PTR
Add-DnsServerResourceRecordA -Name "bastion.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.8" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "bootstrap-0.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.9" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "control-plane-0.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.10" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "etcd-0.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.10" -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "control-plane-1.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.11" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "etcd-1.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.11" -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "control-plane-2.ocp.dallas"  -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.12" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "etcd-2.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.12" -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "compute-0.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.13" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "compute-1.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.14" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "compute-2.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "192.168.133.15" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "*.apps.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "10.208.242.131" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "api.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "10.208.242.132" -CreatePtr -TimeToLive 00:00:10
Add-DnsServerResourceRecordA -Name "api-int.ocp.dallas" -ZoneName "ibm.local" -AllowUpdateAny -IPv4Address "10.208.242.132" -CreatePtr -TimeToLive 00:00:10

# Create DNS SRV record for etcd
Add-DnsServerResourceRecord -Srv -ZoneName "ibm.local" -Name "_etcd-server-ssl._tcp.ocp.dallas" -DomainName "etcd-0.ocp.dallas.ibm.local"  -Priority 10 -Weight 0 -Port 2380
Add-DnsServerResourceRecord -Srv -ZoneName "ibm.local" -Name "_etcd-server-ssl._tcp.ocp.dallas" -DomainName "etcd-1.ocp.dallas.ibm.local"  -Priority 10 -Weight 0 -Port 2380
Add-DnsServerResourceRecord -Srv -ZoneName "ibm.local" -Name "_etcd-server-ssl._tcp.ocp.dallas" -DomainName "etcd-2.ocp.dallas.ibm.local"  -Priority 10 -Weight 0 -Port 2380
```
{: pre}

## Related links
{: #vcs-openshift-runbook-dns-related}

* [{{site.data.keyword.cloud_notm}} for VMware Solutions and {{site.data.keyword.redhat_openshift_notm}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-intro)
* [Prerequisites for installation](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-prereq-intro)
* [{{site.data.keyword.redhat_openshift_notm}} NSX configuration](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-nsxedge-intro)
* [{{site.data.keyword.redhat_openshift_notm}} 4.14 user provider infrastructure installation](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-install-intro)
* [{{site.data.keyword.redhat_openshift_notm}} 4.14 additional configuration](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-config-intro)
