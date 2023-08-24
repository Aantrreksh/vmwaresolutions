---

copyright:

  years:  2019, 2023

lastupdated: "2023-08-22"

keywords: VMware Aria, VMware Aria info, tech specs VMware Aria, vRealize info

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# VMware Aria Operations and VMware Aria Operations for Logs on IBM Cloud overview
{: #vrops_overview}

The VMware Aria Operations and VMware Aria Operations for Logs service is not available to Business Partner users.
{: important}

VMware Aria® Operations™ (formerly known as VMware vRealize® Operations™) and VMware Aria Operations™ for Logs (formerly known as VMware vRealize® Log Insight™) on {{site.data.keyword.cloud_notm}} deploys the VMware Aria Operations and VMware Aria Operations for Logs Enterprise Edition tools. These tools help you operate and monitor the performance, health, and capacity of your {{site.data.keyword.IBM}}-hosted, dedicated VMware environment. VMware Aria Operations for Logs helps you troubleshoot issues by using log files more quickly. VMware Aria Operations and VMware Aria Operations for Logs on {{site.data.keyword.cloud_notm}} is a non-IBM product that is offered under terms and conditions from VMware, not IBM.
{: shortdesc}

These tools are deployed by using the IBM advanced automation and are based on a consistent highly available design. VMware Aria Operations includes preinstalled and configured Management Packs to provide deeper visibility into the core VMware Software Defined Data Center components like VMware NSX®, vSAN™, and HCX™. The automation provides optimized dashboards out of the box so that you can monitor the full VMware stack more easily.

{{site.data.content.para-promotion-services}}

The service versions available for deployment are VMware Aria Operations 8.12 and VMware Aria Operations for Logs 8.12.
{: note}

## Technical specifications for VMware Aria Operations and VMware Aria Operations for Logs
{: #vrops_overview-specs}

For more information about resource requirements and capacity checking for some services, see [Resource requirements for services](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices#vc_addingservices-resource-requirements).

The following VMware Aria components are ordered and included in the service:
* VMware Aria Operations Enterprise Edition
* VMware Aria Operations for Logs Enterprise Edition

For more information about the design, requirements, and preconfigured management packs, see [Operations management architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-arch).

## Considerations when you delete VMware Aria Operations and VMware Aria Operations for Logs
{: #vrops_overview-remove}

Review the following considerations before you delete the service:

* Only the virtual machines (VMs) that were deployed during the initial installation of VMware Aria Operations and VMware Aria Operations for Logs are deleted. Any node that is deployed after the installation is not cleaned up.
* Before you delete the service, you must remove any personal VM from storage that is deployed with this service. VMware Aria Operations and VMware Aria Operations for Logs orders only personal VMs if it’s not vSAN.
* The VXLAN, DLR, and the Edge Gateway that were created during the initial deployment of VMware Aria Operations and VMware Aria Operations for Logs is deleted. The VMs that you deployed on VXLAN lose connectivity after the deletion of VMware Aria Operations and VMware Aria Operations for Logs begins.
* If you delete VMware Aria Operations and VMware Aria Operations for Logs, you need to remove the Syslog Server from the NSX Manager and the NSX Controller manually.
* If you installed the VMware Aria Operations and VMware Aria Operations for Logs service before VMware Solutions v4.0, and you then delete that service, you must manually remove the DNS entries. For more information, see [Manually removing the DNS entries](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices#vc_deletingservices-DNS-entries).

### Removing the Syslog Server from the NSX Manager
{: #vrops_overview-remove-nsx-manager}

1. Log in to the console of the NSX Manager Appliance.
2. Select **Manage Appliance Settings**.
3. Under the **General** tab, remove the Syslog Server configuration.

### Removing the Syslog Server from the NSX Controller nodes (NSX-T only)
{: #vrops_overview-remove-nsx-controller-nsx-t}

1. Gather the NSX Manager's IP address, username, and password to use in the following commands.
2. View the NSX-T Manager's current Syslog configuration by running the following command:

   ```sh
   curl -k -u '<USERNAME>:<PASSWORD>' -XGET https://<IPADDRESS>/api/v1/node/services/syslog/exporters
   {
     "_schema": "NodeSyslogExporterPropertiesListResult",
     "_self": {
       "href": "/node/services/syslog/exporters",
       "rel": "self"
     },
     "result_count": 1,
     "results": [
       {
         "_schema": "NodeSyslogExporterProperties",
         "_self": {
           "href": "/node/services/syslog/exporters/syslog1",
           "rel": "self"
         },
         "exporter_name": "syslog1",
         "level": "INFO",
         "port": 514,
         "protocol": "TCP",
         "server": "10.243.152.6"
       }
     ]
   }
   ```
   {: pre}

3. Delete the NSX-T Manager's Syslog forwarder by running the following command:

   ```sh
   curl -k -u '<USERNAME>:<PASSWORD>' -XDELETE https://<IPADDRESS>/api/v1/node/services/syslog/exporters/syslog1
   ```
   {: pre}

4. Verify the removed Syslog configuration by running the following command:

   ```sh
   curl -k -u '<USERNAME>:<PASSWORD>' -XGET https://<IPADDRESS>/api/v1/node/services/syslog/exporters
   {
     "_schema": "NodeSyslogExporterPropertiesListResult",
     "_self": {
       "href": "/node/services/syslog/exporters",
       "rel": "self"
     },
     "result_count": 0,
     "results": []
   }
   ```
   {: pre}

### Removing the Syslog Server from the NSX Controller nodes (NSX-V only)
{: #vrops_overview-remove-nsx-controller}

1. Log in to the VMware vSphere™ Web Client.
2. Go to **Networking & Security > Installation and Upgrade > Management > NSX Controller Nodes**.
3. Select the NSX Manager that manages the NSX Controller nodes that you want to modify.
4. Click the Common Controller Attributes EDIT link.
5. Remove any Syslog Servers as needed.

## Related links
{: #vrops_overview-related}

* [Ordering VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_ordering)
* [Managing VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-managing_vrops)
