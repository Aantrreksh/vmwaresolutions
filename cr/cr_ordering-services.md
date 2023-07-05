---

copyright:

  years:  2022, 2023

lastupdated: "2023-06-12"

keywords: Cyber Recovery add service, add service Cyber Recovery, Cyber Recovery order service, order service Cyber Recovery

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering services for Cyber Recovery instances
{: #cr_addingservices}

You can order various add-on services for your Cyber Recovery instance. For example, Caveonix RiskForesight™ is a recommended service. You can also add optional services, such as Red Hat® OpenShift® for VMware® and Zerto.

## Available services for Cyber Recovery instances
{: #cr_addingservices-available-services}

The following table shows the services that are available to Cyber Recovery instances. The table also shows the installed service versions.

| Service name | Current version |
|--------------|-----------------|
| [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations) | 4.1 |
| [Entrust CloudControl™](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-cc_considerations) | 6.6 |
| [F5® BIG-IP®](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations) | BIG-IP VE 17.1 |
| [FortiGate® Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations) | 7.2.5 |
| [VMware HCX™](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations) | Periodically updated to the most recent version |
| [Juniper® vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview) | 3.0 (23.1R2) |
| [Red Hat OpenShift for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview) | 4.12 |
| [Veeam®](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) | 12 |
| [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) | VMware Aria® Operations™ 8.12 and VMware Aria Operations™ for Logs 8.12 |
| [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr) | 9.7u3 |
{: caption="Table 1. Available services for Cyber Recovery instances" caption-side="bottom"}

## Promotions for services
{: #cr_addingservices-service-promotions}

{{site.data.keyword.vmwaresolutions_full}} offers promotion pricing for some services. The promotions offer a number of months at no cost for service licenses, if the service has license charges.

You can use one promotion (promo) code for one or more services when you:
* Order a new Cyber Recovery instance
* Add a service to a Cyber Recovery instance
* Order a stand-alone service license, such as Caveonix or Veeam

For services that charge per host, promo codes apply only to the hosts in the order or in the current environment. Examples of such services are HCX, Entrust CloudControl, and VMware Aria® Operations™ and VMware Aria Operations™ for Logs.

You can use one promo code per order. Multiple promo codes are not allowed. However, you can use a promo code multiple times per account. A promo code might apply to multiple services, for example, Veeam and Caveonix RiskForesight.

After you start an order, enter the promo code for your services in the promo code box and click **Apply**. If you decide to use a different promo code, enter that code in the box, and click **Apply** again to calculate a new price.

If you apply a promo code for a service and then delete the service from your order, you must also remove the promo code from the order.

Promotion pricing starts when the promo is applied. The pricing is automatically changed to the recurring price when the promotion period ends. You can see the discounts, promotion price, and recurring price in the PDF file generated for your order.

## Resource requirements for services
{: #cr_addingservices-resource-requirements}

Some services require a minimum amount of resources to be installed.

For certain services, the system completes a capacity check on the targeted clusters before it installs the service in your environment. The check is completed against the available capacity of the targeted cluster in the environment to ensure that the service components can fit.

During deployment, if the capacity check fails, the service is not installed and the service status is set to **Capacity Validation Failed** on the console. In addition, a console message with more details is displayed and you are notified by email. The message displays the expected capacity for all services that do not meet the requirements.

To install the service, you must increase the capacity in your cluster either by adding more VMware ESXi™ servers or by freeing up RAM, CPU, or disk space. After that, you can add the service or services again. To remove the existing service that is in a **Capacity Validation Failed** state, click the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to it.

The following table provides the resource requirements for the services for which a capacity check is completed.

| Service name | Resource requirements |
|:------------ |:--------------------- |
| Caveonix RiskForesight | CPU - 8 CPUs \n RAM - 32 GB \n Storage - 100 GB |
| F5 BIG-IP[^f5bigip] | CPU - 4, 8, or 16 CPUs, depending on license and bandwidth chosen \n RAM - 8, 16, or 32 GB, depending on license and bandwidth chosen |
| FortiGate Virtual Appliance | CPU - 2, 4, 8, 16, or 32 CPUs, depending on deployment size chosen \n RAM - 4, 6, or 12 GB, depending on deployment size chosen |
| Entrust CloudControl | CPU - 4 CPUs \n RAM - 16 GB \n Storage - 186 GB VMDK |
| Juniper vSRX | You must have enough available capacity to accommodate two VMs with the following requirements, on different hosts: \n CPU - 6 CPUs \n RAM - 16 GB \n Storage - 18 GB \n If you install Juniper vSRX on clusters with 25 Gb uplink speed, the following capacity requirements apply. \n CPU - 10 CPUs \n RAM - 16 GB \n Storage - 18 GB |
| {{site.data.keyword.redhat_openshift_notm}} | If you install {{site.data.keyword.redhat_openshift_notm}} with vSAN™ storage, the following capacity requirements apply. \n CPU - 9 CPUs \n RAM - 120 GB \n Storage - 1,170 GB \n If you install {{site.data.keyword.redhat_openshift_notm}} with NFS storage, a new 2-TB NFS data store, which is dedicated to {{site.data.keyword.redhat_openshift_notm}}, is ordered. |
| Veeam | If you select Veeam as a VSI option, there is no capacity requirement. \n If you select Veeam as a VM option, the following capacity requirements apply. \n CPU - 8 CPUs \n RAM - 32 GB \n Storage - 100 GB \n If you select Veeam as a bare metal server option, there is no capacity requirement. |
| VMware HCX | For the HCX Management Appliance VM: \n CPU - 4 CPUs \n RAM - 12 GB \n Storage - 60 GB VMDK |
| VMware Aria Operations and VMware Aria Operations for Logs | CPU - 18 CPUs \n RAM - 208 GB \n If you install VMware Aria Operations with vSAN storage, you must have an estimated 750 GB of vSAN storage. \n If you install VMware Aria Operations with NFS storage, you do not have a storage requirement because NFS storage is ordered as part of the instance order. |
| Zerto | CPU - 2 CPUs \n RAM - 4 GB |
{: caption="Table 2. Resources required for the services that the system checks for capacity requirements" caption-side="bottom"}

[^f5bigip]: See the table in [Considerations when you install F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations#f5_considerations-install-table).

### Formulas for calculating space requirements for services
{: #cr_addingservices-resource-requirements-spacecalc-forms}

The following formulas are used to calculate the space requirements for the services and the management overheads. The formulas apply to management clusters, workload clusters, gateway clusters, and single-node management clusters.

#### Formula to calculate the number of available cores
{: #cr_addingservices-resource-requirements-spacecalc-forms-cores}

`AvailableCores = [HostCoreCount - HostOverheadCores - (HostVSanOverheadCorePercentage * HostCoreCount)] * (HostCount - vSphereHAHostTolerance) - MgmtOverheadCores`

The following table lists the variables that are used in the previous formula.

| Variable | Description | Unit | vSAN example | NFS example |
|:-------- |:----------- |:---- |:------------ |:----------- |
| AvailableCores | The number of cores available for workloads and services in the environment | Cores | 38 | 43 |
| HostCount | The number of hosts in the default cluster | Hosts | 4 | 4 |
| HostCoreCount | The number of raw cores available in each host in the default cluster | Cores | 16 | 16 |
| HostOverheadCores | The number of cores that are reserved by the ESXi server as overhead | Cores | 0.1 | 0.1 |
| MgmtOverheadCores[^mgmtcores] | The number of cores reserved by the Cyber Recovery management components (Cyber Recovery, PSC, AD/DNS, Edges) | Cores | 5 | 5 |
| vSphereHAHostTolerance[^vspherehacores] | The number of hosts to tolerate in the vSphere HA configuration | Hosts | 1 | 1 |
| HostVsanOverheadCorePercentage | The percentage of a host's cores used by vSAN | % | 10 | 0 |
{: caption="Table 3. Description of variables in formula 1" caption-side="bottom"}

[^mgmtcores]: Management cluster only. No core reservation for the workload cluster, the gateway cluster, and the single-node management cluster.

[^vspherehacores]: Management and workload clusters only. No hosts are reserved for the gateway cluster or the single-node management cluster.

#### Formula to calculate the available memory
{: #cr_addingservices-resource-requirements-spacecalc-forms-memory}

`AvailableMemory = [HostMemory - HostOverheadMemory - HostVsanOverheadMemory - (HostVsanOverheadMemoryDiskPercentage * HostVsanCapacityDiskSize)] * (HostCount - vSphereHAHostTolerance) - MgmtOverheadMemory`

The following table lists the variables that are used in the previous formula.

| Variable | Description | Unit | vSAN example | NFS example |
|:-------- |:----------- |:---- |:------------ |:----------- |
| AvailableMemory | The number of GB of memory available for workloads and services in the environment | GB | 693 | 860 |
| HostCount | The number of hosts in the default cluster | Hosts | 6 | 6 |
| HostMemory | The number of raw GB of memory available in each host in the default cluster | GB | 192 | 192 |
| HostVsanCapacityDiskSize | The number of GB of a capacity of each vSAN capacity SSD disk on this host | GB | 960, 1,946, or 3,891 | 0 |
| HostOverheadMemory | The number of GB of memory that is reserved by the ESXi server as overhead | GB | 4.6 | 4.6 |
| MgmtOverheadMemory[^mgmtmem] | The number of GB of memory reserved by the Cyber Recovery management components (Cyber Recovery, PSC, AD/DNS, Edges) | GB | 77 | 77 |
| vSphereHAHostTolerance[^vspherehamem] | The number of hosts to tolerate in the vSphere HA configuration | Hosts | 1 | 1 |
| HostVsanOverheadMemoryDiskPercentage | The number of GB of memory reserved by vSAN management (represented as percentage of one of the capacity vSAN disks) | % | 2.75% | 2.75% |
| HostVsanOverheadMemory | The number of GB of memory reserved by vSAN management regardless of disk size | GB | 7 | 0 |
{: caption="Table 4. Description of variables in formula 2" caption-side="bottom"}

[^mgmtmem]: Management cluster only. No memory reservation for the workload cluster, the gateway cluster, and the single-node management cluster.

[^vspherehamem]: Management and workload clusters only. No hosts are reserved for the gateway cluster or the single-node management cluster.

## Procedure to order services for Cyber Recovery instances
{: #cr_addingservices-procedure}

For Cyber Recovery instances, a recommended service is Caveonix RiskForesight, which manages cyberrisk and compliance risk. You can have many other options, such as Zerto, Entrust CloudControl, and Red Hat OpenShift for VMware Solutions.

For more information, see [Available services for Cyber Recovery instances](/docs/vmwaresolutions?topic=vmwaresolutions-cr_addingservices#cr_addingservices-available-services).

## Results after you order services for Cyber Recovery instances
{: #cr_addingservices-results}

When the installation of the service is completed successfully, you are notified by email, and the service is displayed on the **Services** page of the instance with the **Installed** status.

## Related links
{: #cr_addingservices-related}

* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
