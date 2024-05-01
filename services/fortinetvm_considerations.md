---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-29"

keywords: FortiGate VA, FortiGate Virtual Appliance, tech specs FortiGate VA

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}} overview
{: #fortinetvm_considerations}

FortiGate® Virtual Appliance on {{site.data.keyword.cloud}} deploys a pair of FortiGate Virtual Appliances to your environment, which can help you reduce risk by implementing critical security controls within your virtual infrastructure. FortiGate Virtual Appliance on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from Fortinet, not IBM.
{: shortdesc}

* You can install multiple instances of this service as needed. You can manage this service by using the FortiOS Web Client or the CLI through SSH.
* For {{site.data.keyword.vcf-auto}} with NSX-T™ instances, FortiGate Virtual Appliance is supported for NSX-T 3.1 or later and for VMware vSphere® 7.0.
* For existing NSX-V instances V4.7 and earlier, FortiGate Virtual Appliance is supported for vSphere 6.7.

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some add-on services. Promotional pricing offers a number of months at no cost for a service license, if the service has license charges. For more information, see [Promotions for VMware Solutions add-on services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).

The FortiGate Virtual Appliance version available for deployment is 7.4.3.
{: note}

## Technical specifications for FortiGate Virtual Appliance
{: #fortinetvm_considerations-specs}

For more information about resource requirements and capacity checking for some services, see [Resource requirements for add-on services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

The following components are ordered and included in the FortiGate Virtual Appliance service.

### Virtual machines
{: #fortinetvm_considerations-specs-vms}

* All options include a pair of virtual machines (VMs).
* 2, 4, 8, 16, or 32 CPUs per VM. The number depends on the deployment size.
* 4, 6, or 12 GB RAM per VM. The number depends on the deployment size.

### High availability
{: #fortinetvm_considerations-specs-ha}

Two VMs are deployed and ready for HA or Virtual Router Redundancy Protocol (VRRP) configuration.

### Networking
{: #fortinetvm_considerations-specs-network}

Access to the FortiGate console is provided through a private management network. When deployed to a management or consolidated cluster, FortiGate Virtual Appliance management addresses are drawn from the instance management private portable subnet. When deployed to a gateway cluster, a new private portable subnet is ordered for these addresses.

### License and fees
{: #fortinetvm_considerations-specs-license}

License fees for each VM are applied to each billing cycle. The fees depend on the selected deployment size and monthly subscription license model.

#### Licensing notes
{: #fortinetvm_considerations-notes}

* You cannot change the licensing level after service installation. To change the licensing level, you must delete the existing service and reinstall the service by using a different licensing option.
* If you receive expiration notifications about the FortiGate Virtual Appliance service license, you can ignore them. The license is automatically renewed annually before it expires.

## Uplink speeds, deployment sizes, and CPU models
{: #fortinetvm_considerations-installvalues}

The following information describes the different considerations for the uplink speed, deployment size, and CPU when you install FortiGate Virtual Appliance.

### FortiGate Virtual Appliance on {{site.data.keyword.vcf-auto-short}}
{: #fortinetvm_considerations-installvalues-vcs7}

You can install FortiGate Virtual Appliance on the consolidated cluster or the gateway cluster.

On the consolidated cluster, note the following information:

* You can choose a 10 Gb or 25 Gb uplink speed for the cluster.

   * For 10 Gb, you can select a deployment size from FortiGate-VM02 up to FortiGate-VM32.
   * For 25 Gb, you can select a FortiGate-VM16 or FortiGate-VM32 deployment size.

* The FortiGate-VM32 deployment size requires Cascade Lake 5218 or higher.

On the gateway cluster, note the following information about the uplink speed:

* For 10 Gb, select Cascade Lake 4210 and FortiGate-VM16.
* For 25 Gb, select Cascade Lake 5218 and either FortiGate-VM16 or FortiGate-VM32.

### FortiGate Virtual Appliance on {{site.data.keyword.rw}}
{: #fortinetvm_considerations-installvalues-regworkload}

For {{site.data.keyword.rw}}, you can install FortiGate Virtual Appliance on the gateway cluster. You can deploy the service on a single-zone (new or existing) or multizone (existing only) instance.

* You can install FortiGate Virtual Appliance on gateway clusters with a 10 Gb or 25 Gb uplink speed.
* For 10 Gb, you can install FortiGate-VM16 on Cascade Lake 4210.
* For 25 Gb, you can install FortiGate-VM16 or FortiGate-VM32. The FortiGate-VM32 deployment size requires Cascade Lake 5218 or higher.

### FortiGate Virtual Appliance on vCenter Server 6.7 with NSX-V
{: #fortinetvm_considerations-installvalues-vcs6-7}

On existing NSX-V instances V4.7 and earlier, you can install FortiGate Virtual Appliance on the management cluster.

* You can select a deployment size from FortiGate-VM02 up to FortiGate-VM16.
* You can install FortiGate Virtual Appliance on clusters with a 10 Gb or 25 Gb uplink speed.
* NSX-V clusters with 25 Gb uplink speed support only a deployment size of FortiGate-VM16.

### FortiGate Virtual Appliance on the Security and Compliance Readiness Bundle
{: #fortinetvm_considerations-installvalues-scb}

On the Security and Compliance Readiness Bundle, you can install FortiGate Virtual Appliance on the gateway cluster.

* You can install FortiGate Virtual Appliance on gateway clusters with a 10 Gb or 25 Gb uplink speed.
* For 10 Gb, you can select a deployment size from FortiGate-VM02 up to FortiGate-VM32. The FortiGate-VM32 deployment size requires Cascade Lake 5218 or higher.
* For 25 Gb, you can install FortiGate-VM16 or FortiGate-VM32. The FortiGate-VM32 deployment size requires Cascade Lake 5218 or higher.

## FortiGate Virtual Appliance order example
{: #fortinetvm_considerations-example}

You can order a {{site.data.keyword.vcf-auto-short}} instance with two VMware ESXi™ servers with the following configuration: 16 cores at 2.10 GHz each with 128 GB RAM. For FortiGate Virtual Appliance, you select 8 CPUs / 12 GB RAM for deployment size and any subscription license model.

In this case, a single FortiGate VM requires the following components on each server:
* 2.1 GHz * 8 CPU = 16.8 GHz of CPU
* 12 GB RAM

For two FortiGate VMs, the total is 33.6 GHz CPU and 24 GB RAM.

Each ESXi server has a capacity of 16 cores * 2.1 GHz = 33.6 GHz. So the first two requirements are met if both servers are active and there are at least 16.8 GHz of CPU and 12 GB RAM available on each server.

However, by default, vSphere HA reserves 50% of CPU and RAM for failover on Automated instances that were initially deployed with two ESXi servers. So the capacity is shown in the following formula.

`50% of 2 * 16 cores * 2.1 GHz = 33.6 GHz available`

Since other workloads exist on the ESXi servers, for example, vCenter Server, VMware NSX® Controller, or VMware NSX Edge, by using these resources, the third requirement is not met. The reason is because 33.6 GHz of CPU and 24 GB RAM for the two FortiGate VMs are needed.

In this case, the FortiGate Virtual Appliance installation might fail, unless at least one ESXi server is added to the environment. Also, the vSphere HA failover reservations must be updated to ensure that enough resources are available for two FortiGate VMs.

If more resources are needed to run the FortiGate Virtual Appliance service, you can add more ESXi servers before you install the service.

## Related links
{: #fortinetvm_considerations-related}

* [Ordering FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_ordering)
* [Managing FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-managingfortinetvm)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [General FAQ about VCF for Classic](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Fortinet website](https://www.fortinet.com/){: external}
* [Fortinet Document Library](https://docs.fortinet.com/product/fortigate/7.4){: external}
