---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-02"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware Update Manager overview
{: #vum-overview}

VMware® Update Manager (VUM) uses a multistage process to upgrade vSphere® objects and to apply patches or extensions. This process enables a smooth update procedure with a minimum of system downtime. Before we look at this process, we need to understand the following terms:
* **Inventory Object** - an object within vCenter such as virtual machines (VMs), virtual appliances (VAs), or vSphere ESXi™ hosts.
* **Baseline** - baselines contain a collection of one or more patches, extensions, service packs, bug fixes, or upgrades. Baselines can be classified as patch, extension, or upgrade baselines. There are two types of baselines: Host and VM/VA. Host and VM/VA have predefined baselines by VMware and custom baselines that can be added as required:
- Pre-defined Hosts baselines:
   - Critical host patches
   - Non-critical host patches

- Pre-defined VMs/VAs baselines:
   - VA upgrade to latest
   - VM hardware upgrade to match host
   - VMware tools upgrade to match host

* **Baseline Group** - a set of non-conflicting baselines, which combines different types of baselines, and scans and remediates an inventory object against all of them as a whole. If a baseline group contains both upgrade and patch or extension baselines, the upgrade runs first.
* **Scanning** - Scanning is the process in which the Inventory object or objects are evaluated against the baseline or baseline group.
* **Staging** - Staging ensures that the patches and extensions are downloaded to the vSphere ESXi hosts before the remediation and is an optional step to minimize the time hosts are in maintenance mode.
* **Remediation** - Remediation is the process in which VUM applies patches, extensions, and upgrades to the inventory object or objects.

Therefore, the VUM process is as follows:
* An inventory object, or a group of objects, are scanned for compliance against a baseline or a baseline group.
* After a review, patches and extensions can be optionally staged, before remediated.

The downloading of upgrades, host patches, extensions, and related metadata is a predefined automatic process that can be modified. By default, at regular configurable intervals, VUM contacts VMware or third-party sources to gather the following information about available upgrades, patches, or extensions:

* Metadata about all ESXi 5.5 and ESXi 6.x patches regardless of whether you have hosts of such versions in your environment.
* Metadata about ESXi 5.5 and ESXi 6.x patches and about extensions from third-party vendor URL addresses.
* Notifications, alerts, and patch recalls for ESXi 5.5 and ESXi 6.x hosts.
* Metadata about upgrades for virtual appliances.

VUM supports the recall of patches for hosts that are running ESXi 5.0 or later. A patch is recalled if the released patch has problems or potential issues. After you scan the hosts in your VMware vCenter Server® instance, VUM alerts you if the recalled patch is installed on a certain host. Recalled patches cannot be installed on hosts with VUM. VUM also deletes all the recalled patches from the patch repository. After a patch fix to the problem is released, VUM downloads the new patch to its patch repository. If you installed the problematic patch, VUM notifies you that a fix was released and prompts you to apply the new patch.

The VUM client interface provides the following views:
* Administration view
* Compliance view

## Administration view
{: #vum-overview-admin-view}

To access the administration view, go to **Home > Update Manager** and select the IP address of the Update Manager instance. In the Administration view, you can do the following tasks:
* Configure the Update Manager settings
* Create and manage baselines and baseline groups
* View Update Manager events
* Review the patch repository and available virtual appliance upgrades
* Review and check notifications
* Import ESXi images

## Compliance view
{: #vum-overview-compliance-view}

The compliance view of a selected inventory object is accessed by navigating to **Hosts and Clusters** or **VMs and Templates** and clicking the **Update Manager** tab. In the Update Manager Compliance view, you can do the following tasks:
* View compliance and scan results for each selected inventory object
* Attach and detach baselines and baseline groups from a selected inventory object
* Scan a selected inventory object
* Stage patches or extensions to hosts
* Remediate a selected inventory object

## Related links
{: #vum-overview-related}

* [VMware HCX solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-hcx-archi-intro#hcx-archi-intro)
* [{{site.data.keyword.vmwaresolutions_short}}](https://www.ibm.com/products/vmware)
