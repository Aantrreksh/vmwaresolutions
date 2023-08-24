---

copyright:

  years:  2016, 2023

lastupdated: "2022-08-18"

keywords: KMIP for VMware, KMIP stand-alone, tech specs KMIP

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# KMIP for VMware overview
{: #kmip_standalone_considerations}

The Key Management Interoperability Protocol (KMIP™) for VMware® service provides a highly available service to manage encryption keys that are used by VMware in {{site.data.keyword.cloud}}. This service offers runtime capability to allow customers to create, retrieve, activate, revoke, and destroy the encryption keys. It also provides management capability to maintain the associations between the client credentials and the encryption keys.
{: shortdesc}

The KMIP for VMware service is available as a stand-alone service without being associated to a VMware instance. Each instance of the service can serve one or more VMware vCenter Server® or VMware vSphere® instances.

The supported client applications are vCenter Server 6.7 and 7.0 and vSphere 6.7 and 7.0.

## Technical specifications for KMIP for VMware
{: #technical-specifications-for-kmip-for-vmware-on-ibm-cloud}

For more information about resource requirements and planning for KMIP for VMware, see [Planning for KMIP for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-implementation#kmip-implementation-planning).

The following specifications are included with the KMIP for VMware service:

* A VMware-compatible KMIP
* Two managed services - [Key Protect](https://cloud.ibm.com/catalog/services/key-protect) and [Hyper Protect Crypto Services](https://cloud.ibm.com/catalog/services/hyper-protect-crypto-services)
* Available in multiple geographic regions worldwide
* Highly available KMIP network service endpoints provided in each region

## Before you order KMIP for VMware
{: #kmip_standalone_considerations-install}

KMIP for VMware uses either the IBM Key Protect service or the IBM Hyper Protect Crypto Services (HPCS) service to create, encrypt, and decrypt encryption keys. 

Before you install KMIP for VMware, complete the following tasks and review the following information:

1. Order a usable Key Protect or HPCS service instance in the {{site.data.keyword.cloud_notm}} region where your KMIP for VMware instance is to be hosted. If you are using HPCS, in addition to provisioning the HPCS service, you must also initialize your crypto instance so that HPCS can provide key-related functions.

   For more information, see:
   * [Provisioning the Key Protect service](/docs/key-protect?topic=key-protect-provision)
   * [Provisioning HPCS service instances](/docs/hs-crypto?topic=hs-crypto-provision#provision)
   * [Initializing HPCS service instances using key part files](/docs/hs-crypto?topic=hs-crypto-initialize-hsm#initialize-hsm)
   
2. If you are using Key Protect, complete the following tasks:
   1. Create an {{site.data.keyword.cloud_notm}} service ID by following the steps in [Creating a service ID in the console](/docs/account?topic=account-serviceids&interface=ui#create_serviceid). This service ID is used to access the Key Protect instance that you created.
   2. Grant the following access levels for the service ID:
      * At the platform access level - Viewer authority to your Key Protect or HPCS service instance.
      * At the service access level - Manager authority to your Key Protect or HPCS service instance.
   3. You must have an API key for the created service ID. The API key is required when you order the service.

3. Import or create at least one customer root key (CRK) by using the GUI or API of Key Protect or HPCS.

   If you are using HPCS, the CRK must be created within the default key ring for the HPCS instance.
   {: important}

   For more information about Key Protect, see:
   * [Importing root keys](/docs/key-protect?topic=key-protect-import-root-keys)
   * [Creating root keys](/docs/key-protect?topic=key-protect-create-root-keys)
   * [Creating import tokens](/docs/key-protect?topic=key-protect-create-import-tokens)
   * [IBM Key Protect API](/apidocs/key-protect)

   For more information about HPCS, see:
   * [Importing root keys](/docs/hs-crypto?topic=hs-crypto-import-root-keys)
   * [Creating root keys](/docs/hs-crypto/get-started?topic=hs-crypto-create-root-keys)
   * [Creating import tokens](/docs/hs-crypto?topic=hs-crypto-create-import-tokens)
   * [IBM Cloud Hyper Protect Crypto Services KMS API](/apidocs/hs-crypto)

4. Ensure that your {{site.data.keyword.cloud_notm}} infrastructure account is enabled for Virtual Routing and Forwarding (VRF) and for connectivity to service endpoints. 

   For more information, see:
   * [Virtual Routing and Forwarding on {{site.data.keyword.cloud_notm}}](/docs/direct-link?topic=direct-link-overview-of-virtual-routing-and-forwarding-vrf-on-ibm-cloud)
   * [Enabling service endpoints](/docs/account?topic=account-vrf-service-endpoint#service-endpoint)

5. Only private connection is supported. As a result, you don't need to configure firewall or SNAT rules in vCenter Server for the network connectivity from vCenter Server to the endpoint of the KMIP for VMware instance. For more information, see [KMIP for VMware solution architecture](/docs/vmwaresolutions?topic=vmwaresolutions-kmip-overview).

## Related links
{: #kmip_standalone_considerations-related}

* [Ordering KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_ordering)
* [Managing certificates for KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_addingdeletingcert)
* [Viewing KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_viewing)
* [Deleting KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_deleting)
* [Auditing events for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-at-events)
* [Getting help and support for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
