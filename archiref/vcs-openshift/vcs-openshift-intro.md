---

copyright:

  years:  2019, 2024

lastupdated: "2024-01-31"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware vCenter Server and Red Hat OpenShift architecture overview
{: #vcs-openshift-intro}

The {{site.data.keyword.vmwaresolutions_full}} offering includes fully automated, rapid deployments of VMware® vCenter Server®. This offering complements the on-premises infrastructure and allows existing and future workloads to run on {{site.data.keyword.cloud_notm}} without conversion by using the same tools, skills, and processes that are used on-premises. For more information, see [What is virtualization?](https://www.ibm.com/topics/virtualization){: external}.

{{site.data.keyword.redhat_openshift_full}} on {{site.data.keyword.vmwaresolutions_short}} provides the capability to deploy a {{site.data.keyword.redhat_openshift_notm}} Cluster by using an automated deployment of the VMware Software Defined Data Center (SDDC) architecture. The {{site.data.keyword.redhat_openshift_notm}} Cluster on {{site.data.keyword.cloud_notm}} components are deployed as virtual machines (VM) or appliances by using VMware NSX® software-defined networking.

This reference architecture is for {{site.data.keyword.redhat_openshift_notm}} clusters deployed on a vCenter Server instance. It provides the foundation for customers who are starting their application modernization journey to the {{site.data.keyword.cloud_notm}}.
- **vCenter Server** is an offering from {{site.data.keyword.vmwaresolutions_short}} and is a VMware-based platform that is automatically provisioned on {{site.data.keyword.cloud_notm}}.
- **Red Hat OpenShift** is an application platform for developing and managing containerized applications, which are deployed onto virtualized infrastructure platforms, such as VMware.

![{{site.data.keyword.cloud_notm}} for VMware Solutions and {{site.data.keyword.redhat_openshift_notm}}](../../images/openshift-sddc.svg "{{site.data.keyword.cloud_notm}} for VMware Solutions and {{site.data.keyword.redhat_openshift_notm}}"){: caption="Figure 1. {{site.data.keyword.cloud_notm}} for VMware Solutions and OpenShift" caption-side="bottom"}

## Application modernization on {{site.data.keyword.cloud_notm}}
{: #vcs-openshift-intro-app-mod}

Application modernization is a term that describes the process of transitioning existing applications to use new approaches on the cloud. Customers today are seeking innovative, efficient approaches that help them make this transition based on business and application complexity.

Business pressures demand faster time to market. Your existing estate includes not only applications, but data, processes, business logic, and user interfaces, all of which need to adapt to keep up with new business demands.

Application modernization has the following benefits:
* Improved developer productivity
* Increased operational efficiency
* Reduced cost to build new capabilities
* Expanded capacity delivered in a short time

IBM understands that 70% of private cloud adoption is driven by the need to modernize application environments. However, most organizations are approaching application modernization in a staged approach, which requires a hybrid and multi cloud landscape, where:
* Complex and monolithic legacy applications that typically run on mainframes or UNIX systems remain on-premises.
* x86 environments used for Systems of Record (SoR), applications that are security sensitive, and regulated workloads are placed on a virtualized infrastructure or a private cloud.
* Applications such as SAP® or high-performance computing use bare metal resources.
* Security sensitive and some regulated workloads, which can move to the public cloud are moving to dedicated environments.
* Systems of engagement (SoE) such as web, mobile, IoT, AI, or Video are moving to public clouds.

For example, a common pattern is to have front-end SOE applications that are deployed as containers with databases and legacy middleware that are deployed on VMs on a private cloud.

Because your IT infrastructure and business needs are unique, you need an approach to modernization that helps accelerate business value delivery, reduces your risks, and preserves your existing investments. IBM provides such an approach that is customized to address your unique business and technology needs related to application modernization.

## Related links
{: #vcs-openshift-intro-related}

* [{{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-redhat-arch)
* [{{site.data.keyword.vmwaresolutions_short}} SDDC architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-arch)
* [{{site.data.keyword.cloud_notm}} networking and infrastructure](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-sddc-infra)
* [Storage options on {{site.data.keyword.cloud_notm}} and {{site.data.keyword.redhat_openshift_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-storage)
