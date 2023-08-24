---

copyright:

  years:  2016, 2023

lastupdated: "2023-08-22"

keywords: Entrust CloudControl, tech specs Entrust CloudControl

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Entrust CloudControl on IBM Cloud overview
{: #entrust-cc_considerations}

New installations of Entrust CloudControl® (formerly known as HyTrust CloudControl) are not supported for new or existing deployments of VMware vCenter Server® instances. You can still use or delete existing Entrust CloudControl installations on your existing instances.
{: deprecated}

Entrust CloudControl on {{site.data.keyword.cloud_notm}} enforces and controls compliance against security standards, which includes role-based access control (RBAC), approval, and auditing. Entrust CloudControl on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from Entrust, not IBM.
{: shortdesc}

* Previous installations of Entrust CloudControl 6.6 are supported for existing vCenter Server with NSX-T™ instances.
* Previous installations of Entrust CloudControl 5.6 are supported for existing vCenter Server with NSX-V instances.

## Technical specifications for Entrust CloudControl
{: #entrust-cc_considerations-specs}

Existing Entrust CloudControl installations are preconfigured with connections to the following components:
* Microsoft® Active Directory™
* vCenter Server
* VMware NSX-T

The following components are included in your existing Entrust CloudControl service:

### Entrust CloudControl appliance
{: #entrust-cc_considerations-appliance}

* CPU - 4 CPUs
* RAM - 16 GB
* Disk - 186 GB VMDK
* Network - Placed on VLAN-backed private portable network specified for management

### High availability
{: #entrust-cc_considerations-ha}

Two Entrust CloudControl appliances in an active-passive configuration.

### Licenses and fees
{: #entrust-cc_considerations-licenses}

Per host license - An Entrust CloudControl license for each host in the environment.

