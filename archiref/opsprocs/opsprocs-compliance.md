---

copyright:

  years:  2016, 2024

lastupdated: "2024-07-29"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Compliance
{: #opsprocs-compliance}

Compliance is a set of requirements necessary to meet the minimum controls established by either a regulatory agency or industry best practices. Regularity compliance frameworks are usually broad frameworks that provide guidance on a broad range of technology, whereas industry best practices from vendors are typically technology specific to address technological risks.

The VMware Security Hardening Guides provide prescriptive guidance on how to deploy and operate VMware products in a secure manner. Guides for vSphere are provided in spreadsheet format, with rich metadata to allow for guideline classification and risk assessment. They also include script examples for enabling security automation. Comparison documents are provided if the list changes in guidance in successive versions of the guide.

Many of the controls that are documented in the VMware® Security Hardening Guides are incorporated in the {{site.data.keyword.vmwaresolutions_full}} reference architecture and therefore, automatically deployed, ensure that you tailor the security posture of the platform to your own needs and enterprise policy. The VMware Security Hardening Guides provide the technology-specific controls that are required for you to complete this review. Caveonix RiskForesight automates this compliance task and provides additional regulatory agency guidance.

VMware Aria® Operations™ Manager provides monitoring of VMware objects for violations against the compliance rules in the vSphere Security Configuration Guide. The compliance alerts trigger on the {{site.data.keyword.vcf-auto}} instance, hosts, virtual machines, distributed port groups, or distributed switches, allowing the investigation of the compliance violation. For Health Insurance Portability and Accountability Act (HIPAA) and Payment Card Industry Data Security Standard (PCI DSS) compliance, you can download VMware Aria Operations Manager Compliance Packs from the VMware Solutions Exchange website, licensed, and installed. These Compliance Packs provide Alerts, policies, and Reports to validate the vSphere resources against the HIPAA and PCI hardening guides.

## Related links
{: #opsprocs-compliance-links}

* [FortiGate Security Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fsa_considerations)
* [FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations)
* [F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)
* [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations)
* [Operations Management on {{site.data.keyword.cloud_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-opsmgmt-intro)
* [VMware security hardening guides](https://www.vmware.com/solutions/security/hardening-guides){: external}
