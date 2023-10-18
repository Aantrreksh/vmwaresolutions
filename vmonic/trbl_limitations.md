---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-11"

keywords: troubleshooting, Windows automatic installation, Windows updates

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# General considerations
{: #trbl_limitations}

Review the following considerations when you work with {{site.data.keyword.vmwaresolutions_full}}.

## Automatic installation of updates from Windows Update
{: #trbl_limitations-windows-update}
{: faq}

The Microsoft® Active Directory™ (AD) Domain Services server is automatically set up to download the updates only. It does not install these updates or restart automatically. You must install the updates manually and restart at a scheduled time that avoids any interruptions of the ongoing AD server configuration and other backup jobs. To apply Windows® updates, install the updates manually.

## Related links
{: #trbl_limitations-related}

* [Other considerations](/docs/vmwaresolutions?topic=vmwaresolutions-vcenter_chg_impact)
