---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-06"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Types of VMware software updates
{: #vum-type-updates}

VMware® uses the following terms to describe software updates.

| Term | Definition |
|:---- |:---------- |
| Bulletin | A grouping of one or more VIBs. Bulletins are defined within metadata. |
| Depot | A logical grouping of VIBs and associated metadata that is published online. |
| Host upgrade image | An ESXi™ image that you can import in the Update Manager repository and use for upgrading ESXi hosts. |
| Extension | A bulletin that defines a group of VIBs for adding an optional component to an ESXi host. An extension is usually provided by a third-party provider that is also responsible for patches or updates to the extension. |
| Metadata | Extra data that defines dependency information, textual descriptions, system requirements, and bulletins. |
| Offline bundle compressed file | An archive that encapsulates VIBs and corresponding metadata in a self-contained package that is useful for offline patching. You can't use third-party offline bundles or offline bundles that you generated from custom VIB sets for host upgrade. |
| Patch | A bulletin that groups one or more VIBs together to address a particular issue or enhancement. |
| Roll-up | A collection of patches that is grouped for ease of download and deployment. |
| VA upgrade | Updates for a virtual appliance, which the vendor considers an upgrade. |
| VIB | A single software package. |
{: caption="Table 1. VMware software update terms and definitions" caption-side="bottom"}

## Related links
{: #vum-type-updates-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
