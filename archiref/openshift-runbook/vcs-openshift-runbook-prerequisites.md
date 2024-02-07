---

copyright:

  years:  2019, 2024

lastupdated: "2024-01-30"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Prerequisites for installation
{: #openshift-runbook-runbook-prereq-intro}

Before you can start the build process to install the {{site.data.keyword.redhat_openshift_full}} cluster, the following steps are required.

* Order new subnets for the {{site.data.keyword.redhat_openshift_notm}} environment.
   * A private portable subnet for the {{site.data.keyword.redhat_openshift_notm}} cluster NSX ESG.
   * A public portable subnet for the {{site.data.keyword.redhat_openshift_notm}} cluster NSX ESG.
* Download {{site.data.keyword.redhat_openshift_notm}} 4.7 - Access to a {{site.data.keyword.redhat_full}} subscription to download the installer, pull secret and {{site.data.keyword.redhat_notm}} Enterprise CoreOS OVA.
* Download RHEL 8.0 ISO - Access to a {{site.data.keyword.redhat_notm}} subscription to download the {{site.data.keyword.redhat_notm}} Enterprise Linux® 8.x ISO for the bastion host.
* {{site.data.keyword.cloud}} environment details - Collect the following details for {{site.data.keyword.cloud_notm}} for VMware® Solutions environment.
   * VMware vCenter Server® instance details and passwords
   * The additional private portable subnet information
   * The additional public portable subnet information
* Download and install govc - govc is a VMware vSphere® CLI, an alternative to the GUI, and suited for automation tasks.

## Ordering new subnets for the Red Hat OpenShift environment
{: #openshift-runbook-runbook-prereq-cloud-subnets}

1. Log in to the [{{site.data.keyword.vmwaresolutions_short}} console](https://cloud.ibm.com/vmware).
2. Select **Classic Infrastructure>Network>IP management>Subnets**.
3. Click **Order IP Subnets**.

Review the following requirements.
* 8 Public portable addresses assigned to the Public VLAN collected in the previous step.
* 64 Private portable addresses assigned to the Private VLAN collected in the previous step.

## Downloading Red Hat OpenShift 4.7
{: #openshift-runbook-runbook-prereq-download41}

Access the [{{site.data.keyword.redhat_openshift_notm}} Infrastructure Providers page](https://console.redhat.com/openshift/install/vsphere/user-provisioned){: external}.

1. Download the installer.
2. Download the Pull Secret.
3. Download the {{site.data.keyword.redhat_notm}} Enterprise Linux CoreOS (RHEL CoreOS) OVA image or download the OVA by using the following code. Replace 4.x and 4.x.3 with the current {{site.data.keyword.redhat_openshift_notm}} version, for example, 4.7.
   `curl -O https://mirror.openshift.com/pub/openshift-v4/dependencies/rhcos/4.x/latest/rhcos-4.x.3-x86_64-vmware.x86_64.ova`
4. Download the command-line tools if you want to run the commands from a desktop or outside Bastion host.

## Downloading RHEL 8.0 ISO
{: #openshift-runbook-runbook-prereq-downloadiso}

Download the ISO image for the bastion host.

1. Go to the {{site.data.keyword.redhat_notm}} [Product downloads](https://access.redhat.com/downloads){: external} page.
2. Click **RHEL 8.x Release** and select the 8.x version.
3. Download the source ISO images.
4. The ISO file name is `rhel-8.x-x86_64-dvd.iso`.

## Collecting vCenter Server instance details
{: #openshift-runbook-runbook-prereq-cloud}

Access the {{site.data.keyword.cloud_notm}} environment details.

1. Log in to the [{{site.data.keyword.vmwaresolutions_short}} console](https://cloud.ibm.com/vmware).
2. Click the {{site.data.keyword.vmwaresolutions_short}} instance under **Deployed Instances**.
3. From the **Summary** page, collect the vCenter and Active Directory information.
4. Click **Infrastructure** and select the cluster.
5. Under **Network Interfaces**, collect the Public and Private VLANs.

## Downloading and installing govc
{: #openshift-runbook-runbook-prereq-govc}

The `govc` command is used to upload the OVF and ISO to a datastore from the jump-server or remote device.

If your jump-host or remote device uses Windows®, then download from [Downloads](https://github.com/vmware/govmomi/releases){: external}.

If your remote device uses macOS, then use the following command: `brew install govmomi/tap/govc`

If you need to install Homebrew, see [Installing Homebrew on a Mac](https://treehouse.github.io/installation-guides/mac/homebrew){: external}.

If your jump-host or remote device uses Linux, complete the following steps:

1. Download govc and make it executable. Run `curl -L https://github.com/vmware/govmomi/releases/download/v0.20.0/govc_linux_amd64.gz | gunzip > /usr/local/bin/govc`.
2. Run `chmod +x /usr/local/bin/govc`.

## Validating Distributed PortGroup and Datastore names
{: #openshift-runbook-runbook-prereq-netstorage-ic4v}

vCenter Server deployment uses deployment-specific naming for the datastores and distributed PortGroups. This runbook uses 'vsanDatastore', 'SDDC-DPortGroup-Mgmt' and 'SDDC-DPortGroup-External'. You need to use your vCenter Server deployment-specific network and storage names in your deployment configurations. For example, you might have datastore such as 'workload_share_YgkI8' (in case {{site.data.keyword.filestorage_full_notm}} is used for the datastore) or your private portgoup can be like 'fra04test-fra04-test01-dpg-mgmt'.  

You can validate the private and public Distributed PortGroup names and the datastore names for your deployment by using GOVC.

```bash
export GOVC_URL='10.208.17.2'
export GOVC_USERNAME='administrator@vsphere.local'
export GOVC_PASSWORD='xxxxx'
export GOVC_INSECURE=1

# Distributed Port Group names
govc ls network | grep -E 'dpg-mgmt|SDDC-DPortGroup-Mgmt' | awk -F / '{print $4}'
govc ls network | grep -E 'dpg-external|SDDC-DPortGroup-External' | awk -F / '{print $4}'

# Datastore names
govc ls datastore | grep -E 'vsan|share' | awk -F / '{print $4}'
```
{: pre}

Pick your deployment-specific values and use them throughout the runbook.

## Uploading the OVA image to vCenter
{: #openshift-runbook-runbook-prereq-cloud-ic4v}

You must upload and import the RHEL ISO and RHEL CoreOS OVA downloads from the previous steps into the vCenter Server instance datastore. You must rename the OVA image to *rhcos-latest* in order for the image to work with the Terraform templates used later in the build process.

On the jump-server or remote device, by using an editor of your choice, such as Visual Studio Code, copy the following and change for your values. Replace the x in 4.x.3 with the current {{site.data.keyword.redhat_openshift_notm}} version, for example, 4.7.

```bash
export GOVC_URL='10.208.17.2'
export GOVC_USERNAME='administrator@vsphere.local'
export GOVC_PASSWORD='xxxxx'
export GOVC_INSECURE=1
export GOVC_NETWORK='SDDC-DPortGroup-Mgmt'
export GOVC_DATASTORE='vsanDatastore'

rhcos-4.x-x86_64-vmware.x86_64.ova

govc import.spec ./rhcos-4.x-x86_64-vmware.x86_64.ova | python -m json.tool > rhcos.json
vi rhcos.json
  - replace  "Network": "SDDC-DPortGroup-Mgmt"
  - leave name as "VM network"
govc import.ova -options=./rhcos.json -name=rhcos-4.x-x86_64-vmware.x86_64.ova
govc vm.markastemplate vm/rhcos-latest
```
{: pre}

## Uploading the ISO image to vCenter storage
{: #openshift-runbook-runbook-prereq-cloud-iso}

Use the following govc example to upload the ISO image for the creation of the bastion node:

```bash
export GOVC_URL='10.208.17.2'
export GOVC_USERNAME='administrator@vsphere.local'
export GOVC_PASSWORD='xxx'
export GOVC_INSECURE=1
export GOVC_DATASTORE='vsanDatastore'
govc datastore.mkdir isos
govc datastore.upload rhel-8.x-x86_64-dvd.iso isos/rhel-8.x-x86_64-dvd.iso
```
{: pre}

## Related links
{: #vcs-openshift-runbook-prerequisites-related}

* [{{site.data.keyword.redhat_openshift_notm}} NSX DLR configuration](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-nsxdlr-intro)
* [{{site.data.keyword.redhat_openshift_notm}} Bastion node setup](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-bastion-intro)
* [Visual Studio Code](https://code.visualstudio.com/){: external}
