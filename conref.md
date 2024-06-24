---

copyright:
  years: 2022, 2024

lastupdated: "2024-04-29"

keywords: IBM Cloud for VMware Solutions, getting started, vmware solutions offerings, services for vmwaresolutions, vmwaresolutions use cases

subcollection: vmwaresolutions

content-type: conref

---

{{site.data.keyword.attribute-definition-list}}

# Content references for VMware Solutions subcollection
{: #conref-vmwaresolutions}

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- cr/cr_orderinginstance-consolidwkld.md
- vcenter/vc_orderinginstance-consold-cluster.md
- vcenter/vc_addingclusters.md
- vsphere/vs_orderinginstances-bare-metal.md -->

CONTENT:

For **Cascade Lake** servers, choose from the following CPU models and supported RAM sizes:
{: #cascade-para-intro}

| CPU model | Cores | GHz | Storage type | RAM options |
|:--------- |:----- |:--- |:------------ |:----------- |
| Dual Intel Xeon Silver 4210 | 20 | 2.2 | Up to 12 drives | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 5218 | 32 | 2.3 | Up to 12 drives | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Gold 6248 | 40 | 2.5 | Up to 12 drives | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Dual Intel Xeon Platinum 8260 | 48 | 2.4 | Up to 12 drives | 128 GB, 192 GB, 384 GB, 768 GB, 1.5 TB |
| Quad Intel Xeon Gold 6248 | 80 | 2.5 | Up to 24 drives | 384 GB, 768 GB, 1.5 TB, 3 TB |
| Quad Intel Xeon Platinum 8260 | 96 | 2.4 | Up to 24 drives | 384 GB, 768 GB, 1.5 TB, 3 TB |
{: caption="Table 1. Options for Cascade Lake bare metal servers" caption-side="bottom"}
{: #simpletabtable-cascade}


For **SAP-certified Cascade Lake** servers, choose from the following configurations:
{: #sap-para-intro}

| CPU model     | Cores     | GHz     | RAM         | Storage type |
|:------------- |:----------|:--------|:------------|:------------ |
| Dual Intel Xeon Gold 5218 (BI.S4.NW192) | 32 | 2.3 | 192 GB | Up to 12 drives |
| Dual Intel Xeon Gold 5218 (BI.S4.NW384) | 32 | 2.3 | 384 GB | Up to 12 drives |
| Dual Intel Xeon Gold 6248 (BI.S4.NW768) | 40 | 2.5 | 768 GB | Up to 12 drives |
| Dual Intel Xeon Platinum 8260 (BI.S4.NW768_v2) | 48 | 2.4 | 768 GB | Up to 12 drives |
| Dual Intel Xeon Platinum 8280M (BI.S4.NW1500) | 56 | 2.7 | 1.5 TB | Up to 12 drives |
| Dual Intel Xeon Platinum 8280M (BI.S4.NW3000) | 56 | 2.7 | 3 TB | Up to 12 drives |
{: caption="Table 2. Options for SAP-certified Cascade Lake bare metal servers - NetWeaver" caption-side="bottom"}
{: tab-title="NetWeaver"}
{: tab-group="SAP-certified Intel servers"}
{: class="simple-tab-table"}
{: #simpletabtable-sap-netweaver}


| CPU model     | Cores     | GHz     | RAM         | Storage type |
|:------------- |:----------|:--------|:------------|:------------ |
| Dual Intel Xeon Gold 5218 (BI.S4.H2.192) | 32 | 2.3 | 192 GB | Up to 12 drives |
| Dual Intel Xeon Gold 5218 (BI.S4.H2.384) | 32 | 2.3 | 384 GB | Up to 12 drives |
| Dual Intel Xeon Gold 6248 (BI.S4.H2.768) | 40 | 2.5 | 768 GB | Up to 12 drives |
| Dual Intel Xeon Platinum 8280M (BI.S4.H2.1500) | 56 | 2.7 | 1.5 TB | Up to 12 drives |
| Dual Intel Xeon Platinum 8280M (BI.S4.H2.3000) | 56 | 2.7 | 3 TB | Up to 12 drives |
| Quad Intel Xeon Platinum 8280M (BI.S4.H4.3000) | 112 | 2.7 | 3 TB | Up to 24 drives |
| Quad Intel Xeon Platinum 8280M (BI.S4.H4.6000) | 112 | 2.7 | 6 TB | Up to 24 drives |
{: caption="Table 2. Options for SAP-certified Cascade Lake bare metal servers - HANA and NetWeaver" caption-side="bottom"}
{: tab-title="HANA and NetWeaver"}
{: tab-group="SAP-certified Intel servers"}
{: class="simple-tab-table"}
{: #simpletabtable-sap-hana}

<!-- Conref section END. -->

<!--Conref section START.

INFORMATION:
The section is referenced by the following files:

- cr/cr_orderinginstance-consolidwkld.md
- vcenter/scb-orderinginstance-cons-work-cluster.md
- vcenter/vc_addingclusters.md
- vcenter/vc_orderinginstance-consold-cluster.md
- vrw/vrw-orderinginstance-mgmt.md
- vrw/vrw-orderinginstance-primary.md
- vrw/vrw-orderinginstance-witness.md
- vrw/vrw-orderinginstance-wkld.md
- vsphere/vs_orderinginstances-network.md -->

CONTENT:

The uplink speed provides two options:
* 10 Gb, which is selected by default.
* 25 Gb, which is available only for specific pods and data center locations. The following table shows the available locations for the 25 Gb uplink speed.
{: #uplink-speed-options-list}

| Data center | Pod |
|:----------- |:--- |
| TOK02 | 02 |
| TOK04 | 01 |
| TOK05 | 01 |
{: caption="Table. Available locations for 25 Gb uplink speed - Asia-Pacific" caption-side="bottom"}
{: tab-title="Asia-Pacific"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-ap}

| Data center | Pod |
|:----------- |:--- |
| FRA02 | 02 |
| FRA04 | 01 |
| FRA05 | 01 |
| LON04 | 01 |
| LON06 | 01 |
| MAD02 | 01 |
| MAD04 | 01 |
| MAD05 | 01 |
| PAR04 | 01 |
| PAR05 | 01 |
| PAR06 | 01 |
{: caption="Table. Available locations for 25 Gb uplink speed - Europe" caption-side="bottom"}
{: tab-title="Europe"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-eur}

| Data center | Pod |
|:----------- |:--- |
| TOR04 | 01 |
| WDC04 | 04 |
| WDC06 | 01 |
{: caption="Table. Available locations for 25 Gb uplink speed - NA East" caption-side="bottom"}
{: tab-title="NA East"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-naeast}

| Data center | Pod |
|:----------- |:--- |
| DAL10 | 03 |
| DAL12 | 01 |
| DAL13 | 02 |
{: caption="Table. Available locations for 25 Gb uplink speed - NA South" caption-side="bottom"}
{: tab-title="NA South"}
{: tab-group="Data centers"}
{: class="simple-tab-table"}
{: #simpletable-uplink-speed-locations-nasouth}

<!-- Conref section END. -->

<!--Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_orderinginstance-procedure.md
- vcenter/vrw-orderinginstance-procedure.md -->

CONTENT:

**CAUTION** Managing any {{site.data.keyword.vmwaresolutions_short}} components (which were installed into your {{site.data.keyword.cloud_notm}} account when you ordered the instance) from outside the VMware Solutions console can make your environment unstable. The following activities are considered management activities:
*  Adding, modifying, returning, or removing components
*  Expanding or contracting instance capacity through adding or removing ESXi servers
*  Powering off components
*  Restarting services
{: #caution-component-management}

<!-- Conref section END. -->

<!--Conref section START.

INFORMATION:
The section is referenced by the following files:
- services/addingzertodr.md
- services/caveonix_considerations.md
- services/f5_considerations.md
- services/hcx_considerations.md
- services/juniper_overview.md
- services/ocp_overview.md
- services/veeamvm_overview.md
- services/vrops_overview.md -->

CONTENT:

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some add-on services. Promotional pricing offers a number of months at no cost for a service license, if the service has license charges. For more information, see [Promotions for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).
{: #para-promotion-services}

<!--Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_deletinginstance.md
- vcenter/vc_deletinginstance_multi.md
- vcenter/vc_hybrid_deletinginstance.md
- vcenter/vc_hybrid_deletinginstance_multi.md -->

CONTENT:

When you delete a {{site.data.keyword.vcf-auto}} instance, the following components are released sequentially:
1. All deployed services
2. NFS storage
3. The Support fee for NSX-T instances or the Support and Services fee for NSX-V instances
4. VMware® product licenses
5. VMware ESXi™ servers
6. Subnets
7. VLANs
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


<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_addingservers.md
- vcenter/vc_hybrid_addingremovingservers.md
- vcenter/vc_removingservers.md -->

CONTENT:

Whenever possible, add ESXi servers by using the {{site.data.keyword.vmwaresolutions_full}} console because changes that you make on the VMware vSphere® Web Client are not synchronized with the {{site.data.keyword.vmwaresolutions_short}} console. Therefore, add ESXi servers to vCenter Server only for on-premises ESXi servers or ESXi servers that you don't manage in the {{site.data.keyword.vmwaresolutions_short}} console.
{: important}
{: #para-vcenteraddESXiservers}

Whenever possible, remove ESXi servers by using the {{site.data.keyword.vmwaresolutions_full}} console because changes that you make on the VMware vSphere® Web Client are not synchronized with the {{site.data.keyword.vmwaresolutions_short}} console. Therefore, remove ESXi servers from vCenter Server only for on-premises ESXi servers or ESXi servers that you don't manage in the {{site.data.keyword.vmwaresolutions_short}} console.
{: important}
{: #para-vcenterremoveESXiservers}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_addingclusters.md
- vcenter/vc_hybrid_addingviewingclusters.md
- vcenter/vc_deletingclusters.md -->

CONTENT:

Whenever possible, add clusters by using the {{site.data.keyword.vmwaresolutions_full}} console and not the VMware vSphere® Web Client. Changes that you make on the vSphere Web Client are not synchronized with the VMware Solutions console. If you want to add clusters to {{site.data.keyword.vcf-auto}} instances by using the vSphere Web Client, do so only for on-premises clusters or clusters that you don't manage in the VMware Solutions console.
{: important}
{: #para-vcenteraddclusters}

Whenever possible, delete clusters by using the {{site.data.keyword.vmwaresolutions_full}} console and not the VMware vSphere® Web Client. Changes that you make on the vSphere Web Client are not synchronized with the VMware Solutions console. If you want to delete clusters from {{site.data.keyword.vcf-auto}} instances by using the vSphere Web Client, do so only for on-premises clusters or clusters that you don't manage in the VMware Solutions console.
{: important}
{: #para-vcenterremoveclusters}

<!-- Conref section END. -->

<!--Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_orderinginstance-sys.md
- vcenter/vrw-orderinginstance-resource.md -->

CONTENT:

You can also specify an instance name that meets the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* No consecutive hyphens are allowed.
* The instance name must start with a lowercase alphabetic character.
* The instance name must end with a lowercase alphabetic or numeric character.
* The maximum length of the instance name is 10 characters.
* The instance name must be unique within your account.
{: #orderinginstance-inst-name-list}


<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vrw-orderinginstance-wkld.md
- vcenter/vrw-orderinginstance-primary.md
- vcenter/vrw-orderinginstance-edge.md -->

CONTENT:

You can also specify a cluster name that meets the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* The cluster name must start with a lowercase alphabetic character.
* The cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the cluster name is 10 characters.
* The cluster name must be unique within your account.
{: #orderinginstance-cluster-name-list}


<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_addingclusters.md
- vcenter/vc_orderinginstance-consold-cluster.md -->

CONTENT:

You can also specify a new cluster name that meets the following requirements:
* Only lowercase alphabetic, numeric, and hyphen (-) characters are allowed.
* The cluster name must start with a lowercase alphabetic character.
* The cluster name must end with a lowercase alphabetic or numeric character.
* The maximum length of the cluster name is 30 characters.
* The cluster name must be unique within the {{site.data.keyword.vcf-auto}} instance.
{: #cluster-name-requirements-list}


<!-- Conref section END. -->

<!--Conref section START.

INFORMATION:
The section is referenced by the following files:
- cr/cr_orderinginstance-gen-info.md
- vcenter/vc_orderinginstance-sys.md
- vsphere/vs_orderinginstances-sys.md
- vrw/vrw-orderinginstance-config.md -->

CONTENT:

Use resource groups to organize the resources in your account for access control and billing purposes. The default resource group in your account is selected. You can also select another resource group according to your needs. The resource group that you select cannot be changed after the instance is created.
{: #para-orderinginstance-resource-group}

If **No resource group available** is displayed in this field, you currently do not have permissions to any resource group in this account. Contact the account owner to be assigned an Editor or Administrator role on a resource group in the account. For more information, see [{{site.data.keyword.cloud_notm}} IAM roles](/docs/account?topic=account-userroles).
{: note}
{: #note-orderinginstance-resource-group}

Click **Browse configurations** to open the configuration manager side panel. Here, you can choose a configuration from the list of saved templates to update it and then save it as a new configuration template.
{: #paraone-orderinginstance-inst-config}

If you do not see any configurations in the list, then you do not have any saved templates and might want to create one. To create a configuration, first specify the settings for your instance as a configuration template without placing an order. To save the settings, click **Save configuration** on the **Summary** pane.
{: #paratwo-orderinginstance-inst-config}

Select whether to order a new primary instance or a secondary instance for an existing primary instance.
{: #para-orderinginstance-primary-secondary}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- cr_orderinginstance-consolidwkld.md
- scb-orderinginstance-cons-work-cluster.md
- vc_addingclusters.md
- vc_orderinginstance-addl-clusters.md
- vc_orderinginstance-consold-cluster.md -->

CONTENT:

* If you are planning to use NFS storage, you can order 3-51 servers.
* If you are planning to use vSAN™ storage, you can order 4-51 servers.
* All servers that you order have the same configuration.
{: #number-of-baremetal-servers-consol}

* If you are planning to use NFS storage, you can order 2-59 servers.
* If you are planning to use vSAN™ storage, you can order 4-59 servers.
* All servers that you order have the same configuration.
{: #number-of-baremetal-servers-wkld}

<!--Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_vcs_80_upgrade.md
- vcenter/vc_vsphere_70_upgrade.md -->

CONTENT:

The time to complete the upgrade is unknown. It is possible that it might take several maintenance windows to completely upgrade an environment. Running up-leveled and down-leveled versions of the SDDC software is supported by VMware® during the upgrade process. However, some functions such as vMotion, might be limited during this process.
{: #para-vcs80upgrade-prereq}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- vcenter/vc_orderinginstance-sys.md
- vrw/vrw-orderinginstance-config.md -->

CONTENT:

vCenter Server 7 is selected by default.
{: #para-vcsversion80-vcsline1}

For new instances, vCenter Server 8 is available to order. However, for existing instances or clusters with vCenter Server 7, you can add only vCenter Server 7 clusters or hosts.
{: #para-vcsversion80-vcsline2}

vSphere 8 is not yet available to order from the VMware Solutions console.
{: note}
{: #note-vcsversion80-vsphere8}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- shared/iam_vcd.md
- shared/shared-monitor.md
- shared/shared-vmwaas-migration.md
- shared/shared_accessing-vcd-console.md
- shared/shared_creating-endpoints.md
- shared/shared_data_security.md
- shared/shared_deleting-endpoints.md
- shared/shared_deletinginstance.md
- shared/shared_iam-integration.md
- shared/shared_migration.md
- shared/shared_modifying-endpoints.md
- shared/shared_ordering.md
- shared/shared_overview.md
- shared/shared_planning.md
- shared/shared_pricing.md
- shared/shared_resizeinstance.md
- shared/shared_vcd-ops-guide.md
- shared/shared_veeam.md
- shared/shared_viewing-endpoints.md
- shared/shared_viewing-vdc-details.md
- shared/shared_viewing-vdc-summary.md
- shared/shared_zerto-cloud-connector-delete.md
- shared/shared_zerto-cloud-connector-order.md
- shared/shared_zerto-cloud-connector-view.md
- shared/shared_zerto-portal.md
- vmonic/eos-vmware-shared.md
- vmonic/faq_shared-eos.md
- vmonic/faq_shared.md  -->

CONTENT:

{{site.data.keyword.vm-shared}} is no longer available for new deployments. Existing instances will continue to be supported until 15 January 2025. Ensure that you migrate all your {{site.data.keyword.vm-shared}} resources to [{{site.data.keyword.vmware-service-full}}](/docs/vmware-service) by 15 January 2025. For more information, see [End of Support for {{site.data.keyword.vm-shared}} deployments](/docs/vmwaresolutions?topic=vmwaresolutions-eos-vmware-shared).
{: deprecated}
{: #shared-deprecated-note}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- cr/cr_planning.md
- vcenter/vc_planning.md
- vrw/vrw-planning.md
- vsphere/vs_planning.md -->

CONTENT:

The VMware® licensing model is changed. You are entitled to the [VMware software products](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_packaging-pricing#vmwaresol_packaging-pricing-impact) that are included in the VMware Cloud Foundation™ bundle. To request VMware NSX® license upgrades and other licensing changes, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).
{: #vmware-licensing}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
cr/cr_orderinginstance-consolidwkld.md
cr/cr_orderinginstance-gen-info.md
cr/cr_orderinginstance-order-procedure.md
vcenter/scb-orderinginstance-cons-work-cluster.md
vcenter/vc_addingclusters.md
vcenter/vc_orderinginstance-consold-cluster.md
vcenter/vc_orderinginstance-licensing.md
vcenter/vc_orderinginstance-procedure.md
vrw/vrw-orderinginstance-licensing.md
vrw/vrw-orderinginstance-primary.md
vrw/vrw-orderinginstance-procedure.md
vrw/vrw-orderinginstance-wkld.md
vsphere/vs_orderingbasedonexistingconfig.md
vsphere/vs_orderinginstances-licensing.md
vsphere/vs_orderinginstances-procedure.md
vsphere/vs_vsphereoverview.md -->

Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Use this feature only if you are upgrading or migrating an existing BYOL cluster.
{: attention}
{: #attnnote-byol}

Bring Your Own License (BYOL) is no longer supported except for migrations or upgrades of existing BYOL clusters. Add a host to a BYOL cluster only if you are upgrading or migrating an existing BYOL cluster.
{: attention}
{: #attnnote-addhost-byol}

<!-- Conref section END. -->

<!-- Conref section START.

INFORMATION:
The section is referenced by the following files:
- services/hcx_considerations.md
- services/hcx_ordering.md -->

The automated deployment process is not supported for BYOL (Bring Your Own License). You must complete the HCX deployment process manually.
{: important}
{: #impnote-deploymanual-hcx}

<!-- Conref section END. -->
