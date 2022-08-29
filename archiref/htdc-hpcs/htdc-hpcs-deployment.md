---

copyright:

  years:  2019, 2022

lastupdated: "2022-07-14"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deployment
{: #htdc-hpcs-deployment}

New installations of Entrust DataControl® (formerly known as HyTrust DataControl) are no longer supported for new or existing deployments of vCenter Server® instances. You can still use or delete existing Entrust DataControl installations on your existing instances.
{: deprecated}

At a high level, you must complete the following three activities to configure Entrust DataControl® to use Hyper Protect Crypto Services:

* Deploy and configure Hyper Protect Crypto Services
* Create an {{site.data.keyword.cloud}} Service ID
* Deploy and configure Entrust DataControl

Detailed instructions for each of these activities are contained within the product information websites. The following information gives an overview of the activities with links to the more detailed step-by-step instructions.

## Hyper Protect Crypto Services
{: #htdc-hpcs-deployment-hpcs}

* Provision an IBM HPCS instance - [Provisioning service instances](/docs/hs-crypto?topic=hs-crypto-provision).
* Set up the IBM HPCS environment.
   * Verify API endpoint.
   * Set up CLI - Install the {{site.data.keyword.cloud_notm}} CLI, if not already installed. For more information, see [Getting started with the {{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).
   * Install TKE plug-in - Using the CLI, log in and install the Trusted Key Entry plug-in, `ibmcloud plugin install tke`.
   * Set up local directory for key files - On your local workstation, create a directory for the primary key part files and signature key part files. The directory is stored in the variable CLOUDTKEFILES.
* Manage crypto units in a service instance.
   * Display assigned crypto units.
   * Add crypto units - Using the CLI, select the crypto unit so that you can perform operations against it.
* Load primary key - To create and load a primary key into a primary key register, create a signature key so that you can sign the operation of creating the primary key.
   * Create signature keys - Using the CLI, create a signature key by using a username and password and select the signature key.
   * Manage administrators:
      * Add Administrators - Add an admin user, and signature key, to the crypto unit so it can perform operations.
      * Exit imprint mode - Exit imprint mode as the initial setup is complete.
   * Create primary key parts - It is good practice to create multiple parts of a primary key and split across different people in the enterprise. These people need to use their keys at the same time. Create a primary key part, choosing a highly secure password. At least two primary key parts are required, so repeat this process.
   * The two primary key parts and the signature key are on the workstation, in the directory CLOUDTKEFILES. They need to be on the same machine to add the primary key parts to an HSM crypto unit.
   * Load primary key.
      * Load new primary key - Passwords for all three keys are required. These passwords are different, known to different people, and stored on different systems.
      * Commit primary key register - Commit this primary key register. The CLI prompts for the password for the signature key for the administrator with access to the crypto unit. You now have a fully committed primary key.
      * Activate primary key - Two registers exist for primary keys in the crypto unit, one for a new key and one for the current key. To activate this primary key, it needs to become the current key. On the {{site.data.keyword.cloud_notm}} portal, on the HPCS instance Manage tab, verify that the HSM primary key is configured.
* Create a root key - IBM HPCS uses the recommended envelope encryption mechanism of taking a key that is used to encrypt data, the data encryption key or DEK, and encrypting the key itself with a root key. This root key never leaves the HSM.
   * Using the {{site.data.keyword.cloud_notm}} portal, view the {{site.data.keyword.cloud_notm}} resources, and find your IBM HPCS instance.
   * Click **Add Key** and then generate a new root key.
   * Review [Creating root keys](/docs/hs-crypto?topic=hs-crypto-create-root-keys) for more information of this step.
* Create a standard key - Perform this operation to [create a standard key](/docs/hs-crypto?topic=hs-crypto-create-standard-keys).

## Service ID
{: #htdc-hpcs-deployment-serviceid}

* Create a Service ID. For more information, see [Creating and working with service IDs](/docs/account?topic=account-serviceids).

| Parameter                           | Example                          |
| ----------------------------------- | -------------------------------- |
| Name                                | HPCS01                           |
| Description                         | For Entrust and HPCS             |
| Group                               | Public Access                    |
| Access policy - Services            | Hyper Protect Crypto Services    |
| Access policy - Region              | Frankfurt                        |
| Access policy - Service Instance ID | Hyper Protect Crypto Services-5c |
| Access policy - Platform access     | Viewer                           |
| Access policy - Service access      | Reader                           |
| API Key - Name                      | HPCSAPI01                        |
| API Key - Description               | For Entrust and HPCS             |
{: caption="Table 1. Service ID example" caption-side="bottom"}

Copy the API key or click Download to save it. You cannot view this API key again and you cannot retrieve it.

## Entrust DataControl
{: #htdc-hpcs-deployment-htdc}

* Order Entrust DataControl.
* Update static routes on the Entrust DataControl VMs. For more information, see [Managing Entrust DataControl](/docs/vmwaresolutions?topic=vmwaresolutions-managing-entrust-dc).
* Configure the customer ESG to use SNAT to allow communication between VMs to be encrypted connected to the NSX overlay networks and the Entrust DataControl virtual machines, which are connected to the {{site.data.keyword.cloud_notm}} underlay network. For more information, see [Add a SNAT rule](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.4/com.vmware.nsx.admin.doc/GUID-BEF4D960-5F8A-4DE5-84F6-0160DF916FDA.html){: external} and [Add a firewall rule](https://docs.vmware.com/en/VMware-NSX-Data-Center-for-vSphere/6.4/com.vmware.nsx.admin.doc/GUID-C7A0093A-4AFA-47EC-9187-778BDDAD1C65.html){: external}.
* Configure Entrust DataControl. For more information, see [Entrust DataControl](https://www.entrust.com/-/media/documentation/datasheets/datacontrol-ds.pdf){: external}.
   * Initializing the KeyControl™ webGUI.
   * Authenticating New KeyControl Nodes.
   * Creating a Cloud Admin User Account.
   * Creating a Cloud VM Set by using an HPCS KEK. A VM must be part of a Cloud VM Set before it can be encrypted. For an HPCS KEK, you must specify the HPCS server information when you create the Cloud VM Set. Select **Use HPCS KEK** from the list and click Save to view the HPCS KEK properties. The following information is required:

| Parameter | Example |
| --------- | ------- |
| HPCS URL - The URL for the IBM HPCS server to be used by the Cloud VM Set. Available from the Manage Instance web page on the {{site.data.keyword.cloud_notm}} portal. | `https://api.private.eu-de.hs-crypto.cloud.ibm.com:9133` |
| HPCS API Key - The API key to be used to connect to the IBM HPCS server. The Service ID API Key.  | `rsC_SawDQ0GEOGSjsTXruArwQ9fC73WKv-87dVVTdf_i` |
| HPCS Instance ID - The instance ID for your IBM HPCS server. Available from the Manage Instance web page on the {{site.data.keyword.cloud_notm}} portal. | `5e03d770-558d-4699-a7c6-8c98a17f5f5a` |
| HPCS Root Key - The Key ID in the IBM HPCS server to be used for generating a KEK. This value is optional. If you do not include the root key, then KeyControl creates one in HPCS. | `121b4f6c-8147-4194-b9c4-367f33fd8555` |
{: caption="Table 2. Cloud VM Set example" caption-side="bottom"}

* Install the Policy Agent - The Entrust DataControl Policy Agent is a software module that runs on Microsoft® Windows® and Linux® operating systems, and which provides encryption of virtual disks and individual files. When a user attempts to access an encrypted disk, the Policy Agent queries Entrust DataControl to validate the request, and returns the information to the user if Entrust DataControl authorizes the request. A Policy Agent must be installed in each VM, and on each disk, to be encrypted with Entrust DataControl.

## Related links
{: #htdc-hpcs-deployment-related}

*  [Getting started with {{site.data.keyword.cloud_notm}} Hyper Protect Crypto Services](/docs/hs-crypto?topic=hs-crypto-get-started)
*  [Entrust DataControl overview](/docs/vmwaresolutions?topic=vmwaresolutions-entrust-dc_considerations)
