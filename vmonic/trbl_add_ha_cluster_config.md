---

copyright:

  years:  2016, 2024

lastupdated: "2024-05-24"

keywords: troubleshooting, vSphere configuration issue, HA cluster issue

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Why do I see a vSphere console configuration issue when I add a high-availability cluster?
{: #trbl_add_ha_cluster_config}
{: troubleshoot}

When you add a High Availability (HA) cluster configuration with only one file share, the following configuration issue is seen on the VMware ESXi™ hosts:
{: tsSymptoms}

`The number of heartbeat datastores for host is 1, which is less than required: 2`

This issue occurs if redundancy is not in shared storage to allow for data store heart beating.
{: tsCauses}

For more information about how to fix the problem, see [HA error: "The number of heartbeat datastores for host is 1, which is less than required: 2"](https://knowledge.broadcom.com/external/article/318871/ha-error-the-number-of-heartbeat-datasto.html){: external}.
{: tsResolve}
