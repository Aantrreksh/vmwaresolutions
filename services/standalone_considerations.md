---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-03"

keywords: VMware HCX standalone, HCX on-premises, tech specs HCX

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Considerations for on-premises VMware HCX instances
{: #standalone_considerations}

Review the following considerations before you install or delete the VMware HCX® instances that you ordered for on-premises use.

A VMware vCenter Server® instance with HCX is limited to three simultaneous connections from on-premises sites.
{: note}

## Considerations before you install on-premises HCX instances
{: #standalone_considerations-install}

The HCX components must be installed both on {{site.data.keyword.cloud}} and in your on-premises VMware vSphere® environment. It is recommended that you install the HCX service into your vCenter Server instance before you install the on-premises HCX instance.

For more information, see [Considerations when you install HCX](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_ordering#hcx_considerations-install).

### Notes for HCX installations
{: #standalone_considerations-install-notes}

* Before the service is installed in your environment, a check is performed against the available capacity of the default cluster in the environment to ensure that the service components can fit.
* If the capacity check fails, the service is not installed and the service status is set to **Capacity Validation Failed** on the console. In addition, a console message with more details is displayed and you are notified by email.
* To install the service, you must increase the capacity in your default cluster. Either add more hosts or release RAM, CPU, or disk space, and then add the service again in the console. Then, you can delete the existing service in the **Capacity Validation Failed** state by clicking the **Delete** icon ![Delete icon](../../icons/delete.svg "Delete") next to it.

### IP address requirements
{: #standalone_considerations-ip}

For full HCX functions, you need at least five private IP addresses that have internet access.

### Deployment process for on-premises HCX instances
{: #standalone_considerations-deploy}

You must complete the following tasks for a successful installation of the on-premises HCX instance:

1. In the {{site.data.keyword.vmwaresolutions_short}} console, order the on-premises HCX instance. For more information, see [Ordering on-premises HCX instances](/docs/vmwaresolutions?topic=vmwaresolutions-standalone_orderingserviceinstances).
2. In the **HCX Cloud Console**, complete the following steps:
    1. Click the **Administration** tab.
    2. On the **System Updates** tab, click **REQUEST DOWNLOAD LINK**.
    3. Click **COPY LINK**, and then use this link to download the HCX Enterprise Client onto an on-premises environment with access to your on-premises vSphere environment.
3. In the VMware® vSphere Web Client, deploy the HCX Enterprise Client as an HCX Manager virtual appliance (HCX Manager) into your on-premises environment.

   You must deploy the on-premises HCX Manager on a private network and allow it to access the public network. You can use an NSX Edge, Vyatta, or similar gateways to allow internet access to the on-premises HCX Manager. If the gateways used for private network access and public network access are different, use the default gateway to allow for public network access and the on-premises **HCX Manager Admin Console** to create a static route for private network access.
   {: note}

4. After the HCX Manager deployment is completed, use the **HCX Manager Admin Console** to activate the on-premises HCX Manager. To obtain an activation key for the on-premises HCX Manager, order an on-premises HCX instance in the {{site.data.keyword.vmwaresolutions_short}} console. For more information, see [Ordering on-premises HCX instances](/docs/vmwaresolutions?topic=vmwaresolutions-standalone_orderingserviceinstances).
5. If you used a self-signed SSL certificate when you order the HCX service, you must import the certificate into the on-premises HCX Manager by completing the following steps.
    1. In the on-premises **HCX Manager Admin Console**, click the **Administration** tab.
    2. From the left navigation pane, click **Trusted CA Certificate**, and then click **IMPORT** on the right.
    3. Click **URL**, and then enter the URL of the certificate you want to apply. The URL is the **HCX Cloud IP** (``https://<cloud-side public IP>``), which you can find on the HCX service details page in the {{site.data.keyword.vmwaresolutions_short}} console.
    4. Click **APPLY**.

The basic setup of the on-premises HCX Manager is complete. You can proceed to pair the on-premises HCX site with the cloud-side HCX site. For more information, see [VMware HCX documentation](https://docs.vmware.com/en/VMware-HCX/index.html){: external}.

## Related links
{: #standalone_considerations-related}

* [Viewing on-premises HCX instances](/docs/vmwaresolutions?topic=vmwaresolutions-standalone_viewingserviceinstances)
* [Glossary of HCX terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_glossary)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
