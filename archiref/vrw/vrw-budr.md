---

copyright:

  years:  2020, 2023

lastupdated: "2023-06-16"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Business continuity
{: #vrw-budr}

{{site.data.keyword.cloud}} for VMware® Regulated Workloads provides business continuity only at the management and edge layers.

## Management cluster
{: #vrw-budr-management}

The management cluster relies upon native vSphere® DRS capabilities to keep management services available to the platform administrators. Even with the configuration of the vSphere DRS features, manual intervention is sometimes necessary to restore access to management services. The use of shared storage minimizes the necessity of manual restoration activities if a VMware ESXi™ host is lost.

| System | Backup option | Frequency |
|---|---|---
|**Active Directory / DNS** | Image through the Veeam® agent | Daily |
|**vCenter** | Backup server file| Daily |
|**NSX-T™ Controllers** | Backup server file | Daily|
|**VMware Aria® Operations™ Manager** | VMDK through Veeam | Daily |
|**VMware Aria Operations™ for Logs** | VMDK through Veeam | Daily |
|**Virtual Machine Backup Server** | VMDK through Veeam| |
|**Juniper vSRX** | Backup server file through SCP from vSRX | Commit change |
{: caption="Table 1. Backup options" caption-side="bottom"}

### Veeam backup server
{: #vrw-budr-management-veeam}

Veeam on {{site.data.keyword.cloud_notm}} delivers reliable backup for virtual machines (VMs) within the {{site.data.keyword.cloud_notm}} for VMware Regulated Workloads environment.

Veeam provides continuous backup of the management stack for protection against disasters. If corruption of any management stack component occurs, Veeam also provides rapid restoration to known good states. Veeam can also provide backup services for the workload cluster. The single site deployment must use the Veeam bare metal option to provide an acceptable backup repository.

The Veeam environment is provisioned initially with a single VM. The SaaS provider can extend this instance to their custom requirements, including remote database, more proxy servers, and scaling out of the backup repository.

Veeam is deployed to the management regions in both availability zones (AZ) for use in an MZR.

## Gateway cluster
{: #vrw-budr-edge}

The gateway cluster does not use any vSphere resiliency features and backup of the gateway VMs is not performed. The gateway appliances deliver resilience at the application layer through formation of a high-availability cluster at the time of deployment. When you are using the vSRX, it is recommended that the rescue configuration is set anytime a change is made to the running configuration. To update it, in operational mode, run `request system configuration rescue save`. The use of an SCP server to automatically back up the configuration anytime changes are made is optional and left to the client to implement.

```sh
vSRX config archive on commit

system {
  archival {
    configuration {
      transfer-on-commit;
      archive-sites {
        scp://username@host:<port>url-path password password;
      }
    }
  }
}

[edit system archival configuration]
archive-sites {
  ftp://username@host:<port>url-path password password;
  scp://username@host:<port>url-path password password;
  file://<path>/<filename>;
  http://username@host: url-path password password;
}

```

## Workload cluster
{: #vrw-budr-workload}

Business continuity at the workload layers is the responsibility of the SaaS provider to design, implement, and maintain.

Veeam backup server is the recommended solution.

## Related links
{: #vrw-budr-related}

* [IBM Cloud compliance programs](https://www.ibm.com/cloud/compliance)
* [Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview)
* [vSRX archival configuration](https://www.juniper.net/documentation/en_US/junos/topics/task/configuration/junos-software-system-management-router-configuration-archiving.html#id-10944516){: external}
