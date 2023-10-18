---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-06"

keywords: Zerto certificate, Zerto config, update Zerto replication

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing Zerto
{: #managingzertodr}

After the Zerto service is deployed into your instance, you can configure or update Zerto Virtual Replication. You can also deploy more Virtual Replication Appliances to newly added VMware® ESXi™ servers.

## Using your own certificate for Zerto
{: #managingzertodr-ssl-cert}

Always use your own SSL certificate for Zerto Virtual Manager (ZVM). After you deploy Zerto, replace the SSL certificate for ZVM with your own certificate. To change the default security certificate for your ZVM, follow these steps:

1. Open the Zerto Diagnostics utility on the Windows® virtual machine that is running the ZVM.
2. Choose **Reconfigure Zerto Virtual Manager**.
3. Ensure that the VMware vCenter Server® configuration is correct, and click **Next**.
4. In the **HTTP Certificate** section, check the **Replace SSL Certificate** box.
5. Click browse (...) and then locate and select the new SSL certificate.
6. Enter the new SSL certificates associated password and click **Next**.
7. The utility verifies the necessary vCenter Server connectivity. After verified, click **Next** and the ZVM is reconfigured.

## Managing the configuration of Zerto replications
{: #managingzertodr-manage}

To manage the configuration of Zerto replications, log in to the Zerto Virtual Replication console by using the vCenter Server credentials with administrator permissions. For example, re-pairing Zerto instances or configuring virtual protection groups to replicate virtual machines.

When you're replicating between different {{site.data.keyword.cloud}} Zerto instances, you can configure replication directly between the Zerto instances. If you're replicating between the {{site.data.keyword.cloud_notm}} Zerto instance and your own data center, you must install Zerto yourself in your own data center. This instance can license itself automatically when you pair it with the {{site.data.keyword.cloud_notm}} Zerto instance.

Zerto replication doesn't support Network Address Translation (NAT) traversal. Establishing connectivity between the {{site.data.keyword.cloud_notm}} Zerto instance and your own data center might require customization of routes on the Zerto Virtual Manager appliances or Zerto Virtual Replication Appliances (VRAs) on either side. Establishing connectivity might also require secure tunneling between the sites. When you're configuring or reconfiguring routes on Zerto Virtual Manager appliances, you must ensure that all Zerto Virtual Manager appliances can connect successfully to `zerto.com` for usage reporting. You can verify this connection by opening a browser session to `https://www.zerto.com` from the Zerto Virtual Manager appliance.

The Management VMware NSX Edge™ Services Gateway (ESG) is preconfigured to allow outbound HTTPS (TCP port 443) communications that originate from Zerto Virtual Manager.
{: note}

## Updating Zerto Virtual Replication
{: #managingzertodr-update}

To update Zerto Virtual Replication, open an IBM Support ticket by following the steps in [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support) to get the Zerto installation executable file for your environment.

## Deploying VRAs to newly added ESXi servers
{: #managingzertodr-deploy}

When you add or remove ESXi servers for the primary cluster of your instance, VRAs are automatically deployed or removed. VRAs aren't automatically deployed to ESXi servers in the secondary clusters of your instance. You can deploy VRAs yourself from the Zerto Virtual Replication console.

## Related links
{: #managingzertodr-related}

* [Zerto overview](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr)
* [Ordering Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering)
* [Ordering Zerto stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_ordering_licenses)
* [Managing Zerto stand-alone licenses](/docs/vmwaresolutions?topic=vmwaresolutions-zerto_managing_licenses)
* [Zerto product documentation](https://www.zerto.com/myzerto/technical-documentation/){: external}
* [Zerto disaster recovery](https://www.zerto.com/solutions/use-cases/disaster-recovery/){: external}

