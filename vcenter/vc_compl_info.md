---

copyright:

  years:  2016, 2024

lastupdated: "2024-09-18"

keywords: vcf automated compliance, compliance info, vcf automated policy

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Compliance information for {{site.data.keyword.vcf-auto-short}}
{: #vc_compl_info}

Review the following information for details about compliance for {{site.data.keyword.vcf-auto}} instances.

## Customer versus IBM responsibility for {{site.data.keyword.vcf-auto-short}}
{: #vc_compl_info-responsibility}

The following diagram provides details about the customer (you) and {{site.data.keyword.IBM}} responsibilities for compliance activities.

![Customer versus IBM responsibility matrix](../images/customer_ibm_responsibility_matrix.svg "Customer versus IBM responsibility matrix"){: caption="Figure 1. Customer versus IBM responsibility matrix for {{site.data.keyword.vcf-auto-short}}" caption-side="bottom"}

## Health data restrictions
{: #vc_compl_info-health-data-restrictions}

The following terms apply only to the {{site.data.keyword.vcf-auto-short}} offering.

### HIPAA
{: #vc_compl_info-hipaa}

Notwithstanding information in the data sheet for this Cloud Service regarding the Health Information Portability and Accountability Act of 1996 ("HIPAA") and the permitted use of Health Information and Health data as Types of Personal Data and Special Categories of Personal Data (collectively, "Health Data") with this Cloud Service, use of Health Data with this Cloud Service is subject to the following limitations and conditions:

vCenter Server

Only the offerings that are previously listed can be provisioned to implement the HIPAA Privacy and Security Rule controls for use with Health Data if Client notifies IBM in advance that Client will use Health Data with the Cloud Service and IBM confirms in writing that the Cloud Service will be provisioned for Health Data usage. The Cloud Service cannot be used for the transmission, storage, or other usage of any Health Data protected under HIPAA unless (i) Client provides IBM such notification; (ii) IBM and Client have entered into an applicable Business Associate Agreement; and (iii) IBM provides Client with express- written confirmation that the Cloud Service can be used with Health Data. In no event, shall the Cloud Service be used for processing PHI as a healthcare clearinghouse within the meaning of HIPAA.

If a system failure occurs, a third-party service provider might request debugging artifacts from the client (logs, core memory dumps). It is the client’s sole responsibility to gather and transmit these artifacts to the third-party provider. The IBM support team might assist by providing links to documentation or providing direction through screen sharing sessions. However, the client is responsible for cleansing the data of any PHI and ensuring that it is properly encrypted before it is transmitted. It is also the client’s responsibility to evaluate whether they require a BAA to be executed with the third-party provider before data is sent.

## Personal information and regulated data
{: #vc_compl_info-personal-info-and-regulated-data}

This Cloud Service is not designed to any specific security requirements for regulated content, such as personal information or sensitive personal information. Client is responsible to determine whether this Cloud Service meets Clients needs regarding the type of content Client uses in connection with the Cloud Service.

## Policy configurations
{: #vc_compl_info-default-policy-config}

For V3.1 or later, the generated password for {{site.data.keyword.vcf-auto-short}} primary instances is 15 characters in length. Previously, the generated password was the vCenter Server default value of 8 characters in length.

The following table details vCenter Server policy configurations for a new primary instance.

| Policy | V3.1 or later | V3.0 or earlier |
|:------------- |:------------------------------ |:------------- |
| vCenter password policy | Minimum length of 15 characters | Minimum length of 8 characters (vCenter default) |
| vCenter lockout policy | Maximum of three failed login attempts | Maximum of five failed login attempts (vCenter default) |
| vCenter lockout policy | 900 seconds between login failures | 180 seconds between login failures (vCenter default) |
{: caption="Table 1. vCenter policy configurations" caption-side="bottom"}

The generated NSX Manager password for {{site.data.keyword.vcf-auto-short}} primary instances is 15 characters in length. Previously, the generated password was 8 characters in length.

## Policy for accessing clients instances
{: #vc_compl_info-policy-for-access-client-inst}

vCenter Server environments, which are delivered as {{site.data.keyword.vmwaresolutions_short}}, provide a VMware® management platform layer for our clients to manage the virtualization capabilities. Throughout the lifecycle of {{site.data.keyword.vmwaresolutions_short}} products and services, IBM Support might be required to help guarantee their success. Usually, intervention by IBM Support is the result of a client request (that is, a support ticket). However, on rare occasions, IBM Support might assist proactively and without a client–written support ticket to prevent future issues. This access is through the {{site.data.keyword.cloud_notm}} internal support network and is documented through a support ticket that is opened by IBM Support and continuously monitored by {{site.data.keyword.cloud_notm}} SOC. At no time will IBM Support modify instance configuration without prior consent from the client. The access is to the VMware management components and to the {{site.data.keyword.cloud_notm}} management components and never to the client's virtual machines or applications.

## Proactive support
{: #vc_compl_info-proactive-support}

### Proactive support for initial provisioning
{: #vc_compl_info-proactive-support-for-initial-provision}

* During the initial ordering and provisioning of an instance or service, IBM Support might access client instances and information without prior notification of the client to ensure that orders are properly fulfilled.
* IBM Support actively monitors instance lifecycle operations such as adding new hosts, in addition to the ordering, provisioning, and installation processes.
* To fix issues that arise or might arise in the future, IBM Support might take a number of actions. These actions include, but are not limited to, reviewing client order details, restarting automation jobs, performing operating system reload operations, or opening {{site.data.keyword.cloud_notm}} tickets by using the provided client {{site.data.keyword.cloud_notm}} user ID and API key.

### Proactive support for steady-state operations
{: #vc_compl_info-proactive-support-for-steady-state-operations}

* On rare occasions, IBM Support might require access to client instances during steady-state operations to proactively troubleshoot an instance issue or to verify function of provisioned services or components.
* This access is through the {{site.data.keyword.cloud_notm}} internal support network. At no time will IBM Support modify instance configuration without prior consent from the client.
* Access is to the VMware management components and to the {{site.data.keyword.cloud_notm}} management components and never to the client's virtual machines or applications.

### Support tickets
{: #vc_compl_info-support-tickets}

* vCenter Server environments are not actively monitored by IBM, and IBM Support does not enter the VMware management layer under normal operations without a client–written support ticket.
* When a client opens a support ticket for an instance, service, or provisioning issue, the ticket is quickly assigned to the appropriate IBM Support team, who is the primary party responsible for resolving the issue.
* Due to the level of specialization that is required to maintain superior technical expertise at the team level, it is sometimes necessary to involve more than one support team in resolving a particular software problem. This is easily handled, as our support teams are all networked together and work as one to resolve whatever problems or issues arise.
* To investigate the issue, IBM might need to access information on your system relative to the failure or might need to re-create the failure to get more information.
* A client–generated support ticket serves as acknowledgment that IBM Support can access the VMware management layer for investigation, debugging, and triage. If maintenance outage or changes to the environment are required, IBM Support requests extra-documented confirmation from the client through tickets as part of our change management process.
* For more information about support tickets, see the [IBM Support Guide](https://www.ibm.com/support/pages/ibm-support-guide) and follow the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

## Client responsibilities
{: #vc_compl_info-client-responsibilities}

* While we commend clients that take steps to make their environments more secure, it must be noted that some practices might have adverse effects on the effectiveness of VMware Solutions.
* Clients are accountable for the firewalls that they create and the resulting limitations that are imposed on communications between the VMware Solutions components. These firewalls might also hinder the ability of IBM Support to access client instances and resolve issues. For more information about minimum recommended firewall configuration, see [Ports that are used by VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-vmwaresol_ports-vmwareuses).
* Clients are fully responsible for encrypting the data in their system.
* Upon initial deployment, the offering’s automation and client’s account are separate. The client is allowed and encouraged to change all passwords that IBM provides in the console.
* vCenter access and credentials are created during initial deployments and provided to the client. As part of the requirement of our offering, IBM Support must retain full access to the management layer to provide life–cycle management and support to our clients.
* For more information about the credentials that are used by IBM automation and IBM Support, see [IBM user IDs](/docs/vmwaresolutions?topic=vmwaresolutions-audit_user_ids). By leaving these credentials active, you are granting IBM permission to access the environment for satisfying provisioning requests or providing support as outlined here. You can revoke these credentials to prevent IBM access to the environment. If IBM later needs to satisfy a provisioning request or provide support, you are required to provide updated credentials to IBM Support.
* If credentials such as passwords are changed at any time, IBM Support may no longer be able to help you recover lost or forgotten credentials or even troubleshoot your environments.
* For more information about this issue and related concerns, see [Considerations when changing passwords for NSX components](/docs/vmwaresolutions?topic=vmwaresolutions-vc_networkingonvcenterserver#vc_networkingonvcenterserver-change-nsx-component-password-considerations) and [Considerations about changing vCenter Server artifacts](/docs/vmwaresolutions?topic=vmwaresolutions-vcenter_chg_impact).

### Communication and troubleshooting
{: #vc_compl_info-communication-troubleshooting}

* IBM does not warrant that our products are defect free, however we do endeavor to fix them to work as designed. Clients play a large role in this effort.
* While IBM Support is available to provide assistance throughout the lifecycle of the product, support might be limited by the information and access provided by the client.
* The client is responsible for providing in–depth documentation at the time of a failure and responding timely to IBM Support when further clarification is needed.
* Clients are also responsible for following the guidelines in this document to grant consent to proactive support.
* By declining consent or failing to abide by the guidelines provided, the client assumes the responsibility of possible lag in problem resolution that is caused by communication delays between the client and support team.
* The client must be prepared to perform more technical troubleshooting that would otherwise be done by IBM Support. IBM provides appropriate documentation and assistance where necessary.

### Security measures
{: #vc_compl_info-security-measures}

* Management of Cloud Service - Client is responsible for managing administration, operation, maintenance, and security of the applications, including underlying middleware.
* Service Integrity and Availability - IBM forwards to the Client all network intrusion notifications detected for this Cloud Service. It is the Client’s responsibility to ascertain the impact of each notification that is reported. Client is notified of hardware failures. Monitoring and responding to OS or software failures is the responsibility of the Client, engaging IBM support as required.
* Activity Logging - Client is responsible for activity logging of OS/System and Database/Applications, as needed.
* Encryption - Client is responsible for configuring and managing all encryption (for both data at rest and in transit), as needed.
* Business Continuity and Disaster Recovery - Client is responsible for configuring and managing all business continuity and disaster recovery processes, as needed.

### Third-party services
{: #vc_compl_info-third-party-services}

* Third-party software or code is included or bundled with some of our IBM offerings. This code is included for your convenience but is not considered part of the IBM program.
* These non–IBM programs are licensed directly by their providers. Client agrees to use the non–IBM programs under the provider’s terms and conditions. These terms are provided in the IBM licensing agreement that accompanies the IBM offering at time of purchase.
* IBM does testing to ensure that the third-party products work with IBM programs and that they function correctly.
* IBM Support diagnoses client problems by using the knowledge of how our IBM offerings work with the third-party software. After it is concluded that the IBM program is working correctly, but the issue still exists, IBM must refer the client to the third-party vendor for further diagnosis.
* For more information about client responsibilities regarding third-party software or code, see the [IBM Support Guide](https://www.ibm.com/support/pages/ibm-support-guide).

## Consent to accessing client environments
{: #vc_compl_info-consent-to-access-client-environment}

* IBM Support requires access to client instances to ensure their proper provisioning and upkeep. Clients are responsible for controlling and providing the access that is required.
* A client–written support ticket serves as acknowledgment of and consent to IBM Support accessing a client instance to address the concerns that are described in said support ticket.
* Clients are responsible for following the guidelines in this document to grant consent to proactive support. By declining consent or failing to abide by the guidelines provided, the client assumes the responsibility of delays in problem determination and solution that is caused by communication delays between the client and support team and possible more technical troubleshooting.

## Initial provisioning
{: #vc_compl_info-initial-provision}

* At the time of initial provisioning and ordering, the client is presented with this document.
* By submitting the order, the client agrees to these terms and thus grants consent to IBM Support to access their instances at any time without prior notification to swiftly resolve issues that pertain to the environment or to prevent future failures.
* This consent applies to all instances currently being ordered throughout their lifecycle. Instances and instance components that are provisioned in the future might require extra consent.

## Steady-state operations
{: #vc_compl_info-steady-state-operations}

If the client does not grant consent to proactive support for an instance in the initial provisioning and ordering, they must include explicit consent in any future service tickets, if wanted. Statements of consent must follow the set guidelines or are considered void.

## Related links
{: #vc_compl_info-related}

* [{{site.data.keyword.vcf-auto-short}} overview](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
