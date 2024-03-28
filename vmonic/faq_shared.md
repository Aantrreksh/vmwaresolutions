---

copyright:

  years:  2016, 2024

lastupdated: "2024-03-20"

keywords: FAQ vmware solutions shared, vmware solutions shared questions

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# General FAQ about VMware Shared
{: #faq-vmwaresolutions-shared}

{{site.data.content.shared-deprecated-note}}

Find answers to frequently asked questions about the VMware Shared offering.

## What is VMware Shared?
{: #faq-shared}
{: faq}

VMware Shared is a multitenant VMware® infrastructure solution based on a robust VMware® product called VMware Cloud Director. You can use this solution to rapidly create, migrate, and use your virtual machines (VMs) in the Cloud.

## What are my options to use resources with VMware Shared?
{: #faq-shared-options}
{: faq}
{: support}

You are provided with the following two consumption models:
* **On-demand**. With this consumption model, you pay only for the compute resources that you use, in an hourly pricing model.
* **Reserved**. With this consumption model, you can reserve compute resources in advance to ensure that your capacity is available when you need it. Billing for **Reserved** is available monthly, yearly, or on a multi-year basis. Other resources, such as storage and egress, are billed per usage, regardless of the consumption model.

## Why do I want to subscribe to VMware Shared?
{: #faq-shared-subscribe}
{: faq}

With VMware Shared, you can extend your VMs to the Cloud with ultimate capacity flexibility and scalability. Whether you are looking to begin your cloud journey with a Development or Test environment, a disaster recovery site, or a full enterprise-grade hybrid cloud transformation, VMware Shared provides a cost-effective and self-service way to start moving your VMs to the cloud within minutes.

With IBM managing the infrastructure up to the hypervisor, you do not need to worry about managing patches, upgrades, and monitoring, which gives you more time and resources to focus on innovation. In addition, with a native like VMware experience, you can use your existing VMware resources and skill sets.

## What user accounts do I need for VMware Shared?
{: #faq-user-accts-shared}
{: faq}
{: support}

* **IBMid account**. This account is required to access the {{site.data.keyword.vmwaresolutions_short}} console. The console is a stand-alone user interface that is separate from the {{site.data.keyword.slportal}}. For more information, see [Getting started](/docs/vmwaresolutions?topic=vmwaresolutions-getting-started).
* **{{site.data.keyword.cloud_notm}} account**. This account is required for provisioning. You can sign up for an {{site.data.keyword.cloud_notm}} account by using an existing **IBMid** or by creating a new **IBMid**.
* **{{site.data.keyword.cloud_notm}} infrastructure account**. This account is used to log in to the {{site.data.keyword.cloud_notm}} infrastructure customer portal that provides some additional function to manage infrastructure products and services. You can get an {{site.data.keyword.cloud_notm}} infrastructure account by upgrading your **{{site.data.keyword.cloud_notm}} account** to a billable account, or by linking your existing {{site.data.keyword.cloud_notm}} infrastructure account with your {{site.data.keyword.cloud_notm}} account. The {{site.data.keyword.cloud_notm}} infrastructure account that you are using must meet certain requirements. For more information, see [Signing up for required accounts](/docs/vmwaresolutions?topic=vmwaresolutions-signing_required_accounts).

## How do I associate my {{site.data.keyword.cloud_notm}} infrastructure credentials with the VMware Solutions console?
{: #faq-associate-credentials-shared}
{: faq}
{: support}

When you order your instance for the first time, follow the instructions on the **Settings** page in the console. These instructions help you locate and copy the {{site.data.keyword.cloud_notm}} infrastructure username and API key from the {{site.data.keyword.slportal}}. The {{site.data.keyword.cloud_notm}} infrastructure credentials are stored in the {{site.data.keyword.vmwaresolutions_short}} console after the first order. Future orders automatically use the stored credentials.

## How do I connect my on-premises environment to VMware Shared?
{: #faq-shared-connect}
{: faq}
{: support}

Each virtual data center has an Edge Services Gateway (ESG) which provides network connectivity to the virtual data center. On-premises connectivity to the customer virtual data center can be accomplished in the following ways:
* IPsec tunnel over the internet to the ESG
* SSL VPN tunnel over the internet to the ESG
* Direct internet access through the ESG to the VMs by using NAT or load balancing

Along with the internet access methods, you can use {{site.data.keyword.cloud_notm}} service endpoints to access your virtual data centers from other {{site.data.keyword.cloud_notm}} accounts. This way, you can use DirectLink or other on-premises environments to access your {{site.data.keyword.cloud_notm}} account network options. Then, from your cloud account, you can connect into your virtual data centers by using the Cloud Service Endpoint method.

## How are my VMware virtual platform consumptions billed?
{: #faq-billing-shared}
{: faq}

All costs for the physical and virtual infrastructure and the licenses that result from the instance are charged to your {{site.data.keyword.cloud_notm}} account. When you order an instance, you must have an {{site.data.keyword.cloud_notm}} account and provide the {{site.data.keyword.slapi_short}} key that is associated with the account.

## How do I choose the data centers for my instances?
{: #faq-data-center-shared}
{: faq}

The instance deployments have strict physical infrastructure requirements, which vary among {{site.data.keyword.cloud_notm}} data centers. When you place your instance order, the available data centers are listed within regions and you can select the one that you want from the list.

For more information, see [{{site.data.keyword.cloud_notm}} data center availability](/docs/vmwaresolutions?topic=vmwaresolutions-shared_planning#shared_planning-dc-availability).

## How long does it take for my instance to be deployed?
{: #faq-deploy-shared}
{: faq}

You can check the status of the instance on the [instance details page](/docs/vmwaresolutions?topic=vmwaresolutions-shared_viewing-vdc-summary#shared_viewing-vdc-summary-procedure) from the {{site.data.keyword.vmwaresolutions_short}} console.

## How can I view a list of all notifications?
{: #faq-notification-shared}
{: faq}

To view the complete notification history, click **Notifications** from the left navigation pane.

## What if I have issues with VMware Shared?
{: #faq-support-shared}
{: faq}
{: support}

If you need assistance with {{site.data.keyword.vmwaresolutions_short}}, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support).

## Can I bring my own firewall?
{: #faq-byof}
{: faq}

Yes. Each customer virtual data center comes with an edge firewall in the ESG and a distributed firewall that protects the internal virtual data center environment. If you want to bring your own firewall such as Fortinet or Cisco CSR, you can do so and run it between the ESG and your internal virtual machines.

## Can I bring my own IP addresses?
{: #faq-byip}
{: faq}

You can bring your own IP addresses within your virtual data centers with a few restrictions:
* The IP addresses `166.9.0.0/16` is reserved for {{site.data.keyword.cloud_notm}} service endpoints.
* The IP addresses `52.117.132.0/24` is reserved for other {{site.data.keyword.cloud_notm}} services.

Other than the IP addresses used for internet access on each customer ESG, you can use any IP address that you want. Typically, you use an IPsec tunnel from the on-premises environment to your virtual data centers, which provides transparent networking with full BYIP capabilities.

## Can I bring a custom image?
{: #faq-customimage}
{: faq}

Yes. VMware Cloud Director supports the same set of guest operating systems as VMware vSphere® 6.7. For more information, see [VMware Guest OS Compatibility Guide](https://www.vmware.com/resources/compatibility/pdf/VMware_GOS_Compatibility_Guide.pdf){: external}.

VMware Shared provides Microsoft® Windows® server 2016/2019 templates. You can provide your own image to run other versions.

## What are the Service Level Agreement options with VMware Shared?
{: #faq-sla}
{: faq}

VMware Shared uses the {{site.data.keyword.cloud_notm}} standard Service Level Agreement (SLA). SLAs are not offered for virtual machines and vApps. For more information, see [{{site.data.keyword.cloud_notm}} Service Description](https://www.ibm.com/support/customer/csol/terms/?id=i126-6605).

## Do I get vCenter access?
{: #faq-vcenter-access}
{: faq}
{: support}

No.

## Related links
{: #faq_shared-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [User accounts and settings](/docs/vmwaresolutions?topic=vmwaresolutions-useraccount)
* [Accessing the console](/docs/vmwaresolutions?topic=vmwaresolutions-loginmethod)
* [Notifications](/docs/vmwaresolutions?topic=vmwaresolutions-notifications)
