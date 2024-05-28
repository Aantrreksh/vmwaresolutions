---

copyright:

  years:  2019, 2024

lastupdated: "2024-05-21"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Red Hat OpenShift architecture
{: #vcs-openshift-redhat-arch}

The {{site.data.keyword.vmwaresolutions_full}} offerings provide automation to deploy VMware® technology components in
{{site.data.keyword.cloud_notm}} data centers across the globe. The architecture consists of a single cloud region. It supports the ability to extend into more cloud regions that are located in another geography or into another {{site.data.keyword.cloud_notm}} pod within the same data center.

![{{site.data.keyword.redhat_openshift_notm}} architecture](../../images/openshift-components.svg){: caption="Figure 1. Red Hat OpenShift architecture" caption-side="bottom"}

## Bastion hosts
{: #vcs-openshift-redhat-arch-bastion-host}

The Management host is a {{site.data.keyword.redhat_full}} Enterprise Linux® 8.0 virtual machine (VM). This VM hosts services to install and configure the {{site.data.keyword.redhat_openshift_full}} instance and provides utilities to manage the {{site.data.keyword.redhat_openshift_notm}} environment. This host is normally deployed in the VXLAN Subnet.

## Bootstrap hosts
{: #vcs-openshift-redhat-arch-bootstrap-host}

The bootstrap node is a {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS (RHCOS), a new container-oriented operating system designed for running containers. The node is a temporary node that is used to start the installation.

## Control Plane hosts
{: #vcs-openshift-redhat-arch-control-plane-host}

The control plane hosts are {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS (RHCOS), a new container-oriented operating system designed for running containers. The control plane nodes are known as the control plane, where Kubernetes services such as API server, etcd, and controller manager are defined. An NSX® load balancer is configured to spread load across these VMs for ports 6443 and 22623, exposing the `api` and `api-int` functions.

## Worker hosts
{: #vcs-openshift-redhat-arch-worker-host}

The worker hosts are {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS (RHCOS), a new container-oriented operating system designed for running containers. The worker nodes are known as the data-plane, where the actual Kubernetes workloads are deployed. An NSX load balancer is configured to spread load across these VMs for ports 80 and 443, exposing the wildcard DNS and *.apps.

## Common services
{: #vcs-openshift-redhat-arch-common-svc}

The {{site.data.keyword.redhat_openshift_notm}} deployment uses the following components of the {{site.data.keyword.vmwaresolutions_short}} SDDC architecture to help with the execution and installation:

- Time services
- Domain name resolution
- NSX load balancers
- NSX DHCP services
- NSX software defined networking

For more information, see [{{site.data.keyword.vmwaresolutions_short}} SDDC architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-arch).

## Related links
{: #vcs-openshift-redhat-arch-related}

* [{{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-intro)
* [System context for {{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-syscontext)
* [{{site.data.keyword.cloud_notm}} networking and infrastructure](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-sddc-infra)
* [Storage options on {{site.data.keyword.cloud_notm}} and {{site.data.keyword.redhat_openshift_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-storage)
