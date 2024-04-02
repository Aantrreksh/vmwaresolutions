---

copyright:

  years:  2024

lastupdated: "2024-04-02"

keywords: vmware solutions shared, vmware shared, migration, migration partner, partners for assisted migration

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Migrating from VMware Shared to {{site.data.keyword.vmware-service_short}}
{: #shared_migration}

{{site.data.content.shared-deprecated-note}}

## Migration options
{: #shared_migration-options}

You can migrate your workloads from {{site.data.keyword.cloud}} for VMware Shared to {{site.data.keyword.vmware-service_full}}. Since {{site.data.keyword.vmware-service_short}} is based on VMware Cloud Director, it retains the same console that is used for VMware Shared. You also benefit from performance improvements, options of network edge tier, greater global coverage, and a small price rebalancing, which make {{site.data.keyword.vmware-service_short}} the ideal landing zone for your workloads.

Depending on the size and complexity of your workloads, you can migrate them by using a self-service migration tool. If you need assistance, you can choose a partner to help with some migration activities or ask them to do a full migration for you.

You can use VMware Cloud Director Availability (VCDA) to migrate your workloads. A supporting video can guide you through the technical aspects of using the tool. After migration, you might have other workloads on the cloud or on-premises to migrate. The VCDA tool can do a full migration for you. However, you are not charged for using VCDA to migrate your workloads from VMware Shared to {{site.data.keyword.vmware-service_short}}.

### Considerations about your environment
{: #shared_migration-environment}

Complete the following steps:
* Gather information about your hosts and virtual machines (VMs), their size, and relationships.
* Note any network components that are specific to you.
* Review the [technical considerations about migrating](/docs/vmwaresolutions?topic=vmwaresolutions-shared-vmwaas-migration).

### Considerations about your target architecture
{: #shared_migration-target-architecture}

Answer the following questions:
* Are all your hosts and VMs ready to be migrated as-is without changes?
* Do you need to migrate VMs and hosts?
* Is it better to do some consolidation during this process?
* Do you need to update your network configuration?

### Considerations about your migration skills
{: #shared_migration-skills}

* Review the VCDA how-to guides and video in [Migrating VMware Shared workloads to VMware as a Service with cloud-to-cloud connections](/docs/vmware-service?topic=vmware-service-vcda-migrating-cloudtocloud-shared).
* Review the VCDA documentation in [VMware Cloud Director Availability for VMware as a Service overview](/docs/vmware-service?topic=vmware-service-tenant-vcda).
* Review the {{site.data.keyword.vmware-service_short}} setup guide on how to get started on your target environment in [VMware as a Service overview](/docs/vmware-service?topic=vmware-service-vmware-aas-overview).
* Review the options with your technical team.

You can choose to migrate your workloads on your own or get assistance from a partner to migrate either partially or fully.

## Partners for assisted migration
{: #shared_migration-partners}

The following table shows a list of partners that can help you with the migration of VMs from VMware Shared to {{site.data.keyword.vmware-service_short}}:

| Migration partner | Description |
|:----------------- |:----------- |
| IBM Technology Expert Labs - Cloud | Technology Expert Labs - Cloud (TEL-Cloud) is a professional services organization that is powered by an experienced team of {{site.data.keyword.cloud_notm}} experts. It provides deep technical expertise, valuable tools, proven methodologies for designing and building {{site.data.keyword.cloud_notm}} solutions, and professional services for all aspects of {{site.data.keyword.cloud_notm}} adoption. Also, it is specialized in Cloud Native development, Hyper Protect Crypto Service (HPCS), IBM Kubernetes Services (IKS), Red Hat OpenShift Kubernetes Service (ROKS), Satellite, Security Compliance Center (SCC), VMware, and associated core capabilities in {{site.data.keyword.cloud_notm}} for networking, firewalls, security, back up, and disaster recovery. TEL-Cloud provides professional services for {{site.data.keyword.cloud_notm}} in a simple offering framework of architect and build services. For more information, see [Partner with IBM Technology Expert Labs](https://cloud.ibm.com/catalog/services/partner-with-technology-expert-labs). |
| IBM Consulting | IBM Consulting Migration Service offers a comprehensive solution to seamlessly transfer your DC/IT infrastructure, workloads, applications, and data across diverse environments securely and efficiently. With a focus on minimizing disruption and maximizing efficiency, IBM uses its extensive expertise in multi-cloud, hybrid by design, and data management to ensure a smooth migration process. The migration service encompasses comprehensive planning, discovery and assessment, execution, platform design and build, security, and post-migration support. It also includes DC exit, Asset Divestiture, and decommission by enabling organizations to achieve their migration objectives. By using advanced tools, assets, methods, and best practices, IBM helps businesses mitigate risks, optimize performance, and achieve migration goals on time and within budget. In addition to the migration services, IBM boasts robust capabilities in VMware environments. Through strategic partnerships and deep integration with VMware technologies, IBM delivers innovative solutions. IBM expertise in VMware environments spans virtualization management, software-defined networking, storage optimization, hybrid cloud integration, and license optimization. Using VMware solutions such as VMware Cloud Foundation™, VVF, vSAN, IBM helps businesses build agile, scalable, and resilient IT infrastructures that drive growth and innovation. With IBM support, organizations can maximize the value of their VMware investments by unlocking new opportunities for efficiency and agility in a dynamic business landscape. For more information, see [IBM Consulting](https://www.ibm.com/consulting). |
| PrimaryIO | PrimaryIO is a Silicon Valley-based company that provides solutions that support the Cloud Journey. The company has expertise in data and networking and is involved in project services to provide tightly managed, predictable, fixed-priced migrations. With an IBM Cloud-based Disaster Recovery platform solution (ProtectIO), migrations become an integral component of the experience-enhanced offerings and skill set. PrimaryIO offers NSX-V to NSX-T migrations, cloud-connection (to on-premises) services, on-premises migrations to {{site.data.keyword.cloud_notm}} and VCDA to {{site.data.keyword.vmware-service_short}}. All of these migration efforts have analogous steps that are integrated into client-transparent project plans with milestone and progress achievement visibility. For more information about migration services for PrimaryIO, see [VMware Cloud Migration Services (VMwaaS VPC NSX-T)](https://cloud.ibm.com/catalog/services/vmware-cloud-migration-services-vmwaas-vpc-nsx-t). |
{: caption="Table 1. Migration partners" caption-side="bottom"}

### Full migration assistance
{: #shared_migration-full}

The following table describes the migration activities and available partners if you need full migration assistance:

| Migration activities | IBM Technology Expert Labs - Cloud | IBM Consulting | PrimaryIO |
|:-------------------- |:---------------------------------: |:-------------: |:--------: |
| Fewer than 300 VMs to migrate | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
| More than 300 VMs to migrate | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Existing IBM Consulting client | | ![Available](../../../icons/checkmark-icon.svg) | |
{: caption="Table 2. Migration activities - full migration assistance" caption-side="bottom"}

### Partial migration assistance
{: #shared_migration-partial}

The following table describes the migration activities and available partners if you need partial migration assistance:

| Migration activities | IBM Technology Expert Labs - Cloud | IBM Consulting | PrimaryIO |
|:----- |:-----: |:-----: |:-----: |
| Fewer than 300 VMs to migrate | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
| More than 300 VMs to migrate | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) | ![Available](../../../icons/checkmark-icon.svg) |
| Existing IBM Consulting client | | ![Available](../../../icons/checkmark-icon.svg) | |
| Need an architect for 2 or 5 days to assist or plan | ![Available](../../../icons/checkmark-icon.svg) | | |
| Need technical expertise to build and migrate for 5 days | ![Available](../../../icons/checkmark-icon.svg) | | |
| Analysis of current environment, migration approach, and planning | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
| Network planning and migration approach | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
| Project management | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
| Network and edge migration | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
| Validate, test plan, and migrate a sample number of VMs | ![Available](../../../icons/checkmark-icon.svg) | | ![Available](../../../icons/checkmark-icon.svg) |
{: caption="Table 3. Migration activities - partial migration assistance" caption-side="bottom"}

## Related links
{: #shared_migration-related}

* [IBM Technology Expert Labs - Cloud](https://cloud.ibm.com/catalog/services/partner-with-technology-expert-labs)
* [IBM Consulting](https://www.ibm.com/consulting)
* [VMware Cloud Migration Services (VMwaaS VPC NSX-T)](https://cloud.ibm.com/catalog/services/vmware-cloud-migration-services-vmwaas-vpc-nsx-t)
