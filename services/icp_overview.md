---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-12"

keywords: IBM Cloud Private

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# {{site.data.keyword.cloud_notm}} Private Hosted
{: #icp_overview}

The {{site.data.keyword.cloud}} Private Hosted service is no longer supported. Use the [{{site.data.keyword.redhat_openshift_notm}} for VMware](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview) service instead.
{: deprecated}

The {{site.data.keyword.cloud_notm}} Private Hosted service automatically deploys {{site.data.keyword.cloud_notm}} Private Hosted and {{site.data.keyword.cloud_notm}} Automation Manager on your {{site.data.keyword.vcf-auto}} instances. This service brings the power of microservices and containers to your VMware® environment on {{site.data.keyword.cloud_notm}}. With this service, you can extend the same familiar VMware and {{site.data.keyword.cloud_notm}} Private operational model and tools from on-premises into the {{site.data.keyword.cloud_notm}}.
{: shortdesc}

## Deploying additional nodes
{: #icp_overview-deploy-nodes}

If you want to deploy additional nodes, review the following information:
* Use the {{site.data.keyword.cloud_notm}} Private Ubuntu template (Ubuntu1604) that is deployed with your initial {{site.data.keyword.cloud_notm}} Private Hosted installation.
* To find the Ubuntu template, in the VMware vSphere® Web Client, go to the **VMs and Templates** tab, under the `cam` folder.
* The default password for the Ubuntu template is `icponcloud`. It is recommended that you change this password before you use the template.
* {{site.data.keyword.vmwaresolutions_short}} does not offer support for applying updates and patches for the Ubuntu template. You must monitor and apply these updates yourself.

## Considerations when you delete {{site.data.keyword.cloud_notm}} Private Hosted
{: #icp_overview-remove}

* Only the virtual machines (VMs) that were deployed during the initial installation of the {{site.data.keyword.cloud_notm}} Private Hosted service are deleted. Any node that is deployed after the installation is not cleaned up.
* {{site.data.keyword.cloud_notm}} deletes the VXLAN, DLR, and the Edge Gateway that was created during the initial deployment of {{site.data.keyword.cloud_notm}} Private Hosted. The VMs that you deployed on VXLAN will lose connectivity after the removal of the {{site.data.keyword.cloud_notm}} Private Hosted service is started.
