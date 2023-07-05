---

copyright:

  years:  2019, 2023

lastupdated: "2023-05-22"

keywords: openshift for vmware, request openshift for vmware, tech specs openshift vmware

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Red Hat OpenShift for VMware overview
{: #ocp_overview}

The {{site.data.keyword.redhat_openshift_full}} for VMware® service deploys an {{site.data.keyword.redhat_openshift_notm}} cluster by using an automated deployment of the VMware SDDC (Software Defined Data Center) architecture. The {{site.data.keyword.redhat_openshift_notm}} components are deployed as virtual machines (VMs) or appliances by using VMware NSX® software-defined networking.

The {{site.data.keyword.redhat_openshift_notm}} version available for deployment is 4.12.
{: note}

Review the following information before you install the {{site.data.keyword.redhat_openshift_notm}} for VMware service:
* {{site.data.keyword.redhat_openshift_notm}} for VMware cannot be installed on multiple VMware vCenter Server® instances in a multisite configuration. Before you install {{site.data.keyword.redhat_openshift_notm}} for VMware on an instance, verify that the service is not installed on any other instances in the multisite configuration.
* {{site.data.keyword.redhat_openshift_notm}} for VMware is supported for vCenter Server instances with VMware vSphere® 7.0 and VMware NSX-T™ 3.1 or later.
* {{site.data.keyword.redhat_openshift_notm}} for VMware is not supported for new deployments or for ordering post-deployment for vCenter Server with NSX-V instances with vSphere 6.7.

Existing installations of {{site.data.keyword.redhat_openshift_notm}} for VMware can be used or deleted for vSphere 6.7 instances.

{{site.data.keyword.vmwaresolutions_full}} offers promotions for some services. Promotional pricing offers a number of months without charge for a service licenses, if the service has license charges. For more information, see [Promotions for VMware Solutions services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-service-promotions).

The cluster consists of the following components:
* Three primary nodes
* Three worker nodes, all running {{site.data.keyword.redhat_full}} CoreOS
* Two VMware NSX® VMs
* A {{site.data.keyword.redhat_notm}} CoreOS template
* A bastion VM running CoreOS

For more information about the architecture, see [{{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-redhat-arch).

## Technical specifications for Red Hat OpenShift for VMware
{: #ocp_overview-specs}

The following capacity requirements apply only if your vCenter Server instance is using vSAN™ storage. If you are using NFS, a new 2-TB NFS datastore, which is dedicated to {{site.data.keyword.redhat_openshift_notm}}, is ordered.

The solution topology has the following requirements:
* 9 CPUs
* 120 GB RAM
* 1,170 GB storage

For more information about resource requirements and capacity checking, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

To successfully deploy {{site.data.keyword.redhat_openshift_notm}} for VMware on vCenter Server, you must have a {{site.data.keyword.redhat_notm}} account and the pull secret key from your account. All {{site.data.keyword.redhat_notm}} accounts have an associated pull secret, which you can retrieve by [logging in to your {{site.data.keyword.redhat_notm}} account](https://cloud.redhat.com/openshift/install/vsphere/user-provisioned){: external}. You must purchase {{site.data.keyword.redhat_notm}} support entitlements through {{site.data.keyword.redhat_notm}} and, if needed, send information for all {{site.data.keyword.redhat_openshift_notm}} support issues to {{site.data.keyword.redhat_notm}}.

### Selection of the target cluster for installation
{: #ocp_overview-select-target-cluster}

During deployment and Day 2 operations, you are prompted for the cluster. You can install the service on the management cluster or any workload cluster.

### Bastion details
{: #ocp_overview-bastion}

The bastion VM contains an installation directory with the files and tools that are needed to manage and expand the {{site.data.keyword.redhat_openshift_notm}} cluster.   

You can log in to the bastion VM by using SSH and the credentials that are provided on the {{site.data.keyword.redhat_openshift_notm}} for VMware service details page. To run commands as the `root` user, use the command `sudo -i`.

In addition, most commands for {{site.data.keyword.redhat_openshift_notm}} management must be run from the installation directory. You can change to the installation directory with the command `cd /opt/ocpinstall`.

Any commands that require the `openshift-install`, `oc`, or `kubeadmin` tools must reference the files that are located in the installation directory by prefixing the command name with `./`. For example, `./oc whoami` instead of `oc whoami`.

The {{site.data.keyword.redhat_openshift_notm}}-related files from the bastion include an SSH key, an installation configuration file, command-line tools, and a `kubeconfig` file. The exact location of the installation configuration directory on the bastion is shown on the service details page.

### SSH key
{: #ocp_overview-bastion-ssh-key}

The SSH key on the bastion is installed on all {{site.data.keyword.redhat_openshift_notm}} cluster VMs, which allows SSH login from the bastion into any cluster VM. The full path to the SSH key is displayed on the service details page. For security purposes, it is highly recommended that you generate a new SSH key and update the cluster VMs with the new key. For more information, see [Changing the SSH key on the {{site.data.keyword.redhat_openshift_notm}} bastion](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_managing#ocp_managing-change-ssh-key).

When you log in to a cluster VM from the bastion, you must connect as the `core` user as shown in the following example: `root@bastion# ssh core@control-plane0`.

### High availability
{: #ocp_overview-high-avail}

The {{site.data.keyword.redhat_openshift_notm}} VMs are deployed with DRS rules to ensure that they are on physically separate hosts. If a host must be replaced or redeployed, you must adjust the preconfigured DRS rules before you proceed.

### Installation configuration files
{: #ocp_overview-bastion-install-config-file}

The installation configuration file `install-config.yaml.bak` is located in the installation directory on the bastion. The file is a copy of the original `install-config.yaml` file that was used by the `openshift-install` program to generate the ignition files. The generated ignition files can also be found in the installation directory on the bastion.

The `oc` and `kubectl` command-line tools from the {{site.data.keyword.redhat_openshift_notm}} client software are on the bastion. The installer program, named `openshift-install`, is used to install {{site.data.keyword.redhat_openshift_notm}} and can also be used to generate fresh ignition files.  

The bastion also holds a file that is named `auth/kubeconfig`, needed for authentication. This file holds the initial kubeadmin credentials that are created during installation. Before you initially use the `oc` or `kubectl` tools, you must set the KUBECONFIG environment variable with the path to this file. For example, `export KUBECONFIG=auth/kubeconfig`.

After that is done, any commands you run will be as the `kubeadmin` user. You can verify the user account by running the command `./oc whoami`.

After you configure your authentication and any additional users, you no longer need to source this file, and you can log in as the user that you created.

### Red Hat subscriptions
{: #ocp_overview-redhat-subscr}

The {{site.data.keyword.redhat_openshift_notm}} cluster is associated with the {{site.data.keyword.redhat_notm}} account from the pull secret that was provided during installation. To assign subscriptions or manage the cluster, you can view the cluster in the {{site.data.keyword.redhat_notm}} portal under **Systems** or **Clusters**.

## Assigning Red Hat subscriptions and entitlements to your Red Hat OpenShift cluster
{: #ocp_overview-assign-cluster}

1. Log in to your {{site.data.keyword.redhat_openshift_notm}} cluster web console.
2. Click **Home > Dashboards**. Make a note of the cluster ID that is displayed.
3. Click **Administration > Cluster Settings**.
4. Click **OpenShift Cluster Manager** under the channel, version, and update information.
   * Ensure that the cluster ID that is displayed matches the cluster ID from step 2.
   * If the cluster is not attached to a subscription, a message is displayed with a link that you can use to find this cluster in the {{site.data.keyword.redhat_notm}} customer portal. Use the link to assign the appropriate subscription and entitlement to the cluster.

   If you do not have enough subscriptions and entitlements, contact a {{site.data.keyword.redhat_notm}} Sales representative.

For more information, see [{{site.data.keyword.redhat_openshift_notm}} subscriptions information and known issues](https://access.redhat.com/articles/4105561){: external}.

## Configuring authentication
{: #ocp_overview-conf-auth}

By default, the {{site.data.keyword.redhat_openshift_notm}} installer creates a `kubeadmin` user that you can use to log in to the cluster. Create authentication backends or more users, as needed, for security purposes.

For more information about how to configure {{site.data.keyword.redhat_openshift_notm}} authentication, see [Understanding authentication](https://docs.openshift.com/container-platform/4.7/authentication/understanding-authentication.html){: external}.

## Updating your Red Hat OpenShift cluster
{: #ocp_overview-update-clus}

For more information about updating {{site.data.keyword.redhat_openshift_notm}}, see:

* [Updating a cluster within a minor version using the web console](https://docs.openshift.com/container-platform/4.7/updating/updating-cluster-within-minor.html){: external}.
* [Updating a cluster within a minor version using the CLI](https://docs.openshift.com/container-platform/4.7/updating/updating-cluster-cli.html){: external}.

## Considerations when you install Red Hat OpenShift for VMware
{: #ocp_overview-consid-install}

* Before the service is installed in your environment, a check is completed against the available capacity of the target cluster in the environment to ensure that the service components can fit. The storage capacity check applies only to vSAN storage. For NFS clusters, a new NFS datastore, dedicated to {{site.data.keyword.redhat_openshift_notm}}, is added.
* The cluster is associated with the {{site.data.keyword.redhat_notm}} account from the pull secret that is provided.
* The **Latency Sensitivity** setting of the {{site.data.keyword.redhat_openshift_notm}} cluster VMs can affect Kubernetes scheduling performance. By default, the setting is set to **Normal**, but it can be set to **High** if you encounter Kubernetes performance issues.

## Considerations when you delete Red Hat OpenShift for VMware
{: #ocp_overview-consid-remove}

* Before you delete {{site.data.keyword.redhat_openshift_notm}} for VMware, you must remove any additional VMs that you created in the `ocp` directory on VMware. The VMware Solutions automation removes only the items that were deployed during the initial installation of {{site.data.keyword.redhat_openshift_notm}} (VMs, storage, and NSX). Any node that is deployed after the installation is not cleaned up.
* The VXLAN, DLR, and the Edge Gateway that were created during the initial deployment of {{site.data.keyword.redhat_openshift_notm}} for VMware is deleted. The VMs that you deployed on VXLAN will lose connectivity after the removal of {{site.data.keyword.redhat_openshift_notm}} for VMware starts.
* If your cluster uses NFS storage, deleting {{site.data.keyword.redhat_openshift_notm}} deletes the NFS datastore that was added during installation.
* If you are using a vSAN datastore, delete any persistent volumes that you no longer need before you uninstall {{site.data.keyword.redhat_openshift_notm}}. Any volumes that are not deleted will remain in the vSAN storage after the {{site.data.keyword.redhat_openshift_notm}} uninstallation.
* Before you delete the service, you must remove any personal VMs that were deployed with this service, from the storage. {{site.data.keyword.redhat_openshift_notm}} only orders personal VMs if it’s not vSAN.

## Related links
{: #ocp_overview-related}

* [vCenter Server and {{site.data.keyword.redhat_openshift_notm}} architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-intro)
* [VMware Solutions and {{site.data.keyword.redhat_openshift_notm}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-intro)
* [{{site.data.keyword.redhat_openshift_notm}} Container Platform 4.7 documentation](https://docs.openshift.com/container-platform/4.7/welcome/index.html){: external}
* [{{site.data.keyword.redhat_openshift_notm}} Container Platform 4.7 release notes](https://docs.openshift.com/container-platform/4.7/release_notes/ocp-4-7-release-notes.html){: external}
* [What's new in {{site.data.keyword.redhat_openshift_notm}}](https://www.openshift.com/learn/whats-new){: external}
* [Succeeding with {{site.data.keyword.redhat_openshift_notm}} and VMware’s Software-Defined Datacenter (SDDC)](https://blog.openshift.com/red-hat-openshift-and-vmware-better-together/){: external}
