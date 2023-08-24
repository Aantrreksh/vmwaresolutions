---

copyright:

  years:  2016, 2023

lastupdated: "2023-08-22"

keywords: VMware HCX, HCX, tech specs HCX

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware HCX on IBM Cloud overview
{: #hcx_considerations}

The VMware HCX service is not available to Business Partner users.
{: important}

VMware HCX™ on {{site.data.keyword.cloud_notm}} extends the networks of on-premises data centers into {{site.data.keyword.cloud}}, and it helps you migrate virtual machines (VMs) to and from {{site.data.keyword.cloud_notm}} without any conversion or change. HCX creates an abstraction layer that enables application mobility and infrastructure hybridity through securely stretched networks. You can modernize your VMware® environment without the need to refactor or modify your existing application, as HCX enables a seamless transformation. With HCX, you can bring your IP subnet ranges into {{site.data.keyword.cloud_notm}} and ensure the IP consistency through a hybrid deployment and by providing high-level security with end-to-end Suite B encryptions. VMware HCX on IBM Cloud is a non-IBM product that is offered under terms and conditions from VMware, not IBM.
{: shortdesc}

The HCX version available for deployment is periodically updated to the most recent version of HCX. VMware® requires you to be on one of their supported versions in order for you to open a support request for HCX. For more information, see [VMware HCX release notes](https://docs.vmware.com/en/search/#/VMware%20HCX%204.0.1%20Release%20Notes){: external}.
{: note}

For VMware vCenter Server with NSX-T™ instances, HCX is supported for NSX-T 3.1 or later and for VMware vSphere® 7. HCX requires you to use one of the following licenses from {{site.data.keyword.cloud_notm}}:

* NSX Data Center SP Base
* NSX Data Center SP Professional
* NSX Data Center SP Advanced
* NSX Data Center SP Enterprise Plus

For vCenter Server® with NSX-V instances (VMware Solutions V4.7 and earlier), HCX is supported for vSphere 6.7. HCX requires you to use one of the following licenses from {{site.data.keyword.cloud_notm}}:

* NSX Advanced
* NSX Enterprise

For more information, see [Comparison chart for VMware NSX-T, NSX-V, and vSAN](/docs/vmwaresolutions?topic=vmwaresolutions-solution-appendix).

{{site.data.content.para-promotion-services}}

A VMware vCenter Server® instance with HCX is limited to three simultaneous connections from on-premises sites.

## Technical specifications for HCX
{: #hcx_considerations-specs}

The following components are ordered and included in the HCX service.

On-premises HCX instances include only licensing and activation.
{: note}

### HCX Management Appliance VM
{: #hcx_considerations-vm}

* CPU - 4 CPUs
* RAM - 12 GB
* Disk - 60 GB VMDK

More HCX appliances are deployed during configuration as necessary for L2 connectivity, WAN optimization, and gateway connections.

### Networking
{: #hcx_considerations-networking}

* One public portable subnet with 16 IP addresses
* Two private portable subnets with 64 IP addresses
* Eight IP addresses from private portable vMotion subnet

For more information about resource requirements and capacity checking, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

### NFS storage
{: #hcx_considerations-nsf-storage}

If the service mesh target cluster is not a vSAN™ cluster, NFS storage (with 500 GB and 10 IOPS/GB) is ordered.

For vCenter Server with NSX-V instances, the service mesh target cluster is the default cluster.
{: note}

### VMware NSX Edge Services Gateways for HCX management (NSX-V only)
{: #hcx_considerations-nsx}

An active-passive pair of VMware NSX Edge Services Gateways for HCX management is ordered.
* CPU - 6 CPUs
* RAM - 8 GB
* Disk - 3 GB VMDK

## Considerations when you install HCX
{: #hcx_considerations-install}

Review the following considerations before you install HCX.

### Requirements on the number of ESXi servers
{: #hcx_considerations-esxi-servers}

The HCX service mesh target cluster cannot have more than 51 VMware ESXi servers. HCX requires eight IP addresses in the vMotion subnet from the service mesh target cluster. Because of this requirement, if the number of ESXi servers exceeds 51, no IP addresses in the vMotion subnet are available for HCX.

For existing vCenter Server with NSX-V instances, the service mesh target cluster is the default cluster.
{: note}

### Requirements on firewall rules
{: #hcx_considerations-firewall}

Before you install the HCX service, you must add a firewall rule to any existing firewalls.

1. From the VMware Solutions console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance to view the clusters in it.
3. Click the **Infrastructure** tab and select the cluster where you want to install the HCX service.
4. Go to the **Network interface** section on the cluster page.
5. Collapse the **Public VLAN** option and collapse the subnet with the description that corresponds to the portable subnet of the particular cluster.
6. Use the IP address from the Service T0 uplink2 Virtual IP address to route the traffic in the firewall rule. The firewall rule is required to allow all outbound HTTPS traffic so that the HCX Manager virtual appliance (HCX Manager) can register itself.
7. After the HCX Manager installation is completed, you can remove the firewall rule.

In addition, you must configure firewall rules to allow HCX to function properly. For more information, see [VMware HCX port access requirements](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-port-req#hcx-archi-port-req).

## Considerations when you delete HCX
{: #hcx_considerations-delete}

Review the following considerations before you delete the HCX service:

* Before you delete the service, you must remove any personal VMs from storage that is deployed with this service. HCX only orders personal VMs if it’s not vSAN.
* Ensure that the service mesh and extended networks between the on-premises source site and the IBM Cloud target sites are deleted. To remove the service mesh and extended networks, use the HCX user interface in the on-premises VMware vSphere Web Client.
* Ensure that the site pairings between the on-premises source site and the IBM Cloud target sites are removed. To remove the site pairings, use the HCX user interface in the on-premises VMware vSphere Web Client.
* If you delete a workload cluster and that cluster is the service mesh cluster, the HCX service is automatically deleted.
* The deletion of HCX is automated. The following procedures are completed for the successful deletion of this service:
   * The HCX license that is ordered for the cloud-side HCX Manager is deactivated.
   * HCX Manager is deleted.
   * The vMotion IP addresses that were reserved for HCX are released.
   * The HCX management edge appliances are deleted.

Only the VMs that were deployed during the initial installation of the HCX instances are deleted. Any node that is deployed after the installation is not cleaned up.
{: note}

## Related links
{: #hcx_considerations-related}

* [Ordering HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering)
* [Managing HCX](/docs/vmwaresolutions?topic=vmwaresolutions-managinghcx)
* [Glossary of HCX terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_glossary)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [VMware Hybrid Cloud Extension overview](https://cloud.vmware.com/vmware-hcx){: external}
* [VMware Hybrid Cloud Extension documentation](https://cloud.vmware.com/vmware-hcx/resources){: external}
