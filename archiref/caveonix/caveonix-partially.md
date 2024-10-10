---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Partially distributed
{: #caveonix-partially}

After the automated deployment is completed, you can manually scale out by increasing RAM and disk in the initial virtual machine (VM) and add three scale-out VMs. The RiskForesight™ configuration script can be run to enable and configure the application components on all four VMs.

This deployment model is expected to service up to 500 assets with up to 30 days of data indexing.

Select the next available IP addresses from the {{site.data.keyword.cloud}} private portable subnet. Configure FQDN names in ADDNS.

Find the details of the base VM, scale-out VM, and Remote collector VM in the following table:
|Parameter | Value |
|--------- |------ |
| Type | Base |
| VM qty | 1 |
| vCPU | 16 |
| RAM | 64 GB |
| Disk | 1,000 GB |
| OS | CentOS 7 |
| Installed application components | UI, App, Plug-ins, Central collector, Index datastore, Messaging datastore, Relational datastore, Remote collector |
{: class="simple-tab-table"}
{: caption="Base VM parameters" caption-side="bottom"}
{: #table1}
{: tab-title="Base VM"}
{: tab-group="partially-caveonix"}

| Parameter | Value |
|---|---|
| Type | Scale-out |
| VM qty | 3 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 4 TB |
| OS | CentOS 7 |
| Installed application components | Data nodes (scale-out) |
{: caption="Scale-out VM parameters" caption-side="bottom"}
{: #table2}
{: tab-title="Scale-out VM"}
{: tab-group="partially-caveonix"}
{: class="simple-tab-table"}

| Parameter | Value |
|-----------|-------|
| VM qty | As required |
| vCPU | 8 |
| RAM | 8 GB |
| Disk | 1 TB |
| OS | CentOS 7 |
| Installed application components | Remote collector |
{: caption="Remote collector VM parameters" caption-side="bottom"}
{: #table3}
{: tab-title="Remote collector VM"}
{: tab-group="partially-caveonix"}
{: class="simple-tab-table"}
