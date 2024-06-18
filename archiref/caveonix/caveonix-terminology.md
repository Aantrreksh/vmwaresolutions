---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Glossary of Caveonix terms
{: #caveonix-terminology}

This glossary provides some descriptions for terms that are associated with the Caveonix RiskForesight™ solution:

* **NIST Special Publication 800-53** - A Risk Management Framework that address security control.
* **Security Content Automation Protocol (SCAP)** - A method for using specific standards to enable the automated vulnerability management, measurement, and policy compliance evaluation of systems deployed in an organization. Checklists standardize and enable automation of the linkage between computer security configurations and the NIST Special Publication 800-53 controls framework.
   * The National Vulnerability Database (NVD) is the US government content repository for SCAP.
   * SCAP allows security administrators to scan computers, software, and other devices based on a predetermined security baseline. The scans determine whether the configuration and software patches are implemented to the standard that they are being compared to.

Review the following SCAP components:
* Common Vulnerabilities and Exposures (CVE) - A list of publicly known cybersecurity vulnerabilities.
* Common Configuration Enumeration (CCE) – A list of security-related system configuration issues.
* Common Platform Enumeration (CPE) - A structured naming scheme for information technology systems, software, and packages.
* Common Weakness Enumeration (CWE) – A list of common software security weaknesses.
* Common Vulnerability Scoring System (CVSS) - Provides a way to capture the main characteristics of a vulnerability and produce a numerical score that reflects its severity.
   * Extensible Configuration Checklist Description Format (XCCDF) - A specification language for writing security checklists, benchmarks, and related kinds of documents. An XCCDF document represents a structured collection of security configuration rules for some set of target systems.
   * Open Vulnerability and Assessment Language (OVAL) – A language that is used to encode system details, and an assortment of content repositories. The language standardizes the three main steps of the assessment process:
      * Representing configuration information of systems for testing.
      * Analyzing the system (vulnerability, configuration, and patch state)
      * Reporting the results of this assessment.
* **Security Technical Implementation Guide (STIG)** - A cybersecurity methodology for standardizing security protocols within networks, servers, computers, and logical designs to enhance overall security. When these guidelines are implemented, they enhance security for software, hardware, physical, and logical architectures to further reduce vulnerabilities.
* **Service Provider** - The top-level organization.
* **Cloud Provider** - Provides the infrastructure that the software-defined cloud operates on. RiskForesight can be configured for multiple Cloud Providers.
* **Organizations** - Tenant organizations and suborganizations of the service provider. If the asset repository is VMware vCenter® Server Appliance (VCSA), the organization or tenant list must be created manually.
* **Roles** - Pre-configured roles and service provider-created roles. Preconfigured roles are not editable by the service provider.
* **Organization Users** - Users of the Tenant Organizations and Sub-Organizations.
* **Asset Repository** - An integration point that enables RiskForesight to synchronize the current asset across the CSP (Cloud Service Provider) management zone and customer zone. The current version of RiskForesight supports the synchronization for VMware® Cloud Director and VCSA. It also supports data collection from VMware NSX® Manager. Assets are collected from the Asset Repository. The Service Provider assigns Assets that are collected from VCSA to Tenant Organizations and Sub-Organizations of the Service Provider. An Asset can be assigned only to one Organization.
* **Remote Access** - Provides end machine credentials to enable scans for vulnerability and compliance monitoring and to collect system events logs. The Service Provider can enable remote access for their own assets only. Tenants have control over remote access from their Assets.
* **Applications and Subapplications** - A logical way to group assets. Example application - SAP. Example subapplications - SAP Front End, SAP Middle Tier, and SAP Back End.
* **Locations** - Assets are uniquely grouped by Location, Cloud Provider, and Asset Repository.
* **Environments** - A way to group Assets and Applications. Each Environment is assigned a risk factor 1 - 10. This factor is applied in the risk score calculation. Service Provider defines the Environments
* **Tasks** - They are used in RiskForesight to complete the following actions:
   * Periodically synchronize the asset repository with RiskForesight.
   * Perform SCAP vulnerability and compliance scans.
   * Collect network flows and other information that uses NSX scans.
   * Collect information about the software that runs on monitored assets.
   * Collect syslog and system events for assets.
* **Task Types** - The following tasks are supported:
   * **VMware vCenter Scan** - Collects Assets from vCenter.
   * **VMware VCD Scan** - Collects Assets from VCD.
   * **VMware NSX Scan** - Collects network information and network flow from NSX Manager.
   * **SCAP Scan** - This scan type is used for scanning workloads for compliance risk and cyberrisk. This scan is based on the SCAP (Security Content Automation Protocol). Future releases are planned to support custom content in the OVAL format.
   * **Software Scan** - This scan collects the software inventory that is installed on the target workload under management. This inventory is then available for search through the search option on the user interface.
   * **LogExtract** - This scan supports log collection from Microsoft® Windows and Linux® workloads. The results are used for forensics purposes and ingested through machine learning to produce useful information.
   * **AMQP Task** - This AMQP task is used for collecting live events from the VCD to enable real-time sync. RiskForesight consumes Asset add, delete, and update events and acts on these events. For example, if a new asset gets added and RiskForesight received that notification through AMQP then it updates the database immediately and starts the compliance risk and cyberrisk scan.
   * **VMware Infrastructure Scan** - This scan carries out an infrastructure scan of the VMware Assets.
   * **VMware Vulnerability Scan** - This scan carries out a Vulnerability scan of the VMware Assets.
* **Compliance Regime** - Available through license; NIST, NESA, PCI, ISO, HIPAA, GDPR, Custom, FFIEC, FedRAMP Low, FedRAMP Moderate, FedRAMP High
* **Policy Manager** - The Policy Manager serves the policy creation function for an Organization based on the machine learning output. Caveonix provides three types of machine learning jobs per organization, which are noneditable. Additional jobs are not supported yet.

   The following jobs are currently supported:
   * Caveo Logs
   * Caveo Networks
   * Caveo Scan

* **Anomaly** - Based on the anomalies that are found in the data, you can configure the policies act based on the user-defined conditions. You can select the job type and configure Boolean conditions for the anomaly score and you can define an action when the condition is true.

See the following example:
```text
Job: "Caveo Logs" Anomaly score is > 90 then Mark asset for quarantine and send Notification to slack Channel.`
Job: "Caveo Network" Anomaly score is > 95 then quarantine the asset and send email notification and also send UI notification.
```
