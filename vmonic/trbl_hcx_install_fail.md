---

copyright:

  years:  2020, 2023

lastupdated: "2023-07-28"

keywords: troubleshooting, installation fail HCX, installation fail BYOL NSX Data Center Enterprise Plus

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Why does the installation fail for HCX with BYOL NSX Data Center Enterprise Plus?
{: #trbl_hcx_install_fail}
{: troubleshoot}

When you install VMware HCX with a BYOL NSX Data Center Enterprise Plus license, you must ensure that you select the correct license for NSX-T. In the **Licensing** section, under the dropdown for NSX, select **Enterprise Plus**.
{: tsSymptoms}

If you select the incorrect NSX-T license, the installation bypasses the HCX installation and it continues, but you get an error message.
{: tsCauses}

You can correct the problem in one of the following ways:
{: tsResolve}

* To request that your BYOL NSX Data Center Enterprise Plus license key is updated, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support). After your key is updated, you can install HCX again.
* Select an appropriate NSX license edition. After that, HCX is installed without using your BYOL key. An activation key is generated for you and the extra charge for the HCX service is added.
