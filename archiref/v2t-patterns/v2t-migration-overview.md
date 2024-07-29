---

copyright:

  years:  2022, 2024

lastupdated: "2024-07-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# NSX-V to NSX-T migration overview
{: #v2t-overview}

Starting with version 4.0, VMware NSX-T Data Center is known as VMware NSX. This document uses NSX-T and NSX-V for clarity between the two NSX solutions.
{: note}

This documentation provides a validated approach and guidance for existing {{site.data.keyword.vmwaresolutions_full}} customers with VMware {{site.data.keyword.vcf-auto-short}}® with NSX-V instances. In that way, they can move and migrate their workloads to new {{site.data.keyword.vcf-auto-short}} with NSX-T™ instances (also referred as V2T migration). This documentation is not primarily aimed at customers that want to migrate on-premises workloads to {{site.data.keyword.cloud_notm}}, although some of the approach and guidance is applicable.

While VMware documentation describes a number of migration approaches, only the coexist or lift-and-shift approaches are validated by {{site.data.keyword.cloud_notm}}. In the co-existing approach, NSX-V, and NSX-T are run side by side and new workloads are placed on the new NSX-T environment and old workloads are decommissioned on the NSX-V environment. When the NSX-V environment is empty, it can be de-provisioned. This approach is not discussed further in the documentation, but it can be a validated option if you want to follow this path.
{: note}

In the lift-and-shift approach, the {{site.data.keyword.cloud_notm}} automation is used to deploy a new {{site.data.keyword.vcf-auto-short}} instance on the same or different VLANs. With this action, you can perform both NSX-V to NSX-T migration and workload migration.

With the lift-and-shift migration, you can:

* Be flexible to plan the migration based on your workload requirements.
* Adopt a modular migration approach, for example, partial subnet evacuation.
* Configure a different network topology in the NSX-T environment.
* Failback of a migration wave, as the existing NSX-V environment is still running.
* Over time, gradually migrate specific parts of the NSX-V workloads.
* Logically extend networks between both environments and move the workloads gradually from NSX-V to NSX-T.

The journey from NSX-V to NSX-T requires careful planning and preparation. You must be familiar with NSX-T concepts and administration tasks before any migration. This journey must involve the following steps:

* Education - Training for the team who migrates to NSX-T and then runs NSX-T.
* Migration planning and preparation - Review the current NSX-V environment to understand the complexity of the migration, and key business drivers that impact migration. Select the topology for the target NSX-T environment.
* Target platform selection, deployment, and configuration - This step also includes the setting-up of migration tools such as L2 bridging or VMware HCX. Or also third-party tools such as SPJ's cITopus or ReSTNSX's Migration Assistance Tool.
* Configuration migration - These tasks include the setting up of the overlay components, which include NSX-T segments, routing, load balancing, edge firewall, distributed firewall, and tagging. Configuration migration can be done manually through scripting, such as Terraform or third-party tools such as SPJ's cITopus.
* Workload migration - This step includes layer 2 network stretching, if required, and virtual machine migration. Migration techniques include VMware HCX migrations or Advanced vCenter vMotion.

An example of a high-level migration workflow that uses the lift-and-shift migration approach with NSX-T L2 Bridge is as follows:

* Deploy the new {{site.data.keyword.vcf-auto-short}} with NSX-T instance.
* Create your required NSX-T network topology and configure the necessary network services.
* Configure an NSX-T Edge bridge to extend the NSX-V VXLAN/logical switch/virtual wire to an overlay segment in NSX-T.
* Use the VMware Migration Coordinator to migrate (copy across) the Distributed Firewall (dFW) configuration.
* The dFW only migration mode of the migration coordinator must be run only one time. After the dFW configuration is migrated to NSX-T, do not update the dFW configuration in the NSX-V environment.
* Switch the default gateway to the NSX-T environment.
* Use NSX-T Edge bridge and vSphere vMotion to migrate workload VMs to the overlay segment in NSX-T.
* Migrate the Security Tags to the workload VMs in NSX-T.
* Continue with all NSX-V logical switches until all VMs be evacuated from the NSX-V environment.
* Decommission the old {{site.data.keyword.vcf-auto-short}} with NSX-V environment.

Depending on the source environment complexity and the skills, experience and time commitments of your team you might want to engage professional services. This action can develop a migration plan and also run the migration for you.
{: note}

## Considerations for migration
{: #v2t-overview-considerations}

You must be familiar with NSX-T concepts and administration tasks before any migration. Review the following information:

* [VMware Learning for NSX-T education](https://www.broadcom.com/support/education/vmware){: external}
* [{{site.data.keyword.cloud_notm}} VMware NSX-T Architecture](/docs/vmwaresolutions?topic=vmwaresolutions-nsx-t-design)
* [{{site.data.keyword.vcf-auto-short}} Overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [NSX-V to NSX-T 3.x Migration Coordinator](https://nsx.techzone.vmware.com/resource/nsx-v-nsx-t-3x-migration-coordinator#_Toc57645169){: external}

## Related links
{: #v2t-overview-links}

* [PrimaryIO NSX-V to NSX-T fast track migration service](https://hdm.primaryio.com/lp/nsxvtot){: external}
* [VMware Cloud Migration Services](https://cloud.ibm.com/catalog/services/vmware-cloud-migration-services)
* [cITopus tool for VMware NSX](https://spjsolutions.com){: external}
* [MAT - ReSTNSX's migration assistance tool](https://www.restnsx.com/post/migration-assistance-tool-mat){: external}
