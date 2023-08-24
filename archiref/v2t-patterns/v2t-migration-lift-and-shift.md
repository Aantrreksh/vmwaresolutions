---

copyright:

  years:  2022

lastupdated: "2023-08-09"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# NSX-V to NSX-T lift-and-shift migration approach
{: #v2t-lift-and-shift}

VMware NSX-V to VMware NSX-T™ migration in {{site.data.keyword.cloud}} is done by following the VMware® lift-and-shift migration model. In this model, you deploy a new NSX-T infrastructure on new server hardware so you can benefit from the Cloud consumption model.

In {{site.data.keyword.cloud_notm}}, you need to deploy a new vCenter Server® with NSX-T instance, which then runs in parallel with the existing vCenter Server with NSX-V instance. The NSX-T architecture is different than the NSX-V architecture, though they share similar concepts for overlay networking, distributed routing, and firewalling.


![NSX-V to NSX-T lift–and-shift migration approach](../../images/v2t-diagrams-lift-and-shift.svg "NSX-V to NSX-T migration in IBM Cloud is done by following the VMware lift-and-shift migration model"){: caption="Figure 1. NSX-V to NSX-T lift–and-shift migration approach" caption-side="bottom"}

1. Your existing NSX-V based instance was deployed previously and it hosts the current workloads and NSX-V network configurations. Before you start the migration, you need to have a thorough understanding of the environment, the workloads that are deployed on it, and the NSX-V and underlay network configurations.
2. Before you deploy a new NSX-T based vCenter Server target, analyze your capacity needs. Optimize and size your new hosts and clusters by using the latest hardware options available in {{site.data.keyword.cloud_notm}}. Check the options in the VMware Solutions console, or contact your local Sales representative for more details.
3. You can deploy the new vCenter Server with NSX-T instance in new VLANs and a new pod, or you can use existing VLANs. 25GE NICs might not be available on the same pod. Also, you cannot move the subnets between VLANs, if, for example, you need to reuse the public IP addresses. Analyze your networking needs and then decide.
4. Migrate your network configurations from NSX-V to NSX-T. As the NSX-T architecture is different, you have the opportunity to design and implement the overlay network and configurations based on NSX-T best practices. NSX-T offers scripting capabilities or you can use Terraform to define your topology. You can alternatively use NSX-T Migration Coordination tool or third-party tools to migrate your existing network configurations, firewall, and load-balancing rules.
5. To minimize network downtime, L2 extension is typically used between NSX-V logical switches and NSX-T overlay segments. You can use either NSX-T Bridging or HCX™ Network Extension here. HCX provides tools for bulk and vMotion migrations, too.
6. After your network configurations are migrated or prepared for migration, you can start to migrate your workloads between the environments. Here you have a choice of various methods. With HCX, you have a single tool to do both L2 extension and migration. You can also use Advanced vMotion and storage vMotion between the environments. In addition, you can use services and tools from [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr) or [Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview).

When you deploy a new vCenter Server with NSX-T instance, you get a new Active Directory (AD). If you customized your AD, you must migrate these changes to the AD of the new instance.
{: note}

In your VM migration between the NSX-V and NSX-T environments, the new vCenter Server instance is provisioned with new storage, both vSAN and NFS.
{: note}

## Considerations for NSX-V to NSX-T migrations
{: #v2t-lift-and-shift-considerations}

To ensure that your migration is seamless and to minimize the downtime, design the migration and its phases and waves carefully. Due to the differences in the architecture, opens you the possibility redesign parts of your network instead of just mirroring the configurations to best match your requirements and NSX-T best practices.

If you do not think that you have skills in the house, you can get help from various service providers. For example, the {{site.data.keyword.cloud_notm}} partner PrimaryIO provides [an optional pro service](/catalog/services/hdm-cloud-connect-nsx-v-to-nsx-t#about) to help you [accelerate your NSX-V to NSX-T migration](https://hdm.primaryio.com/lp/nsxvtot){: external}.

## Related links
{: #v2t-lift-and-shift-links}

* [Requirements for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [NSX-T Data Center Migration Guide](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/migration/GUID-7899A104-2662-4FC9-87B2-F4688FAEBBBA.html){: external}
* [Preparing for a Lift-and-Shift Migration](https://docs.vmware.com/en/VMware-NSX-T-Data-Center/3.2/migration/GUID-BC8C6568-754A-4F73-812C-8D5424BF7EA2.html){: external}
