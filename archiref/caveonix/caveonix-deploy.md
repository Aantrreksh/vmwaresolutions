---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Deployment models for Caveonix RiskForesight
{: #caveonix-deploy}

Review the deployment models for Caveonix RiskForesight™ along with the installation process.

When you select the {{site.data.keyword.vmwaresolutions_full}} RiskForesight option, you do not have to follow all the steps in the deployment as the initial ones are automated. However, if you want to scale out the solution after the initial deployment, a detailed understanding of the complete deployment and architecture is required.

The RiskForesight installation consists of the following high-level steps:

1. [Initial planning and prerequisites](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix-step1) – Understanding and selecting a deployment option, configuring DNS to provide FQDN/IP resolution for the application components.
2. [Virtual machine deployment](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix-step2) – Deploying the VMs from an OVF template. All application components are installed on the VM.
3. [Application configuration](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix-step3) – Running the Caveonix configuration script that configures the application components on each of the VMs.
4. [Application setup](/docs/vmwaresolutions?topic=vmwaresolutions-caveonix-step4) – Setting up the Service Provider and a Tenant or Organization so that the application becomes accessible for the users.

The automated installation provisions one VM and configures all the application components on that VM.
{: note}

## Deployment sizing
{: #caveonix-deploy-sizing}

The sizing of the deployment is calculated by using the following volumes.

| Data type | Volume |
|---|---|
| Scans per day | 1 |
| Scan data (MB) | 20 |
| Log data (MB) | 500 |
| Flow data (MB) | 200 |
| Asset data (MB) |46 |
| Total storage per asset per day (MB) | 766 |
| Data replication multiplier | 2 |
| Total index storage per asset per day (MB) | 1,532 |
{: caption="Volumes" caption-side="bottom"}

The Data Replication Multiplier is set to 2 as the Index store (Elastic Search) uses by default n+1 replication of the indexes.
{: note}

The number of scaling VMs is calculated from the number of assets and the number of days of data to index.

| Number of assets | 100 | 500 | 5000 |
|---|---|---|---|
| Days of data | 30 | 30 | 30 |
| Total index storage per asset per day (MB) | 1532 | 1532 | 1532 |
| Total index storage per asset per 30 days (TB) | 4 | 22 | 219 |
| Data supported per scaling node (TB) | 0 | 8 | 8 |
| Scaling VMs required | 0 | 3 |27 |
{: caption="Scaling VM parameters" caption-side="bottom"}

The following table shows how the amount of storage that is required is calculated.

| Number of assets |100 | 500 | 5,000 |
|---|---|---|---|
| Long-term data retention (months) | 8 | 8 | 8 |
| Total storage per asset per day (MB) | 766 | 766 | 766 |
| Days of data | 30 | 30 | 30 |
| Near-term data retention (TB) | 7 | 33 | 329 |
| Long-term data retention (TB) | 18 | 88 | 877 |
{: caption="Storage parameters" caption-side="bottom"}

From a data perspective, data is used as follows:
- Scan data is used in compliance management.
- Log data is used in forensic management.
- Policy and flow data are used in risk management. Flow data is available from NSX Manager only.

Data storage has three tiers:
- Replicated
- Near term
- Long term

The following table provides a summary of the deployments.

|Deployment model | All-in-one | Partially distributed | Fully distributed |
|---|---|---|---|
| Number of assets | 100 | 500 | 5,000 |
| Online data generated in 30 days (TB) | 4 | 22 | 219 |
| Nearline data retention (90 days) (TB) | 7 | 33 | 329 |
| Offline data retention (8 months) (TB) | 18 | 88 | 877 |
| Total data storage retention (1 year) (TB) | 28 |142 | 1,425 |
| Base VMs | 1 | 1 | 20 |
| Scaling VMs | 0 | 3 | 28 |
| Total VMs | 1 | 4 | 48 |
{: caption="Summary" caption-side="bottom"}

### Notes
{: ##caveonix-deploy-sizing-notes}

When you delete the Caveonix RiskForesight service, the {{site.data.keyword.vmwaresolutions_short}} automation deletes only the single all-in-one Caveonix VM that was deployed and the dedicated private subnet that was ordered for it. Therefore,
* If you scaled out the Caveonix VM into multiple VMs, those additional VMs are not removed.
* If you used the IP addresses of the dedicated private subnet on additional VMs, those VMs must be assigned new IP addresses to continue to function.
* If you delete {{site.data.keyword.vcf-auto}} instance A with the Caveonix RiskForesight service installed, and you used the IP addresses of the dedicated private subnet that is ordered for the service in {{site.data.keyword.vcf-auto-short}} instance B, the dedicated private subnet is canceled upon deletion of {{site.data.keyword.vcf-auto-short}} instance A.
