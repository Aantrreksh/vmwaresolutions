---

copyright:

  years: 2023

lastupdated: "2023-10-13"

keywords: backup proxy, how to create backup proxy

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Backup proxy
{: #veeam_proxies_backup_proxy}

A backup proxy is an architecture component that sits between the file share and other components of the backup infrastructure. The backup proxy operates as a data mover that transfers data between the source file share and the backup repository. The backup proxy processes jobs and delivers backup and restore traffic.

To create a backup proxy, complete the following steps: 

1. Start the Veeam Backup and Replication console.
2. Click **Backup infrastructure** in the left pane.
3. Select **Backup proxies** on the left panel.
4. Click **Add proxy** and select **Backup proxy**.
5. Select the backup server from the **Choose server** list and add the **Max concurrent tasks**.
6. Add traffic rules.
7. Review the changes and click **Finish**.

Sometimes, the backup proxy might not be able to use some transport modes due to known limitations. For more information, see [Transport modes](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes). If you assign the backup proxy role to a hardened repository, only the network mode is available. Other transport modes are grayed out.
{: note}

## Related links
{: #veeam_proxies_backup_proxy-links}

* [Add endurance storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_req#veeam_proxies_req-links)
* [VMware backup proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_vmware_backup_proxy)
* [VMware CDP proxy](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_vmware_cdp_proxy)
* [Transport modes](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_proxies_transp_modes)

