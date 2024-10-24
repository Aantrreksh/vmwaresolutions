---

copyright:

  years:  2024

lastupdated: "2024-10-24"

keywords: vmware add-ons, firewall add-ons, vsan add-on, vmware avi add-on

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware add-ons for VMware Cloud Foundation
{: #vmware-add-ons}

You must order separately a number of VMware® add-ons for your VMware Cloud Foundation™ bundle.

## VMware Avi Load Balancer add-on
{: #vmware-add-ons-nsx-avi}

Avi Load Balancer (formerly NSX Advanced Load Balancer) is available as a VMware add-on. The basic load-balancing function of VMware NSX® will be removed by Broadcom when new licenses are issued in the future.

If you need load balancing for your environment, order the Avi Load Balancer from the {{site.data.keyword.cloud}} console.

## VMware NSX firewall add-ons
{: #vmware-add-ons-nsx-firewall}

VMware by Broadcom extracted the distributed and gateway firewalls from VMware NSX into the VMware Cloud Foundation bundle and made it a separate add-on, which is available for purchase in the {{site.data.keyword.cloud_notm}} console. You must purchase licenses for the number of cores that are required for your environment separately.

Currently, the NSX firewall add-ons do not issue a license key. Later, VMware by Broadcom will disable the NSX firewall add-ons and require new license keys. The VMware Solutions team will work with you in the future to obtain the license keys.

The NSX firewall add-on is the same for both the distributed and the gateway firewall. You must order the appropriate number of firewall cores for your environment.

* If you are ordering a new {{site.data.keyword.vcf-auto}} instance, the minimum gateway firewall cores are calculated for your order.
* If you are an existing customer, you must purchase NSX firewall licenses separately for the number of cores that are required for your environment.
* To calculate the number of firewall cores that you need for your environment and to confirm the cost (depending on whether you use distributed, gateway, or no firewall), contact your IBM Business Partner representative or IBM Support.

For on-demand, the cost for the firewall add-on is $12.50 per core, per month. Discounts are available depending on your contract commitment.

* **Distributed firewall**: For this option, all host cores that are running VMware NSX must be licensed for the DFW Firewall Add-On. This is done because virtual network segments span the entire environment and a virtual machine (VM) can run on any host.
* **Gateway firewall**: For this option, the vCPUs that are running on the edge VMs provide the gateway firewall service, therefore they are counted. To get the edge VMs properly configured, the VMs are sized and 4 cores per vCPU in the edge VMs are calculated.

For example, by using the sizing guidance at [NSX Edge VM System Requirements](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/installation/GUID-22F87CA8-01A9-4F2E-B7DB-9350CA60EA4E.html){: external} if you choose a large edge, then each edge requires 8 vCPU, therefore 32 cores to be licensed: `8 vCPUs in the VM * 4 cores per vCPU = 32 cores`

As many environments use multiple edges for redundancy, 2 large edges (8 vCPUs each) require 64 cores worth of licensing: `2 edge VMs * 8 vCPUs per edge * 4 cores per vCPU = 64 cores`

## vSAN add-on
{: #vmware-add-ons-vsan}

VMware vSAN is included at a rate of 1 TiB per VMware Cloud Foundation core.

To calculate the amount of vSAN storage for your entire environment, see [Counting Cores for VMware Cloud Foundation and vSphere Foundation and TiBs for vSAN](https://knowledge.broadcom.com/external/article?legacyId=95927){: external}.  If you need more than 1 TiB of vSAN, order the  new vSAN add-on from the {{site.data.keyword.cloud_notm}} console.

The vSAN add-on is priced at $21 per TiB of vSAN per month. Discounts are available depending on your contract commitment.

## Ordering the VMware add-ons
{: #vmware-add-ons-order}

You can order the VMware add-ons from the {{site.data.keyword.cloud_notm}} console. Later, this process will provide license keys that you can install on VMware NSX. Currently, these keys are not available or required.

1. Click **Infrastructure > Classic Infrastructure** from the left navigation menu.
2. Click **Manage > VMware licenses**.
3. Order the VMware add-on.

You can also cancel the VMware add-ons from the {{site.data.keyword.cloud}} console.

## What to do next
{: #vmware-add-ons-next}

If applicable to you, complete the following tasks:

* If you ordered the Avi Load Balancer add-on, also install an Avi (NSX ALB) license key. For more information, see [Using NSX Advanced Load Balancer License File](https://docs.vmware.com/en/VMware-NSX-Advanced-Load-Balancer/30.1/Administration-Guide/GUID-AF9067C3-2F07-45E5-A9E6-3A696066EEAB.html){: external}.
* If you are planning to order VMware Cloud Foundation for VPC instances, also [configure the NSX firewalls for VCF for VPC instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-firewall) after you deployed your VCF for VPC instance.

## Related links
{: #vmware-add-ons-links}

* [VMware Avi Load Balancer](https://www.vmware.com/products/cloud-infrastructure/avi-load-balancer ){: external}
* [Gateway Firewall](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-A52E1A6F-F27D-41D9-9493-E3A75EC35481.html){: external}
* [Distributed Firewall](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/administration/GUID-6AB240DB-949C-4E95-A9A7-4AC6EF5E3036.html){: external}
* [NSX Edge VM System Requirements](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/installation/GUID-22F87CA8-01A9-4F2E-B7DB-9350CA60EA4E.html){: external}
* [Counting Cores for VMware Cloud Foundation and vSphere Foundation and TiBs for vSAN](https://knowledge.broadcom.com/external/article?legacyId=95927){: external}
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
