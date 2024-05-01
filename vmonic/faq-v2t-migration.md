---

copyright:

  years:  2022, 2024

lastupdated: "2024-04-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# FAQ about VMware NSX-V to NSX-T migration
{: #faq-v2t-migration}

## What happens to the networking or storage assets when I delete an Automated instance?
{: #faq-v2t-migration-existing-assets}

When you delete a {{site.data.keyword.vcf-auto}} instance, the networking (VLANs with private and public subnets) and storage ({{site.data.keyword.filestorage_full}}) assets are cancelled together with the {{site.data.keyword.cloud_notm}} bare metal Servers. If you have networking or storage assets in your migration, open a support ticket to ensure that {{site.data.keyword.cloud_notm}} decouples the VLANs and related subnets and NFS storage from the original instance. Then, these assets are not cancelled when the {{site.data.keyword.vcf-auto-short}} instance is deleted.

The following recommendations apply:

* Design your migration so that you avoid the use of assets from the existing {{site.data.keyword.vcf-auto-short}} instance, which is to be deleted.
* If you need any existing assets, note and list all assets carefully.
* Open the support ticket before you delete the instance. List all assets that you want to maintain to ensure that these assets are decoupled from the original instance. If this process is not followed, the assets cannot be recovered after deletion.

## Can I attach my existing {{site.data.keyword.filestorage_full_notm}} to the new Automated instance?
{: #faq-v2t-migration-storage}

If you are using NFS storage, you can manually attach the NFS storage to the new instance and perform a cross–vCenter vMotion without requiring a storage vMotion. You must authorize the NFS subnet from their new instance to the NFS storage.

The following recommendations apply:

* Configure static `/etc/hosts` entries on the new hosts for the storage hostnames for bootstrap purposes.
* Configure static routes on the new hosts to ensure that traffic to the NFS is driven over the NFS subnet and storage VLAN.
* After migration, open a support ticket to ensure that {{site.data.keyword.cloud_notm}} decouples the NFS storage from the original instance. Then, the storage is not cancelled when the original instance is deleted.

## Can I reuse my existing Active Directory in the new Automated instance?
{: #faq-v2t-migration-ad}

Most customers do not use the AD/DNS servers that are deployed with vCenter Server, but instead added their own domain controllers as an extra identity source to vCenter Server and NSX® Manager.

You can preserve the existing Active Directory™ (AD) controllers for ongoing use if you are aware of the following information:

* The new instance deploys new domain controllers that it must use for DNS and authenticating the IBM automation users.
* If you are using virtual machines (VMs), the domain controllers from the old instance can be migrated to the new instance. If you are using VSIs, the domain controllers from the old instance can be used by the new instance. If the new instance is deployed with a different root domain than the original instance, the domain controllers can be added as an identity source to vCenter Server and NSX Manager. So, if the old instance domain is `example.cloud.local`, the new instance can be named `example.cloud2.local`. The original AD can be configured to delegate DNS for this domain to the new AD, and users can log in using their existing `user@example.cloud.local` identities to access resource hostnames like `instance1-vc.example.cloud2.local`.
* If the original AD is deployed as a VSI, open a support ticket to ensure that IBM Support decouples the VSI from the original instance. This action ensures that the VSI is not cancelled when the original instance is deleted.
* In all cases, it is advised to back up the original controllers before you remove the original {{site.data.keyword.vcf-auto-short}} instance.

## Can I use vMotion with vSphere Encryption between the old and the new instance?
{: #faq-v2t-migration-encryption}

With VMware vSphere® encryption, it is possible to perform an advanced cross vCenter vMotion on vSphere encryption–protected VMs. You need to upgrade the source vCenter to v7.0 or later and connect both vCenters to the same Key Management System (KMS) and assign it the same name. Also, ensure that you have equivalent storage encryption policies in each vCenter Server.

## What happens to assets that were deployed manually?
{: #faq-v2t-migration-manual-custom}

If you added deployed assets to the instance manually, after initial deployment, the automation does not know about them. Therefore, you must migrate the assets to the new instance manually.

## I have VMware workloads on {{site.data.keyword.cloud_notm}} bare metal servers with vSphere 6.5 and 6.7 and the support is ending. I am not using NSX for my workloads. What do I need to do keep the environment supported, and what options do I have?
{: #faq-v2t-migration-6x-classic}

General support for vSphere® 6.x ended on 15 October 2022. For more information, see [End of general support for vSphere 6.5 and vSAN 6.5 or 6.6](https://kb.vmware.com/s/article/83223){: external} and [VMware product lifecycle matrix](https://www.vmware.com/#/){: external}.

Instances with {{site.data.keyword.cloud_notm}} bare metal servers with vSphere 6.7 cannot be ordered post 21 June 2022. {{site.data.keyword.cloud_notm}} support for ordering all update levels of vSphere 6.5 ended on 10 October 2021, and vSphere 6.5 cannot be ordered post 21 June 2022. 

{{site.data.keyword.cloud_notm}} recommends an upgrade to vSphere 7.x. If you ordered your servers from the Bare metal catalog for {{site.data.keyword.cloud_notm}} Classic Infrastructure, you have the following options.

* Check whether your server and its hardware options are compatible with vSphere 7.0. For more information, see [VMware compatibility guide](https://www.vmware.com/resources/compatibility/search.php){: external}. Alternatively, if you are running vCenter, you can upgrade your vCenter, set up vSphere Update Manager (VUM) or vSphere Lifecycle Manager, and run Hardware Compatibility Checks for the upgrade.
* Order new {{site.data.keyword.cloud_notm}} bare metal servers with vSphere 7.x from the Bare metal catalog for {{site.data.keyword.cloud_notm}} Classic Infrastructure or from the VMware Solutions console, the {{site.data.keyword.vcf-flex}} offering. Configure your vSphere host and vCenter Server and migrate the workloads. After the workloads are migrated, you can remove the VMware ESXi™ hosts from vCenter Server and decommission the old servers through the {{site.data.keyword.cloud_notm}} portal. 

## I have an old VMware vSphere instance, {{site.data.keyword.cloud_notm}} bare metal servers with vSphere 6.5 or 6.7, and the support is ending. I am not using NSX for my workloads. What do I need to do to keep the environment supported, and what options do I have?
{: #faq-v2t-migration-6x-vss}

General support for vSphere 6.x ended on 15 October 2022. For more information, see [End of general support for vSphere 6.5 and vSAN 6.5 or 6.6](https://kb.vmware.com/s/article/83223){: external} and [VMware product lifecycle matrix](https://www.vmware.com/#/){: external}.

Instances with {{site.data.keyword.cloud_notm}} bare metal servers with vSphere 6.7 cannot be ordered post 21 June 2022. {{site.data.keyword.cloud_notm}} support for ordering all update levels of VMware vSphere 6.5 ended on 10 October 2021, and VMware vSphere 6.5 cannot be ordered post 21 June 2022. 

{{site.data.keyword.cloud_notm}} recommends an upgrade to vSphere 7.x. If you ordered your servers from the VMware Solutions console, you have the following options.

* Check whether your server and its hardware options are compatible with vSphere 7.0. For more information, see [VMware compatibility guide](https://www.vmware.com/resources/compatibility/search.php){: external}. Alternatively, you can upgrade your vCenter Server, set up vSphere Update Manager (VUM) or vSphere Lifecycle Manager, and run hardware compatibility checks for the upgrade.
* Order new {{site.data.keyword.cloud_notm}} bare metal servers with vSphere 7.x from the VMware Solutions console, the {{site.data.keyword.vcf-flex}} offering. Configure your vSphere host and vCenter Server, and migrate the workloads. After the workloads are migrated, you can remove the ESXi hosts from vCenter and decommission the old servers from the {{site.data.keyword.cloud_notm}} portal. 

## I have an old vCenter Server with NSX-V instance, {{site.data.keyword.cloud_notm}} Bare Metal Servers with vSphere 6.5 or 6.7, and the support is ending. What do I need to do to keep the environment supported, and what options do I have?
{: #faq-v2t-migration-6x-vcs}

General support for vSphere 6.x ended on 15 October 2022. For more information, see [End of general support for vSphere 6.5 and vSAN 6.5 or 6.6](https://kb.vmware.com/s/article/83223){: external} and [VMware product lifecycle matrix](https://www.vmware.com/#/){: external}.

In addition, the old vCenter Server instances with vSphere 6.5 or 6.7 typically run NSX-V 6.4. NSX-V 6.4 was End of General Support on 16 January 2022 and End of Technical Guidance on 16 January 2023. VMware® by Broadcom and IBM have an exclusive agreement to support NSX-V until 15 January 2025.

{{site.data.keyword.cloud_notm}} recommends an upgrade to vSphere 7.x and NSX-T™ 3.x or later.

To migrate from NSX-V to NSX-T (also called a V2T migration), {{site.data.keyword.cloud_notm}} uses a migration approach that is called _lift-and-shift_. In the lift-and-shift approach, the {{site.data.keyword.cloud_notm}} automation is used to deploy a new {{site.data.keyword.vcf-auto-short}} instance. You need to migrate network configurations from NSX-V to NSX-T and migrate workloads between instances. {{site.data.keyword.cloud_notm}} provides extensive documentation for a validated approach and guidance for existing {{site.data.keyword.vmwaresolutions_short}} customers with {{site.data.keyword.vcf-auto-short}} instances. 

## How do I know whether my {{site.data.keyword.cloud_notm}} bare metal server hardware is suitable for in-place vSphere 7.x upgrade?
{: #faq-v2t-migration-7x-hw-support}

You can check whether your server and its hardware options are compatible with vSphere 7.x. For more information, see [VMware compatibility guide](https://www.vmware.com/resources/compatibility/search.php){: external}.

Alternatively, you can upgrade your vCenter, set up vSphere Update Manager (VUM) or vSphere Lifecycle Manager, and run Hardware Compatibility Checks for the upgrade.

## What are the different ways that I can use {{site.data.keyword.cloud_notm}} bare metal servers for VMware workloads in {{site.data.keyword.cloud_notm}}?
{: #faq-v2t-migration-vmware-platforms}

You can use a VMware® platform on {{site.data.keyword.cloud_notm}} in the following ways.

* Bare Metal - Use the Bare metal catalog for {{site.data.keyword.cloud_notm}} Classic Infrastructure and order a bare metal server with vSphere as the Operating System. For more information, see [VMware for Classic](/docs/vmware).
* {{site.data.keyword.vcf-flex-short}} - Use the VMware Solutions console to provision IBM-hosted VMware hosts. For more information, see [{{site.data.keyword.vcf-flex-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview).
* {{site.data.keyword.vcf-auto-short}} - Use the VMware Solutions console to provision an IBM-hosted private cloud based on vSphere, NSX, and optionally vSAN. For more information, see [{{site.data.keyword.vcf-auto-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview).

Upgrade and migration processes vary depending on the consumption model.
{: note}

## What is the impact if I don't upgrade vSphere 6.x on my {{site.data.keyword.cloud_notm}} bare metal hosts?
{: #faq-v2t-migration-6x-impact}

Upgrading your vSphere software is a customer responsibility and the decision to upgrade to a supported version is yours. However, your business might be at risk because VMware by Broadcom is under no obligation to provide product patches and updates, such as security updates and bug fixes. If {{site.data.keyword.cloud_notm}} provides your vSphere licenses, then IBM Support cannot assist you with vSphere issues until you upgrade.

See also [different ways to run VMware workloads in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-faq-v2t-migration#faq-v2t-migration-vmware-platforms).

## What is the impact if I don't upgrade vSphere 6.x on my old VMware vSphere hosts?
{: #faq-v2t-migration-6x-impact-vss}

Upgrading your vSphere software is a customer responsibility and the decision to upgrade to a supported version is yours. However, your business might be at risk because VMware by Broadcom is under no obligation to provide product patches and updates, such as security updates and bug fixes. If {{site.data.keyword.cloud_notm}} provides your vSphere licenses, then IBM Support cannot assist you with vSphere issues until you upgrade.

See also [different ways to run VMware workloads in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-faq-v2t-migration#faq-v2t-migration-vmware-platforms).

## What is the impact if I don't upgrade vSphere 6.x on my old instance hosts?
{: #faq-v2t-migration-6x-impact-vcs}

Upgrading your vSphere software is a customer responsibility and the decision to upgrade to a supported version is yours. However, your business might be at risk because VMware by Broadcom is under no obligation to provide product patches and updates, such as security updates and bug fixes. {{site.data.keyword.cloud_notm}} support for ordering all update levels of vSphere 6.x ended on 10 October 2021 and you can no longer order new instances with vSphere 6.x.

{{site.data.keyword.cloud_notm}} recommends upgrading to 7.x. If your old instance is running NSX-V, consider moving to {{site.data.keyword.vcf-auto-short}}. This lift and shift upgrade approach can be more beneficial due to the end of support of NSX-V. You might benefit from a target platform with updated hardware, upgraded VMware software, NSX-T, and less of an impact lift and shift migration rather than an in-place upgrade.

See also [different ways to run VMware workloads in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-faq-v2t-migration#faq-v2t-migration-vmware-platforms).

## If I'm using BYOL on my {{site.data.keyword.cloud_notm}} bare metal hosts, how does it impact the upgrade?
{: #faq-v2t-migration-6x-upgrade-impact-byol}

Upgrading vSphere software is your responsibility. However, with Bring Your Own License (BYOL) you can access VMware by Broadcom Support directly by using your license agreement. {{site.data.keyword.cloud_notm}} provides support for your bare metal servers infrastructure on {{site.data.keyword.cloud_notm}}.

For more information about upgrading, see [VMware ESXi upgrade VMware vSphere 6.7](https://docs.vmware.com/en/VMware-vSphere/6.7/com.vmware.esxi.upgrade.doc/GUID-FE668788-1F32-4CB2-845C-5547DD59EB48.html){: external} and [vSphere upgrade VMware vSphere 6.5](https://docs.vmware.com/en/VMware-vSphere/6.5/com.vmware.vsphere.upgrade.doc/GUID-FE668788-1F32-4CB2-845C-5547DD59EB48.html){: external}. As part of the upgrade planning, consider moving to {{site.data.keyword.vcf-auto-short}}, this lift-and-shift upgrade approach might be more beneficial.

See also [different ways to run VMware workloads in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-faq-v2t-migration#faq-v2t-migration-vmware-platforms).

## If I am using BYOL on my old vCenter Server hosts how does this impact the upgrade?
{: #faq-v2t-migration-6x-upgrade-impact-byol-vcs}

Upgrading vSphere software is your responsibility. However, with Bring Your Own License (BYOL) you access VMware by Broadcom Support directly by using your license agreement. {{site.data.keyword.cloud_notm}} provides support for your bare metal servers infrastructure on the {{site.data.keyword.cloud_notm}}. For more information, see [Upgrading vCenter Server vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade). If your old vCenter Server instance is running NSX-V, consider moving to {{site.data.keyword.vcf-auto-short}}. This lift and shift upgrade approach might be more beneficial due to the end of support of NSX-V.

See also [different ways to run VMware workloads in {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-faq-v2t-migration#faq-v2t-migration-vmware-platforms).

## What products are running in an Automated instance?
{: #faq-v2t-migration-what-products}

For a {{site.data.keyword.vcf-auto-short}} instance, the following information is displayed on the VMware Solutions user interface.

* VMware NSX networking solution - NSX
* NSX for vSphere - 4.1.0.2
* NSX license edition - VMware NSX Advanced

This instance is running NSX version 4.1.0.2. Due to the licensing agreement between {{site.data.keyword.cloud_notm}} and VMware by Broadcom, NSX-V licenses were being used for NSX-T instances. Newer {{site.data.keyword.vcf-auto-short}} instances use NSX-T licenses, so the instance is correctly licensed.

## Can I do an in-place vSphere upgrade for vSphere 6.7 in my old vCenter Server with NSX-T instance?
{: #faq-v2t-migration-67nsxt-upgrade}

Yes, but we strongly advise deploying a new {{site.data.keyword.vcf-auto-short}} instance and then use the lift and shift migration approach. For more information about the in place vSphere upgrade, see [Upgrading vCenter Server vSphere software from vSphere 6.5 or 6.7 to 7.0](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade) and the [important considerations](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vsphere_70_upgrade#vc_vsphere_70_upgrade-considerations).

Also, review the following key considerations:

* At the end of the documented process, your {{site.data.keyword.vcf-auto-short}} instance is running vSphere 7.0 Update 1c with N-VDS distributed switches. This configuration is different than the currently supported [Software BOM for Automated instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_bom#vc_bom-software), which is vSphere 7.0 Update 3c with Distributed vSwitch 7.0.0.
* For more information about the migration of N-VDS to VDS switches for vSphere 7.0 or later and NSX-T Data Center 3.0 and later, see [Migrate host switch to vSphere Distributed Switch](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.1/administration/GUID-1039A36F-F55E-4A0A-B6C6-2C383F4A716D.html){: external}. Currently, this procedure is not verified on a VMware Solutions vCenter Server instance.
* {{site.data.keyword.cloud_notm}} is undertaking an assessment of the N-VDS to VDS conversion and the required changes to the automation database to allow this in-place upgrade.
* Currently, Day 2 automation workflows such as add host or add cluster, are not tested against old vCenter Server instances that are upgraded from vSphere 6.7 to 7 and still using N-VDS distributed switches. Customers must assume that this automation might fail and that if this automation is required then the lift and shift migration approach used. If this automation is not needed, you can use the upgrade process that is documented.
* A workaround for the featur of adding nodes and clusters is to use the {{site.data.keyword.vcf-flex-short}} offering. For more information, see [{{site.data.keyword.vcf-flex-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereoverview). You must complete a number of manual tasks after the automated deployment.
* A workaround for add-on services is to deploy them manually using the documented reference architectures, see the Solution architectures on Classic and Solution Guides sections at [Getting started with VMware Solutions](/docs/vmwaresolutions).

## Can I reuse the portable subnets that are deployed for my old vCenter Server with NSX-V instance?
{: #faq-v2t-migration-nsx-v-instance-portable-subnets}

When you delete an old vCenter Server® instance, the networking (VLANs with private and public subnets) is cancelled together with the {{site.data.keyword.cloud_notm}} bare metal servers. If you have networking assets in your migration, open a support ticket to ensure that IBM Support decouples the VLANs and related subnets from the original instance. Then, these assets are not cancelled when the instance is deleted.

The following recommendations apply:

* Design your migration so that you avoid the use of assets from the existing vCenter Server instance, which is to be deleted.
* If you need any existing assets, note and list all assets carefully.
* Open the support ticket before you delete the instance. List all assets that you want to maintain to ensure that these assets are decoupled from the original instance. If this process is not followed, the assets cannot be recovered after deletion.

However, if you have overlapping IP addressing challenges, the note the following guidance:

* You can still continue to use your existing instance management subnet, if it has IP addresses available and you don't use any IP addresses for your own use. The new instance uses new IP addresses for vCenter Server, NSX-T managers, and Active Directory servers (if AD servers are running on the VMware VMs) from the new instance management subnet. Reusing existing management subnet is not possible for these components until you delete the existing VCS.
* In addition, the NSX-T T0 gateways are provisioned with new IP addresses from the portable private and portable public subnets for customer workload edge. NSX-T T0 gateways do not support secondary IP addresses on their uplinks.
* You can manually configure an existing subnet for the NSX-T T0 gateway uplinks, but only one subnet can be configured in T0.
* If you are using secondary IP subnets on the uplinks, you need to redesign the topology. For example, you can order [new static subnets](/docs/subnets?topic=subnets-about-subnets-and-ips#static-subnets) and route these subnets to NSX-T T0 HA VIP. These IP subnets and addresses can be used with NSX-T NAT rules, load balancing or on overlay attached VMs.

## Can I reuse existing portable subnets that are ordered outside the VMware Solutions console?
{: #faq-v2t-migration-customer-portable-subnets}

If you ordered private or public portable subnets outside the VMware Solutions console, and you use these subnets with your workloads by running on VMware clusters, you can still continue to use these IP addresses if your new instance was deployed on the same VLANs as the existing NSX-V based solution was.

If you are using these IP addresses on ESGs for NAT rules or other services, be aware that the NSX-T T0 gateways do not support secondary IP addresses on their uplinks. The NSX-T T0 gateway in the new instance is provisioned with new IP addresses from the portable private and portable public subnets for customer workload edge. You can manually configure an existing subnet for the NSX-T T0 gateway uplinks, but only one subnet can be configured in T0. If you are using secondary IP subnets on the uplinks, you need to redesign the topology. For example, you can order [new static subnets](/docs/subnets?topic=subnets-about-subnets-and-ips#static-subnets) and route these subnets to NSX-T T0 HA VIP. These IP subnets and addresses can be used with NSX-T NAT rules, load balancing, or on overlay attached VMs.

## Related links
{: #faq-v2t-migration-links}

* [General FAQ about VCF for Classic](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [Considerations about changing vCenter Server artifacts](/docs/vmwaresolutions?topic=vmwaresolutions-vcenter_chg_impact)
