---

copyright:

  years:  2024

lastupdated: "2024-02-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Caveonix RiskForesight Security and Compliance Center integration
{: #caveonix-scc}

The {{site.data.keyword.cloud}} Security and Compliance Center is a comprehensive Cloud-Native Application Protection Platform (CNAPP) solution suite that you can use to centrally manage your organization’s security, risk, and compliance response to regulatory standards. It enables your security and DevOps teams to secure sensitive data and protect workloads with real-time threat detection and prioritization of vulnerabilities. For more information, see [Getting started with Security and Compliance Center](/docs/security-compliance?topic=security-compliance-getting-started).

The Caveonix Security Baselines for VMware profile is now available in the Security and Compliance Center. The Caveonix Security Baselines for VMware is a collection of controls that are designed to validate the compliance of VMware® infrastructure components that run on {{site.data.keyword.cloud_notm}}. For more information, see [Change log: Caveonix Security Baselines for VMware](/docs/security-compliance?topic=security-compliance-caveonix-vmware).

The integration is only available with the Caveonix Cloud 5.0 version. If you do not have this version, open an {{site.data.keyword.cloud_notm}} Support ticket to {{site.data.keyword.vmwaresolutions_full}} to get the upgrade package and instructions.
{: restriction}

## Integration overview
{: #caveonix-scc-overview}

The integration allows Caveonix Cloud to send VMware infrastructure findings to the Security and Compliance Center Dashboard. Caveonix Cloud conducts comprehensive infrastructure compliance scans encompassing VMware NSX-T, VMware ESXi, and VMware vCenter Server components. After the vulnerability assessment process is successfully completed, Caveonix Cloud forwards the findings and you can access the evaluated findings through the Security and Compliance Center dashboard. The integration uses a Security and Compliance Center Batch job in Caveonix Cloud, which transmits the assessed findings to the Security and Compliance Center platform. Currently, Caveonix Cloud supports 267 rules to evaluate VMware infrastructure findings.

If you are using the Security and Compliance Center private endpoints, then no connection to the Internet from your Caveonix Cloud instance is required. Any firewall that you placed between the Caveonix Cloud instance and the private endpoint needs an outbound policy that enables TCP port 443. If you are using the public Security and Compliance Center endpoints, then a connection to the Internet from your Caveonix Cloud instance is required. Use a firewall or configure a proxy server to enable this communication as the Caveonix Cloud instance is only connected to the {{site.data.keyword.cloud_notm}} private network.
{: note}

## Security and Compliance Center tasks
{: #caveonix-scc-scc}

Before any integration is possible, you must have a Security and Compliance Center instance. Complete the following steps:

1. [Create an instance](/docs/security-compliance?topic=security-compliance-getting-started&interface=ui#gs-instance)
2. [Assign access](/docs/security-compliance?topic=security-compliance-getting-started&interface=ui#gs-access)
3. [Configure storage](/docs/security-compliance?topic=security-compliance-getting-started&interface=ui#gs-storage)

When you have a Security and Compliance Center instance available, complete the following steps:

1. [Create an API key](https://cloud.ibm.com/docs/security-compliance?topic=security-compliance-setup-caveonix&interface=ui#caveonix-create-key)
2. [Create a connection](https://cloud.ibm.com/docs/security-compliance?topic=security-compliance-setup-caveonix&interface=ui#caveonix-create-connection)
3. [Create an attachment](https://cloud.ibm.com/docs/security-compliance?topic=security-compliance-setup-caveonix&interface=ui#caveonix-attachment)

## Caveonix Cloud tasks
{: #caveonix-scc-integration}

Complete the following steps to configure your Caveonix Cloud to integrate with your Security and Compliance Center instance and view VMware findings in the Security and Compliance Center dashboard.

Before you start the Caveonix Cloud configuration, you need the following information from when you created the Security and Compliance Center attachment in the previous steps:

* Provider Type Instance ID - This ID is in a format like `9fca0e468f9edb36868b4c02f18952ee` and is available on the Integrations page in Security and Compliance Center for the connection you created in a previous step.
* Endpoint - The Security and Compliance Center endpoint can be either public or private. The format that is required for Caveonix Cloud is just the base address and not the full URL provided on the Security and Compliance Center Integrations page for the connection you created in a previous step. For example, the private endpoint in us-south is `https://private.us-south.compliance.cloud.ibm.com`
* Security and Compliance Center instance ID - This ID can be found from the full endpoint URL and it has a format `https://private.us-south.compliance.cloud.ibm.com/instances/<Security_and_Compliance_Center_instance_ID>/v3/provider_data`. For example, `6bc66f11-171c-4b8b-b2ba-edaa81805011`
* Attachment ID - The attachment ID can be found on the Security and Compliance Center Integrations page and it has a format similar to this example: `417a4a07-9a20-454c-8bf3-9d2ad8043690`

It is assumed that your Caveonix Cloud instance was deployed by the {{site.data.keyword.vmwaresolutions_short}} automation and the following steps are completed in Caveonix Cloud:

* An Organization is created.
* A VMware Asset Repository is created.
* A VMware Infrastructure Compliance Scan Job is scheduled and run.

If you are using a proxy, then it is deployed and configured and you updated the Caveonix Cloud central collector by completing the following steps:

1. Edit the Central Collector application.properties file at `/bin/caveonix/centralcollector/application.properties`
2. Remove the `#` from the following parameters and inserted the required values of your proxy in the following lines:

   ```text
   #proxy.url=
   #proxy.port=
   #proxy.user=
   #proxy.pass=
   ```

3. Save the `/bin/caveonix/centralcollector/application.properties` file and restart the Central Collector service by using `sudo systemctl restart centralcollector`

The following tasks are performed on your Caveonix Cloud instance:

1. Configure the Security and Compliance Center integration in the Event Log Collector module. The event log collector provides authentication information to submit infrastructure findings to the Security and Compliance Center. You need the following details when you configure an Event Log Collector module:
   * Security and Compliance Center URL
   * Security and Compliance Center Instance ID
   * Attachment ID
   * Provider Type Instance ID
   * API key

   Currently, Caveonix Cloud supports one event log collector per instance.
   {: note}

2. Create a Security and Compliance Center Batch Job. This batch job collects infrastructure vulnerabilities to identify security risks. This job posts the VMware infrastructure findings (NSX-T, ESXi, and vCenter Server) to your Security and Compliance Center instance. Findings are posted to your Security and Compliance Center instance in batches of 100. This batch job submits the infrastructure findings periodically, at the wanted frequency, for example, once a day.

## Viewing VMware findings in the Security and Compliance Center dashboard
{: #caveonix-scc-view}

When integrated, your Caveonix Cloud provides a centralized management platform for VMware Infrastructure findings in your Security and Compliance Center dashboard. On the dashboard, the Caveonix Cloud attachment is shown in the Detailed Results section. When you select this attachment, the following information is displayed:

* Overview - The Overview tab provides a graphical representation of your compliance for your selected scan.
* Controls - The Controls tab provides an overview of the controls that were evaluated. The controls and their compliance status are listed for the time that the scan was done.
* Resources - The Resources tab provides a view of the results for each evaluated resource.

When you are reviewing the details on the dashboard, be aware of the following information:

* Your vCenter Server instance includes three NSX managers in a load-balanced cluster. Caveonix Cloud is configured with an asset repository, which points to the FQDN of the load balancer and so is registered as an infrastructure asset type. As the load-balancer points to an NSX manager, it gets registered as an infrastructure asset type. The other two NSX managers get registered as VM asset types. Caveonix Cloud sends findings only for assets of the infrastructure type, which includes the ESXi hosts, vCenter Server, and the two entries for NSX Manager.
* Caveonix Cloud registers the vCenter Server infrastructure components as vCenter, NSX, ESXi, or ESX-VM. The ESXi-VM category is used for the VMs hosted on the ESXi hosts. Within Security and Compliance Center, if there are more findings for VMs on the host than for the ESXi host itself, then Security and Compliance Center displays ESXi-VM rather than ESXi.
* The number of total, passed, and failed findings might differ when viewed in Security and Compliance Center and Caveonix Cloud. This is due to the way that Security and Compliance Center summarizes the results from Caveonix Cloud. In Caveonix Cloud, the findings for each VM hosted on the ESXi host is counted whereas in Security and Compliance Center only a single finding from all VMs hosted on the ESXi host is counted. If there are 4 VMs that pass and 1 VM that fails then Security and Compliance Center summarizes this as 1 failure. Additionally Caveonix Cloud has a finding status of warning and Security and Compliance Center does not, therefore, these findings are not displayed in Security and Compliance Center.
* Currently, the fix to the findings is not displayed in the Security and Compliance Center. To see the fix, log in to Caveonix Cloud.

## Related links
{: #caveonix-scc-related}

* [Caveonix RiskForesight on {{site.data.keyword.cloud_notm}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
* [Getting started with Security and Compliance Center](/docs/security-compliance?topic=security-compliance-getting-started&interface=ui)
* [Caveonix website](https://caveonix.com/){: external}
