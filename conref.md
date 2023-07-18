---

copyright:
  years: 2022, 2023

lastupdated: "2023-07-12"

keywords: IBM Cloud for VMware Solutions, getting started, vmware solutions offerings, services for vmwaresolutions, vmwaresolutions use cases

subcollection: vmwaresolutions

content-type: conref

---

{{site.data.keyword.attribute-definition-list}}

# Content references for VMware Solutions subcollection
{: #conref-vmwaresolutions}

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_orderinginstance-bare-metal.md (*file removed*)
- vcenter\vc_orderinginstance-consold-cluster.md
- vcenter\vc_addingclusters.md

CONTENT:

For **Skylake** servers, you can choose the following CPU models and a supported RAM size, which depends on the NSX networking solution.
{: #skylake-para-intro}

Skylake servers are not supported for VMware vSphere® Enterprise Plus 7.0u1 instances.
{: note}
{: #skylake-note}

| CPU model     | Cores     | GHz     | RAM         |
|:------------- |:----------|:--------|:----------- |
| Dual Intel® Xeon® Silver 4110 processor | 16 | 2.1 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5120 processor | 28 | 2.2 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6140 processor | 36 | 2.3 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
{: caption="Table 1. Options for Skylake bare metal servers - NSX-T instances" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NSX-T instances"}
{: tab-group="SkyLake Intel servers"}
{: #simpletabtable-skylake-nsxt}


| CPU model     | Cores     | GHz     | RAM         |
|:------------- |:----------|:--------|:----------- |
| Dual Intel® Xeon® Silver 4110 processor | 16 | 2.1 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5120 processor | 28 | 2.2 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6140 processor | 36 | 2.3 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
{: caption="Table 1. Options for Skylake bare metal servers - NSX-V instances" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NSX-V instances"}
{: tab-group="SkyLake Intel servers"}
{: #simpletabtable-skylake-nsxv}

VMware NSX-V is no longer supported for new deployments of vCenter Server instances V4.7 and later.
{: note}
{: #vcenter-nsxv-note-skylake}

For **Cascade Lake** servers, you can choose the following CPU models and a supported RAM size, which depends on the NSX networking solution.
{: #cascade-para-intro}

| CPU model     | Cores     | GHz     | RAM         |
|:------------- |:----------|:--------|:----------- |
| Dual Intel Xeon Silver 4210 processor | 20 | 2.2 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 processor | 32 | 2.3 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 processor | 40 | 2.5 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6250 processor | 16 | 3.9 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 processor | 48 | 2.4 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 processor | 80 | 2.5 | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 processor | 96 | 2.4 | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 2. Options for Cascade Lake bare metal servers - NSX-T instances" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NSX-T instances"}
{: tab-group="Cascade Lake Intel servers"}
{: #simpletabtable-cascade-nsxt}


| CPU model     | Cores     | GHz     | RAM         |
|:------------- |:----------|:--------|:----------- |
| Dual Intel Xeon Silver 4210 processor | 20 | 2.2 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 processor | 32 | 2.3 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 processor | 40 | 2.5 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6250 processor | 16 | 3.9 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 processor | 48 | 2.4 | 64 GB, 96 GB, 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 processor | 80 | 2.5 | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 processor | 96 | 2.4 | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 2. Options for Cascade Lake bare metal servers - NSX-V instances" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NSX-V instances"}
{: tab-group="Cascade Lake Intel servers"}
{: #simpletabtable-cascade-nsxv}

VMware NSX-V is no longer supported for new deployments of vCenter Server instances V4.7 and later.
{: note}
{: #vcenter-nsxv-note-cascadelake}


For **SAP-certified Cascade Lake** servers, you can select from the following configurations:
{: #sap-para-intro}

| CPU model     | SAP certification | Cores     | GHz     | RAM         | Storage type |
|:------------- |:------------------|:----------|:--------|:------------|:------------ |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.NW192) | NetWeaver | 32 | 2.3 | 192 GB | Up to 12 Drivers |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.NW384) | NetWeaver | 32 | 2.3 | 384 GB | Up to 12 Drivers |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.NW768) | NetWeaver | 40 | 2.5 | 768 GB | Up to 12 Drivers |
| Dual Intel Xeon Platinum 8260 processor (Cascade Lake, BI.S4.NW768_v2) | Netweaver | 48 | 2.4 | 768 GB | Up to 12 Drivers |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.NW1500) | Netweaver | 56 |2.7 | 1.5 TB | Up to 12 Drivers |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.NW3000) | Netweaver | 56 | 2.7 | 3 TB | Up to 12 Drivers |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.H2.192) | HANA and NetWeaver | 32 | 2.3 | 192 GB | Up to 12 Drivers |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.H2.384) | HANA and NetWeaver | 32 | 2.3 | 384 GB | Up to 12 Drivers |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.H2.768) | HANA and NetWeaver | 40 | 2.5 | 768 GB | Up to 12 Drivers |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H2.1500) | HANA and NetWeaver | 56 | 2.7 | 1.5 TB | Up to 12 Drivers |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H2.3000) | HANA and NetWeaver | 56 | 2.7 | 3 TB | Up to 12 Drivers |
| Quad Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H4.3000) | HANA and NetWeaver | 112 | 2.7 | 3 TB | Up to 24 Drivers |
| Quad Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H4.6000) | HANA and NetWeaver | 112 | 2.7 | 6 TB | Up to 24 Drivers |
{: caption="Table 3. Options for SAP-certified Cascade Lake - NetWeaver and HANA" caption-side="bottom"}
{: #simpletabtable-sap-netweaverandhana}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:

- cr\cr_addingclusters.md
- cr\cr_orderinginstance-consolidwkld.md
- cr\cr_orderinginstance-edge.md
- vcenter\scb-orderinginstance-cons-work-cluster.md
- vcenter\vc_addingclusters.md
- vcenter\vc_orderinginstance-addl-clusters.md
- vcenter\vc_orderinginstance-consold-cluster.md
- vrw\vrw-orderinginstance-edge.md
- vrw\vrw-orderinginstance-mgmt.md
- vrw\vrw-orderinginstance-primary.md
- vrw\vrw-orderinginstance-witness.md
- vrw\vrw-orderinginstance-wkld.md
- vsphere\vs_orderinginstances-network.md

CONTENT:

The uplink speed provides two options:
* 10 Gb, which is selected by default.
* 25 Gb, which is available only for specific pods and data center locations. The following table shows the available locations for the 25 Gb uplink speed.
{: #uplink-speed-options-list}

The uplink speed provides two options:
* 10 Gb, which is selected by default.
* 25 Gb, which is available only for specific pods and data center locations. The following table shows the available locations for the 25 Gb uplink speed.
{: #uplink-speed-options-cascadelake-list}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific | TOK02 | 02 |
| Asia-Pacific | TOK04 | 01 |
{: caption="Table 1. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-ap}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Europe | FRA04 | 01 |
| Europe | FRA05 | 01 |
| Europe | LON04 | 01 |
| Europe | LON06 | 01 |
| Europe | MAD02 | 01 |
| Europe | MAD04 | 01 |
| Europe | MAD05 | 01 |
| Europe | PAR04 | 01 |
| Europe | PAR05 | 01 |
| Europe | PAR06 | 01 |
{: caption="Table 1. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-eur}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA East | TOR04 | 01 |
| NA East | WDC04 | 05 |
| NA East | WDC06 | 01 |
{: caption="Table 1. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-naeast}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA South | DAL12 | 01 |
| NA South | DAL13 | 02 |
{: caption="Table 1. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-nasouth}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific | TOK02 | 02 |
| Asia-Pacific | TOK04 | 01 |
{: caption="Table 2. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers for uplink speed"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-other-ap}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Europe | FRA05 | 01 |
| Europe | LON04 | 01 |
| Europe | LON06 | 01 |
| Europe | MAD02 | 01 |
| Europe | MAD04 | 01 |
| Europe | MAD05 | 01 |
{: caption="Table 2. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers for uplink speed"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-other-eur}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA East | TOR04 | 01 |
| NA East | WDC04 | 05 |
| NA East | WDC06 | 01 |
{: caption="Table 2. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers for uplink speed"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-other-naeast}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| NA South | DAL12 | 01 |
| NA South | DAL13 | 02 |
{: caption="Table 2. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers for uplink speed"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-other-nasouth}

Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_orderinginstance-procedure.md
- vcenter\vrw-orderinginstance-procedure.md

CONTENT:

**CAUTION** Managing any {{site.data.keyword.vmwaresolutions_short}} components (which were installed into your {{site.data.keyword.cloud_notm}} account when you ordered the instance) from outside the VMware Solutions console can make your environment unstable. The following activities are considered management activities:
*  Adding, modifying, returning, or removing components
*  Expanding or contracting instance capacity through adding or removing ESXi servers
*  Powering off components
*  Restarting services
{: #caution-component-management}

Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- services\vrops_overview.md
- services\veeamvm_overview.md
- services\managing-ss-sap.md
- services\entrust-cc_considerations.md
- services\hcx_considerations.md
- services\f5_considerations.md
- services\caveonix_considerations.md

CONTENT:

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some services. Promotional pricing offers a number of months without charge for a service license, if the service has license charges. For more information, see [Promotions for VMware Solutions services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).
{: #para-promotion-services}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- services\juniper_overview.md
- services\addingzertodr.md

CONTENT:

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some add-on services. Promotional pricing offers a number of months without charge for a service license, if the service has license charges. For more information, see [Promotions for VMware Solutions add-on services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).
{: #para-promotion-add-on-services}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_deletinginstance.md
- vcenter\vc_deletinginstance_multi.md
- vcenter\vc_hybrid_deletinginstance.md
- vcenter\vc_hybrid_deletinginstance_multi.md

CONTENT:

When you delete a vCenter Server instance, the following components are released sequentially:
1. All deployed services
2. The Support fee for NSX-T instances or the Support and Services fee for NSX-V instances
3. VMware® product licenses
4. VMware ESXi™ servers
5. Subnets
6. VLANs
{: #deletinginstance-components-list}

Review the following information before you proceed.
* Any existing VLANs that you own, outside of {{site.data.keyword.vmwaresolutions_full}}, are not deleted.
* Any VLANs that contain your own resources, such as gateways or Veeam® servers are not deleted.
* Any VLANs or subnets without attached gateways or servers are deleted even though you might have IP addresses assigned to it from the subnets to your VMs.
{: #deletinginstance-delete-vlans}

Because of resource dependencies, the components in your instance are not released immediately when you delete the instance. For example, the VLANs and the VLAN primary subnets cannot be deleted until the ESXi servers are fully reclaimed by the {{site.data.keyword.cloud_notm}} infrastructure, which happens at the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle. At the end of the billing cycle, which is typically 30 days, the subnets and VLANs are deleted and the instance deletion is completed.
{: #deletinginstance-delete-info}

You are billed until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle for the deleted instance.
{: important}
{: #deletinginstance-important-note}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_addingservers.md
- vcenter\vc_hybrid_addingremovingservers.md
- vcenter\vc_removingservers.md

CONTENT:

Whenever possible, add ESXi servers by using the {{site.data.keyword.vmwaresolutions_full}} console because changes that you make on the VMware vSphere® Web Client are not synchronized with the {{site.data.keyword.vmwaresolutions_short}} console. Therefore, add ESXi servers to vCenter Server only for on-premises ESXi servers or ESXi servers that you don't manage in the {{site.data.keyword.vmwaresolutions_short}} console.
{: #para-vcenteraddESXiservers}

Whenever possible, remove ESXi servers by using the {{site.data.keyword.vmwaresolutions_full}} console because changes that you make on the VMware vSphere® Web Client are not synchronized with the {{site.data.keyword.vmwaresolutions_short}} console. Therefore, remove ESXi servers from vCenter Server only for on-premises ESXi servers or ESXi servers that you don't manage in the {{site.data.keyword.vmwaresolutions_short}} console.
{: #para-vcenterremoveESXiservers}

Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_addingclusters.md
- vcenter\vc_hybrid_addingviewingclusters.md
- vcenter\vc_deletingclusters.md

CONTENT:

Whenever possible, add clusters by using the {{site.data.keyword.vmwaresolutions_full}} console and not the VMware vSphere® Web Client. Changes that you make on the vSphere Web Client are not synchronized with the VMware Solutions console. If you want to add clusters to vCenter Server instances by using the vSphere Web Client, do so only for on-premises clusters or clusters that you don't manage in the VMware Solutions console.
{: #para-vcenteraddclusters}

Whenever possible, delete clusters by using the {{site.data.keyword.vmwaresolutions_full}} console and not the VMware vSphere® Web Client. Changes that you make on the vSphere Web Client are not synchronized with the VMware Solutions console. If you want to delete clusters from vCenter Server instances by using the vSphere Web Client, do so only for on-premises clusters or clusters that you don't manage in the VMware Solutions console.
{: #para-vcenterremoveclusters}

Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_orderinginstance-sys.md
- vcenter\vrw-orderinginstance-resource.md

CONTENT:

You can also specify an instance name that meets the following requirements:
* Only lowercase alphabetic, numeric, and dash (-) characters are allowed.
* No consecutive dash characters are allowed.
* The instance name must start with a lowercase alphabetic character.
* The instance name must end with a lowercase alphabetic or numeric character.
* The maximum length of the instance name is 10 characters.
* The instance name must be unique within your account.
{: #orderinginstance-inst-name-list}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vs_orderinginstance-sys.md
- vcenter\vrw-orderinginstance-wkld.md
- vcenter\vrw-orderinginstance-primary.md
- vcenter\vrw-orderinginstance-edge.md

CONTENT:

You can also specify a cluster name that meets the following requirements:
* Only lowercase alphabetic, numeric, and dash (-) characters are allowed.
* The cluster name must start with a lowercase alphabetic character.
* The cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the cluster name is 10 characters.
* The cluster name must be unique within your account.
{: #orderinginstance-cluster-name-list}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_addingclusters.md
- vcenter\vc_orderinginstance-consold-cluster.md

CONTENT:

You can also specify a new cluster name that meets the following requirements:
* Only lowercase alphabetic, numeric, and dash (-) characters are allowed.
* The cluster name must start with a lowercase alphabetic character.
* The cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the cluster name is 30 characters.
* The cluster name must be unique within the vCenter Server instance.
{: #cluster-name-requirements-list}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- cr\cr_orderinginstance-gen-info.md
- vcenter\vc_orderinginstance-sys.md

CONTENT:

Use resource groups to organize the resources in your account for access control and billing purposes. The default resource group in your account is selected. You can also select another resource group according to your needs. The resource group that you select cannot be changed after the instance is created.
{: #para-orderinginstance-resource-group}

If **No resource group available** is displayed in this field, you currently do not have the permission to add the instance to any resource group in this account. Contact the account owner to be assigned an Editor or Administrator role on a resource group in the account. For more information, see [IAM access](/docs/account?topic=account-userroles).
{: note}
{: #note-orderinginstance-resource-group}

Click **Browse configurations** to open the **Instance configuration manager** side panel. In this side panel, you can choose a configuration from the list of saved configuration templates to update it and then save it as a new configuration template, or to delete it.
{: #paraone-orderinginstance-inst-config}

If you do not see any configuration names in the **Instance configuration manager**, then you do not have any existing saved configuration templates and might want to create one. To create a new configuration, specify settings for your instance first as a configuration template without placing an order. To save the settings, click **Save configuration** on the **Summary** pane.
{: #paratwo-orderinginstance-inst-config}

Select whether to order a new primary instance or a secondary instance for an existing primary instance.
{: #para-orderinginstance-primary-secondary}

Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- cr_orderinginstance-consolidwkld.md
- vc_orderinginstance-consold-cluster.md
- scb-orderinginstance-cons-work-cluster.md
- vc_orderinginstance-addl-clusters.md
- vc_addingclusters.md

CONTENT:

* If you are planning to use NFS storage, you can order 3-51 servers.
* If you are planning to use vSAN™ storage, you can order 4-51 servers.
* All servers that you order have the same configuration.
{: #number-of-baremetal-servers}

* If you are planning to use NFS storage, you can order 2-59 servers. However, for production workloads, a minimum of 3 servers is recommended. For more information, see [Is a two-node vCenter Server instance highly available?](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions#is-a-two-node-vcenter-server-instance-highly-available)
* If you are planning to use vSAN™ storage, you can order 4-59 servers.
* All servers that you order have the same configuration.
{: #exception-number-of-baremetal-servers}

Conref section END.

For more information about the conref.md file template, see [Using conrefs to reuse chunks of content within your subcollection](https://test.cloud.ibm.com/docs/writing?topic=writing-conrefs).
