---

copyright:

  years:  2019, 2024

lastupdated: "2024-05-21"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# System context for {{site.data.keyword.vcf-classic-short}} and Red Hat OpenShift architecture
{: #vcs-openshift-syscontext}

The following diagram shows the system context for this reference architecture. A system context diagram is a high-level diagram that provides an initial view of the system. It defines the key elements of a system, the boundary of the system, and the entities that interact with it, along with the interaction.

![VMware Solutions and {{site.data.keyword.redhat_openshift_full}} System Context](../../images/openshift-systemcontext.svg){: caption="Figure 1. {{site.data.keyword.vmwaresolutions_full}} and {{site.data.keyword.redhat_openshift_notm}} system context" caption-side="bottom"}

## Actors
{: #vcs-openshift-syscontext-actors}

The system context diagram identifies the following actors:

* **VMware administrator** - The administrator is responsible for the ongoing deployment and maintenance of the VMware® environment.
* **{{site.data.keyword.redhat_openshift_notm}} administrator** - The administrator is responsible for the ongoing deployment and maintenance of the {{site.data.keyword.redhat_openshift_full}} environment.
* **Application user** - The users of the applications that are deployed in the VMware and {{site.data.keyword.redhat_openshift_notm}} environment.

## Systems
{: #vcs-openshift-syscontext-systems}

The system context diagram identifies the following systems:

* **NSX Edge** - Virtual appliances that manage north-south traffic into and out of the {{site.data.keyword.vcf-classic}} instance.
* **NSX load balancer** - Used by {{site.data.keyword.redhat_openshift_notm}} for access to control plane and worker hosts. Load balancing is a function within the NSX® Edge, providing an L4/7 application load balancer.  
* **{{site.data.keyword.vmwaresolutions_short}} Active Directory** - Used for vCenter and NSX Manager authentication and can be extended to be used by {{site.data.keyword.redhat_openshift_notm}}.
* **{{site.data.keyword.vmwaresolutions_short}} DNS** - Used by the VMware and {{site.data.keyword.redhat_openshift_notm}} environment to provide FQDN registration and resolution. DNS is configured to forward lookups to shared IBM DNS servers, allowing the resolution of public endpoints.
* **{{site.data.keyword.cloud_notm}} shared NTP** - Used to maintain time synchronization within the environment.
* Persistent volumes:
   * **vSAN** - vSphere® provider and storage class configured in {{site.data.keyword.redhat_openshift_notm}} environment that allows ReadWriteOnce persistent volumes to be stored as virtual machine disks. The {{site.data.keyword.cloud_notm}} {{site.data.keyword.redhat_openshift_notm}} environment allows ReadWriteMany persistent volumes.
   * **Block** - {{site.data.keyword.cloud_notm}} provider and storage class configured in {{site.data.keyword.redhat_openshift_notm}} environment that allows ReadWriteOnce persistent volumes.
* **Public internet** - Provide access to the {{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} environment to communicate with the public internet.
* **{{site.data.keyword.cloud_notm}} private network** - Provide access to the {{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} environment to communicate with the {{site.data.keyword.cloud_notm}} private network and services.

## Related links
{: #vcs-openshift-syscontext-related}

* [{{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-intro)
* [{{site.data.keyword.vmwaresolutions_short}} SDDC architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-arch)
* [{{site.data.keyword.cloud_notm}} networking and infrastructure](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-sddc-infra)
* [Storage options on {{site.data.keyword.cloud_notm}} and {{site.data.keyword.redhat_openshift_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-storage)
