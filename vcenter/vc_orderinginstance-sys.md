---

copyright:

  years:  2016, 2023

lastupdated: "2023-06-20"

keywords: vCenter Server order instance, order vCenter Server, order vCenter Server instance

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# General information
{: #vc_orderinginstance-sys-settings}

Specify or accept the following settings when you order a VMware vCenter Server® instance.

## VMware vSphere version
{: #vc_orderinginstance-vsphere-license}

VMware vSphere® Enterprise Plus 7 is ordered by default.

### Notes on upgrading to vSphere 7
{: #vc_orderinginstance-vsphere-v6-7-upgrade}

For vCenter Server instances with vSphere 6.7, upgrading to vSphere 7 is supported for selected configurations. If you want to use vSphere 7, you can:
* Deploy a new vSphere 7 instance and migrate your current workloads to the new instance.
* Contact [IBM Support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) for assistance with your upgrade process.

Migrating your workloads is recommended if you want to:
* Perform a hardware refresh.
* Migrate from VMware NSX–V to VMware NSX–T™.
* Migrate your existing NSX–T topology with separate management and workload clusters to a converged topology.

## VMware NSX networking solution
{: #vc_orderinginstance-nsx}

For new instances, the VMware NSX® networking solution is NSX-T.

## Instance name
{: #vc_orderinginstance-inst-name}

The instance name is set to **vcs-_xx_** by default, where _xx_ represents two randomly generated alphabetic characters.

{{site.data.content.orderinginstance-inst-name-list}}

## Resource group
{: #vc_orderinginstance-resource-group}

{{site.data.content.para-orderinginstance-resource-group}}

{{site.data.content.note-orderinginstance-resource-group}}

## Instance configuration name
{: #vc_orderinginstance-inst-config}

{{site.data.content.paraone-orderinginstance-inst-config}}

{{site.data.content.paratwo-orderinginstance-inst-config}}

## Instance type
{: #vc_orderinginstance-primary-secondary}

{{site.data.content.para-orderinginstance-primary-secondary}}

## Related links
{: #vc_orderinginstance-sys-related}

* [Licensing](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-licensing-settings)
* [Procedure to order vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure)
