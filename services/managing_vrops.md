---

copyright:

  years:  2019, 2024

lastupdated: "2024-04-09"

keywords: VMware Aria console, VMware Aria license, login VMware Aria console, vRealize console

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing VMware Aria Operations and VMware Aria Operations for Logs
{: #managing_vrops}

## Accessing the VMware Aria Operations Manager console
{: #managing_vrops-access-vrops-console}

To access the VMware Aria® Operations™ Manager console, complete the following steps:

1. On the service details page for VMware Aria Operations and VMware Aria Operations™ for Logs, click **VMware Aria Operations Manager console**.
2. Log in by using the credentials listed on the same service details page.
3. When you log in to the VMware Aria Operations Manager console for the first time after installation, the VMware Aria Operations Manager Configuration wizard prompts you to enter your license (product key). Ensure that you select the **Product evaluation (no key required)** option to proceed.

## Starting the adapter instance for vSAN
{: #managing_vrops-start-adapter}

You must manually start the Management Pack adapter instance for vSAN™. Complete the following steps:

1. Log in to the VMware Aria Operations Manager console.
2. Click the vSAN adapter.
3. Click Edit, then test the connection and accept the certificate when prompted.
4. Start the adapter instance.

## Accessing the VMware Aria Operations for Logs console
{: #managing_vrops-access-vlog-console}

To access the VMware Aria Operations for Logs console, complete the following steps:

1. On the service details page for VMware Aria Operations and VMware Aria Operations for Logs, click **VMware Aria Operations for Logs console**.
2. Log in by using the credentials listed on the same service details page.

## Redeploying VMware Aria Operations and VMware Aria Operations for Logs
{: #managing_vrops-redeploy-vrops}

You might encounter a situation where the file systems become filled to approximately 98% capacity. This scenario can result in inconsistencies with a Cassandra database or with the VMware Aria suite of products that are deployed with IBM automation.

If VMware Aria Operations and VMware Aria Operations for Logs are deployed with IBM automation, you can remove the service or product. Use the VMware Solutions console to remove the service or product. Then, use the VMware Solutions console to redeploy it.

If you deployed the service or product in another way, you must redeploy it using the process that you originally used for deployment.

## Known issues
{: #managing_vrops-issues}

Some of the following warnings might appear. You can ignore these warning messages:
* `NSX Logical Router is violating NSX Hardening guide (targeting workload-nsx-dlr)`
* `NSX Routing Edge Service is violating the NSX Hardening guide (targeting customer-nsx-edge)`
* `NSX Manager is violating NSX Hardening guide`
* `No backup of the environment is recorded`

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

1. Log in to the VMware vSphere® Web Client.
2. Go to **Networking & Security > Installation and Upgrade > Management > NSX Controller Nodes**.
3. Select the NSX Manager that manages the NSX Controller nodes that you want to modify.
4. Click the Common Controller Attributes EDIT link.
5. Remove any Syslog Servers as needed.

## Related links
{: #managing_vrops-related}

* [VMware Aria Operations and VMware Aria Operations for Logs overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)
* [Ordering VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_ordering)
