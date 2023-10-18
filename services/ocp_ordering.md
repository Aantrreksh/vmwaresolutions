---

copyright:

  years:  2019, 2023

lastupdated: "2023-10-05"

keywords: Red Hat OpenShift for VMware, OpenShift configuration, order OpenShift

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Ordering Red Hat OpenShift for VMware
{: #ocp_ordering}

You can include the {{site.data.keyword.redhat_openshift_full}} for VMware® service with a new VMware vCenter Server® instance or add the service to your existing instance.

## Considerations when you install Red Hat OpenShift for VMware
{: #ocp_overview-consid-install}

* Before the service is installed in your environment, a check is completed against the available capacity of the target cluster in the environment to ensure that the service components can fit. The storage capacity check applies only to vSAN storage. For NFS clusters, a new NFS data store, dedicated to {{site.data.keyword.redhat_openshift_notm}}, is added.
* The cluster is associated with the {{site.data.keyword.redhat_notm}} account from the pull secret that is provided.
* The **Latency Sensitivity** setting of the {{site.data.keyword.redhat_openshift_notm}} cluster VMs can affect the Kubernetes scheduling performance. This value is preset to **Normal**, but you can change it to **High** if you encounter Kubernetes performance issues.

## Ordering Red Hat OpenShift for VMware for a new instance
{: #ocp_ordering-new}

1. When you [order the instance](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-procedure), scroll down to the **Add-on services** section. Red Hat OpenShift for VMware is in the **Transformation and modernization of VMware applications** category. 
2. Open the category, locate Red Hat OpenShift for VMware, and toggle its switch on.
3. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_ordering#ocp_ordering-config), then click **Save**.

## Ordering Red Hat OpenShift for VMware for an existing instance
{: #ocp_ordering-existing}

1. On the instance details page, click the **Services** tab.
2. Click **Add** to add the service.
3. On the **Add services** page, locate the **Red Hat OpenShift for VMware** service in the **Transformation and modernization of VMware applications** section and toggle its switch on.
4. Click **Edit** to review and specify [the configuration information](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_ordering#ocp_ordering-config), then click **Save**.

## Red Hat OpenShift for VMware configuration
{: #ocp_ordering-config}

When you order the service, you must provide a {{site.data.keyword.redhat_full}} pull secret. This pull secret is used to associate the new {{site.data.keyword.redhat_openshift_notm}} cluster with your existing {{site.data.keyword.redhat_notm}} account. You can obtain a copy of your pull secret by [logging in to your {{site.data.keyword.redhat_notm}} account](https://cloud.redhat.com/openshift/install/vsphere/user-provisioned){: external} and clicking **Copy Pull Secret**.

## Setting up DNS to access your Red Hat OpenShift console
{: #ocp_ordering-dns-setup}

{{site.data.keyword.redhat_openshift_notm}} depends on DNS to function properly. The `ocp` wildcard zone in your VMware environment root zone resolves all names to the IP address of the {{site.data.keyword.redhat_openshift_notm}} cluster application. This way, all applications that run within {{site.data.keyword.redhat_openshift_notm}} are routed through the Load Balancer, as needed.

Because the {{site.data.keyword.redhat_openshift_notm}} web console runs as an application within {{site.data.keyword.redhat_openshift_notm}}, your system must properly resolve DNS names before you can connect to the {{site.data.keyword.redhat_openshift_notm}} web console. You must complete the following steps before you open the {{site.data.keyword.redhat_openshift_notm}} console:

1. Ensure that you are connected to your environment by using the {{site.data.keyword.cloud_notm}} infrastructure VPN.
2. Ensure that the system used to connect to the {{site.data.keyword.redhat_openshift_notm}} web console can properly resolve hostnames in the DNS zone for your VMware environment. For an existing DNS infrastructure, configure the DNS delegation. Therefore, the queries for hostnames within the VMware instance's root zone are handled by the AD DNS server that is running within your VMware environment.

Alternately, you can configure your local `hosts` file with the following entries so you can access the {{site.data.keyword.redhat_openshift_notm}} web console. Use the following example:

   `APPLICATION_IP  console-openshift-console.apps.ocp.ROOTDOMAIN`

   `APPLICATION_IP  oauth-openshift.apps.ocp.ROOTDOMAIN`

In the previous example:
* Replace `APPLICATION_IP` with the {{site.data.keyword.redhat_openshift_notm}} application IP address shown in the {{site.data.keyword.redhat_openshift_notm}} service details page.
* Replace `ROOTDOMAIN` with the root domain shown on the Summary page for the vCenter Server instance.

## Related links
{: #ocp_ordering-related}

* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
