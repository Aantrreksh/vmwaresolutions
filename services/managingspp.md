---

copyright:

  years:  2016, 2023

lastupdated: "2023-07-17"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing IBM Spectrum Protect Plus
{: #managingspp}

New installations of the IBM Spectrum® Protect Plus service are no longer supported for new or existing deployments of vCenter Server instances. You can still use or delete existing IBM Spectrum Protect Plus installations on your existing instances. If you want to install IBM Spectrum Protect Plus yourself, see [IBM Spectrum Protect Plus documentation](https://www.ibm.com/docs/en/spp){: external}.
{: deprecated}

## Accessing the IBM Spectrum Protect Plus management console
{: #managingspp-console}

To manage the IBM Spectrum Protect Plus service, you must access the IBM Spectrum Protect Plus management console by completing the following steps:
1. Use the {{site.data.keyword.cloud}} infrastructure VPN or a jump server to allow access to the IP address of the IBM Spectrum Protect Plus virtual machine (VM). You can find the IP address on the service details page for IBM Spectrum Protect Plus in the {{site.data.keyword.vmwaresolutions_short}} console.
2. To access the IBM Spectrum Protect Plus management console, click **View IBM Spectrum Protect Plus console** on the service details page for IBM Spectrum Protect Plus. Then, log in by using the credentials that are listed on the same service details page.

## Applying updates to IBM Spectrum Protect Plus
{: #managingspp-updates}

You are responsible for maintaining IBM Spectrum Protect Plus to keep it updated to the most recent version. Download the required updates from [IBM Spectrum Protect Plus Support](https://www.ibm.com/mysupport/s/topic/0TO50000000IQWtGAO/spectrum-protect-plus){: external}.

## Updating the operating system of the IBM Spectrum Protect Plus VM
{: #managingspp-update-os}

To update the operating system of the IBM Spectrum Protect Plus VM, you must log in as the `serveradmin` user. The `serveradmin` user password is the same as the password from the service details page for IBM Spectrum Protect Plus.
