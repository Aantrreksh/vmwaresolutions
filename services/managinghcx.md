---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-28"

keywords: HCX updates, HCX management console, login HCX console

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}


# Managing VMware HCX
{: #managinghcx}

## Accessing the HCX management consoles
{: #managinghcx-accessing-consoles}

To manage the VMware HCX® service, you must access the HCX Cloud console or the HCX Manager Admin console:
1. Use the {{site.data.keyword.cloud}} infrastructure VPN or a jump server to allow access to the IP address of the HCX Manager virtual appliance (HCX Manager). You can find the IP address on the HCX service details page in the {{site.data.keyword.vmwaresolutions_short}} console.
2. To access the HCX Cloud console, click **View HCX Cloud console** on the HCX service details page, and then log in by using the VMware vCenter Server® credentials.
3. To access the HCX Manager Admin console, click **View HCX Manager Admin console** on the HCX service details page. Then, log in by using the HCX Manager credentials that are listed on the same service details page.

For more information, see [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Applying updates to HCX
{: #managinghcx-updates}

HCX is deployed with the most recently tested build of VMware Hybrid Cloud Extension technology. VMware® provides updates to the builds regularly, which include important fixes and new features. These builds are pushed to HCX installations automatically, including on-premises HCX installations.

To apply any maintenance fixes pushed to your environment, you must use the HCX Manager Admin console in your on-premises data center and your vCenter Server instance.

Open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) for the following situations:
* You do not see a build update that you are expecting
* You have problems with HCX
* You want to have the most recent HCX build pushed to your system immediately

## Related links
{: #managinghcx-related}

* [HCX overview](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_considerations#hcx_considerations)
* [Glossary of HCX terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcx_glossary)
* [VMware Hybrid Cloud Extension overview](https://cloud.vmware.com/vmware-hcx){: external}
* [VMware Hybrid Cloud Extension documentation](https://cloud.vmware.com/vmware-hcx/resources){: external}
