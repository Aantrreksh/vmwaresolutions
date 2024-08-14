---

copyright:

  years:  2021, 2024

lastupdated: "2024-08-12"

keywords: add service, order service, add-on service

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering services for Automated instances
{: #vc_addingservices}

You can order services for your {{site.data.keyword.vcf-auto}} instances, such as a disaster recovery solution. Add-on services support varies between {{site.data.keyword.vcf-auto-short}} and existing {{site.data.keyword.vcf-auto-short}} with NSX-V instances V4.7 and earlier.

If you want to migrate your F5 BIG-IP or Veeam services from VMware NSX-V to VMware NSX-T, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: note}

## Before you add services to Automated instances
{: #vc_addingservices-prereq}

* Adding services to instances with VMware vSphere® 6.5 is not supported.
* For existing multizone instances, adding services is not supported. However, you can view or delete existing add-on services. After a service is deleted, it cannot be reinstalled.
* By default, the service assumes that NSX-T is installed. For existing instances V4.7 and earlier, if NSX-T is not supported for a service, then NSX-V is used.

## Available services for Automated instances
{: #vc_addingservices-available-services}

The following table shows the services that are available to Automated instances, together with the service versions.

| Service name | Current version | Notes |
|:------------ |:--------------- |:----- |
| [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations) | 5.0 | |
| [F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations) | BIG-IP VE 17.1.1 | |
| [FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations) | 7.4.3 | |
| [VMware HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations) | Periodically updated to the most recent version | |
| [{{site.data.keyword.IBM}} Security Services for SAP](/docs/vmwaresolutions?topic=vmwaresolutions-managing-ss-sap) |   | |
| [Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview) | 3.0 (23.4R1) | |
| [KMIP for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations) | 2.0 | |
| [{{site.data.keyword.redhat_openshift_notm}} for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview) | 4.15 | NSX-T only \n If you want to add the service to an existing instance with an NSX-T version earlier than 3.1, you must first upgrade to 3.1 or later. |
| [Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) | 12.1 | |
| [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) | VMware Aria® Operations™ 8.17.1 and VMware Aria Operations™ for Logs 8.17 | |
| [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr) | 9.7u4 | VMware vSphere 7 only |
{: caption="Table 1. Available services for Automated instances" caption-side="bottom"}

## Promotions for services
{: #vc_addingservices-service-promotions}

{{site.data.keyword.vmwaresolutions_full}} offers promotion pricing for some services. The promotions offer a number of months without any charge for service licenses, if the service has license charges.

You can use promotion (promo) codes for one or more services when you:
* Order a new Automated instance
* Add a service to an Automated instance
* Order a stand-alone service license, such as Caveonix or Veeam®

For services that charge per host, promo codes apply only to the hosts in the order or in the current environment. Examples of such services are HCX™ and VMware Aria® Operations™ and VMware Aria Operations™ for Logs.

You can use one promo code per order. Multiple promo codes are not allowed. However, you can use a promo code multiple times per account. A promo code might apply to multiple services, for example, Veeam and Caveonix RiskForesight™.

After you start an order, enter the promo code for your services in the promo code box and click **Apply**. If you decide to use a different promo code, enter that code in the box and click **Apply** again to calculate a new price.

If you apply a promo code for a service and then delete the service from your order, you must also remove the promo code from the order.

Promotion pricing starts when the promo code is applied. The pricing is automatically changed to the recurring price when the promotion period ends. You can see the discounts, the promotion price, and the recurring price in the PDF file generated for your order.

## Resource requirements for services
{: #vc_addingservices-resource-requirements}

Some services require a minimum amount of resources to be installed.

For certain services, the system completes a capacity check on the targeted clusters before it installs the service in your environment. The check is completed against the available capacity of the targeted cluster in the environment to ensure that the service components can fit.

During deployment, if the capacity check fails, the service is not installed and the service status is set to **Capacity Validation Failed** on the console. In addition, a console message with more details is displayed and you are notified by email. The message displays the expected capacity for all services that do not meet the requirements.

To install the service, you must increase the capacity in your cluster either by adding more VMware ESXi™ servers or by freeing up RAM, CPU, or disk space. After that, you can add the service (or services) again. To remove the existing service in the **Capacity Validation Failed** state, click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to it.

The following table provides the resource requirements for the services for which a capacity check is completed.

| Service name | Resource requirements |
|:------------ |:--------------------- |
| Caveonix RiskForesight | CPU - 8 CPUs \n RAM - 32 GB \n Storage - 100 GB |
| F5 BIG-IP[^f5bigip] | CPU - 4, 8, or 16 CPUs, depending on license and bandwidth chosen \n RAM - 8, 16, or 32 GB, depending on license and bandwidth chosen |
| FortiGate Virtual Appliance | CPU - 2, 4, 8, 16, or 32 CPUs, depending on deployment size chosen \n RAM - 4, 6, or 12 GB, depending on deployment size chosen |
| Juniper vSRX | You must have enough available capacity to accommodate two VMs with the following requirements, on different hosts: \n CPU - 6 CPUs \n RAM - 16 GB \n Storage - 18 GB \n If you install Juniper vSRX on clusters with 25 Gb uplink speed, the following capacity requirements apply. \n CPU - 10 CPUs \n RAM - 16 GB \n Storage - 18 GB |
| {{site.data.keyword.redhat_openshift_notm}} | If you install {{site.data.keyword.redhat_openshift_notm}} with vSAN™ storage, the following capacity requirements apply. \n CPU - 9 CPUs \n RAM - 120 GB \n Storage - 1,170 GB \n If you install {{site.data.keyword.redhat_openshift_notm}} with NFS storage, a new 2-TB NFS datastore, which is dedicated to {{site.data.keyword.redhat_openshift_notm}}, is ordered. |
| Veeam | If you select Veeam as a VSI option, capacity requirements don't apply. \n If you select Veeam as a VM option, the following capacity requirements apply. \n CPU - 8 CPUs \n RAM - 32 GB \n Storage - 100 GB \n If you select Veeam as a bare metal server option, capacity requirements don't apply. |
| VMware HCX | For each gateway in the active-passive pair of NSX-V Edge Services Gateways: \n CPU - 6 CPUs \n RAM - 8 GB \n Storage - 3 GB VMDK \n For the HCX Management Appliance VM: \n CPU - 4 CPUs \n RAM - 12 GB \n Storage - 60 GB VMDK |
| VMware Aria Operations and VMware Aria Operations for Logs | CPU - 18 CPUs \n RAM - 208 GB \n If you install VMware Aria Operations with vSAN storage, you must have an estimated 750 GB of vSAN storage. \n If you install VMware Aria Operations with NFS storage, you do not have a storage requirement because NFS storage is ordered as part of the instance order. |
| Zerto | CPU - 2 CPUs \n RAM - 4 GB |
{: caption="Table 2. Resources required for the services that the system checks for capacity requirements" caption-side="bottom"}

[^f5bigip]: See the table in [Considerations when you install F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations#f5_considerations-install-table).

### Formulas for calculating space requirements for services
{: #vc_addingservices-resource-requirements-spacecalc-forms}

The following formulas are used to calculate the space requirements for the services and the management overheads. The formulas apply to management clusters, workload clusters, gateway clusters, and single-node management clusters.

#### Formula to calculate the number of available cores
{: #vc_addingservices-resource-requirements-spacecalc-forms-cores}

`AvailableCores = [HostCoreCount - HostOverheadCores - (HostVSanOverheadCorePercentage * HostCoreCount)] * (HostCount - vSphereHAHostTolerance) - MgmtOverheadCores`

The following table lists the variables that are used in the previous formula.

| Variable | Description | Unit | vSAN example | NFS example |
|:-------- |:----------- |:---- |:------------ |:----------- |
| AvailableCores | The number of cores available for workloads and services in the environment | Cores | 38 | 43 |
| HostCount | The number of hosts in the default cluster | Hosts | 4 | 4 |
| HostCoreCount | The number of raw cores available in each host in the default cluster | Cores | 16 | 16 |
| HostOverheadCores | The number of cores that are reserved by the ESXi server as overhead | Cores | 0.1 | 0.1 |
| MgmtOverheadCores[^mgmtcores] | The number of cores reserved by the vCenter Server management components (vCenter Server, PSC, AD/DNS, Edges) | Cores | 5 | 5 |
| vSphereHAHostTolerance[^vspherehacores] | The number of hosts to tolerate in the vSphere HA configuration | Hosts | 1 | 1 |
| HostVsanOverheadCorePercentage | The percentage of a host's cores used by vSAN | % | 10 | 0 |
{: caption="Table 3. Description of variables in formula 1" caption-side="bottom"}

[^mgmtcores]: Management cluster only. No core reservation for the workload cluster, the gateway cluster, and the single-node management cluster.

[^vspherehacores]: Management and workload clusters only. No hosts are reserved for the gateway cluster or the single-node management cluster.

#### Formula to calculate the available memory
{: #vc_addingservices-resource-requirements-spacecalc-forms-memory}

`AvailableMemory = [HostMemory - HostOverheadMemory - HostVsanOverheadMemory - (HostVsanOverheadMemoryDiskPercentage * HostVsanCapacityDiskSize)] * (HostCount - vSphereHAHostTolerance) - MgmtOverheadMemory`

The following table lists the variables that are used in the previous formula.

| Variable | Description | Unit | vSAN example | NFS example |
|:-------- |:----------- |:---- |:------------ |:----------- |
| AvailableMemory | The number of GB of memory available for workloads and services in the environment | GB | 693 | 860 |
| HostCount | The number of hosts in the default cluster | Hosts | 6 | 6 |
| HostMemory | The number of raw GB of memory available in each host in the default cluster | GB | 192 | 192 |
| HostVsanCapacityDiskSize | The number of GB of a capacity of each vSAN capacity SSD disk on this host | GB | 960, 1,946, or 3,891 | 0 |
| HostOverheadMemory | The number of GB of memory that is reserved by the ESXi server as overhead | GB | 4.6 | 4.6 |
| MgmtOverheadMemory[^mgmtmem] | The number of GB of memory reserved by the vCenter Server management components (vCenter Server, PSC, AD/DNS, Edges) | GB | 77 | 77 |
| vSphereHAHostTolerance[^vspherehamem] | The number of hosts to tolerate in the vSphere HA configuration | Hosts | 1 | 1 |
| HostVsanOverheadMemoryDiskPercentage | The number of GB of memory reserved by vSAN management (represented as a percentage of one of the capacity vSAN disks) | % | 2.75% | 2.75% |
| HostVsanOverheadMemory | The number of GB of memory reserved by vSAN management regardless of disk size | GB | 7 | 0 |
{: caption="Table 4. Description of variables in formula 2" caption-side="bottom"}

[^mgmtmem]: Management cluster only. No memory reservation for the workload cluster, the gateway cluster, and the single-node management cluster.

[^vspherehamem]: Management and workload clusters only. No hosts are reserved for the gateway cluster or the single-node management cluster.

## Procedure to order services for Automated instances
{: #vc_addingservices-procedure}

To order a service for your Automated instance, click the appropriate service link in [Available services for Automated instances](#vc_addingservices-available-services). Review the considerations for the service and check the components that are deployed.

Then, follow the instructions in the ordering topic for your chosen service to be installed on the instance. For more information, see:
* [Ordering Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_ordering)
* [Ordering F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_ordering)
* [Ordering FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_ordering)
* [Ordering VMware HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering)
* [Ordering Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-ordering)
* [Ordering Red Hat OpenShift for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_ordering)
* [Ordering Veaam](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_ordering)
* [Ordering VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_ordering)
* [Ordering Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering)

## Results after you order services for Automated instances
{: #vc_addingservices-results}

When the installation of the service is completed successfully, you are notified by email, and the service is displayed on the **Services** page of the instance with the **Installed** status.

## Related links
{: #vc_addingservices-related}

* [General FAQ about VCF for Classic](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
