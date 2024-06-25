---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-09"

keywords: Entrust CloudControl, tech specs Entrust CloudControl

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Entrust CloudControl on {{site.data.keyword.cloud_notm}} overview
{: #entrust-cc_considerations}

New installations of Entrust CloudControl™ (formerly HyTrust CloudControl) are not supported for new or existing deployments of {{site.data.keyword.vcf-auto}} instances. You can still use or delete existing Entrust CloudControl installations on your existing instances.
{: deprecated}

Entrust CloudControl on {{site.data.keyword.cloud}} enforces and controls compliance against security standards, which includes role-based access control (RBAC), approval, and auditing. Entrust CloudControl on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from Entrust, not IBM.
{: shortdesc}

* Previous installations of Entrust CloudControl 6.6 are supported for existing {{site.data.keyword.vcf-auto-short}} with NSX-T™ instances.
* Previous installations of Entrust CloudControl 5.6 are supported for existing {{site.data.keyword.vcf-auto-short}} with NSX-V instances.

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
