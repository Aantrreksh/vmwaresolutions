---

copyright:
  years: 2022, 2023

lastupdated: "2023-06-22"

keywords: IBM Cloud for VMware Solutions, getting started, vmware solutions offerings, services for vmwaresolutions, vmwaresolutions use cases

subcollection: vmwaresolutions

content-type: conref

---

{{site.data.keyword.attribute-definition-list}}

# Content references for vmwaresolutions subcollection
{: #conref-vmwaresolutions}

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_orderinginstance-bare-metal.md (*file removed*)
- vcenter\vc_orderinginstance-cluster.md
- vcenter\vc_addingclusters.md

CONTENT:

For **Skylake** servers, you can choose the following CPU models and a supported RAM size, which depends on the NSX networking solution.
{: #skylake-para-intro}

Skylake servers are not supported for VMware vSphere® Enterprise Plus 7.0u1 instances.
{: note}
{: #skylake-note}

| CPU model     | Cores     | GHz     | RAM sizes   |
|:------------- |:----------|:--------|:----------- |
| Dual Intel® Xeon® Silver 4110 processor | 16 | 2.1 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5120 processor | 28 | 2.2 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6140 processor | 36 | 2.3 | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
{: caption="Table 1. Options for Skylake bare metal servers - NSX-T instances" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NSX-T instances"}
{: tab-group="SkyLake Intel servers"}
{: #simpletabtable-skylake-nsxt}


| CPU model     | Cores     | GHz     | RAM sizes   |
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

| CPU model     | Cores     | GHz     | RAM sizes   |
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


| CPU model     | Cores     | GHz     | RAM sizes   |
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


For **SAP-certified** servers, you have the following options:
* **NetWeaver**, for which the CPU and RAM size are preset.
* **HANA**, for which you can choose the CPU model with its supported RAM size, which depends on the NSX networking solution.
{: #sap-para-intro}

| CPU model     | Cores     | GHz     | RAM sizes   |
|:------------- |:----------|:--------|:----------- |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.NW192) | 32 | 2.3 | 192 GB |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.NW384) | 32 | 2.3 | 384 GB |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.NW768) | 40 | 2.5 | 768 GB |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.NW768_v2) | 48 | 2.4 | 768 GB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.NW1500) | 56 | 2.7 | 1.5 TB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.NW3000) | 56 | 2.7 | 3 TB |
{: caption="Table 3. Options for SAP-certified bare metal servers - NetWeaver" caption-side="bottom"}
{: class="simple-tab-table"}
{: tab-title="NetWeaver"}
{: tab-group="SAP-certified Intel servers"}
{: #simpletabtable-sap-netweaver}


| CPU model     | Cores     | GHz     | RAM sizes |
|:------------- |:----------|:--------|:--------- |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.H2.192) | 32 | 2.3 | 192 GB |
| Dual Intel Xeon Gold 5218 processor (Cascade Lake, BI.S4.H2.384) | 32 | 2.3 | 384 GB |
| Dual Intel Xeon Gold 6248 processor (Cascade Lake, BI.S4.H2.768) | 40 | 2.5 | 768 GB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H2.1500) | 56 | 2.7 | 1.5 TB |
| Dual Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H2.3000) | 56 | 2.7 | 3 TB |
| Quad Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H4.3000) | 112 | 2.7 | 3 TB |
| Quad Intel Xeon Platinum 8280M processor (Cascade Lake, BI.S4.H4.6000) | 112 | 2.7 | 6 TB |
{: caption="Table 3. Options for SAP-certified bare metal servers - HANA" caption-side="bottom"}
{: tab-title="HANA"}
{: tab-group="SAP-certified Intel servers"}
{: class="simple-tab-table"}
{: #simpletabtable-sap-hana}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:

- vcenter\vc_orderinginstance-edge.md
- vcenter\vrw-orderinginstance-edge.md
- vcenter\vrw-orderinginstance-mgmt.md
- vcenter\vrw-orderinginstance-primary.md
- vcenter\vrw-orderinginstance-wkld.md
- vsphere\vs_orderinginstances-network.md
- cr\cr_orderinginstance-edge.md
- vrw\vrw-orderinginstance-witness.md
- vcenter\scb-orderinginstance-cons-work-cluster.md

CONTENT:

The uplink speed provides two options:
* 10 Gb, which is selected by default.
* 25 Gb, which is available only for **Cascade Lake** and **SAP-certified** bare metal servers and for specific data center locations. The following table shows the available locations for the 25 Gb uplink speed.
{: #uplink-speed-options-list}

The uplink speed provides two options:
* 10 Gb, which is selected by default.
* 25 Gb, which is available only for specific locations. The following table shows the available {{site.data.keyword.cloud}} data centers for the 25 Gb uplink speed.
{: #uplink-speed-options-cascadelake-list}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific | TOK02 | 02 |
| Asia-Pacific | TOK04 | 01 |
| Asia-Pacific | TOK05 | 01 |
| Europe | FRA02 | 02 |
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
| NA East | TOR04 | 01 |
| NA East | WDC04 | 05 |
| NA East | WDC06 | 01 |
| NA East | WDC07 | 01 |
| NA South | DAL10 | 03 |
| NA South | DAL12 | 01 |
| NA South | DAL13 | 02 |
{: caption="Table 1. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: #simpletable-uplink-speed-locations}

| Geography | Data center | Pod |
|:--------- |:----------- |:--- |
| Asia-Pacific | TOK02 | 02 |
| Asia-Pacific | TOK04 | 01 |
| Asia-Pacific | TOK05 | 01 |
| Europe | FRA02 | 02 |
| Europe | FRA05 | 01 |
| Europe | LON04 | 01 |
| Europe | LON06 | 01 |
| Europe | MAD02 | 01 |
| Europe | MAD04 | 01 |
| Europe | MAD05 | 01 |
| NA East | TOR04 | 01 |
| NA East | WDC04 | 05 |
| NA East | WDC06 | 01 |
| NA East | WDC07 | 01 |
| NA South | DAL10 | 03 |
| NA South | DAL12 | 01 |
| NA South | DAL13 | 02 |
{: caption="Table 2. Available locations for 25 Gb uplink speed" caption-side="bottom"}
{: #simpletable-uplink-speed-locations-other}

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

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some services. Promotional pricing offers a number of months free of charge for a service’s licenses, if the service has license charges. For more information, see [Promotions for VMware Solutions services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).
{: #para-promotion-services}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- services\juniper_overview.md
- services\addingzertodr.md

CONTENT:

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some add-on services. Promotional pricing offers a number of months free of charge for a service’s licenses, if the service has license charges. For more information, see [Promotions for VMware Solutions add-on services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).
{: #para-promotion-add-on-services}


Conref section END.

Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter\vc_deletinginstance.md
- vcenter\vc_deletinginstance_multi.md
- vcenter/vc_hybrid_deletinginstance.md
- vcenter/vc_hybrid_deletinginstance_multi.md

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
* Any existing VLANs that you own, outside of {{site.data.keyword.vmwaresolutions_full}}, will not be deleted.
* Any VLANs that have your own resources added to them, such as gateways or Veeam® servers will not be deleted.
* Any VLANs or subnets without attached gateways or servers will be deleted even though you might have IP addresses assigned from the subnets to your VMs.
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
- vcenter\vc_orderinginstance-cluster.md

CONTENT:

You can also specify a new cluster name that meets the following requirements:
* Only lowercase alphabetic, numeric, and dash (-) characters are allowed.
* The cluster name must start with a lowercase alphabetic character.
* The cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the cluster name is 10 characters.
* The cluster name must be unique within the vCenter Server instance.
{: #cluster-name-requirements-list}


Conref section END.


For details about the conref.md file template, see [Using conrefs to reuse chunks of content within your subcollection](https://test.cloud.ibm.com/docs/writing?topic=writing-conrefs).
