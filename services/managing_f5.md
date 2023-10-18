---

copyright:

  years:  2016, 2023

lastupdated: "2023-09-26"

keywords: F5 console, BIG-IP Web UI, login F5 console

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing F5 BIG-IP
{: #managing_f5}

## Accessing the BIG-IP web UI consoles
{: #managing_f5-big-ip-consoles}

To manage the F5 BIG-IP® service, log in to the primary or secondary BIG-IP web UI consoles by using the corresponding credentials. You can find the corresponding credentials on the F5 BIG-IP service details page.

For more information about viewing the service details, see [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices).

## Considerations when you delete F5 BIG-IP
{: #f5_considerations-remove}

Review the following considerations before you delete the service:

* Before you delete the F5 BIG-IP service, ensure that the existing BIG-IP VE configuration is removed correctly. Specifically, network traffic must be routed around BIG-IP VE instead of through BIG-IP VE. Otherwise, the existing data traffic from your environment might be impacted.

* If you installed the F5 BIG-IP service before VMware Solutions v4.0 and then deleted that service, you must manually remove the DNS entries. For more information, see [Manually removing the DNS entries](/docs/vmwaresolutions?topic=vmwaresolutions-vc_deletingservices#vc_deletingservices-DNS-entries).

## Related links
{: #managing_f5-related}

* [F5 BIG-IP overview](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
* [F5 website](https://www.f5.com/){: external}
