---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-31"

keywords: Caveonix, Caveonix RiskForesight, tech specs Caveonix

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Caveonix RiskForesight on {{site.data.keyword.cloud_notm}} overview
{: #caveonix_considerations}

Caveonix RiskForesight™ on {{site.data.keyword.cloud}} can help to manage cyberrisk and compliance risk with proactive monitoring and automated defense controls to protect against threats and to meet industry or government regulations. Caveonix RiskForesight on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from Caveonix, not IBM.
{: shortdesc}

{{site.data.content.para-promotion-services}}

The current Caveonix RiskForesight version that is installed is 5.0.
{: note}

A Caveonix RiskForesight license is valid for five years. Ordering Caveonix RiskForesight for VMware® vCenter Server instances, VMware Regulated Workloads, and Security and Compliance Readiness Bundle instances differs. For more information, see [Licenses and fees](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations#caveonix_considerations-tech-specs-license-fee).

## Technical specifications for Caveonix RiskForesight
{: #caveonix_considerations-specs}

For more information about resource requirements and capacity checking for some services, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

The following components are ordered and included in the Caveonix RiskForesight service.

### vCenter Server resources
{: #caveonix_considerations-tech-specs-vcenter}

* CPU - 8 CPUs
* RAM - 32 GB
* Disk - 100 GB

### Network
{: #caveonix_considerations-tech-specs-network}

A dedicated private subnet with 32 IP addresses is ordered.

### Licenses and fees
{: #caveonix_considerations-tech-specs-license-fee}

A Caveonix RiskForesight license key is ordered for each instance of the service.

If you order Caveonix RiskForesight for a VMware Regulated Workloads or Security and Compliance Readiness Bundle instance, you are charged for a per-host license for every host on the instance. This way of charging for Caveonix RiskForesight is new in Version 4.1. However, you are not charged for per-VM licenses.

If you order Caveonix RiskForesight for a VMware vCenter Server® instance, you are charged for the number of per-VM licenses that you choose at installation. This method of charging for Caveonix RiskForesight is the same as in previous releases. You can select 10 - 25,000 VMs to license.

If you order Caveonix RiskForesight for a VMware Regulated Workloads or Security and Compliance Readiness Bundle instance, the host-based licenses are hidden. Caveonix RiskForesight is deployed with a 25,000 VM key. You do not need to upgrade.

Caveonix RiskForesight licenses that are ordered separately from the Resources page are not per-host. Therefore, it is recommended that you do not order new Caveonix RiskForesight licenses and apply the key to your Caveonix RiskForesight service on Regulated Workloads or Security and Compliance Readiness Bundle instances. Ordering in this way will:

* Provide less coverage than when the license was initially deployed.
* Result in you being charged twice for Caveonix RiskForesight licenses because your initial license cannot be canceled. Therefore, you pay for both per-host and per-VM licensing.

You can still order Caveonix RiskForesight licenses for other types of instances, for example, for VMware vServer Center instances.

## Related links
{: #caveonix_considerations-related}

* [Ordering Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_ordering)
* [Managing Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-managingcaveonix)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
