---

copyright:

  years:  2020, 2024

lastupdated: "2024-04-03"

keywords: vmware regulated workloads, vmware regulated workloads order instance, order vmware regulated workloads, vmware regulated workloads instances

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Requirements for {{site.data.keyword.rw}}
{: #vrw-orderinginstance-req}

The {{site.data.keyword.rw}} offering includes a secure-by-default architecture that follows the {{site.data.keyword.IBM}} unique policy controls framework. It provides continuous compliance monitoring and the highest level of data encryption (FIPS 140-2 Level 4).

Price calculations are automatically generated when you access the {{site.data.keyword.rw}} instance order page. Default selections include the Data Center SP Professional license for NSX-T™, the Dual Intel® Xeon® Platinum 8260 processor / 48 cores, 2.4 GHz CPU model, 768 GB RAM, the vSAN™ Advanced license for both workload and consolidated clusters, and four 3.8 TB SSD vSAN capacity disks for workload clusters.

Ensure that you complete the following tasks:
* If you are ordering an instance for the first time, complete the tasks in the **Before you begin** section on the ordering page. For more information, see [Setting up your environment for your first order](/docs/vmwaresolutions?topic=vmwaresolutions-completing_checklist).
* Review the information in [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).
* Review the information in [{{site.data.keyword.rw}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-overview).
* Review the domain name format. The domain name is used to generate the username and server names of the instance.

| Name        | Value format |
|:------------|:------------ |
| Domain name | `<root_domain>` (Microsoft® Active Directory™ domain name) |  
| vCenter Server® login username | `<user_id>@<root_domain>` (Microsoft® Active Directory user) or `administrator@vsphere.local` |
| vCenter Server (with embedded PSC) FQDN | `<instance_name>-vc.<root_domain>`. The maximum length is 50 characters. Any hyphens (-) are removed from the instance name. |
| Single Sign-On (SSO) site name | `<root_domain>` |
| Fully qualified ESXi server name | `<host_prefix><n>.<root_domain>`, where `n` is the sequence of the VMware vSphere® ESXi™ server. The maximum length is 50 characters. |
| NetBIOS name | First string of `<root_domain>`. The maximum length is 15 characters. |
{: caption="Table 1. Value format for instance and domain names" caption-side="bottom"}

After the instance is provisioned, do not modify any values that are set during the instance order. Otherwise, the instance might become unusable.
{: attention}

## Related links
{: #vrw-orderinginstance-reqs-related}

* [{{site.data.keyword.rw}} reference architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-archi-overview)
