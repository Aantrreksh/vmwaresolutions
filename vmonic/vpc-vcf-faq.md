---

copyright:

  years:  2023, 2024

lastupdated: "2024-04-15"

keywords: vmware cloud foundation, IBM Cloud, vpc, faq

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# General FAQ about {{site.data.keyword.vcf-vpc-short}}
{: #vpc-vcf-faq}

## I am not used to {{site.data.keyword.vcf-vpc-short}} and it uses new terms for me, where can I get more information?
{: #vpc-vcf-faq-vcf-glossary}
{: faq}

You can use the VMware Cloud Foundation™ documentation for most Day 2 operations. For more information, see [About getting started with {{site.data.keyword.vcf-vpc-short}}](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-getting-started/GUID-F77789E2-5A3E-4055-AA4D-904DB2DDC8C3.html?hWord=N4IghgNiBcIG4FsDuYBOBTABAYwgewFcATTAM0IDsiwAXASzwpAF8g){: external}.

Exceptions apply, some of which are documented in this FAQ. If you need assistance for the administration of your {{site.data.keyword.vcf-vpc}} instance, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

To understand the terms used in VMware Cloud Foundation 4.5.x, see [VMware Cloud Foundation glossary](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-2AC7AC13-2A70-478D-AE6B-6193BAEB793D.html){: external}.

## How can I reduce or expand my {{site.data.keyword.vcf-vpc-short}} instance capacity?
{: #vpc-vcf-faq-expanding-capacity}
{: faq}

You can add or remove hosts to the cluster by using the VMware Solutions console. The minimum number of hosts per cluster is 4 and the maximum is 25.

Adjust the VMware Cloud Foundation management and workload host pool sizes when you deploy the instance.
{: note}

## Can I have more than one VI Workload Domains in my {{site.data.keyword.vcf-vpc-short}} instance?
{: #vpc-vcf-faq-domains-limitations}
{: faq}

Currently, only one VI Workload Domain is supported.

## Can I have more than a cluster per Workload Domain?
{: #vpc-vcf-faq-domains-clusters}
{: faq}

Currently, only one cluster per Domain is supported. This limitation is valid for both Management and Workload Domains.

## How do I keep my {{site.data.keyword.vcf-vpc-short}} instance software up to date?
{: #vpc-vcf-faq-vcf-updates}
{: faq}

SDDC Manager automates the entire system lifecycle, that is, from configuration and provisioning to upgrades and patching. SDDC Manager is connected to the VMware Depot after initial provisioning. You can select the bundles to download and you can apply updates and upgrades on your own.

Before you complete an update, review the release notes and the FAQ section.

## Can I upgrade my VMware Cloud Foundation 4.5.2 to version 5.x?
{: #vpc-vcf-faq-upgrade-5-0}
{: faq}

Yes. For more information, see [VMware Cloud Foundation 5.0 – Important information and knowledge base articles](https://kb.vmware.com/s/article/91751){: external}.

## What is the Async Patch tool and how can I use it with my {{site.data.keyword.vcf-vpc-short}} instance?
{: #vpc-vcf-faq-async-patch}
{: faq}

You can use the Async Patch tool to apply critical patches to certain VMware Cloud Foundation components (VMware NSX Manager, VMware vCenter Server, and VMware ESXi) outside of {{site.data.keyword.vcf-vpc-short}} releases.

For example, you can use the Async Patch tool to get a vCenter Server patch that addresses a critical security issue as described in a VMware Security Advisory (VMSA). You can use the Async Patch tool to download the patch and upload it to the internal LCM repository on the SDDC Manager appliance. Then, you use the SDDC Manager UI to apply the patch to your instance.

As the {{site.data.keyword.vcf-vpc-short}} instance does not provide you with the credentials to log in to VMware software depot, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support). The {{site.data.keyword.cloud_notm}} Support team can provide you access to these Async Patch bundles.
{: important}

For more information, see [Async Patch tool](https://docs.vmware.com/en/VMware-Cloud-Foundation/services/ap-tool/GUID-49818DF1-94EA-4C85-8CB6-6EFFCE5F8060.html){: external}.

## How do I keep the Aria Suite software in my {{site.data.keyword.vcf-vpc-short}} instance up to date?
{: #vpc-vcf-faq-aria-updates}
{: faq}

In {{site.data.keyword.vcf-vpc-short}}, VMware Aria Suite Lifecycle Manager (formerly vRealize Suite Lifecycle Manager) provides lifecycle management capabilities for Aria Suite components and VMware Workspace ONE Access, including automated deployment, configuration, patching, and upgrade, and content management across these products. Aria Suite Lifecycle Manager is deployed as part of the automation.

For more information about the Aria Suite supported upgrade paths in VMware Cloud Foundation, see [vRealize Suite (Aria Suite) install and upgrade paths on VMware Cloud Foundation](https://kb.vmware.com/s/article/88829){: external}.

## How do I manage certificates in Aria Suite installations?
{: #vpc-vcf-faq-aria-certificates}
{: faq}

For Aria Suite (formerly vRealize Suite) certificates, you must manually generate self-signed certificates in Aria Suite Lifecycle Manager (formerly vRealize Suite Lifecycle Manager).

For more information about how to generate self-signed certificates in vRealize Suite Lifecycle Manager (currently Aria Lifecycle Manager) 8.8.2P6, see [Replace the certificate of the vRealize Suite Lifecycle Manager instance](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/com.vmware.vcf.vxrail.doc/GUID-DC03F8FF-543E-46D2-AFCF-1468EA966B63.html?hWord=N4IghgNiBcIOYFMB2CBOYAuCAEBnAlnCgCbYBuquEAxgLYgC+QA){: external}.

## How do I manage certificates in SDDC manager?
{: #vpc-vcf-faq-sddc-certificates}
{: faq}

You can use the SDDC Manager UI to manage certificates in a {{site.data.keyword.vcf-vpc-short}} instance, including integrating a certificate authority, generating and submitting certificate signing requests (CSR) to a certificate authority, and downloading and installing certificates.

For more information, see [Managing certificates in VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-80431626-B9CD-4F21-B681-A8F5024D2375.html?hWord=N4IghgNiBcIMYFMBOAXAlgMzXMKEgF8g){: external}.

Starting with the VMware Cloud Foundation 4.4 release, SSH Service on ESXi hosts is disabled on new and upgraded VMware Cloud Foundation deployments. You must enable the SSH service for each ESXi host.
{: important}

## Can I add edge nodes to an NSX Edge Cluster?
{: #vpc-vcf-faq-nsx-edge-nodes}
{: faq}

In {{site.data.keyword.vcf-vpc-short}} instances, the High Availability setting for and Tier 0 Gateway is set as Active-Standby and uses HA VIP. For this reason, the process that is documented in [Add edge nodes to an NSX edge cluster](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-ED90A614-B670-4E1C-9143-82896F147F74.html){: external} cannot be used.

When you deploy the solution, it is recommended to select a large enough NSX and edge node size.

## Can I deploy more clusters in another zone in my {{site.data.keyword.vpc_short}} instance?
{: #vpc-vcf-faq-vpc-zones}
{: faq}

Currently, {{site.data.keyword.vcf-vpc-short}} instances support {{site.data.keyword.vcf-vpc-short}} deployments with a Single Availability Zone. One vCenter Server is deployed to the Management Domain and that vCenter and its ESXi hosts provide the compute capacity to all management components for the SDDC, such as the SDDC Manager, vCenter for the Workload Domain and the NSX Manager clusters for management and workload domains.

## What storage options do I have with my {{site.data.keyword.vcf-vpc-short}} instance?
{: #vpc-vcf-faq-storage}
{: faq}

Currently, for {{site.data.keyword.vcf-vpc-short}} instances, all principal and supplemental storage that is deployed as part of automation is vSAN storage only.

## What are the password policies and how do I manage passwords in {{site.data.keyword.vcf-vpc-short}}?
{: #vpc-vcf-faq-passwords-vcf}
{: faq}

The initial passwords for your {{site.data.keyword.vcf-vpc-short}} instance are randomly generated as part of the provisioning and starting procedure.

During initial deployment, the VMware Solutions automation creates an IBM automation account that is named **ibm_admin**, which will be used only to get your updated password. If you changed the initial password, retrieving the updated password is necessary for running Day 2 operations, such as adding or removing hosts.

We don’t recommend you to change the **ibm_admin** password, but if you changed it, you must follow these steps so that you can complete the Day 2 operations successfully:

1. Go to the {{site.data.keyword.vcf-vpc-short}} instance details page.
2. Click the **Access information** tab and scroll down to the **SDDC Manager** section.
3. Under the **IBM Automation** account, click **Update password** and enter your updated **ibm_admin** password.

For more information about the supported password policies in VMware Cloud Foundation, see [Configuring password complexity policies in VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-operations/GUID-22C6746A-6703-47E5-B17A-313EC959EC62.html){: external}.

You can rotate and update some of these passwords by using the password management functions in the SDDC Manager UI. You can rotate passwords for the following accounts:

* The accounts used for service consoles, such as the ESXi root account.
* The single sign-on administrator account.
* The default administrative user account used by virtual appliances.
* Service accounts that are automatically generated during powering on, host commissioning, and workload creation.

   Service accounts have a limited set of privileges and are created for communication between products. Passwords for service accounts are randomly generated by SDDC Manager. You cannot manually set a password for the service accounts. To update the credentials for service accounts, you can rotate the passwords.

To provide optimal security and proactively prevent any passwords from expiring, rotate passwords every 80 days.

For more information, see:

* [Password management](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-1D25D0B6-E054-4F49-998C-6D386C800061.html?hWord=N4IghgNiBcIA5gM6IO4HsBOATABAWzADswBzAUzzMIBcQBfIA){: external}
* [Password policy configuration for VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-operations/GUID-18A95158-30F5-460F-AF80-33F25B6533D0.html){: external}

## I have an issue with my {{site.data.keyword.vcf-vpc-short}} passwords, what can I do?
{: #vpc-vcf-faq-passwords}
{: faq}

Passwords are shown on the **Access information** tab. These passwords are the passwords that were randomly generated during the provisioning. If you changed the passwords post initial provisioning and you have password issues, you can use SDDC Manager to get these passwords for the components.

SSH into the SDDC manager by using user `vcf`. You can view the passwords by using one of the following mechanisms:

* Using the `lookup_passwords` command on the SDDC manager virtual machine. You can run the command in the following ways:

   * Run the command: `lookup_passwords -u username@domain -p password -e entityType -n pageNo -s pageSize` providing proper values to arguments.
   * Use `lookup_passwords -h` to view help information, which lists details about each of the arguments. Run the command and enter the value when prompted: `lookup_passwords`

* Using password management SDDC APIs:

   1. Request a bearer token to access the APIs: `curl -X POST -H "Content-Type: application/json" -d '{"username": "username@domain","password": "password"}' --insecure https://localhost/v1/tokens | json_pp`
   2. Run the lookup API: `curl -X GET -H "Content-Type:application/json" -H  "Authorization: Bearer <token value>"  'localhost/v1/credentials?resourceType=PSC' | json_pp`

      For more information, see [{{site.data.keyword.vcf-vpc-short}} API reference](https://developer.vmware.com/apis/vcf/4.5.1/credentials/){: external}.

## How do I back up and restore {{site.data.keyword.vcf-vpc-short}} components?
{: #vpc-vcf-faq-operations-backups-vcf}
{: faq}

{{site.data.keyword.vcf-vpc-short}} system backups are configured to use SDDC manager. Backups are configured to use the folder `/nfs/vmware/vcf/nfs-mount/backup` on the SDDC manager. You can change this configuration post-deplyoment to fit your own backup requirements.

For more information about how to back up and restore {{site.data.keyword.vcf-vpc-short}}, see [Backup and restore of VMware Cloud Foundation](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-admin/GUID-F8634D37-FA26-40DF-A135-62D0265DA4FA.html){: external}.

## What are the best practices to operate {{site.data.keyword.vcf-vpc-short}}?
{: #vpc-vcf-faq-operations-best-practice}
{: faq}

For more information about best practices and step-by-step instructions to operate {{site.data.keyword.vcf-vpc-short}}, see [VMware Cloud Foundation operations guide](https://docs.vmware.com/en/VMware-Cloud-Foundation/4.5/vcf-operations/GUID-BE7C1509-709A-4A56-875B-EAC5EA61BB56.html){: external}.
