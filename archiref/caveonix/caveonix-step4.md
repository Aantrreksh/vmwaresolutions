---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Step 4 - Application setup
{: #caveonix-step4}

After the virtual machines (VMs) are deployed and the application components are installed, the Caveonix RiskForesight™ solution can be set up for the service provider and the first tenant or organization.

The Service Provider is the top-level organization. The service provider supports one or more tenants or organizations. The service provider assigns assets that are collected from the VMware vCenter appliance to the tenant or organization, who then assigns them to applications or subapplications. These applications are then subject to a compliance regime.

This step is initially completed by the {{site.data.keyword.vmwaresolutions_full}} automation that uses information that is supplied by the client during the ordering process and default information. The setup process can be started by the client, post deployment, to modify the Service Provider or Tenant Organization as required postinstallation.

The Service Provider setup has the following substeps.
1. Organization Detail - Add the details for the parent organization for your cloud service provider. This organization can have multiple physical locations and multiple data centers. Organizations for your tenants and suborganizations for your service provider are added later.
2. Locations – Map the infrastructure into RiskForesight "Locations”. The Assets are grouped by location, cloud provider, and asset repository.
3. Environments - Optional. Environments are a way to group assets. For example, VMware Solutions Support, DR Site, Production.
4. Cloud Provider - Add the “providers” that provide the infrastructure that your application runs on.
5. Asset Repositories - An Asset Repository associates a set of assets with an Organization, a Cloud Provider, and a Location.
6. Organizations - Create suborganization for your own operations and additional organizations - one for each of your service provider tenants. Each tenant must go through their own setup process - including creating their own suborganizations.
7. Organization Users - Create and assign Users to Tenant Organizations and Sub-Organizations of the Service Provider.
8. Task Scheduler – Configure tasks to complete the following actions: synchronize with the asset repository, perform SCAP vulnerability and compliance scans, collect NSX network flows, collect information about the software that is running on monitored assets, and collect syslog and system events for assets.

The Tenant or Organization Setup has the following substeps.
1. Organization - Add details for your primary organization. You can also create suborganizations. Use organizations to segment your users, or as one of the ways to group your assets. You can create more organizations with one of your existing organizations as parent. When you create a new organization, you can select the **Business Impact Value**, which is used to generate cyberrisk scores.
2. Organization Assets - New assets / workloads are automatically grouped by location, cloud provider, and asset repository. Assets can be assigned to only one organization at a time. The Service Provider needs to assign assets to an organization.
3. Associate Environment and Location – Optional. Environments are defined by the Service Provider.
4. Create Sub-Applications or Applications – Used to group assets across locations and organizations and see their associated flows and policies. Create applications that match business and IT services. For example, Application=SAP, Sub-Applications=SAP Front End, SAP Middle Tier, and SAP Back End. **Business Impact Value** corresponds to an application and compliance regimes apply to an application.
5. Remote Access - Remote Access is required to run scans on assets, can be a default service account or an asset-specific account.
6. Task Scheduler - Schedule scans to run on a periodic basis. The types of tasks include; SCAP Scan-Vulnerability, SCAP Scan-XCCDF, NSX Flow Scan, Software Scan, Log Extract Scan.

The following information is collected from the user at time of order and is used in the application setup.

|Setup stage |Parameter |
|---|---|
|Organization / Asset repositories | Organization name |
|Organization | Phone Number |
|Organization | Email |
|Organization / Asset Repositories | Address Line 1 |
|Cloud Provider / Asset Repositories |Name |
|Cloud Provider |Description |
|Cloud Provider |POC email |
|Cloud Provider |Type|
|Cloud Provider |POC Name |
|Cloud Provider |POC Phone |
{: caption="Table 1. Information collected from the user" caption-side="bottom"}

The following default information is used in the application setup.

| Setup stage | Parameter |
|---|---|
| Environment | Environment Name is set to “Initial”|
| Environment | Score is set to 5|
| Asset Repository | Two Asset Repositories are configured; vCenter and NSX Manager. Host URL set to `https://vCenter_fqdn` and `https://NSX Manager_fqdn` |
| Asset Repository | Two Asset Repositories are configured; vCenter and NSX Manager, both use the same username. Username set to vCenter administrator username|
| Asset Repository | Two Asset Repositories are configured; vCenter and NSX Manager, both use the same password. Password is set to vCenter administrator password
| Asset Repository | Two Asset Repositories are configured; vCenter and NSX Manager, both use the same password. Type is set to vCenter for one repository and NSX for the other
| Task | Four tasks are set up; Asset Scan, NSX Flows, VMware® Infrastructure Scan, and VMware Vulnerability. ScanName is set to DC1AssetScan, NSXFlows, VMWInfraScan, VMWVulnScan |
| Task | Four tasks are set up; Asset Scan, NSX Flows, VMware Infrastructure Scan, and VMware Vulnerability. Type is set to vCenter, NSX, VMwareInfrastructureScan, VMwareVulnerabilityScan |
| Task | Schedule is set to hourly for `DC1AssetScan` and daily for the others |
{: caption="Table 2. Default information used in application setup" caption-side="bottom"}
