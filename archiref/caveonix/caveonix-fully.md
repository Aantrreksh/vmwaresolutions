---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Fully distributed
{: #caveonix-fully}

More base virtual machines (VMs) and scale-out VMs are added according to the number of assets and data retention requirements.

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
{: caption="Base - user interface" caption-side="bottom"}

The following table shows the applications and plug-ins parameters.

|Parameter | Value |
|---|---|
| Type | Base |
| VM qty | 2 |
| vCPU | 8 |
| RAM | 16 GB |
| Disk | 500 GB |
| OS | CentOS 7 |
| Installed application components | App, plug-ins |
{: caption="Base - applications and plug-ins" caption-side="bottom"}

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
{: caption="Base - Central collector" caption-side="bottom"}

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
{: caption="Base - relational database" caption-side="bottom"}

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
{: caption="Base - messaging datastore" caption-side="bottom"}

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
{: caption="Base - index datastore (primary nodes)" caption-side="bottom"}

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
{: caption="Database - index datastore (data nodes)" caption-side="bottom"}

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
{: caption="Scale-out - data nodes" caption-side="bottom"}

The following table shows the remote collector VM parameters.

|Parameter | Value |
|---|---|
| VM qty | As required |
| vCPU | 8 |
| RAM | 8 GB |
| Disk | 1 TB |
| OS | CentOS 7 |
| Installed application components | Remote collector |
{: caption="Remote collector" caption-side="bottom"}
