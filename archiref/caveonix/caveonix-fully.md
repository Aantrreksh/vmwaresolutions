---

copyright:

  years:  2016, 2022

lastupdated: "2022-12-28"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Fully distributed
{: #caveonix-fully}

Additional base virtual machines (VMs) and scale-out VMs are added according to the number of assets and data retention requirements.

The following table shows the user interface parameters.

| Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 2 |
| vCPU | 2 |
| RAM | 6 GB |
| Disk | 60 GB |
| OS |CentOS 7|
| Installed application components | UI |
{: caption="Table 1. Base - user interface" caption-side="bottom"}

The following table shows the applications and plug-ins parameters.

|Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 2 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 500 GB |
| OS | CentOS 7 |
| Installed application components | App, Plugins|
{: caption="Table 2. Base - applications and plug-ins" caption-side="bottom"}

The following table shows the central collector parameters.

| Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 3 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 500 GB |
| OS | CentOS 7 |
| Installed application components | Central collector (cluster) |
{: caption="Table 3. Base - Central collector" caption-side="bottom"}

The following table shows the relational database parameters.

| Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 2 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 1 TB |
| OS | CentOS 7 |
|Installed application components | Relational datastore (primary or secondary) |
{: caption="Table 4. Base - relational database" caption-side="bottom"}

The following table shows the messaging datastore parameters.

| Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 3 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk |1 TB |
| OS | CentOS 7 |
| Installed application components | Messaging datastore (cluster) |
{: caption="Table 5. Base - messaging datastore" caption-side="bottom"}

The following table shows the index datastore parameters for the primary nodes.

| Parameter | Value |
|---|---|
| Type | Base |
| VM qty |3 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 1 TB |
| OS | CentOS 7 |
| Installed application component |Index Datastore (Primary Nodes) |
{: caption="Table 6. Base - index datastore (primary nodes)" caption-side="bottom"}

The following table shows the index datastore parameters for the data nodes.

| Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 5 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 4 TB |
| OS | CentOS 7 |
| Installed application components | Index datastore (data nodes) |
{: caption="Table 7. Database - index datastore (data nodes)" caption-side="bottom"}

The following table shows the scale-out VM data nodes parameters.

| Parameter | Value |
|---|---|
| Type | Scale-out |
| VM qty | 28 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 4 TB |
| OS | CentOS 7 |
| Installed application components | Data nodes (scale-out) |
{: caption="Table 8. Scale-out - data nodes" caption-side="bottom"}

The following table shows the remote collector VM parameters.

|Parameter | Value |
|---|---|
| VM qty | As required |
| vCPU | 8 |
| RAM | 8 GB |
| Disk | 1 TB |
| OS | CentOS 7 |
| Installed application components | Remote collector |
{: caption="Table 9. Remote collector" caption-side="bottom"}
