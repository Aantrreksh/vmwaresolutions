---

copyright:
  years: 2019, 2023
lastupdated: "2023-09-25"

keywords: release notes, what's new in VMware Solutions, what is new, new features, VMware Solutions release notes, VMware Solutions

subcollection: vmwaresolutions

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}

# Release notes for VMware Solutions
{: #vmwaresolutions-relnotes}

Use these release notes to learn about updates to {{site.data.keyword.vmwaresolutions_full}}, including new features, component updates, usability enhancements, and bug fixes.
{: shortdesc}

## 2023
{: #year-2023}

### 24 August 2023
{: #vmwaresolutions-aug2423}
{: release-note}

VMware vSphere 8 on Cascade Lake - not supported
:   (Updated on 25 September 2023) IBM does not support VMware vSphere® 8.x on Intel® Cascade Lake hardware due to RAID Controller incompatibility and because IBM licenses for vSphere 8.x, VMware vCenter Server® 8.x, and VMware vSAN™ 8.x are not available currently.

   Do not upgrade to vSphere 8.x on Cascade Lake servers. If you upgrade to vSphere 8.x, your environment configuration becomes unsupported by IBM and VMware.
   {: important}

Veeam 12 for VMware Shared
:   Veeam® Backup and Replication 12 (Veeam 12) is now available for deployment with the VMware Shared offering.

VMware NSX 4.1.0.2
:   Newly deployed VMware vCenter Server® and VMware vSphere® instances are provisioned with VMware NSX® 4.1.0.2.

vCenter Server and VMware vSphere BOM updates
:   The following updates are applied to newly deployed instances, clusters, and hosts:

   * VMware vCenter Server Appliance 7.0 Update 3m (build 21784236)
   * VMware vSphere ESXi 7.0 Update 3n (build 21930508)

Mirrored M.2 drives
:   For vCenter Server with vSAN storage and for VMware vSphere instances with vSAN disks, mirrored M.2 drives are provisioned with your order when you add new vSAN clusters or when you add new ESXi servers to existing vSAN clusters and select a new bare metal server configuration.

Entrust CloudControl - deprecated
:   New installations of Entrust CloudControl™ are no longer supported for new or existing deployments of vCenter Server instances. You can still use or delete existing Entrust CloudControl installations on your existing instances.
{: deprecated}

FortiGate® Virtual Appliance v7.4
:   The FortiGate® Virtual Appliance v7.4 add-on service is available for deployment.

Name change for PrimaryIO
:   The PrimaryIO add-on service name is changed to PrimaryIO Migrations and its [About](https://cloud.ibm.com/infrastructure/vmware-solutions/console/newserviceentry/PIO/vcs) page is updated with the most recent feature information.

User interface updates and enhancements
:   The user interface is updated with various messages and tooltips, and provides the following enhancements:

   * For VMware vSphere, the term **cluster** is updated to **instance** throughout the UI, user documentation, and REST APIs.
   * For VMware vSphere instances, the **Instance configuration name** field is changed to a side panel. You can manage your configuration templates from a list of saved configurations in the side panel.

New and updated documentation

   * The [VMware Shared metrics](/docs/vmwaresolutions?topic=vmwaresolutions-shared-monitor#shared-monitor-metrics) are updated with metadata details.
   * New documentation is available to assist with [expanding ordered endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_expand_storage) after ordering the Veeam add-on service.

### 5 July 2023
{: #vmwaresolutions-jul0523}
{: release-note}

VMware vSphere Day 2 support
:   You can view or delete VMware vSphere instances from the VMware Solutions console. You can also add or delete VMware ESXi™ servers, and add or delete licenses for vSphere instances from the VMware Solutions console.

VMware Regulated Workloads multizone instances - deprecated
:   New deployments of VMware Regulated Workloads multizone instances are no longer supported. You can still add or delete clusters, add or remove ESXi servers or NFS storage, and add or remove services for existing multizone instances.
{: deprecated}

Updates to VMware vCenter Server and VMware vSphere instances
:   The following upgrades are applied to newly deployed instances, clusters, and hosts:

   * VMware vCenter Server Appliance 7.0 Update 3l (build 21477706)
   * VMware vSAN Witness 7.0 Update 3l (build 21424296)

Add-on services upgrades
:   The following service versions are now available for deployment:

   * Caveonix RiskForesight™ v4.1
   * FortiGate Virtual Appliance v7.2.5
   * F5® BIG-IP® v17.1
   * Juniper® vSRX v3.0 (23.1R1)
   * Red Hat® OpenShift® v4.12
   * VMware Aria® Operations™ and VMware Aria Operations™ for Logs v8.12
   * Zerto v9.7u3

Name change for VMware vRealize products
:   VMware changed the vRealize® Suite Lifecycle Manager product name to VMware Aria® Suite Lifecycle. All vRealize products that are managed by vRealize Suite Lifecycle Manager are now referred as VMware Aria. The names are updated throughout the {{site.data.keyword.vmwaresolutions_short}} documentation. The following products are rebranded:

   * vRealize Operations and Log Insight is renamed to VMware Aria Operations and VMware Aria Operations for Logs.
   * vRealize Automation is renamed to VMware Aria® Automation™.
   * vRealize Operations (vROps) is renamed to VMware Aria Operations.
   * vRealize Log Insight™ (vRLI) is renamed to VMware Aria Operations for Logs.
   * vRealize Network Insight (vRNI) is renamed to VMware Aria Operations™ for Networks.

REST API
:   The following updates are available:

   * The [VMware Solutions API](/apidocs/vmware-solutions) provides support for viewing and deleting VMware vSphere instances. You can also add or delete ESXi servers, and add or delete licenses for vSphere instances.
   * Also for the VMware Solutions API, you can specify either `quantity` or `host_names` for the number of new hosts to be added in the `hosts_order_data` object.

User interface updates and enhancements
:   The UI (user interface) is updated with various messages and tooltips, and provides the following enhancements:

   * For vCenter Server, Cyber Recovery, and Regulated Workloads instances, the **Instance configuration name** field is changed to a side panel. You can manage your configuration templates from a list of saved configurations in the side panel.
   * The checkbox **Select a different cluster location** is changed to a switch, for consistency with other similar UI options.
   * The **SAP-certified** Cascade Lake selections (**NetWeaver** and **HANA**) are merged into a single option for a more streamlined user experience when you choose the **CPU model** for your servers.
   * The process to [set up your environment for your first order](/docs/vmwaresolutions?topic=vmwaresolutions-completing_checklist#completing_checklist-procedure) is simplified on the UI.

### 3 May 2023
{: #vmwaresolutions-may0323}
{: release-note}

Madrid data centers available
:   (Updated on 22 June 2023) The {{site.data.keyword.cloud_notm}} data centers **Madrid 02**, **Madrid 04**, and **Madrid 05** are now available for deployment.

Bring Your Own License (BYOL) no longer available
:   BYOL is now disabled in the **Licensing** section for VMware vCenter Server® instances, VMware vSphere clusters, adding hosts and clusters, and vRealize Operations and Log Insight service.

VMware NSX-T 4.0.1.1 manual upgrade
:   VMware NSX-T™ version 4.0.1.1 is now available if you want to upgrade your existing NSX-T instances manually. All newly deployed VMware NSX-T instances are still provisioned with NSX-T version 3.2.0.1.

Updates to VMware vCenter Server instances and VMware vSphere clusters
:   The following upgrades are applied to newly deployed instances, clusters, and hosts.
   * VMware vCenter Server Appliance 7.0 Update 3k (build 21290409)
   * VMware vSAN Witness 7.0 Update 3c (build 19193900)

Veeam 12 availability
:   Veeam Backup and Replication 12 (Veeam 12) is now available for deployment with VMware vCenter Server, Cyber Recovery, and VMware Regulated Workloads offerings. Veeam 12 allows you to write directly to {{site.data.keyword.cloud}} Object Storage and it provides other features, such as data protection, improved Recovery Point Objective using Continuous Data Protection for disaster recovery purposes, and general operational efficiency. For more information, see the [Veeam Backup and Replication 12 release notes](https://www.veeam.com/veeam_backup_12_release_notes_rn.pdf){: external}.

New and updated documentation
:   The table of contents is updated for topic rearrangement and removal of outdated content.

User interface updates and enhancements
:   The user interface is updated with various messages and tooltips, and provides the following enhancements.

   * The term **edge gateway cluster** is updated to **gateway cluster** throughout the UI, user documentation, and REST APIs.
   * You can check the prices for VMware Solutions offerings without having to sign in to {{site.data.keyword.cloud_notm}}. However, you might have limited access to some sections of the ordering pages. To place an order, or for a complete access to the ordering pages, you must log in to {{site.data.keyword.cloud_notm}}.
   * The page titles and labels for adding clusters, storage, and services are updated for consistency throughout the user interface.
   * The status of instances and clusters when they are ready to use is updated to **Available**.
   * The UI controls for the separate workload cluster, gateway cluster, and file shares are changed to switches instead of checkboxes.
   * Guidance is provided on the UI for the workload and gateway cluster configuration.
   * A side panel is displayed when you add hosts to vCenter Server, Cyber Recovery, and VMware Regulated Workloads instances.

### 8 March 2023
{: #vmwaresolutions-mar0823}
{: release-note}

VMware Cloud Director upgrade for VMware Shared
:   VMware Solutions 5.2 provides an upgrade to the VMware Shared infrastructure to an updated version of VMware Cloud Director v10.4.1. This release resolves various issues, includes several deprecations, and introduces new features, such as API tokens and edge static routes. For more information, see [VMware Cloud Director 10.4.1 release notes](https://docs.vmware.com/en/VMware-Cloud-Director/10.4.1/rn/vmware-cloud-director-1041-release-notes/index.html){: external}.

End of Marketing for IBM Cloud Secure Virtualization
:   The IBM Cloud Secure Virtualization offering is no longer available for new deployments. Support for existing customers who are using the offering is still provided.
{: deprecated}

Updates to VMware vCenter Server instances and VMware vSphere clusters
:   The following upgrades are applied to newly deployed instances, clusters, and hosts.
   * VMware vCenter Server Appliance 7.0 Update 3j (build 20990077)
   * VMware vSphere ESXi™ 7.0 Update 3k (build 21313628)

Add-on services upgrades
:   The following service versions are now available for deployment:
   * Entrust CloudControl™ v6.6
   * F5® BIG-IP® v17.0
   * vRealize Operations and vRealize Log Insight v8.10
   * Zerto v9.7u1

F5 BIG-IP migration from NSX-V to NSX-T
:   To migrate the F5 BIG-IP service from VMware NSX-V to VMware NSX-T, open an IBM Support ticket by following the steps in Getting help and support.

New and updated documentation
:   Documentation is available to assist with your custom cyber-recovery requirements. For more information, see Cyber Recovery with Bring Your Own appliances.

REST API updates
:   The [VMware Solutions API](/apidocs/vmware-solutions) provides support for getting and canceling billing item IDs for VMware vSphere clusters, deleting hosts from vSphere clusters, and deleting vSphere clusters.

User interface updates and enhancements
:   The user interface is updated with various messages and tooltips, and provides the following enhancements.

   * BYOL notification in the **Licensing** section for VMware vCenter Server instances, VMware vSphere clusters, add hosts and clusters, vRealize Operations and Log Insight, and VMware HCX™ services. Bring Your Own License (BYOL) is no longer supported, except for migrations or upgrades of existing BYOL clusters.
   * The term **edge services cluster** is updated to **edge gateway cluster** throughout the UI, user documentation, and REST APIs.
   * A side panel is now displayed when NFS storage is added to VMware vCenter Server, VMware NSX®, Cyber Recovery, and VMware Regulated Workloads instances.


### 10 January 2023
{: #vmwaresolutions-jan1023}
{: release-note}

VMware Cloud Director upgrade for VMware Shared
:   VMware Solutions 5.1 provides an upgrade to the VMware Shared infrastructure to an updated version of VMware Cloud Director v10.4, which supports up to virtual hardware version 19. For more information about fixed issues, new features, and known issues in the upgraded release, see [VMware Cloud Director 10.4 Release Notes](https://docs.vmware.com/en/VMware-Cloud-Director/10.4/rn/vmware-cloud-director-104-release-notes/index.html){: external}. If you use the VMware Cloud Director API, consider the following updated product support notices:
   * VMware Cloud Director API versions 31.0 and 32.0 are not supported.
   * VMware Cloud Director API versions 33.0, 34.0, 35.0, and 35.2 are deprecated and are not supported starting with the next major release of VMware Cloud Director.

Name change for vRealize Operations Tenant App for VMware Cloud Director
:   VMware changed the vRealize Operations Tenant App for VMware Cloud Director product name to VMware Chargeback. The name is updated throughout the VMware Shared documentation.

Bring Your Own License (BYOL) no longer supported
:   IBM Cloud previously allowed you to bring your own license (BYOL) when you move your existing on-premises VMware workloads to IBM Cloud. BYOL is no longer allowed by VMware. You can no longer bring your own licenses for any new hosts. This restriction applies to all VMware products that are available from IBM Cloud. For existing BYOL servers, you can still upgrade and migrate to refresh software and hardware.

SAP-certified servers updates
:   SAP HANA certified bare metal servers now offer only fixed configurations with defined RAM sizes. Also, new SAP HANA and SAP NetWeaver models are available for deployment with VMware vSphere 7.0u3. These models are available for VMware vCenter Server and Cyber Recovery instances and clusters, and for VMware vSphere clusters. For more information, see SAP-certified.

NetBIOS domain name
:   The first qualifier of the root domain name is now the NetBIOS name by default. It is part of the network diagram when your order vCenter Server and Cyber Recovery instances.

Add-on services upgrades
:   The following service versions are now available to install on deployed instances.
   * FortiGate Virtual Appliance 7.2.2
   * Juniper vSRX v21.4 (R2)

Veeam migration from NSX-V to NSX-T
:   To migrate the Veeam service from VMware NSX-V to VMware NSX-T, open an IBM Support ticket.

REST API
:   For VMware Shared, the V1 API support ended on 31 December 2022. Use the [V2 API](/apidocs/vmware-solutions-shared/vmware-solutions-shared-v2.0.0).

User interface updates and enhancements
:   The left navigation menu in the instance detail page is now changed to tabs. Also, a new tab **Access information** is added, where you can see information such as AD/DNS IP and remote desktop credentials for your instance.

## 2022
{: #year-2022}

### 31 October 2022
{: #vmwaresolutions-oct3122}
{: release-note}

Cyber Recovery
:   The V5.0 release offers a new Cyber Recovery instance. The instance can help you protect your systems and data from cyberthreats and attacks. It can assist you with handling ransomware and help you with other problems and threats.

   The Cyber Recovery instance includes Veeam Backup and Replication 12, a Linux® hardened repository (LHR), and an edge gateway. For more information, see Cyber Recovery overview.

Private network endpoint enhancements
:   You can now edit the private network endpoints allowlisted IP addresses and subnets for your VMware Solutions Shared instance. For more information, see Modifying a private network endpoint for a virtual data center.

Veeam self-service portal for VMware Shared
:   The Veeam self-service portal is now automatically enabled for existing and new VMware Cloud Director organizations. For more information, see Managing Veeam for VMware Shared.

MEX01 data center no longer available
:   (Updated on 14 November 2022) The **Mexico 01** {{site.data.keyword.cloud_notm}} data center is closing on 31 January 2023. This data center is no longer available for deployments.

VMware vSphere 7.0u2 - deprecated
:   (Updated on 14 November 2022) The vSphere 7.0u2 option is no longer available for adding hosts to vCenter Server instances and scaling existing vSphere clusters. For existing instances with vSphere 7.0u2, you can add only ESXi servers with vSphere 7.0u3.
{: deprecated}

Dark mode temporarily unavailable
:   Starting with 14 November 2022, the UI **Dark** mode is temporarily unavailable. Until it becomes enabled again, use **Light** mode.

Hostname prefix updates
:   You can now customize the hostnames prefix individually when you order VMware vCenter Server instances, order new VMware vSphere clusters, and add hosts and clusters to existing instances.

Updates to VMware vCenter Server instances and VMware vSphere clusters
:   The following upgrades are applied to newly deployed instances, clusters, and hosts.
   * VMware vSphere ESXi 7.0 Update 3f (build 20036589)
   * VMware vSphere ESXi 6.7 P08 (build 19997733)

Considerations for selecting a new NSX Data Center SP edition
:   Beginning with the V5.0 release, if you have a BYOL for VMware NSX-T that is not a Data Center SP license, you can now order NSX Data Center SP licenses to replace your licenses. You are responsible to select the appropriate NSX Data Center SP license edition based on your needs.

   Also, beginning with this release, if you have a BYOL Data Center SP edition license, you can start renting NSX Data Center SP edition licenses from IBM. If you already rent an NSX Data Center SP edition license from IBM, you can upgrade and downgrade. If you have VMware HCX and an NSX Data Center Enterprise Plus license, you cannot downgrade your license. If you uninstall HCX, you can then downgrade your license.

Add-on services upgrades
:   The following service versions are now available to install on deployed instances.
   * Caveonix RiskForesight v4.0
   * FortiGate Virtual Appliance v7.2.1
   * Red Hat OpenShift v4.11
   * vRealize Log Insight v8.8
   * Zerto v9.5u3

KMIP support for Key Protect key rings
:   KMIP™ for VMware supports Key Protect key rings. For more information, see Ordering KMIP for VMware instances.

Ordering Veeam stand-alone licenses
:   Starting with this release, if you order Veeam stand-alone licenses, the ordering process automatically starts. You get an email confirming what you ordered. A license key is generated for you. When the key is ready, it is emailed to you. For more information, see Ordering Veeam stand-alone licenses.

   There is no limit to the number of licenses that you can order.

REST API
:   The following updates are available:

   * For VMware Shared, the support date for the [V1 API](/apidocs/vmware-solutions-shared/vmware-solutions-shared-v1.0.0) is being extended until 31 December 2022. To ensure smooth transition in the future, start using the [V2 API](/apidocs/vmware-solutions-shared/vmware-solutions-shared-v2.0.0).
   * For [VMware Solutions API](/apidocs/vmware-solutions), support is provided for Caveonix RiskForesight, Veeam, Zerto, and VMware HCX stand-alone licenses. Also, support for the 2U chassis types is added by using the new `large_chassis_only` parameter.

User interface enhancements
:   The left navigation pane on the VMware Solutions console now groups items as **Resources** and **Licenses** so that they are more aligned with the resource types and names.

### 29 August 2022
{: #vmwaresolutions-aug2922}
{: release-note}

**HKG02** and **SEO01** data centers no longer available
:   (Updated on 20 September 2022) The **Hong Kong 02** and **Seoul 01** {{site.data.keyword.cloud_notm}} data centers are no longer available for deployment.

Price calculation updates for {{site.data.keyword.vmwaresolutions_short}} Shared
:   Price calculations are now automatically generated when you access the order pages for {{site.data.keyword.vmwaresolutions_short}} Shared offerings. For more information about the specific default selections, see Requirements and planning for VMware Solutions Shared.

vRealize Operations Tenant App for VMware Cloud Director availability
:   You can now access the vRealize Operations Tenant App for a VMware Cloud Director for new and existing organizations through the VMware Cloud Director tenant portal. For more information, see Enabling VMware Chargeback.

Standard - Catalog storage policy availability
:   The Standard - Catalog storage policy is now available for storing vApp templates and media files in your VMware Cloud Director catalog. For more information, see VMware Solutions Shared overview.

Private network endpoints for multizone virtual data centers
:   Two private network endpoints are ordered to correspond with each VMware NSX Edge™ Service Gateway when you create a private network endpoint for VMware Solutions Shared multizone virtual data centers.

vCPU and RAM limits for on-demand and reserved virtual data centers
:   The vCPU and RAM limits for VMware Solutions Shared virtual data center orders are now increased. Beginning with the 4.9 release, the maximum vCPU limit is 1 - 2000 and the maximum RAM limit is 1 - 40 TBs for both on-demand and reserved virtual data center orders.

Updates to VMware vCenter Server instances and VMware vSphere clusters
:   The following upgrades are applied to newly deployed instances, clusters, and hosts.
   * VMware vSphere ESXi 7.0 Update 3e (build 19898904)
   * VMware vSphere ESXi 6.7 P07 (build 19898906)

Considerations for selecting a new NSX Data Center SP edition
:   Beginning with the V4.9 release, if your NSX-V instance is using BYOL licenses, you can now order legacy NSX licenses from IBM to replace your own license.

   Also, beginning with this release, if your NSX-T instance is using legacy NSX licenses, you can now order NSX Data Center SP licenses to replace your legacy NSX licenses. You are responsible to select the appropriate NSX Data Center SP license edition based on your needs.

Zerto 9.5u1 support
:   Zerto 9.5u1 is available to install on deployed instances.

   Zerto v9.5u1 is not supported for vSphere 6.5 and 6.7. However, you can order stand-alone licenses for existing vSphere 6.x instances.
   {: note}

HCX Appliance activation with BYOL NSX Data Center Enterprise Plus license
:   If you have a BYOL NSX Data Center Enterprise Plus license and you install VMware HCX, your NSX Data Center Enterprise Plus license key is now used to activate the HCX appliance. For more information, see BYOL HCX Enterprise edition and NSX Data Center Enterprise Plus.

Linux hardened repository for Veeam
:   When you order Veeam, you can order a Linux hardened repository for immutable storage. For more information, see Linux hardened repository for immutable storage.

New and updated documentation
:   The following documentation updates are available.
   * VMware Cloud Foundation on VPC, a new architecture reference for a complete set of software-defined services for compute, storage, network security, Kubernetes management, and cloud management.
   * Deleting vSphere clusters, a new topic about deleting VMware vSphere clusters by managing your resources and canceling hosts and licenses on your own.

REST API updates
:   The [VMware Solutions API](/apidocs/vmware-solutions) provides support for scaling existing VMware vSphere clusters.

User interface updates and enhancements
:   The user interface is updated with various error messages and tooltip enhancements and provides the following enhancements.

   * A vertical progress indicator bar is now available on the ordering page for VMware Solutions Shared offerings. The progress indicator maps to each section and helps to quickly browse to different areas of the page.
   * If you are running VMware NSX-V or a vSphere 6 version on the instances in your environment, you now receive notifications to update your environment to the most recent supported version of NSX or vSphere. You can go to the instance summary page to check the NSX solution type and the vSphere version that is most suitable for your environment.

### 22 June 2022
{: #vmwaresolutions-jun2222}
{: release-note}

VMware vRealize Operations Tenant App V8.6 for VMware Shared
:   The 4.8 release enables a new optional feature for the {{site.data.keyword.vmwaresolutions_short}} tenant portal. VMware vRealize Operations Tenant App V8.6 provides metering capabilities for tenants to monitor their virtual data centers, virtual applications, and virtual machines.

{{site.data.keyword.cloud_notm}} Identity and Access Management enablement for VMware Solutions Shared
:   {{site.data.keyword.cloud_notm}} Identity and Access Management (IAM) is now enabled by default for new sites. You can optionally enable IAM for existing sites. After you integrate your site with IAM, you can use single sign-on to log in to the VMware Cloud Director console from the VMware Solutions console.

   With the IAM integration, role-based access control now uses a site and organization IAM policy for VMware Solutions Shared resources.

{{site.data.keyword.cloud_notm}} data center region and site availability for VMware Solutions Shared
:   You can now select the region where your virtual data center instance is hosted and the {{site.data.keyword.cloud_notm}} data center site where the virtual data center is hosted.

Platform management roles
:   New IAM platform management roles are available for VMware Solutions offerings.

End of Marketing for NSX-V instance deployments
:   VMware® support for all new VMware NSX-V deployments ended on 16 January 2022. However, VMware and IBM® worked closely to extend the existing NSX–V support until 31 December 2023. Beginning on 21 June 2022, you can no longer order new VMware vCenter Server with NSX-V instances.

End of Marketing for vSphere 6.7 instance deployments
:   VMware support for all new VMware vSphere 6.7 deployments ends on 15 October 2022.

VMware vSphere 7.0 Update 3d support
:   vSphere 7.0 Update 3d is available for newly deployed instances. For existing vSphere 7.0u2 instances and clusters, you can add either a vSphere 7.0u2 or a vSphere 7.0u3 host or cluster.

Updates to VMware vCenter Server instances
:   The following upgrades are applied to newly deployed instances, clusters, and hosts.
   * VMware vSphere ESXi 7.0 Update 3d (build 19482537)
   * VMware vCenter Server Appliance 7.0 Update 3d (build 19480866)

Updates to VMware vSphere cluster names
:   The requirements for vSphere cluster names are changed.

VMware ESXi firewall configuration for NFS - issue fixed {: #june-2022-esxi-firewall}
:   {{site.data.keyword.cloud_notm}} identified a problem with the VMware ESXi firewall configuration for NFS feature, which might cause some firewall rules to be lost during the update. This problem is now fixed.

Price calculation updates
:   Price calculations are now automatically generated when you access the order pages for {{site.data.keyword.vmwaresolutions_short}} Dedicated and VMware Regulated Workloads offerings. For more information about the specific default selections, see the requirement information for each offering order.

Cyber recovery with Veeam solution
:   This solution aims for VMware and IBM to accelerate and ensure the development, testing, and implementation of a secure cyber-recovery cloud solution that enables recovery against advanced cyberthreats like ransomware. Copies of critical data are protected with a multi-purpose cyber-recovery cloud solution: a copy target for cloud-native application data for existing cloud or on-premises systems. As an extra {{site.data.keyword.cloud_notm}} option, you can add cyber-recovery sites to isolate copies of critical customer data and to validate data integrity while you also enable recovery from cyberattacks.

Security and Compliance Readiness Bundle - deprecated
:   New deployments of Security and Compliance Readiness Bundle instances are no longer supported. You can still add or delete clusters, add or remove VMware ESXi servers or NFS storage, and add or remove services for existing instances. You can also view and delete your Security and Compliance Readiness Bundle instances.
{: deprecated}

Add-on services upgrades
:   The following service versions are now available to install on deployed instances.
   * Entrust CloudControl v6.5 (formerly known as HyTrust® CloudControl)
   * FortiGate Virtual Appliance v7.0.5
   * Red Hat OpenShift v4.10
   * Zerto v9.0u4

Entrust DataControl - deprecated
:   New installations of Entrust DataControl® are no longer supported for new or existing deployments of vCenter Server instances. You can still use or delete existing Entrust DataControl installations on your existing instances.
{: deprecated}

New and updated documentation
:   The following documentation updates are available.
   * Upgrading VMware vSphere software from vSphere 6.5 or 6.7 to 7.0 with the supported upgrade paths.
   * Managing IAM access for VMware Solutions.

REST API updates
:   New REST APIs are available.

   * (Updated on 31 October 2022) For VMware Shared, a new [V2 API](/apidocs/vmware-solutions-shared/vmware-solutions-shared-v2.0.0) is introduced, which includes the new `site` object. The [V1 API](/apidocs/vmware-solutions-shared/vmware-solutions-shared-v1.0.0) is being deprecated and will be supported until 31 December 2022. To ensure smooth transition in the future, start using the V2 APIs.
   * For the [VMware Solutions API](/apidocs/vmware-solutions), support is provided for VMware vSphere cluster new deployments and for the KMIP for VMware stand-alone service.

User interface updates and enhancements
:   Various error messages and tooltip enhancements are available to assist you in selecting the appropriate setting on the user interface.

   * You can now view site and virtual data center details from the **Resources** page for VMware Shared.
   * The following enhancements are made to the ordering page for {{site.data.keyword.vmwaresolutions_short}} offerings.
      * A vertical progress indicator bar is now available that maps each section on the ordering page and helps to quickly browse to different areas of the page. You can directly jump onto any specific section of the page by clicking the heading in the progress bar. When you scroll through the page, the progress bar also keeps a check on whether the data is entered or not.
      * The CPU model selection tile group is now changed to a list of items in a table. You can select the CPU model of your choice from the table.

### 25 April 2022
{: #vmwaresolutions-apr2522}
{: release-note}

VMware Cloud Director upgrade for VMware Solutions Shared
:   (Updated on 8 May 2022) VMware Solutions provides an upgrade to the VMware Shared infrastructure to VMware Cloud Director (vCD) v10.3.3.

Compute policy support for VMware Solutions Shared virtual data centers
:   You can now choose to enable a compute policy for a VMware Solutions Shared virtual data center. This feature provides a convenient option to choose a compute policy for your virtual machine (VM) from the list of policies that are available for that virtual data center.

vSAN support for VMware Solutions Shared virtual data centers
:   vSAN™ support is now available for Dallas 10 and Dallas 12 VMware Solutions Shared virtual data centers.

VMware vCenter Server instances
:   The 4.7 release applies the following upgrades and improvements for newly deployed instances, clusters, and hosts.
   * VMware vSphere ESXi 7.0 Update 2e (build 19290878)
   * VMware vSphere ESXi 6.7 P06 (build 18828794)
   * VMware vCenter Server Appliance 6.7.0 Update 3q (build 19300125)
   * VMware NSX-T 3.2.0.1.0 (build 19232400)
   * VMware NSX-V 6.4.13 (build 19307994)

VMware ESXi firewall configuration for NFS {: #april-2022-esxi-firewall}
:   (Updated on 7 June 2022) {{site.data.keyword.cloud}} identified a problem with the following feature, which might cause some firewall rules to be lost during the update. This problem is now fixed.

   VMware ESXi attempts to manage the outbound firewall for NFS traffic for you automatically. Under some circumstances, VMware ESXi might not discover all IP addresses for an NFS data store, sometimes resulting in loss of connectivity if the {{site.data.keyword.cloud_notm}} Endurance servers are undergoing maintenance. VMware Solutions corrects the ESXi firewall configuration whenever adding hosts, clusters, or storage to your vCenter Server instance. For more information about ESXi firewall rules, see [NFS client firewall behavior](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.storage.doc/GUID-70686ADB-961A-46BD-B814-48DCF6C5E34B.html){: external}.

Loss of connectivity to NFS storage {: #april-2022-connect-lost}
:   (Updated on 7 June 2022) See Why did my host lose connection to my NFS datastore?

Edge services cluster updates
:   You can now add more than one edge services cluster in the same data center pod.

Price calculation updates
:   Price calculations are now automatically generated when you access the VMware vCenter Server instance order page. Default selections include the Data Center SP Professional license for NSX-T, the Advanced license for NSX-V, the Dual Intel® Xeon® Platinum 8260 processor / 48 cores, 2.4 GHz CPU model, and 768 GB RAM.

VMware Subscription Purchasing Program credits - deprecated
:   Credits for the VMware Subscription Purchasing Program (SPP) are no longer available.
{: deprecated}

Add-on services upgrades
:   The following service versions are now available to install on deployed instances.

   * FortiGate Virtual Appliance v7.0.4
   * Entrust DataControl® v5.5 (formerly known as HyTrust® DataControl)
   * Red Hat OpenShift v4.9.27
   * Zerto v9.0u3

Dizzion
:   Dizzion is now available as a featured service from the VMware Solutions console.

Name change for HyTrust add-on services
:   The company Entrust acquired the HyTrust company. The names of the following services are updated.

   * Entrust CloudControl™
   * Entrust DataControl
   * Entrust KeyControl™, which is deprecated

Veeam VSI, Veeam bare metal, and Zerto configuration changes
:   Beginning with the 4.7 release, the Veeam VSI, Veeam bare metal, and Zerto services are not configured with an {{site.data.keyword.cloud_notm}} Infrastructure portable IP address or with a NAT connection to the public network, even if you have public interfaces in your instance. This update helps to avoid the possibility of asymmetric routing when using a network gateway appliance.

New architecture documentation
:   The following technical documents are now available or updated:
   * VMware Solutions architecture patterns
   * VMware NSX-V to NSX-T migration

User interface updates and enhancements
:   The VMware Solutions documentation now has a [landing page](/docs/vmwaresolutions) where you can get oriented with the content available for the offering.

### 21 February 2022
{: #vmwaresolutions-feb2122}
{: release-note}

VMware Cloud Director upgrade for VMware Solutions Shared
:   (Updated on 15 March 2022) VMware Solutions provides an upgrade to the VMware Shared infrastructure to VMware Cloud Director (vCD) v10.3.2.

VMware vCenter Server instances
:   The 4.6 release applies the following upgrades and improvements for newly deployed instances, clusters, and hosts.
   * VMware vCenter Server Appliance 7.0 Update 3c (build 19234570)
   * VMware NSX-T 3.1.3.5.0 (build 19068434)
   * VMware NSX-V 6.4.12 (build 19066632)
   * VMware vSAN 7.0 Update 2c (build 18426014)

VMware vSAN 7.68 TB SSD disk support for 10 Gb uplink speed
:   For the VMware vSAN component, the 7.68 TB SSD disk type is now supported for VMware vSphere 7.0 or 6.7 instances with 10 Gb uplink speed.

Non-SED disk availability for vSAN storage {: #february-2022-non-sed}
:   For Cascade Lake servers, non-SED vSAN storage disks now replace the option for SSD SED disks for newly deployed instances and when you add hosts and clusters to existing instances. If your initial cluster has vSAN storage, SSD SED disks are no longer available. Non-SED storage disks are ordered.

   SSD SED disks are supported for Skylake servers.
   {: note}

Add-on services upgrades
:   The following service versions are now available to install on deployed instances.

   * FortiGate Virtual Appliance v7.0.3
   * vRealize Log Insight v8.6
   * Zerto v9.0u2

IBM Spectrum Protect Plus - deprecated
:   New installations of the IBM Spectrum® Protect Plus service are no longer supported for new or existing deployments of vCenter Server instances. You can still use or delete existing IBM Spectrum Protect Plus installations on your existing instances. If you want to install IBM Spectrum Protect Plus yourself, see [IBM Spectrum Protect Plus documentation](https://www.ibm.com/docs/en/spp){: external}.
{: deprecated}

REST API updates
:   The following API updates are available:
   * The /v2/supported_config_options REST API displays a list of supported configuration versions.
   * The /v2/disk_types REST API is updated to show that SED disks are only for Skylake servers.
   * A number of REST APIs, such as `/v1/vcenters/nsxt` include the parameters `disks` and `vsan_cache_disks`. For these APIs and for Cascade Lake servers only, do not specify SED disks types.

New architecture documentation
:   The following technical documents are now available:
   * VMware RYO architecture on VPC
   * Interconnectivity for VMware workloads on VPC
   * Fortinet FortiGate solution architecture

User interface updates and enhancements
:   Various error messages and tooltip enhancements are available to assist you in selecting the appropriate setting on the user interface.

## 2021
{: #year-2021}

### 13 December 2021
{: #vmwaresolutions-dec1321}
{: release-note}

NSX-T Data Center SP license availability
:   VMware NSX-T Data Center SP license editions are available for new instances for the following VMware Solutions offerings. Existing instances continue to use the previous NSX licenses for all new clusters and hosts.
   * VMware Solutions Dedicated instances offer Data Center SP Base, Data Center SP Professional, Data Center SP Advanced, or Data Center SP Enterprise Plus.
   * Security and Compliance Readiness Bundle instances offer Data Center SP Professional, Data Center SP Advanced, or Data Center SP Enterprise Plus.
   * VMware Regulated Workloads offer Data Center SP Advanced or Data Center SP Enterprise Plus.

:   NSX-T Data Center SP license restrictions
   * License upgrade is not available for NSX-T Data Center SP license edition.
   * Automated deployment of the VMware HCX service is not supported for VMware vCenter Server instances with the NSX-T Data Center SP Enterprise Plus license edition. However, you can manually deploy HCX outside of the VMware Solutions console. For more information, see [HCX Connector and HCX Cloud installations](https://docs.vmware.com/en/VMware-HCX/4.2/hcx-getting-started/GUID-B1023D31-0458-433B-9ABB-62E8BDD3FEC2.html){: external}.

{{site.data.keyword.cloud_notm}} data center pod availability
:   You can now select the data center pod for your resource deployment. By using this feature, you can deploy new resources to the same pod where you have existing resources.

Support for Dual Intel Xeon Gold 6250 Cascade Lake servers
:   Dual Intel® Xeon® Gold 6250 / 16 cores, 3.9 GHz bare metal servers are available for deployment for vCenter Server instances and VMware vSphere clusters with VMware vSphere 7, and for VMware Regulated Workloads and Security and Compliance Bundle instances.

Multizone support for VMware Solutions Shared
:   VMware Solutions Shared now offers multizone VMware virtual data centers. Multizone is offered for new on-demand and reserved virtual data centers and includes support for Dallas 10 and Dallas 12 {{site.data.keyword.cloud_notm}} data centers.

Add-on services upgrades
:   The following service versions are now available to install on deployed instances.
   * Caveonix RiskForesight v3.1.0
   * Entrust DataControl v5.4
   * IBM Spectrum Protect Plus v10.1.8
   * Red Hat OpenShift v4.7.34
   * vRealize Operations v8.6

About pages for add-on services
:   You can now access overview information about a service from the first page of the VMware Solutions console. From each overview, you can install the service on a new or existing instance.

New endpoints for KMIP for VMware
:   Two new endpoints are now available in the Sao Paulo location for the KMIP for VMware service.

Zerto support for NSX-T
:   Zerto is now supported on vCenter Server instances with vSphere 7 and NSX-T 3.1. Zerto is still supported on vCenter Server instances with NSX-V.

:   Zerto is not supported for instances that are upgraded from vSphere 6.7 to vSphere 7.

New REST API support
:   Added support for the following features:
   * Zerto for vSphere 7 with NSX-T instances and for NSX-V instances
   * Ordering new NSX-T instances with NSX-T Data Center SP licenses
   * Selecting the data center pod location for resource deployment

New release notes format
:   The release notes have been consolidated to one location for you to review the latest and previous offering updates.

### 13 October 2021
{: #vmwaresolutions-oct1321}
{: release-note}

End of Support for instance deployments with vSphere 6.5 {: #october-2021-eos-vsphere5}
:   {{site.data.keyword.cloud_notm}} support for ordering all update levels of VMware vSphere 6.5 ended on 10 October 2021. Beginning on this date, you can no longer order new VMware vCenter Server instances with vSphere 6.5 and your existing vCenter Server instances with vSphere 6.5 become read–only in the VMware Solutions console and through the public REST API.

 VMware vCenter Server instances
:   The 4.4 release applies the following upgrades and improvements for newly deployed instances, clusters, and hosts.

   * VMware vSphere ESXi 7.0 Update 2d (build 18538813)
   * VMware vCenter Server Appliance
      * 7.0 Update 2d (build 18455184)
      * 6.7 Update 3o (build 18485166)
   * VMware NSX-T 3.1.1.0.0 (build 17483185)

Add-on services
:   The following service versions are now available to install on deployed instances.

   * F5 BIG-IP v16.1
   * FortiGate Virtual Appliance v7.0.1
   * HyTrust CloudControl v6.4.1
   * Red Hat OpenShift v4.7.24
   * Zerto v9.0u1

FortiGate Virtual Appliance for multizone instances on VMware Regulated Workloads
:   For VMware Regulated Workloads, you can deploy FortiGate Virtual Appliance on edge services clusters for multizone instances. You can deploy FortiGate Virtual Appliance when you first order the instance or as part of Day 2 operations.

Veeam deployment type displayed on services detail page
:   The deployment type for Veeam is displayed on the service details page. The possible deployment types are VM, VSI, or Bare metal.

Zerto licenses availability
:   You can now order Zerto license without associating it to any vCenter Server instance. When you submit your order, IBM Support requests a license key from Zerto that is then delivered to the email address that is associated with your order.

   You can use the {{site.data.keyword.vmwaresolutions_short}} console to view license details and delete the license.

REST APIs
:   As a result of End of Support for instance deployments with vSphere 6.5, REST APIs for the following tasks for instances with vSphere 6.5 are no longer provided:

   * Adding and deleting clusters
   * Adding and removing ESXi servers
   * Adding and removing storage
   * Adding and deleting services

### 9 August 2021
{: #vmwaresolutions-aug0921}
{: release-note}

VMware vSphere 7.0 Update 2a support
:   The 4.3 release provides VMware vSphere 7.0 Update 2a for newly deployed instances. For existing vSphere 7.0u1 instances and clusters, you can either add a 7.0u1 or 7.0u2 host or cluster.

New disk type for VMware vSAN
:   For the VMware vSAN component, the 7.68 TB SSD SED capacity disk is now available for {{site.data.keyword.cloud_notm}} bare metal servers for newly deployed instances and when you add hosts and clusters to existing instances. The 7.68 TB SSD SED disk type is supported for only VMware vSphere 7.0 or 6.7 instances with 25 Gb uplink speed.

VMware Solutions Shared - Windows pricing metrics
:   (Updated on 1 October 2021) The Microsoft Windows pricing metric is now hourly for VMware Solutions Shared instances.

VMware vCenter Server instances
:   The 4.3 release applies the following upgrades and improvements for newly deployed instances, clusters, and hosts.

   * VMware vSphere ESXi
      * 7.0 Update 2a (build 17867351)
      * 6.7 P05 (build 17700523)
      * 6.5 P06 (build 17477841)
   * VMware vCenter Server Appliance
      * 7.0 Update 2b (build 17958471/17958471)
      * 6.7 Update 3n (build 18010531/18010599)
   * VMware NSX-T 3.1.0.0.0 (build 17107167)
   * VMware NSX-V 6.4.10 (build 17626462)
   * VMware vSAN 7.0 Update 2 (build 17630552) or 6.7 P05

vCenter Server multizone instances - deprecated
:   New deployments of vCenter Server multizone instances are no longer supported.
   {: deprecated}

   You can still add and delete clusters, add and remove ESXi servers, and add and delete storage for existing multizone instances.

VMware Regulated Workloads - support for consolidated cluster
:   Rather than requiring that the VMware Regulated Workloads solution deploys a separate management cluster and separate clusters for workloads, now you can start with a smaller footprint by deploying a consolidated management and workload cluster.

VMware Regulated Workloads - support for save configuration
:   A new **Save configuration** button is added to the **Summary** pane of the ordering page for VMware Regulated Workloads. Use this option to save your instance settings as a configuration template without placing an order. You can manage the configuration templates by further editing or deleting them as well.

Security and Compliance Readiness Bundle
:   A new **Save configuration** button is added to the **Summary** pane of the ordering page for Security and Compliance Readiness Bundle instances. Use this option to save your instance settings as a configuration template without placing an order. You can manage the configuration templates by further editing or deleting them as well.

Add-on services
:   The following service versions are now available to install on deployed instances.

   * Caveonix RiskForesight v3.0.1
   * FortiGate Virtual Appliance v6.4.6
   * Juniper vSRX v20.4 (R2)
   * Red Hat OpenShift v4.7

FortiGate Virtual Appliance
:   FortiGate Virtual Appliance adds the following features.
   * 25 Gb uplink speed on vSphere 7 and NSX-T
   * High-performance deployment size of Fortigate-VM32

   The uplink speed and deployment size require Cascade Lake 5218 or higher.

Juniper vSRX
:   You can install Juniper vSRX on 25 Gb uplink speed consolidated and edge services clusters on vSphere 7 with NSX-T. On 25 Gb uplink speed clusters, only the Content Security Bundle license is available.

REST APIs
:   REST API support for vCenter Server multizone instances is no longer provided as a result of feature deprecation.

### 21 June 2021
{: #vmwaresolutions-jun2121}
{: release-note}

VMware Solutions Shared - Veeam Backup and Replication V11
:   The 4.2 release provides VMware Solutions Shared instances with Veeam Backup and Replication V11 for the Veeam Cloud Connect Replication ready-to-use service.

   For more information about the compatibility requirements between Veeam service providers and tenants, see [Product versions in Veeam Cloud Connect infrastructure](https://helpcenter.veeam.com/docs/backup/cloud/cloud_connect_versions.html?ver=110){: external}.

VMware Solutions Shared - Network High Availability through data center groups
:   VMware Solutions Shared now provides Network High Availability, a VMware Cloud Director feature that allows a VMware Cloud Director network to be anchored in two data centers. This feature enables the network to be resilient and to withstand an outage in any of the two data centers.

VMware vCenter Server instances
:   The 4.2 release applies the following upgrades and improvements for newly deployed instances, clusters, and hosts.

   * VMware vSphere ESXi
      * 7.0 Update 1d (build 17551050)
      * 6.7 P05 (build 17700523)
      * 6.5 P06 (build 17477841)
   * VMware vCenter Server Appliance
      * 7.0 Update 2b (build 17958471)
      * 6.7 Update 3n (build 18010531)
   * VMware NSX-T 3.1.0.0.0 (build 17107167)
   * VMware NSX-V 6.4.10 (build 17626462)
   * VMware vSAN 7.0 Update 1d (build 17551050) or 6.7 P05
   * VMware vSAN Witness 7.0 Update 1d (build 17551050)[^vsanwitness]

[^vsanwitness]: vCenter Server multizone instances only

NSX-T for vCenter Server instances with vSphere 6.7 - deprecated
:   NSX-T is no longer supported for new deployments of vCenter Server instances with vSphere 6.7. NSX-T is available only for vSphere 7. You can still view and manage your existing instances with vSphere 6.7 and NSX-T.
   {: deprecated}

VMware vCenter Server - 25 Gb uplink speed updates
:   Enhanced support is now provided for 25 Gb uplink speed for vCenter Server multizone instances.

   * When you order new vCenter Server multizone instances, 25 Gb is supported for the witness cluster, the consolidated or management cluster, and the workload cluster.
   * When you add clusters to vCenter Server multizone instances, 25 Gb is supported for the workload cluster.

VMware vCenter Server - NFS storage limitation for VMware multizone instances
:   The initial NFS storage that you order is used mainly for management. Its size must be at least 1,000 GB and the performance at least 2 IOPS/GB. Do not delete this storage. If you require extra storage, you can add it post-deployment. The size and performance of the NFS storage added post-deployment can have any of the available values.

VMware vCenter Server - NFS host orders
:   For clusters with NFS storage, where locations with appropriate 1U servers are available, 1U servers (up to 4 drives of storage) are ordered silently rather than 2U servers. For gateway clusters and clusters with vSAN storage, 2U servers are ordered.

Regulated Workloads - 25 Gb Uplink speed
:   Enhanced support is now provided for 25 Gb uplink speed for VMware Regulated Workloads instances, both single-zone and multizone.

   * When you order new VMware Regulated Workloads instances, 25 Gb is supported for the management cluster and the workload cluster.
   * When you add clusters to VMware Regulated Workloads instances, 25 Gb is supported for the workload cluster.

Add-on services
:   The following service versions are now available to install on deployed instances.

   * Caveonix RiskForesight 3.0
   * F5 BIG-IP 15.1.3.1
   * HyTrust CloudControl 6.3.1
   * HyTrust DataControl 5.3[^htdc]
   * Juniper vSRX 3.0 (20.4R1.12)

[^htdc]: vSphere 6.7 for NSX-T and vSphere 6.7 and 6.5 for NSX-V

F5 BIG-IP
:   F5 BIG-IP is supported on vSphere 7 and NSX-T. This support is available on a management cluster.

FortiGate Virtual Appliance
:   Review the following information about FortiGate Virtual Appliance for the 4.2 release.

   * FortiGate Virtual Appliance is supported on VMware vSphere 7 and VMware NSX-T. This support is available on a management cluster and edge services cluster for single-zone instances only. Multizone support is not available.
   * For VMware Regulated Workloads instances and Security and Compliance Readiness Bundle instances, you can install FortiGate Virtual Appliance only on the edge services cluster.
   * The VM16 edition of FortiGate Virtual Appliance is available for all types of clusters. However, it is recommended that the 16 CPU license is used for high-bandwidth edge deployments only. For more information about any VM16 restrictions and Fortinet sizing, see [FortiGate-VM on VMware ESXi data sheet](https://www.fortinet.com/content/dam/fortinet/assets/data-sheets/FortiGate_VM_ESXi.pdf){: external}.
   * You can order multiple FortiGate Virtual Appliances on the management cluster. However, you can have only one pair on each edge services cluster.
   * You cannot install FortiGate Virtual Appliance and Juniper vSRX on the same edge services cluster.
   * After FortiGate Virtual Appliance v6.2.1, you are able to resize the RAM of FortiGate Virtual Appliance regardless of the licensing and pricing you currently have. You can make this change only if the CPU does not change. For more information, see [FortiGate-VM virtual licenses and resources](https://docs.fortinet.com/document/fortigate/6.2.0/vmware-esxi-cookbook/367417/fortigate-vm-virtual-licenses-and-resources){: external}.

HyTrust KeyControl - deprecated
:   New installations of HyTrust KeyControl are no longer supported for new or existing deployments of vCenter Server instances. You can still use or delete existing HyTrust KeyControl installations on your existing instances.
{: deprecated}

Juniper vSRX
:   Review the following information about Juniper vSRX for the 4.2 release:

   * Juniper vSRX is supported on vCenter Server multizone instances.
   * You cannot install Juniper vSRX and FortiGate Virtual Appliance on the same edge services cluster.

KMIP for VMware on {{site.data.keyword.cloud_notm}}
:   Two new endpoints are now available in the **Toronto** location for the KMIP for VMware service.

Veeam on vSphere 6.5 - deprecated
:   New installations of Veeam are no longer supported for new or existing deployments of vCenter Server instances with VMware vSphere 6.5. You can still use or delete existing Veeam installations on your existing vSphere 6.5 instances.
{: deprecated}

REST APIs
:   REST API support is now available for the F5 BIG-IP and FortiGate Virtual Appliance services and for adding edge services clusters to vCenter Server instances.

New and updated documentation
:   The following documentation updates are available.

   * Upgrading vCenter Server vSphere software from VMware vSphere 6.5 or 6.7 to 7.0 now includes important considerations and a section for updating licenses.
   * FAQ is updated to clarify how service license charges are being calculated.

### 5 April 2021
{: #vmwaresolutions-apr0521}
{: release-note}

VMware Solutions Shared - support for Zerto
:   Starting with the 4.1 release, the Zerto service is available and ready-to-use to provide disaster recovery for critical workloads in your virtual data center instances. Additionally, you can order the Zerto Cloud Connector (ZCC) service after you deploy your virtual data center instance. Use ZCC to replicate your on-premises virtual data centers to {{site.data.keyword.cloud_notm}}.

   Charges are incurred only if you choose to use the services.

VMware Solutions Shared - network type options
:   The option to select a private only network or a public and private network is now available when you order VMware Solutions Shared instances.

VMware Solutions Dedicated - upgrade support for vSphere 7.0 instances
:   For VMware vCenter Server instances with VMware vSphere 6.5 or vSphere 6.7, in-place upgrade to vSphere 7.0 is now supported for select configurations. Not all hardware configurations are supported, and the upgrade cannot help you migrate from VMware NSX-V to NSX-T or from a nonconverged NSX-T topology to a converged NSX-T topology.

   You must contact {{site.data.keyword.vmwaresolutions_short}} Support before and after you upgrade your instance.
{: important}

   {{site.data.keyword.cloud_notm}} supports only Cascade Lake bare metal servers for vSphere 7.0 instances. You must ensure that all VMware ESXi servers have the proper firmware and drivers to support 7.0.

   After you complete an upgrade to vSphere 7.0, you can add clusters and hosts to your upgraded instance. When you add a cluster or host to the upgraded instance, you must keep the original deployment configuration, naming, and network topology.

   The following upgrade scenarios are supported:
   * Adding NFS storage, hosts, and clusters (NFS or vSAN) on instances upgraded from vSphere 6.5 or 6.7
   * Adding hosts and clusters on upgraded NSX-V or nonconverged NSX-T instances
   * Adding hosts in an upgraded NFS or vSAN cluster

   {{site.data.keyword.cloud_notm}} recommends that you deploy a new vSphere 7.0 instance and migrate your current network topology and workload to the new instance.
   {: note}

VMware Solutions Dedicated - SAP-certified servers support for vSphere 7
:   The following SAP-certified bare metal server models are now available for deployment with vSphere 7.0. These models are available for vCenter Server instances and clusters, and for VMware vSphere clusters.
   * Dual Intel Xeon Platinum 8280M (Cascade Lake, BI.S4.NW1500)
   * Dual Intel Xeon Platinum 8280M (Cascade Lake, BI.S4.NW3000)
   * Dual Intel Xeon Platinum 8280M (Cascade Lake)
   * Quad Intel Xeon Platinum 8280M (Cascade Lake)

VMware Solutions Dedicated - 25 Gb uplink speed
:   Enhanced support is now provided for the 25 Gb uplink speed option for vCenter Server instances and clusters, and VMware vSphere clusters:
   * This option is now available for vSphere 7.0.
   * More data centers now support this option.

VMware Solutions Dedicated - {{site.data.keyword.cloud_notm}} data centers
:   (Updated on 20 April 2021) The {{site.data.keyword.cloud_notm}} data centers **Sao Paulo 04** and **Sao Paulo 05** are now available for deployment.

VMware Solutions Dedicated - {{site.data.keyword.cloud_notm}} for VMware Mission Critical Workloads
:   The following updates are available for vCenter Server multizone instances:

   * You can select to use IBM-provided or your own licenses for vCenter Server Standard and vSphere Enterprise Plus licenses.
   * You can specify an initial cluster name for your witness and consolidated clusters.
   * You can optionally order an additional workload cluster and an edge services cluster to new vCenter Server multizone instances.
   * You can add or remove the additional workload cluster or edge services cluster to existing vCenter Server multizone instances.
   * You can add or remove VMware ESXi servers to and from your additional workload cluster.
   * You can add or remove services to new or existing vCenter Server multizone instances.

VMware Solutions Dedicated - known issue for {{site.data.keyword.cloud_notm}} for VMware Mission Critical Workloads
:   For Mission Critical Workloads, a known issue with vCenter HA failover exists. If eth0 is not active on the passive node before failover is initiated, the passive node is isolated and fails to take over as the active node. vCenter HA might not activate `eth0` when failover is initiated.
{: important}

VMware Regulated Workloads
:   (Updated on 4 May 2021) The VMware Regulated Workloads offering delivers a new multizone architecture to instances that are deployed in 4.1 and later releases. The multizone architecture can help to prevent downtime for cloud applications and to automate failovers within a cloud region.

Security and Compliance Readiness Bundle
:   The Security and Compliance Readiness Bundle is a prescriptive offering that provides many of the security and compliance features of {{site.data.keyword.cloud_notm}} for Financial Services at a lower entry price. The offering is packaged with security and compliance tools and templates for you to use with your preferred regulation standard.

Add-on services
:   The 4.1 release provides the following service versions on newly deployed instances.

   * BIG-IP VE v15.1.2
   * FortiGate Virtual Appliance 6.4.4
   * HyTrust CloudControl v6.3
   * Veeam v11

Services support for vCenter Server multizone instances
:   Starting with the 4.1 release, the following add-on services are supported on vCenter Server multizone instances.

   * Caveonix RiskForesight
   * HyTrust CloudControl
   * Veeam
   * vRealize Operations and Log Insight

Caveonix RiskForesight
:   Review the following information about Caveonix RiskForesight for the 4.1 release.

   * Caveonix RiskForesight is offered as a per-host license for new deployments of Caveonix on VMware Regulated Workloads and Security and Compliance Readiness Bundle instances. For vCenter Server deployments, Caveonix is still offered as license packs that are priced per virtual machine (VM).
   * A Caveonix RiskForesight license is valid for five years.
   * Deleting Caveonix RiskForesight deletes the initial Caveonix RiskForesight license that was associated with the service.

Veeam on bare metal server
:   You can install Veeam v11 on a bare metal server. This new feature is supported only for vSphere 7.0 with NSX-T.

REST APIs
:   The following API updates are available:

   * The VMware Solutions API provides support for the additional edge services cluster and workload cluster on multizone instances.
   * The VMware Solutions API provides support for the following services on multizone instances: Caveonix RiskForesight, HyTrust CloudControl, Veeam, and vRealize Operations and Log Insight.
   * The `network` option for selecting a private only network or a public and private network is available through the VMware Solutions Shared API.

### 29 January 2021
{: #vmwaresolutions-jan2921}
{: release-note}

VMware Regulated Workloads
:   Starting with the 4.0 release, you can now order VMware Regulated Workloads directly from the VMware Solutions main page. The VMware Regulated Workloads offering includes a secure-by-default architecture that follows IBM's unique policy controls framework, provides continuous compliance monitoring, and offers the highest level of data encryption (FIPS 140-2 Level 4). For VMware Regulated Workloads, only VMware vSphere 7.0 Update 1a is supported.

VMware Solutions Dedicated - VMware vSphere 7.0 Update 1a support
:   You can order vSphere 7.0 Update 1a with your VMware vCenter Server with NSX-T instances and VMware vSphere with NSX-T clusters. vSphere 7.0u1a introduces the following support and enhancements.

   * Smaller instance footprint with support for converged management and workload cluster. vSphere 6.7 and NSX-T require eight hosts when using vSAN storage and five hosts when using NFS storage. vSphere 7.0u1a enables a footprint of four hosts when using vSAN storage and three hosts when using NFS storage.
   * Full support for the HTML5 vSphere Web Client
   * Support for Intel Cascade Lake EVC level
   * The enhanced VMware vSphere Lifecycle Manager (LCM)
   * Enhancements to VMware vSphere Distributed Resource Scheduler (DRS) and VMware vSphere vMotion
   * Security enhancements that include multi–factor authentication (MFA) and vSphere Trust Authority (vTA)

   vSphere 7.0u1a is the exclusive basis for {{site.data.keyword.cloud}} for VMware Regulated Workloads and is available for Cascade Lake and SAP-certified bare metal servers only.

   vSphere 7.0u1a currently does not support 25 Gb uplink speed or High performance with Intel Optane for vSAN storage. Support for these features is planned for a future release. Additionally, vSphere 7.0u1a does not support single-node instances.
   {: note}

VMware Solutions Dedicated - vSAN storage for vSphere 7.0 Update 1a
:   A warning message might be displayed when you log in to vCenter Server through the vSphere Web Client. To remove the warning, download the latest version of the vSAN HCL DB file and update vCenter Server. For more information, see [Updating the vSAN HCL database manually (2145116)](https://kb.vmware.com/s/article/2145116){: external}.

VMware Solutions Dedicated - existing instances and vSphere 7.0 Update 1a
:  For vCenter Server instances with vSphere 6.5 or vSphere 6.7, in-place upgrade to vSphere 7.0 is not currently supported due to changes in VMware license keys and changes in the vCenter Server architecture and topology.
{: note}

   Carefully review the VMware product lifecycle matrix for ESXi and NSX as part of your planning. For more information, see [Product LifeCycle Matrix](https://lifecycle.vmware.com/){: external}.

   {{site.data.keyword.cloud_notm}} plans to publish guidance for upgrading your existing instance to vSphere 7.0 in a future VMware Solutions release. However, an upgrade cannot be supported for all hardware combinations, will not accomplish a migration from NSX-V to NSX-T, and will enable only limited VMware Solutions capabilities at the vSphere 7.0 level.

   Instead, {{site.data.keyword.cloud_notm}} recommends that you deploy a new vSphere 7.0 instance and migrate your current network topology and workload to the new instance.

   Migrating your workload to a new instance is especially recommended if you want to perform a hardware refresh, if you want to migrate from NSX–V to NSX–T, or if you want to migrate your existing NSX–T topology with separate management and workload clusters to a converged topology.

VMware Solutions Dedicated - support for VMware vSAN stretched clusters for vSphere 7.0 Update 1a and NSX-T 3.1
:   VMware vSphere Enterprise Plus 7.0 Update 1a and VMware NSX-T 3.1 are included when you order a VMware vCenter Server stretched cluster across a multizone region. The stretched cluster is deployed as a single consolidated cluster capable of hosting both management and workload clusters.

   With the combination of consolidated cluster and support for a 3-host RAID 1 configuration, you can deploy an instance with a minimum of eight hosts when you use NFS storage for your witness cluster, or nine hosts when you use vSAN storage for your witness cluster.

   Extra features for stretched clusters are planned for future releases, including support for VMware Regulated Workloads, edge services clusters, more workload clusters, and optional add-on services.
   {: note}

VMware Solutions Dedicated - updates for VMware NSX
:   Review the following information about vCenter Server with NSX-T instances for the 4.0 release.

   * New instances of vCenter Server with NSX-T are provisioned with NSX-T 3.1.
   * Day 2 operations continue to be supported for vCenter Server with NSX-T 2.5.1 instances with restrictions.
   * If you want to upgrade your existing vCenter Server with NSX-T instance, {{site.data.keyword.cloud_notm}} recommends that you upgrade directly to NSX-T 3.1 bypassing NSX-T 3.0.x.

VMware Solutions Dedicated - {{site.data.keyword.cloud_notm}} data centers
:   Review the following updates for {{site.data.keyword.cloud_notm}} data centers.

   * The new data centers **Toronto 04** and **Toronto 05** are available for deployment of vCenter Server instances and vSphere clusters.
   * The new region **Toronto** is available for deployment of VMware Mission Critical Workloads.
   * The data center **Oslo 01** is no longer available for new deployments.

Single-node offerings - deprecated
:   The Single-node for Migration and App Modernization and Single-node for Data Protection and Disaster Recovery offerings are no longer provided for new deployments. Full support remains for existing single-node instances.
   {: deprecated}

Add-on services
:  The 4.0 release provides the following service versions on newly deployed instances.

   * Caveonix RiskForesight v2.4
   * HyTrust CloudControl v6.2.1 for vCenter Server with NSX-T
   * Juniper vSRX and Juniper vSRX Gateway Appliance 3.0 (20.1R2)
   * Red Hat OpenShift v4.6
      * New installations of Red Hat OpenShift on vCenter Server require VMware vSphere 7.0 Update 1a with NSX-T 3.1. For NSX-T 2.5.1 deployments, you must upgrade to vSphere 7.0 Update 1a with NSX-T 3.1.
      * During deployment and Day 2 operations, you are prompted for the cluster. You can install the service to the management cluster or any workload cluster.
   * Veeam v10a
   * vRealize Operations v8.2 and Log Insight v8.2

Add-on services that support VMware vSphere 7.0 Update 1a
:   The following add-on services support VMware vSphere 7.0 Update 1a.

   * Caveonix RiskForesight
   * VMware HCX
   * HyTrust CloudControl
   * Juniper vSRX
   * Red Hat OpenShift
   * Veeam
   * vRealize Operations

DNS entries removal
:   For several add-on services, if you installed the service before the {{site.data.keyword.vmwaresolutions_short}} 4.0 release and you then delete the service, you must remove the DNS entries manually.

Caveonix RiskForesight
:   RiskForesight v2.4 applies the following updates.

   * Updates the regulated workload presets to order 50 licenses, rather than 10.
   * Connects to NSX through FQDN, rather than to its IP address.

   When you order RiskForesight, you can now select 10 - 25,000 VMs to license, in increments of 10. The RiskForesight license is valid for five years.

Juniper vSRX
:   For vCenter Server instances, Juniper vSRX management and edge services cluster installations provide the following enhancements.

   * Useful address book entries
   * Security enhancements based on CIS guidelines
   * vSRX logging to vRealize Log Insight if the vRealize Operations add-on service is already installed

KMIP for VMware
:   Previously, KMIP for VMware provided a multitenant service that enables VMware vCenter Server to use IBM Key Protect for {{site.data.keyword.cloud_notm}} (Key Protect) and {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services (HPCS) as its key manager.

   Newly created KMIP for VMware instances that are connected to HPCS now operate as single-tenant services. These services run within the HPCS service and benefit from the features of IBM Secure Service Containers on IBM LinuxONE servers. You can connect only a single KMIP for VMware instance to each HPCS instance.

   KMIP for VMware continues to provide a multitenant service when you connect to Key Protect.

   In addition, two new endpoints are now available in the **Osaka** location for KMIP for VMware.

Red Hat OpenShift for VMware
:   Red Hat OpenShift for VMware is no longer supported for new deployments or for ordering post deployment for the following instances.

   * vCenter Server with NSX-V for vSphere 6.7 or 6.5
   * vCenter Server with NSX-T for vSphere 6.7

   Existing installations of Red Hat OpenShift for VMware can be used or deleted.

VMware HCX
:   HCX is no longer supported for new deployments on vSphere 6.7 with NSX-T or for ordering post deployment on existing vSphere 6.7 instances with NSX-T.
   {: note}

   Review the following information about the VMware HCX service for the 4.0 release.

   * VMware HCX is now offered on vSphere 7.0 Update 1a for vCenter Server with NSX-T 3.1 instances. HCX is not supported on vSphere 6.7 for vCenter Server with NSX-T 3.1 instances.
   * The 12-month commitment for HCX is removed.
   * The private interconnect option is removed. The network connection options are either public or private.
   * You can choose the target cluster for service mesh (NSX-T only).
   * The HCX service is removed if the service mesh target cluster is removed on NSX-T.
   * If the management cluster or HCX service mesh target cluster is private only, the only connection type would be private connection. If the connection type is private, a proxy is required.

VMware vRealize Operations - vSAN storage requirements
:   If you install VMware vRealize Operations and select vSAN storage, you must have an estimated 750 GB of vSAN storage to successfully install vRealize Operations. This storage requirement does not apply to NFS.

REST APIs
:   REST API support for the VMware HCX service is now available.

New and updated documentation
:   The following documentation updates are available.

   * (Updated on 24 February 2021) The Veeam on bare metal reference architecture document is now available in the **Reference** section of the user documentation.
   * A new topic, Managing security and compliance, is now available. The topic provides information about monitoring security and compliance posture with VMware Solutions by using Caveonix RiskForesight.

User interface updates and enhancements
:   The user interface is updated and provides the following enhancements.

   The following enhancements are made to the landing page of {{site.data.keyword.vmwaresolutions_short}} console to better assist you in learning and selecting the appropriate offering and services according to your needs:
   * The previous **Start provisioning** section is renamed to **IaaS platforms**.
   * A new **VMware Regulated Workloads** section is added.
   * The previous **Services** section is renamed to **Add-on services**.

## 2020
{: #year-2020}

### 26 October 2020
{: #vmwaresolutions-oct2620}
{: release-note}

VMware Solutions Shared - support for Dallas 12 and Dallas 13 {{site.data.keyword.cloud_notm}} data centers
:   Starting with release 3.9, Dallas 12 and Dallas 13 {{site.data.keyword.cloud_notm}} data centers are now available for deployment on VMware Solutions Shared instances.

VMware Solutions Shared - Integration with {{site.data.keyword.cloud_notm}} Monitoring
:   You can now use {{site.data.keyword.cloud_notm}} Monitoring to view and customize dashboards to visualize performance, volume of usage, and to define alerts to monitor your environment.

VMware Solutions Dedicated - removed support for VMware vSphere 6.5u3
:   VMware vSphere 6.5u3 is no longer supported for new VMware vCenter Server instances. Full support remains for existing instances, including support to add new hosts and clusters.

   VMware vSphere 6.5u3 is no longer supported for new VMware vSphere clusters. Full support remains for existing clusters, including support to add new hosts.

VMware Solutions Dedicated - VMware NSX updates
:   Review the following information about vCenter Server with NSX-T instances.

   * New instances of vCenter Server with NSX-T are provisioned with NSX-T 3.0.1.1.
   * Day 2 operations continue to be supported for vCenter Server with NSX-T 2.5.1 instances.
   * If you want to upgrade your existing vCenter Server with NSX-T instance, you must upgrade to NSX-T 3.0.2.

VMware Solutions Dedicated - new Cascade Lake server support
:   The following {{site.data.keyword.cloud_notm}} bare metal servers are available for deployment for vCenter Server instances and vSphere clusters with vSphere 6.7.

   * Dual Intel Xeon Platinum 8260 / 48 Cores, 2.4 GHz
   * Quad Intel Xeon Platinum 8260 / 96 Cores, 2.4 GHz

VMware Solutions Dedicated - support for Osaka {{site.data.keyword.cloud_notm}} data centers
:   The following {{site.data.keyword.cloud_notm}} data centers are available for deployment on vCenter Server, VMware vSphere, and {{site.data.keyword.cloud_notm}} for VMware Mission Critical Workloads instances: **Osaka 21**, **Osaka 22**, and **Osaka 23**.

VMware Solutions Dedicated - updates for the edge services cluster
:   The CPU model for new deployments of vCenter Server instance edge services clusters is Dual Intel Xeon Silver 4210 (Cascade).

VMware Solutions Dedicated - increased local disk count
:   For new vCenter Server instances and new clusters added to vCenter Server instances, the local disks option for storage now supports 10 and 12 disks.

Add-on services
:   The 3.9 release provides the following service versions on newly deployed instances.

   * BIG-IP VE v15.1.0.5
   * HyTrust CloudControl v6.2 for vCenter Server with NSX-T

   During the pre-configuration of HyTrust CloudControl v6.2, global PIP is enabled.
   * Juniper vSRX and Juniper vSRX Gateway Appliance 3.0 (20.1R1.11)
   * Red Hat OpenShift for VMware v4.4.23

   You can now install the Red Hat OpenShift for VMware service on vCenter Server with NSX-T instances. For NSX-T, you must have a new vCenter Server instance with NSX-T that is provisioned with NSX-T 3.0.1.1 or you must upgrade from NSX-T 2.5.1 to NSX-T 3.0.2.

HyTrust CloudControl for vCenter Server with NSX-V - deprecated
:   New installations of HyTrust CloudControl are no longer supported for new or existing deployments of vCenter Server with NSX-V instances. You can still view or delete existing HyTrust CloudControl installations on your existing instances.
   {: deprecated}

User interface updates and enhancements
:   A new **Uplink speed** option is available in the **Network interface** section when you order vCenter Server instances, order new vSphere clusters, and add clusters for vCenter Server instances.

### 24 August 2020
{: #vmwaresolutions-aug2420}
{: release-note}

VMware Solutions Shared
:   (Updated on 25 August 2020) VMware Solutions provides an upgrade for the VMware Shared infrastructure to VMware Cloud Director (vCD) v10.1.1. The v10.1.1 update is available to Dallas and Frankfurt {{site.data.keyword.cloud}} data centers.

   The Flash portal is no longer available with the v10.1.1 update.
   {: note}

VMware Solutions Shared - storage policy updates
:   For the existing storage policies in your virtual data center, the default storage policy is now the new *standard* storage policy. Previously, the default storage policy was *4 IOPS/GB*. This default storage policy is automatic for new VMware Solutions Shared instances.

   The 3.8 release introduces *Standard* storage policies and *Encrypted* storage policies. These new storage policies are available for new VMware Solutions Shared instances and added to existing VMware Solutions Shared instances with the VMware Cloud Director (vCD) v10.1.1 upgrade.

   * A standard storage policy is now available for both decrypted and encrypted policies. The standard storage policy has no maximum throughput, but the number of IOPS/GB is not guaranteed.
   * VMware Cloud Director v10.1.1 provides the capability to create encryption-enabled storage policies to all organization virtual data centers. Administrators can encrypt virtual machines (VMs) and disks by associating the VM or disk with a storage policy that has the VM encryption capability.

VMware Solutions Shared - off-site copy mode availability for Veeam Availability Suite
:   Veeam Availability Suite off-site copy mode is now automatically enabled for new and existing VMware Solutions Shared instances.

VMware Solutions Dedicated - VMware vSphere 6.7u3 support
:   You can order VMware vSphere 6.7u3 with your VMware vCenter Server instances and VMware vSphere clusters. vSphere Enterprise Plus 6.7u3 replaces the option to order vSphere Enterprise Plus 6.7u2 with new instances. Additionally, Single-node Trial for Migration and App Modernization and Single-node Trial for Data Protection and Disaster Recovery instances are now ordered with vSphere Enterprise Plus 6.7u3.

   vSphere Enterprise Plus 6.7u3 is available for Skylake, Cascade Lake, and Cascade Lake SAP {{site.data.keyword.cloud_notm}} bare metal servers.

   If you have an existing instance with vSphere Enterprise Plus 6.7u2, you can add new ESXi servers with either vSphere Enterprise Plus 6.7u2 or vSphere Enterprise Plus 6.7u3.
{: note}

VMware Solutions Dedicated - vSphere ESXi 6.7u2 for vSAN storage
:  For vSAN storage, even though vSphere 6.7u3 is selected on the user interface, vSphere ESXi 6.7u2 is installed. This distinction applies to the following scenarios.

   * Newly deployed vCenter Server instances
   * New clusters that are added to new and existing vCenter Server instances
   * New ESXi servers that are added to new and existing vCenter Server instances

   For NFS storage, vSphere ESXi 6.7u3 is installed.

VMware Solutions Dedicated - VMware NSX updates
:   For vCenter Server with NSX-T, new instances are now deployed with NSX-T 3.0.1. Day 2 operations continue to be supported for NSX-T 2.5.1 instances.

   For vCenter Server with NSX-V, new instances are now deployed with NSX-V 6.4.6.

{{site.data.keyword.cloud_notm}} for VMware Mission Critical Workloads
:   All newly deployed {{site.data.keyword.cloud_notm}} for VMware Mission Critical Workloads instances are provisioned with NSX-T.

Add-on services
:   The 3.8 release provides the following service versions on newly deployed instances:

   * BIG-IP VE v15.1.0.4
   * HyTrust CloudControl v6.1.1 for vCenter Server with NSX-T
   * Juniper vSRX and Juniper vSRX Gateway Appliance v19.4R2.6
   * Red Hat OpenShift for VMware v4.4.13

Promotions for VMware Solutions add-on services
:   {{site.data.keyword.vmwaresolutions_short}} offers promotions for some VMware services. Promotional pricing offers a number of months free of charge for a service’s licenses, if the service has license charges.

   You can use one promotion (promo) code for one or more of the following services.

   * Ordering a new VMware vCenter Server
   * Adding a service to an existing vCenter Server
   * Ordering a stand-alone service (license), such as Caveonix or Veeam

Resource requirements for add-on services
:   Capacity checks are performed to ensure that resource requirements are met for services installation. Capacity checks are performed for the following services during instance deployment.

   * Caveonix RiskForesight
   * F5 BIG-IP
   * FortiGate Virtual Appliance
   * HyTrust CloudControl
   * Zerto

Selecting the target cluster for Red Hat OpenShift for VMware
:   The target cluster for installing Red Hat OpenShift varies with the following scenarios.

   * During deployment, you aren't prompted for the cluster. The service is automatically installed to the management cluster.
   * During Day 2 operations, you are prompted for the cluster. You can install the service to a management cluster or a workload cluster.

Deleting services from a cluster before deleting the cluster
:   If you remove a nonmanagement cluster that has services installed on it, the services are also deleted as part of the process.

   Previously, when you removed a nonmanagement cluster, for example, an edge services cluster, any services installed on that cluster were not removed. You had to first delete the services from the cluster and then delete the cluster itself.

   This change affects the Juniper vSRX and Red Hat OpenShift for VMware services.

REST APIs
:   APIs are now available for the Red Hat OpenShift for VMware service.

New and updated documentation
:   A new topic, **Resource requirements for add-on services**, is now available.

   The topic describes how capacity checking works for various services and what resources are required to install certain services, such as Caveonix RiskForesight, Juniper vSRX, and Veeam. The information replaces the documentation that was provided in the overviews of the individual services.

User interface updates and enhancements
:   A checklist is added at the beginning of the ordering pages to help you prepare your environment when you place an order for the first time. This feature does not apply to the following instances and services.

   * Single-node Trial for Migration and App Modernization instances
   * Single-node Trial for Data Protection and Disaster Recovery instances
   * KMIP for VMware instances
   * On-premises VMware HCX instances
   * Caveonix RiskForesight licenses
   * Veeam licenses
