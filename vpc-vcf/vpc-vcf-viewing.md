---

copyright:

  years: 2023

lastupdated: "2023-08-30"

keywords: view vmware cloud foundation instance, vmware cloud foundation instance, view instance, view vmware cloud edition instance

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Viewing VMware Cloud Foundation instances
{: #vpc-vcf-viewing}

View the summary and detailed information of the VMware Cloud Foundation™ instances that are provisioned in your account.

## Procedure to view a summary of VMware Cloud Foundation instances
{: #vpc-vcf-viewing-summary}

1. In the VMware Solutions console, click **Resources > Cloud Foundation** from the left navigation pane.
2. In the **VMware Cloud Foundation** table, review the name, location, creation time, and status of the provisioned instances.

## Procedure to view details for VMware Cloud Foundation instances
{: #vpc-vcf-viewing-details}

1. In the **VMware Cloud Foundation** table, click an instance name.
2. On the **Summary** tab, review the general information of the instance: the deployment infrastructure type, the resource group in which the resources are deployed, the {{site.data.keyword.vpc_full}} ({{site.data.keyword.vpc_short}}) region, and the zone where the instance is deployed. Click the plan to view the software bundles that are installed for the VMware Cloud Foundation instance.

3. Click the **Infrastructure** tab:
   1. In the **Domain** table, review the domain name, domain type, cluster number in the domain, NSX-T Edge cluster in the domain the public floating IP addresses in the domain.
   2. Click the table row to view the detailed information of the selected domain.
      * On the cluster details, view the number of hosts in this cluster.
      * Click the host profile to view the detailed information of the profile.
      * Click the storage type to view the disk information.
      * Click the subnets to view the {{site.data.keyword.vpc_short}} subnets created for this cluster. On the subnets table, click a subnet name to go to the subnet detail page.
      * On the hosts table, view the bare metal server name, the root user password, and the creation time. To go to the bare metal server details page on the {{site.data.keyword.vpc_short}} console, click the bare metal server name.

4. On the **Access Information** tab, view the default username and password for the VMware Cloud Foundation instance.
   * In the **Management domain** section, view the hostname, FQDN, and IP addresses for vCenter Server, VMware NSX-T Data Center, SDDC Manager, and VMware Aria Suite Lifecycle Manager. You can view or copy the password by clicking the icons.
   * For VMware Cloud Foundation instances with **Standard** architecture, in the **Workload domain** section, view the hostname, FQDN, and IP addresses for vCenter Server and VMware NSX-T Data Center. You can view or copy the password by clicking the icons.
   * In the **Windows jump server** section, you can view the public and private IP addresses and admin user password of the Windows jump server. If you did not select to create the jump server, the section is not displayed.

## Related links
{: #vpc-vcf-viewing-links}

* [VMware Cloud Foundation overview](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ovw)
* [Ordering VMware Cloud Foundation instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-ordering)
* [Deleting VMware Cloud Foundation instances](/docs/vmwaresolutions?topic=vmwaresolutions-vpc-vcf-deleting)
