---

copyright:

  years:  2016, 2024

lastupdated: "2024-02-06"

keywords: KMIP for VMware, order KMIP, Key Protect, Hyper Protect Crypto Services, HPCS

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering KMIP for VMware instances
{: #kmip_standalone_ordering}

You can order a KMIP™ for VMware® instance without associating it to any VMware vCenter Server® instance for flexible management of the service and instances.

## Before you begin
{: #kmip_standalone_ordering-req}

Complete the following tasks:

* Configure the {{site.data.keyword.cloud}} infrastructure credentials on the **Settings** page. For more information, see [User accounts and settings](/docs/vmwaresolutions?topic=vmwaresolutions-useraccount).
* Review all the considerations in [Considerations when you install KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_considerations#kmip_standalone_considerations-install).

## Step 1 - Ordering a KMIP for VMware instance
{: #kmip_standalone_ordering-step1}

### Settings
{: #kmip_standalone_ordering-step1-settings}

When you order a KMIP for VMware instance, configure the following settings:

#### Resource group
{: #kmip_standalone_ordering-resource-group}

{{site.data.content.para-orderinginstance-resource-group}}

{{site.data.content.note-orderinginstance-resource-group}}

#### Instance name
{: #kmip_standalone_ordering-config-instance-name}

The instance name is set to **kmip-_xx_** by default, where _xx_ represents two randomly generated alphabet characters.

You can also specify a name for your KMIP for VMware instance.

### Procedure
{: #kmip_standalone_ordering-step1-procedure}

1. In the {{site.data.keyword.vmwaresolutions_short}} console, scroll down to the services section and click **KMIP for VMware** in the **Security and compliance** category.
2. On the **KMIP for VMware** page, configure the service settings as needed.
3. Click **Create**.

### Results of Step 1
{: #kmip_standalone_ordering-step1-results}

* The deployment of the instance starts automatically and you receive console notification that your order request is being processed. The instance is displayed in the **KMIP for VMware** table on the **KMIP for VMware** > **Resources** pages from the {{site.data.keyword.vmwaresolutions_short}} console. The status of the instance is **Installing**.
* When the instance is successfully deployed, its status is changed to **Inactive**.

## Step 2 - Activating the KMIP for VMware instance
{: #kmip_standalone_ordering-step2}

### Prerequisites
{: #kmip_standalone_ordering-step2-prereqs}

If you are using Hyper Protect Crypto Services (HPCS), you must first create a service authorization that allows your KMIP for VMware instance to access your HPCS instance. Then, grant your KMIP for VMware instance both the platform **Viewer** role and the service **VMware KMIP Manager** role to your HPCS instance. For more information, see [Grant service-to-service authorization in IAM](/docs/hs-crypto?topic=hs-crypto-tutorial-kmip-vmware#tutorial-kmip-s2s).

### Settings
{: #kmip_standalone_ordering-step2-settings}

When you enable the nonactive KMIP for VMware instance, provide the following settings according to the key management service that you selected.

| Setting | Description |
|:------- |:----------- |
| **HPCS instances** | The list of available HPCS instances that you can select to use for key management |
| **Customer root key** | The list of customer root keys that are stored in your selected HPCS instance | 
{: caption="Table 1. Configuration settings for HPCS" caption-side="bottom"}
{: class="simple-tab-table"}
{: #simpletabtable1}
{: tab-title="Hyper Protect Crypto Services"}
{: tab-group="Settings when selecting different key management service"}

| Setting | Description |
|:------- |:----------- |
| **API key for service ID**| The API key for the {{site.data.keyword.cloud_notm}} Service ID that is used to access the service instance of Key Protect |
| **Key Manager instance**| The list of available Key Protect instances that you can select to use for key management |
| **Customer root key**| The list of customer root keys that are stored in your selected key manager instance | 
{: caption="Table 1. Configuration settings for Key Protect" caption-side="bottom"}
{: #simpletabtable2}
{: tab-title="Key Protect"}
{: tab-group="Settings when selecting different key management service"}
{: class="simple-tab-table"}

### Procedure
{: #kmip_standalone_ordering-step2-procedure}

1. Select the key management type, either **Hyper Protect Crypto Services** or **Key Protect**.

2. Select a key management service:
   * For **Hyper Protect Crypto Services**, click **Retrieve** to get the list of available HPCS instances and select the one to use for key management.
   * For **Key Protect**, enter your service ID API key, then click **Retrieve** to get the list of available key manager instances and select the one to use for key management.

3. Select the Key Manager instance from the list.

4. For Key Protect, under **Customer key ring**, the names of the key rings that belong to the selected Key Manager instance are displayed. Select the **Customer key ring** from the list.

    For HPCS, the key ring field is not displayed.

5. Under **Customer root key**, the names and values of the root keys are displayed. Select the root key that you want.

6. (Optional) Add client SSL certificates:
    1. Click **Add**.
    2. In the **Add client SSL certificate** window, enter the name and contents of the certificate, and then click **Add**.

       The certificate name cannot be reused within your selected instance. The certificate content must be valid and contain the BEGIN CERTIFICATE and END CERTIFICATE tags. When you use Key Protect, the certificate cannot be reused in the region where the instance is deployed.
       {: restriction}

7. Click **Configure**.

### Results of Step 2
{: #kmip_standalone_ordering-step2-results}

* The configuration of the instance starts automatically. The status of the instance is changed to **Configuring**.
* When the instance is ready to use, the status of the instance is changed to **Installed**.

## Step 3 - (Optional) Adding client SSL certificates
{: #kmip_standalone_ordering-step3}

If you did not add the client SSL certificates in Step 2, you must add it after the instance can be used.

### Procedure
{: #kmip_standalone_ordering-step3-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources** > **KMIP for VMware** from the left navigation pane.
2. In the **KMIP for VMware** table, click the instance that you want to add certificates for.
3. Click **Add**.
4. In the **Add client SSL certificate** window, enter the certificate name and content, and then click **Add**.

   The certificate name cannot be reused within your selected instance. The certificate content must be valid and contain the BEGIN CERTIFICATE and END CERTIFICATE tags, and the certificate cannot be reused in the selected region where the instance is deployed.
   {: attention}

### Results of Step 3
{: #kmip_standalone_ordering-step3-results}

* You get a console notification that your request to add the certificate is being processed.
* When the certificate is added successfully, you get console confirmation and the added certificate is displayed in the **Client SSL certificates** table on the service details page.

## Connecting vCenter Server to the KMIP instance
{: #kmip_standalone_ordering-next}

Connect your vCenter Server to your KMIP instance by using the client certificate that you uploaded to the KMIP instance.

If your KMIP instance is connected to HPCS, you can find details for the single load-balanced KMIP endpoint in your KMIP for VMware instance. Use this endpoint to configure a single key provider in vCenter.

If your KMIP instance is connected to Key Protect, you must use the two regional endpoints for your KMIP for VMware instance to configure a key provider cluster in vCenter Server. You can find the endpoints for each region in the following table:

| Location | Endpoints |
|:-------- |:--------- |
| Dallas | `kmip-1.private.us-south.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.us-south.vmware-solutions.cloud.ibm.com:5696` |
| Frankfurt | `kmip-1.private.eu-central.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.eu-central.vmware-solutions.cloud.ibm.com:5696` |
| London | `kmip-1.private.uk-south.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.uk-south.vmware-solutions.cloud.ibm.com:5696` |
| Osaka | `kmip-1.private.jp-osa.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.jp-osa.vmware-solutions.cloud.ibm.com:5696` |
| Sao Paulo | `kmip-1.private.br-sao.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.br-sao.vmware-solutions.cloud.ibm.com:5696` | 
| Sydney | `kmip-1.private.ap-south.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.ap-south.vmware-solutions.cloud.ibm.com:5696` |
| Tokyo | `kmip-1.private.ap-north.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.ap-north.vmware-solutions.cloud.ibm.com:5696` |
| Toronto | `kmip-1.private.ca-tor.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.ca-tor.vmware-solutions.cloud.ibm.com:5696` |
| Washington DC | `kmip-1.private.us-east.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.us-east.vmware-solutions.cloud.ibm.com:5696` |
| Madrid | `kmip-1.private.eu-es.vmware-solutions.cloud.ibm.com:5696` \n `kmip-2.private.eu-es.vmware-solutions.cloud.ibm.com:5696` |
{: caption="Table 2. KMIP for VMware network service endpoint locations" caption-side="bottom"}

## Related links
{: #kmip_standalone_ordering-related}

* [Viewing KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_viewing)
* [Deleting KMIP for VMware instances](/docs/vmwaresolutions?topic=vmwaresolutions-kmip_standalone_deleting)
* [Auditing events for VMware Solutions](/docs/vmwaresolutions?topic=vmwaresolutions-at-events)
