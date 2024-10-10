---

copyright:

  years:  2019, 2024

lastupdated: "2024-05-21"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# VMware Solutions SDDC architecture
{: #vcs-openshift-arch}

## Common services components
{: #vcs-openshift-arch-common-services}

Common services provide the services that are used by other services in the cloud management platform. Common services include identity and access services, domain name services, and NTP services.

![Common services](../../images/openshift-commonservices.svg){: caption="Common services" caption-side="bottom"}

### Identity and access services
{: #vcs-openshift-arch-identity}

As part of the {{site.data.keyword.vcf-classic}} automation, a Microsoft® Active Directory™ (AD) is employed for Identity Management. A single AD virtual server instance (VSI) is deployed. The vCenter is configured to use AD authentication and you can configure {{site.data.keyword.redhat_openshift_full}} for LDAP authentication.

### Domain Name Services
{: #vcs-openshift-arch-dns}

The {{site.data.keyword.vcf-classic-short}} deployment uses the deployed AD VSIs as DNS servers for the instance. All deployed components, such as, vCenter, PSC, NSX®, and ESXi™ hosts, are configured to point to AD as their default DNS.

### NTP services
{: #vcs-openshift-arch-ntp}

The {{site.data.keyword.vcf-classic-short}} deployment uses the {{site.data.keyword.cloud}} infrastructure NTP servers. All deployed components are configured to use these NTP servers. Having all components within the design that uses the same NTP servers is critical for certificates and AD authentication to function correctly.

## Related links
{: #vcs-openshift-arch-related}

* [{{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-intro)
* [System context for {{site.data.keyword.vcf-classic-short}} and {{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-syscontext)
* [{{site.data.keyword.redhat_openshift_notm}} architecture](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-redhat-arch)
* [Storage options on {{site.data.keyword.cloud_notm}} and {{site.data.keyword.redhat_openshift_notm}}](/docs/vmwaresolutions?topic=vmwaresolutions-vcs-openshift-storage)
