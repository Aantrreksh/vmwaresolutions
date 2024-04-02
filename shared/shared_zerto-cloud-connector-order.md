---

copyright:

  years:  2021, 2024

lastupdated: "2024-04-02"

keywords: zerto, order zerto cloud connector

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering a Zerto Cloud Connector
{: #shared_zerto-cc-order}

{{site.data.content.shared-deprecated-note}}

Optionally order Zerto Cloud Connector (ZCC) as an enhanced Zerto option to link on-premises workloads to {{site.data.keyword.cloud}} and replicate on-premises virtual machines (VMs) to {{site.data.keyword.cloud_notm}}. The Zerto and ZCC services seamlessly integrate as a managed solution to help your enterprise achieve VM replication and disaster recovery. You can order one ZCC per virtual data center.

## Before you begin
{: #shared_zerto-cc-order-prereq}

Review the following limitations that currently exist for ZCC:

* You can create a ZCC only if you have a network that is created in VMware® Cloud Director. Ensure that you do not delete that network, either while the ZCC order is in progress or later.
* If you are ordering a Zerto Cloud Connector, you cannot use the following IP subnets for your on-premises Virtual Replication Appliance or Zerto Virtual Manager deployments:
   * For the Dallas locations:
      * 172.16.3.0/24 - Management
      * 10.37.7.0/24 - DAL13
      * 10.5.30.0/24 - DAL10
      * 10.184.193.0/24 - DAL12
   * For the Frankfurt locations:
      * 172.16.7.0/24 - Management
      * 10.215.201.0/24 - FRA02
      * 10.240.220.0/24 - FRA04
      * 10.13.28.0/24 - FRA05
* You must create Organization networks before you order a ZCC. For more information, see [Creating a network](/docs/vmwaresolutions?topic=vmwaresolutions-shared_vcd-ops-guide#shared_vcd-ops-guide-create-network).

## Procedure to order a Zerto Cloud Connector from the virtual data center
{: #shared_zerto-cc-order-procedure}

1. Under **Enabled services** on the virtual data center details page, click **Order a Zerto Cloud Connector**.
2. Select an organization network and enter the IP address for the new VM to deploy to that network.
3. Review the hourly price and click **Order**. The **Zerto Cloud Connector (ZCC)** table displays on the virtual data center details page and the status changes to **Creating**.
4. You must pair the on-premises workloads to {{site.data.keyword.cloud_notm}} before you can use ZCC. Generate a pairing token when the ZCC status changes to **Ready to use**.
   1. In the **Zerto Cloud Connector (ZCC)** table, expand **Pairing token**.
   2. Click **Generate token**. The generated token link expires in 48 hours and a new token is generated.
   3. Click the **Copy** icon ![Copy icon](../../icons/copy.svg "Copy") to copy the pairing token key.
   4. From the on-premises site, use the pairing token key to link the on-premises virtual data centers to {{site.data.keyword.cloud_notm}}. For more information, see [Zerto technical documentation](https://help.zerto.com/category/WmWare_9.7){: external}.

## Related links
{: #shared_zerto-cc-order-related}

* [VMware Shared overview](/docs/vmwaresolutions?topic=vmwaresolutions-shared_overview)
* [Ordering virtual data centers](/docs/vmwaresolutions?topic=vmwaresolutions-shared_ordering)
* [Accessing the Zerto Self-Service Portal](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-portal)
* [Viewing Zerto Cloud Connector details](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-view)
* [Deleting Zerto Cloud Connector](/docs/vmwaresolutions?topic=vmwaresolutions-shared_zerto-cc-delete)
* [Zerto for VMware vSphere](https://www.zerto.com/solutions/workloads-and-applications/vmware-vsphere/){: external}
* [Zerto Support and Services](https://www.zerto.com/support-and-services/){: external}
