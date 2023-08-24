---

copyright:

  years:  2022, 2023

lastupdated: "2023-08-11"

keywords: troubleshooting, host connection lost, NFS datastore connection lost

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Why did my host lose connection to my NFS datastore?
{: #trbl_esxi_firewall_config_nfs}
{: troubleshoot}

There are several possible reasons for loss of connectivity to storage. One possibility is that {{site.data.keyword.cloud}} was performing maintenance on your endurance storage, which disabled your storage's IP addresses in a rotating fashion. However, your host was not aware of all endurance storage IP addresses.
{: tsSymptoms}

This issue might occur if you have an incorrect entry in the `/etc/hosts` file of your VMware vCenter Server® hosts. The entry was added by the {{site.data.keyword.cloud}} automation for hosts that are part of a management cluster with NFS storage. In the `/etc/hosts` file for these hosts, the entry of the hostname for some endurance storage was hardcoded to a single IP address.
{: tsCauses}

Although endurance storage is resilient, as a result of this misconfiguration, if {{site.data.keyword.cloud_notm}} performs maintenance on that Endurance IP address, access to the datastore is interrupted and VMs might fail.

If your management cluster is using NFS storage, review the `/etc/hosts` file for the hosts in this cluster and delete entries similar to the following example:
{: tsResolve}

```text
10.200.158.59   fsf-sng0101b-fz.service.softlayer.com
```

Also, if you run your Active Directory (AD) domain controllers on endurance storage, a circular dependency exists between your AD controllers, which are on endurance storage and the fact that VMware vSphere® is mounting this storage, which depends on DNS resolution. 

If all your directory controllers are offline, then storage mounts might fail. To recover from this situation, temporarily add entries to `/etc/hosts` for the storage volume. To reduce the likelihood of this situation, you can create extra domain controllers or move at least one of your domain controllers from shared storage to local storage.



