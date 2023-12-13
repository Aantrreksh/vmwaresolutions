---

copyright:

  years:  2016, 2023

lastupdated: "2023-10-31"

keywords: vCenter Server Hybridity add service, view service vCenter Server Hybridity, remove service vCenter Server Hybridity

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Ordering, viewing, and deleting services for vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingremovingservices}

You can order services for your VMware vCenter Server® with Hybridity Bundle instance, such as a disaster recovery solution. When you no longer need these services, you can delete them from your instance.

## Available services for vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingremovingservices-available-services}

The following services are available to VMware vCenter Server with Hybridity Bundle instances, together with the installed service versions.

| Service name | Current version |
|--------------|-----------------|
| [Caveonix RiskForesight](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix_considerations) | 5.0 |
| [F5 BIG-IP](/docs/vmwaresolutions?topic=vmwaresolutions-f5_considerations) | BIG-IP VE 17.1 |
| [FortiGate Virtual Appliance](/docs/vmwaresolutions?topic=vmwaresolutions-fortinetvm_considerations) | 7.4.1 |
| [Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-juniper-overview) | 3.0 (23.2R1) |
| [Veeam](/docs/vmwaresolutions?topic=vmwaresolutions-veeamvm_overview) | 12 |
| [VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview) | VMware Aria® Operations™ 8.12.1 and VMware Aria Operations™ for Logs 8.12 |
| [Zerto](/docs/vmwaresolutions?topic=vmwaresolutions-addingzertodr) | 9.7u3 |
{: caption="Table 1. Available services for vCenter Server with Hybridity Bundle instances" caption-side="bottom"}

## Procedure to add services to vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingremovingservices-adding-procedure}

To apply a service to your vCenter Server with Hybridity Bundle instance, click the links in the table to review the considerations for the service. Then, check the components that are deployed and follow the instructions in the ordering topics to place your order.

### Service installation results
{: #vc_hybrid_addingremovingservices-adding-results}

When the installation of the service is completed successfully, you are notified by email, and the service is displayed on the **Services** tab of the instance details with the **Installed** status.

## Procedure to view services for vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingremovingservices-viewing-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance for which you want to view services.
3. Click the **Services** tab and click a service to review information about it, such as the service status and other details.
4. Depending on the viewed service, you can access the service console by using the credentials that are provided on the service details page and you can manage the service from here.

## Procedure to delete services for vCenter Server with Hybridity Bundle instances
{: #vc_hybrid_addingremovingservices-removing-procedure}

1. From the {{site.data.keyword.vmwaresolutions_short}} console, click **Resources > vCenter Server** from the left navigation pane.
2. In the **vCenter Server** table, click the instance for which you want to delete services.
3. Click the **Services** tab and locate the service instance that you want to delete and click the **Delete** icon.
4. In the **Delete service** window, review the considerations or warnings if there are any. Select **I understand** and click **Delete**.

### Results after you delete a service
{: #vc_hybrid_addingremovingservices-removing-results}

After your request to delete a service is accepted, the service status is changed to **Removing**.

When the service deletion is completed successfully, you are notified by email, and the service is deleted from the **Services** page of the instance.

You are billed until the end of the {{site.data.keyword.cloud_notm}} infrastructure billing cycle for the deleted services.
{: note}
