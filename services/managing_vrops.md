---

copyright:

  years:  2019, 2023

lastupdated: "2023-06-12"

keywords: VMware Aria console, VMware Aria license, login VMware Aria console, vRealize console

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing VMware Aria Operations and VMware Aria Operations for Logs
{: #managing_vrops}

## Accessing the VMware Aria Operations Manager console
{: #managing_vrops-access-vrops-console}

To access the VMware Aria® Operations™ Manager console, complete the following steps:

1. On the service details page for VMware Aria Operations and VMware Aria Operations™ for Logs, click **VMware Aria Operations Manager console**.
2. Log in by using the credentials listed on the same service details page.
3. When you log in to the VMware Aria Operations Manager console for the first time after installation, the VMware Aria Operations Manager Configuration wizard prompts you to enter your license (product key). Ensure that you select the **Product evaluation (no key required)** option to proceed.

## Starting the adapter instance for vSAN
{: #managing_vrops-start-adapter}

You must manually start the Management Pack adapter instance for vSAN™. Complete the following steps:

1. Log in to the VMware Aria Operations Manager console.
2. Click the vSAN adapter.
3. Click Edit, then test the connection and accept the certificate when prompted.
4. Start the adapter instance.

## Accessing the VMware Aria Operations for Logs console
{: #managing_vrops-access-vlog-console}

To access the VMware Aria Operations for Logs console, complete the following steps:

1. On the service details page for VMware Aria Operations and VMware Aria Operations for Logs, click **VMware Aria Operations for Logs console**.
2. Log in by using the credentials listed on the same service details page.

## Redeploying VMware Aria Operations and VMware Aria Operations for Logs
{: #managing_vrops-redeploy-vrops}

You might encounter a situation where the file systems become filled to approximately 98% capacity. This scenario can result in inconsistencies with a Cassandra database or with the VMware Aria suite of products that are deployed with IBM automation.

If VMware Aria Operations and VMware Aria Operations for Logs are deployed with IBM automation, you can remove the service or product. Use the VMware Solutions console to remove the service or product. Then, use the VMware Solutions console to redeploy it.

If you deployed the service or product in another way, you must redeploy it using the process that you originally used for deployment.

## Known issues
{: #managing_vrops-issues}

Some of the following warnings might appear. You can ignore these warning messages:
* NSX Logical Router is violating NSX Hardening guide (targeting workload-nsx-dlr)
* NSX Routing Edge Service is violating the NSX Hardening guide (targeting customer-nsx-edge)
* NSX Manager is violating NSX Hardening guide
* No backup of the environment is recorded

## Related links
{: #managing_vrops-related}

* [VMware Aria Operations and VMware Aria Operations for Logs overview](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_overview)
* [Ordering VMware Aria Operations and VMware Aria Operations for Logs](/docs/vmwaresolutions?topic=vmwaresolutions-vrops_ordering)
