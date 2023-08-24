---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-31"

keywords: Entrust DataControl, tech specs Entrust DataControl

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Entrust DataControl on IBM Cloud overview
{: #entrust-dc_considerations}

New installations of Entrust DataControl® (formerly known as HyTrust DataControl) are not supported for new or existing deployments of VMware vCenter Server® instances. You can still use or delete existing Entrust DataControl installations on your existing instances.
{: deprecated}

## Technical specifications for Entrust DataControl
{: #entrust-dc_considerations-specs}

The following components are included in your existing Entrust DataControl service.

### Entrust DataControl appliance
{: #entrust-dc_considerations-appliance}

* CPU - 2 CPUs
* RAM - 8 GB
* Disk - 20 GB VMDK resident on vSAN in the consolidated cluster
* Network - Placed on a VLAN-backed private portable network specified for management

### High availability
{: #entrust-dc_considerations-ha}

Two Entrust DataControl appliances in an active-active configuration.

### Licenses and fees
{: #entrust-dc_considerations-licenses}

Per host license - An Entrust DataControl license for each host in the environment.
