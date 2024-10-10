---

copyright:

  years:  2024

lastupdated: "2024-10-10"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Architecture patterns for integrating {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection with VMware Cloud Foundation deployment in VPC
{: #arch-pattern-vcf-sccwpp}

This architecture pattern describes how to use {{site.data.keyword.cloud}} Security and Compliance Center Workload Protection with an {{site.data.keyword.vcf-vpc}} deployment in VPC (Virtual Private Cloud).

Security and Compliance Center Workload Protection offers functions to protect your Microsoft Windows® and Linux® virtual machines (VMs) that are hosted on your VMware® environment. These functions include compliance, vulnerability scanning, and threat detection.

Currently, only the threat detection feature is available for Windows VMs.
{: restriction}

Although Security and Compliance Center Workload Protection offers functions for your other {{site.data.keyword.cloud_notm}} services, these functions are not discussed in this pattern. For more information, see [Getting started with {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection](/docs/workload-protection?topic=workload-protection-getting-started).

{{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection implements Sysdig Secure functions. Information that is provided by the Sysdig Secure documentation also applies to Workload Protection.
{: note}

After you provision an instance of the Security and Compliance Center Workload Protection service, you can deploy the agent on your Windows VMs or you can deploy the agent and host scanner on your Linux VMs. The agent collects data that you can use for intrusion detection, while the host scanner is used for posture management and vulnerability scanning capabilities.

## Overview of {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection for VMware workloads
{: #arch-pattern-vcf-sccwpp-overview}

{{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection enables the following three practices for your VMware workloads:

* Threat detection - Threat detection is managed by defining policies, which consist of rules to detect and respond to security violations, suspicious behavior, or anomalous activities within your Windows and Linux VMs. Security and Compliance Center Workload Protection provides customizable, prebuilt policies, which are created and maintained by Sysdig’s Threat Research team. These policies can detect and prevent various security threats, such as: malware, intrusions, and DDoS attacks. The results of these policies can be viewed in Events. For more information, see [Secure Events](https://docs.sysdig.com/en/docs/sysdig-secure/secure-events/){: external}.
* Vulnerabilities - Security and Compliance Center Workload Protection provides a highly accurate view of the vulnerability risks of your Linux VMs. The views include rich details on your vulnerability risks, such as: CVSS vector, score, fix age, and insights from multiple expert feeds including the NIST National Vulnerability Database (NVD) and VulnDB.
* Compliance - Posture management provides the framework that includes controls, guidelines, benchmarks, and standards for managing compliance. With Security and Compliance Center Workload Protection, you can evaluate your Linux VMs against several CIS benchmarks such as CIS Distribution Independent Linux Benchmark and compliance policies. For more information, see [Analyzing compliance postures from detection to remediation](/docs/workload-protection?topic=workload-protection-compliance). Typical use cases include:
   * Check the current compliance status against predefined policies to understand the magnitude of the compliance gap.
   * Demonstrate to an auditor the compliance status at a specific point in time, by creating a report of the compliance status of the VMs.

## Pattern for integrating {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection
{: #arch-pattern-vcf-sccwpp-vcs}

The following diagram shows an example of integrating a VMware Cloud Foundation deployment in VPC with {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection.

![Pattern for integrating Security and Compliance Center Workload Protection ](../../images/arch-pattern-scwpp-vcf.svg "Security and Compliance Center Workload Protection."){: caption="Security and Compliance Center Workload Protection" caption-side="bottom"}

This architecture pattern is summarized as follows:

1. The agents, which are installed on your Windows or Linux VMs, collect data that is used for threat detection, posture management, and vulnerability scanning. For more information, see [Sysdig Agents](https://docs.sysdig.com/en/docs/sysdig-secure/integrations-for-sysdig-secure/data-sources/sysdig-agents/){: external}. The Sysdig Secure Windows Agent provides runtime detection and policy enforcement for host processes on Windows. For more information, see [Windows Hosts](https://docs.sysdig.com/en/docs/installation/sysdig-secure/install-agent-components/windows-host/){: external}. For Linux VMs, the agent has two parts:
   * Agent - Runtime threat detection is provided by the agent, which processes syscall events and metrics, creates capture files, and performs auditing and compliance tasks. For more information about deploying the agent, see [Sysdig Agent](https://docs.sysdig.com/en/docs/installation/sysdig-secure/install-agent-components/hosts/packages/sysdig-agent/){: external}.
   * Vulnerability Host Scanner - The host scanner is used to scan for vulnerabilities on the Linux VM. For more information about deploying the host scanner, see [Vulnerability Host Scanner](https://docs.sysdig.com/en/docs/installation/sysdig-secure/install-agent-components/hosts/packages/vulnerability-host-scanner/){: external}.
2. Your DNS servers need to be able to resolve the Security and Compliance Center Workload Protection endpoint URLs. Configure your DNS servers to use {{site.data.keyword.cloud_notm}} DNS resolvers, if needed.
3. Firewall rules enable the downloading of the agents from the Internet and HTTPS connectivity to the Security and Compliance Center Workload Protection private endpoints. For more information about configuring firewall rules, see [Add a Gateway Firewall Policy and Rule](https://docs.vmware.com/en/VMware-NSX/4.1/administration/GUID-DE6FE8CB-017E-41C8-85FC-D71CF27F85C2.html){: external}.
4. The routing between your VMs and the services that are attached to VPC. For more information, see [Private traffic between Tier-0 and VPC](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-nsx-t-vpc-routing#vpc-vcf-nsx-t-vpc-routing-edge-tier-0-routing-private).
5. The {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection instance. For more information, see:
   * [Provisioning an instance](/docs/workload-protection?topic=workload-protection-provision)
   * [Regions](/docs/workload-protection?topic=workload-protection-regions)
   * [Protecting Linux hosts](/docs/workload-protection?topic=workload-protection-protecting-linux-hosts)
   * [Endpoints](/docs/workload-protection?topic=workload-protection-endpoints)

Agents can be installed as a docker container or as a package installed on the operating system. This pattern assumes the use of an operating system package. References in Sysdig Secure and {{site.data.keyword.cloud_notm}} Cloud Security and Compliance Center Workload Protection documentation to Host Analyzers and Kubernetes Security Posture Management can be ignored when a package is used.
{: note}

## Considerations
{: #arch-pattern-vcf-sccwpp-considerations}

When you design or deploy this architecture pattern, consider the following information:

* For Linux VMs, the agents log file is `/opt/draios/logs/draios.log`.
* This pattern describes firewall policies and SNAT configured on the T0. Use of the T1 is also possible.
* This pattern does not use the distributed firewall. For more information about configuring the distributed firewall, see [FQDN Filtering](https://docs.vmware.com/en/VMware-NSX/4.1/administration/GUID-63262728-CA72-47D2-8E4F-16617B63A9A4.html){: external}.

## Related links
{: #arch-pattern-vcf-sccwpp-links}

* [Getting started with {{site.data.keyword.cloud_notm}} Security and Compliance Center Workload Protection](/docs/workload-protection?topic=workload-protection-getting-started)
* [Sysdig Secure](https://docs.sysdig.com/en/docs/sysdig-secure/){: external}
