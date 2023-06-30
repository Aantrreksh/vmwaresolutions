---

copyright:

  years: 2016, 2023

lastupdated: "2023-06-22"

keywords: IBM Cloud for VMware Solutions, getting started, vmware solutions offerings, services for vmwaresolutions, vmwaresolutions use cases

subcollection: vmwaresolutions

content-type: tutorial
services: vmwaresolutions
account-plan: paid
completion-time: 2h

---

{{site.data.keyword.attribute-definition-list}}

# Getting started with VMware Solutions
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-services="vmwaresolutions"}
{: toc-completion-time="2h"}

In this {{site.data.keyword.vmwaresolutions_full}} getting started tutorial, we take you through the process of ordering an instance and some services for it.
{: shortdesc}

## Before you begin
{: #getting-started-prereqs}

Before you start to work with {{site.data.keyword.vmwaresolutions_short}}, review the following important information about browser requirements, users accounts, deployment options, and services.

### Browser requirements
{: #getting-started-browser-req}

For more information, see [Browsers](/docs/overview?topic=overview-prereqs-platform#browsers-platform).

### User accounts
{: #getting-started-user-accts}

You need an {{site.data.keyword.cloud_notm}} account and an {{site.data.keyword.cloud_notm}} infrastructure account. These accounts must meet certain requirements.

| Account | Description |
|:------- |:---------- |
| IBMid | By using the **IBMid**, you can have a single login username for all IBM products and services that you use, including {{site.data.keyword.cloud_notm}}. {{site.data.keyword.vmwaresolutions_short}} is provided as an infrastructure solution in the {{site.data.keyword.cloud_notm}} catalog. To access the {{site.data.keyword.vmwaresolutions_short}} console, you must have an **IBMid**. \n \n To use your **IBMid** to log in to the {{site.data.keyword.vmwaresolutions_short}} console, you must associate the **IBMid** with an {{site.data.keyword.cloud_notm}} account. When you log in to the console for the first time, you are asked to associate your existing **IBMid** with an {{site.data.keyword.cloud_notm}} account, or to sign up for a new {{site.data.keyword.cloud_notm}} account. The new {{site.data.keyword.cloud_notm}} account is automatically associated with your **IBMid**. You go through this process only one time. \n \n If you have problems when you associate your **IBMid** with an {{site.data.keyword.cloud_notm}} account, see [Why is my password incorrect?](/docs/account?topic=account-ts_logintoibm) |
| {{site.data.keyword.cloud_notm}} account | To order and use {{site.data.keyword.cloud_notm}} services, an {{site.data.keyword.cloud_notm}} account is required. Billing information is associated with the {{site.data.keyword.cloud_notm}} account. The price of the physical and virtual infrastructure and the resulting licenses are charged to your {{site.data.keyword.cloud_notm}} account. |
| {{site.data.keyword.cloud_notm}} infrastructure account | For more information, see [The {{site.data.keyword.cloud_notm}} infrastructure account](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts#signing_required_accounts-infra). \n \n You can link {{site.data.keyword.cloud_notm}} infrastructure accounts with {{site.data.keyword.cloud_notm}} accounts to use combined infrastructure as a service (IaaS) and platform as a service (PaaS) resources. Then, you can access IaaS resources and PaaS resources from a single login. Linking your accounts also provides you with a single invoice for all the PaaS and IaaS resources that you use. \n \n If you do not have an {{site.data.keyword.cloud_notm}} infrastructure account, request one by following the procedure in [Signing up for an {{site.data.keyword.cloud_notm}} infrastructure account](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts#signing_required_accounts-infra), and then link your {{site.data.keyword.cloud_notm}} infrastructure account with your {{site.data.keyword.cloud_notm}} account by following the procedure in [Upgrading your account](/docs/account?topic=account-upgrading-account). \n \n If you have an {{site.data.keyword.cloud_notm}} infrastructure account, you can link it with your {{site.data.keyword.cloud_notm}} account by following the procedure in [Upgrading your account](/docs/account?topic=account-upgrading-account).
{: caption="Table 1. Required user accounts" caption-side="bottom"}

### Deployment offerings
{: #getting-started-depl-offerings}

Review and choose your deployment offering.

| Deployment offering | Description |
|:------------------- |:----------- |
| [VMware as a Service](/docs/vmwaresolutions?topic=vmwaresolutions-vmware-aas-overview) | This offering provides the VMware Cloud Director platform as a managed service. IBM® performs the configuration, hosting, operations, and lifecycle management of the VMware® software so you can quickly deploy your VMware-based cloud computing environments. |
| [VMware Shared](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview) | This offering provides standardized and customizable deployment choices of VMware® virtual data center environments. |
| [VMware vSphere®](/docs/vmwaresolutions?topic=vmwaresolutions-vs_vsphereclusteroverview) | This offering provides a customizable virtualization service that combines VMware-compatible bare metal servers, hardware components, and licenses, to build your own IBM-hosted VMware environment. |
| [VMware vCenter Server](/docs/vmwaresolutions?topic=vmwaresolutions-vc_vcenterserveroverview) | This offering allows you to deploy a VMware virtual environment by using custom compute, storage, and network resources to best fit your business needs. |
| [VMware Regulated Workloads](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-overview) | This offering includes a secure-by-default architecture that follows IBM's unique policy controls framework, it provides continuous compliance monitoring, and the highest level of data encryption (FIPS 140-2 Level 4). |
| [Cyber Recovery](/docs/vmwaresolutions?topic=vmwaresolutions-cr_overview) | This offering provides air-gapped protection, immutable storage, and rapid recovery of applications and data for ransomware protection. |
{: caption="Table 2. Deployment offerings" caption-side="bottom"}

### Add-on services
{: #getting-started-add-on-services}

Review and choose services for your deployment.

#### Security and compliance services
{: #getting-started-serv-sec-compl}

The following table describes the security and compliance services that are available.

| Service name | Description |
|:------------ |:----------- |
| [Caveonix RiskForesight™](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations) | This service manages cyberrisk and compliance risk with proactive monitoring and automated defense controls to protect against threats and to meet industry or government regulations. |
| [FortiGate® Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations) | This service deploys a pair of FortiGate Virtual Appliances to your environment, which can help you reduce risk by implementing critical security controls within your virtual infrastructure. |
| [F5 BIG-IP®](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations) | This service provides intelligent L4-L7 load balancing and traffic management services at a local and global scale, robust network and web application firewall protection, and secure and federated application access. |
| [Entrust CloudControl™](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-cc_considerations) | This service enforces and controls compliance against security standards, and provides detailed role-based access control (RBAC), approval, and auditing capabilities.
| [KMIP™ for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations) | This service provides a highly available service to manage encryption keys that are used by VMware in {{site.data.keyword.cloud_notm}}. By using the runtime capability, you can manage encryption keys and to maintain the associations between the client credentials and the encryption keys. |
| [Juniper® vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview) | This service provides security and networking services at the perimeter or edge in virtualized private or public cloud environments. Within a VMware infrastructure, vSRX runs as a VM within the VMware vSphere environment. The vSRX provides a complete Next-Generation Firewall (NGFW) solution. |
{: caption="Table 3. Security and compliance services" caption-side="bottom"}

#### Data resiliency and migration services
{: #getting-started-serv-buss-cont}

The following table describes the data resiliency and migration services that are available.

| Service name | Description |
|:------------ |:----------- |
| [HCX™](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations#hcx_considerations) | This service can extend the networks of on-premises data centers into {{site.data.keyword.cloud_notm}}, which allows VMs to be migrated to and from the {{site.data.keyword.cloud_notm}} without any conversion or change. |
| [PrimaryIO HDM](/docs/vmwaresolutions?topic=vmwaresolutions-managing_pio) | This service decouples VMs and storage (VMDKs) to seamlessly move workloads to and from {{site.data.keyword.cloud_notm}} faster and efficiently. |
| [Veeam®](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) | This service integrates directly with your VMware hypervisors to help your enterprise achieve high availability. You can control both the backup and restore of all VMs for your infrastructure from the Veeam console. |
| [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr) | This service provides replication and disaster recovery capabilities, which can be integrated into the deployment offerings to protect and recover data in your VMware virtual environment on {{site.data.keyword.cloud_notm}}. |
| [Managed Disaster Recovery Services by Kyndryl](https://www.kyndryl.com/us/en/services/cyber-resilience) | Our partner Kyndryl offers fully managed disaster recovery (DR) environment services with or without orchestration. |
{: caption="Table 4. Data resiliency and migration services" caption-side="bottom"}

#### Featured workload solutions
{: #getting-started-serv-feat-sol}

The following table describes the featured workload solutions services that are available.

| Service name | Description |
|:------------ |:----------- |
| [Dizzion](/docs/vmwaresolutions?topic=vmwaresolutions-dizzion-overview) | This service provides more service-level choices, multicloud integration, compliance, protection, and simplified management for the teams that are in charge with environment optimization. |
| [IBM Security Services for SAP®](/docs/vmwaresolutions?topic=vmwaresolutions-managing-ss-sap) | This service offers a cybersecurity solution to automate the monitoring and protection of SAP applications on {{site.data.keyword.cloud_notm}}, and to keep workloads compliant and secure from inside and outside threats. |
{: caption="Table 5. Featured workload solutions" caption-side="bottom"}

#### Other services
{: #getting-started-serv-other}

The following table describes other services that are available.

| Service category | Service name | Description |
|:---------------- |:------------ |:----------- |
| Transformation and modernization | [Red Hat® OpenShift® for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview) | This service brings together the power of the Red Hat OpenShift Container Platform and the VMware software-defined data center stack. |
| Management tools | [vRealize® Operations™ and Log Insight™](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) | This service deploys the VMware vRealize Operations (vROps) and VMware vRealize Log Insight (vRLI) tools, which help you operate and monitor the performance, health, and capacity of your IBM-hosted, dedicated VMware environment. |
{: caption="Table 6. Other services" caption-side="bottom"}

## Accessing the VMware Solutions console
{: #getting-started-step1}
{: step}

The VMware Solutions console is the user interface where you order and manage your deployments. Each deployment is managed as an instance in the console. The console is a stand-alone user interface that is separate from the {{site.data.keyword.cloud_notm}} infrastructure customer portal.

To access the {{site.data.keyword.vmwaresolutions_short}} console:
1. Go to https://cloud.ibm.com/vmware.
2. Log in to the console with your **IBMid**.

## Setting up your environment for your first order
{: #getting-started-step2}
{: step}

Decide upon a deployment offering, which is managed as an instance in the console, and then ensure that your environment is ready for your order. Follow the instructions in the **Before you begin** section on the ordering page. The instructions might vary depending on the instance type that you select.

For more information about how to set up your environment for your first order, see [Setting up your environment for your first order](/docs/vmwaresolutions?topic=vmwaresolutions-completing_checklist).

## Ordering an instance
{: #getting-started-step3}
{: step}

After you set up your environment properly, begin the ordering process.

For more information about how to order an instance, see the following topics based on your selected deployment:
* [Ordering virtual data center instances](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [Ordering vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_orderinginstance-req)
* [Ordering vSphere clusters](/docs/vmwaresolutions?topic=vmwaresolutions-vs_orderinginstances-req)
* [Ordering VMware Regulated Workloads instances](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-orderinginstance-req)

## Viewing the instance
{: #getting-started-step4}
{: step}

After you place an instance order in **Step 3**, the deployment of the instance starts automatically. You can track the status of the deployment by viewing the instance details. When the instance deployment is completed, you can view the summary and detailed information of the instance and its services on the instance details page too.

For more information about how to view the instance you ordered, see the following topics based on your selected deployment:
* [Viewing and managing virtual data center instances](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary)
* [Viewing vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Viewing vSphere clusters](/docs/vmwaresolutions?topic=vmwaresolutions-vc_viewinginstances)
* [Viewing VMware Regulated Workloads instances](/docs/vmwaresolutions?topic=vmwaresolutions-vrw-view-delete-instance)
