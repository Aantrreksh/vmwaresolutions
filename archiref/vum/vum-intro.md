---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-07"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware Update Manager introduction
{: #vum-intro}

As the system administrator of a {{site.data.keyword.vcf-auto}} instance, review the instructions on how to configure VMware® Update Manager (VUM) to maintain the currency of your {{site.data.keyword.vcf-auto-short}} instance.

After 21 June 2022, provisioning new {{site.data.keyword.vcf-auto-short}} instances with NSX–V is no longer supported. However, you can add hosts and clusters to your existing NSX–V deployments. IBM strongly recommends that clients immediately assess their NSX–V networks and plan a much earlier migration to NSX–T.
{: note}

After 21 June 2022, you can no longer order new {{site.data.keyword.vcf-auto-short}} instance with vSphere 6.7. After 15 October 2022, the {{site.data.keyword.vcf-auto-short}} instances with vSphere 6.7 are read–only in the VMware Solutions console. You can no longer add or remove hosts and clusters until you upgrade to vSphere 7.0.
{: note}

If you have a {{site.data.keyword.vcf-auto-short}} instance that is deployed with vSphere 7, then VMware® added new functions and rebranded it as vSphere Lifecycle Manager (vLCM). For more information, read this blog entry [vSphere 7 – lifecycle management](https://blogs.vmware.com/vsphere/2020/04/vsphere-7-patching-lifecycle-management.html){: external}

VUM enables centralized, automated patch and version management for VMware vSphere® and it allows you to complete the following tasks in your {{site.data.keyword.vcf-auto-short}} environment:
* Upgrade and patch the vSphere ESXi hosts.
* Install and update third-party software on the hosts.
* Upgrade virtual machine hardware, VMware Tools, and virtual appliances.

This document also describes the processes to maintain the following components of your {{site.data.keyword.vcf-auto-short}} instance:
* VMware vCenter® Server Appliance (VCSA)
* NSX®
* vSAN™

This document describes the use of a proxy server implementation, based on CentOS and Squid, to enable VUM to access the VMware repositories. When VUM requests a resource from the update server at VMware, the request is sent to the proxy server first and the proxy server then sends the request to the update server through the External Services Gateway (ESG). After the resource is obtained by the proxy server, it sends the resource to VUM.

![Overview diagram](../../images/vum-vcsproxy.svg "Overview diagram"){: caption="Figure 1. Overview diagram" caption-side="bottom"}

In vSphere 6.7, VUM is integrated within the VCSA, and as the VUM client component is a plug-in that runs on the vSphere Web Client it is automatically enabled after deployment of the VCSA. However, VUM has no access to the internet to access the VMware repositories.

This documented configuration uses the all-in-one, Internet-connected VUM deployment model that uses the {{site.data.keyword.cloud_notm}} public network to provide internet access to download upgrades and patches.

Clients requiring the use of alternative internet connections must investigate the VMware vSphere Update Manager Download Service (UMDS), which is beyond the scope of this publication.

While VUM can be configured to import updates from a shared repository or import patches and extensions manually from a compressed file, these details aren't discussed in this document.

In vSphere 6.7 and later, it's no longer supported to register VUM to a VCSA during installation of the VUM server on a separate Windows system you can't deploy VUM in a VM within the {{site.data.keyword.vcf-auto-short}} instance.

This information is organized into the following sections:
* [VMware Update Manager overview](/docs/vmwaresolutions?topic=vmwaresolutions-vum-overview) - Describes the VUM process and introduces key terms that are needed to understand the operations and UI of the tool.
* **Installation, Configuration, and Usage** - Describes the steps that are required to get VUM working in a {{site.data.keyword.vcf-auto-short}} instance:
   * [Initial configuration](/docs/vmwaresolutions?topic=vmwaresolutions-vum-init-config) - A one-time task to complete the following processes:
      * Configure NSX networking to allow the proxy server access to the internet.
      * Install and configure a proxy server to provide internet access for VUM.
      * The initial setup of VUM to use the proxy server.
   * [Collecting the metadata](/docs/vmwaresolutions?topic=vmwaresolutions-vum-metadata) - VUM downloads metadata about the upgrades, patches, or extensions through a predefined automatic process that you can modify. At regular configurable intervals, VUM contacts VMware, or third-party sources, to gather the most recent metadata about available upgrades, patches, or extensions.
   * [Creating baselines](/docs/vmwaresolutions?topic=vmwaresolutions-vum-baselines) - Use the pre-defined baselines and baseline groups or create custom ones. Baselines and baseline groups are then attached to inventory objects.
   * [Scanning and review](/docs/vmwaresolutions?topic=vmwaresolutions-vum-scanning) - Inventory objects are scanned, and the results are reviewed to determine how they comply with the baselines and baseline groups. Scan results can be filtered by text search, group selection, baseline selection, and compliance status selection.
   * [Staging and remediation](/docs/vmwaresolutions?topic=vmwaresolutions-vum-staging) - Patches and extensions can be optionally staged before remediation to ensure that they are downloaded to the host. During remediation, VUM applies the patches, extensions, and upgrades to the inventory objects.

This document assumes that you have one primary {{site.data.keyword.vcf-auto-short}} instance that is deployed, or a number of separate primary {{site.data.keyword.vcf-auto-short}} instances. If you have primary and secondary {{site.data.keyword.vcf-auto-short}} instances that are deployed and that use Single Sign On (SSO), see [SSO-linked vCenters](/docs/vmwaresolutions?topic=vmwaresolutions-vum-updating-vcsa).

If you deployed a {{site.data.keyword.vcf-auto-short}} instance with vSAN, see [Updating vSAN clusters](/docs/vmwaresolutions?topic=vmwaresolutions-vum-updating-vsan) first.

If you want to update the {{site.data.keyword.cloud_notm}} infrastructure management automation, use the {{site.data.keyword.vmwaresolutions_short}} console.

On the [{{site.data.keyword.vmwaresolutions_short}} console](https://cloud.ibm.com/vmware), you can complete the following actions:
* Upgrade licenses for example, upgrade NSX Base to another version.
* Initiate updates to the {{site.data.keyword.vcf-auto-short}} instance.
* View the status of updates.
* View the installed updates.

This facility enables the automated updating for the management components of the {{site.data.keyword.vcf-auto-short}} instances only. VMware product updates must be applied by using the procedures that are detailed in this document.

## Related links
{: #vum-intro-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
