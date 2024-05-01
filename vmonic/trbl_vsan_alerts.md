---

copyright:

  years:  2016, 2024

lastupdated: "2024-04-29"

keywords: troubleshooting, SAN health, virtual SAN issue

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# How do I manage vSAN Health alerts and warnings?
{: #trbl_vsan_alerts}
{: troubleshoot}
{: support}

You might see alerts and warnings that relate to Virtual SAN (vSAN™) Health issues on the VMware vSphere® Web Client Monitor page.
{: tsSymptoms}

These warnings are nonissues and do not indicate functional problems.
{: tsCauses}

Use the following steps to clear the warnings from the vSphere Web Client:
{: tsResolve}

1. Go to http://partnerweb.vmware.com/service/vsan/all.json and save the JSON file, with the name `all.json`, on your local system.
2. Ensure that you completed the steps in [vCenter console timeout](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_timeout_vc_console).
3. On the details page of the instance, click **vCenter console**, and log in to the vSphere Web Client by using the credentials displayed on the {{site.data.keyword.vmwaresolutions_full}} console.
4. On the vSphere Web Client, go to **Manage > Settings** and open the **Virtual SAN > Health > HCL Database** section. Click **Update from file**, then upload the `all.json` file that you saved previously.
5. To clear the warnings, go to the **Alarms** pane on the upper right of the vSphere Web Client. Right-click each of the alarms, and select **Reset to green**.

For more information, see [How to download offline vSAN HCL file for vSAN Health Check plug-in](https://williamlam.com/2015/05/how-to-download-offline-vsan-hcl-file-for-vsan-health-check-plugin.html){: external}.

On the vSAN health page, the following warning might be displayed with the recommendation to restart host.
{: tsSymptoms}

`vSAN extended configuration in sync.`

The warning is a nonissue and does not indicate functional problems.
{: tsCauses}

Restart the vSAN Health page to resolve the issue.
{: tsResolve}

On the vSAN health page, the following warning message might be displayed.
{: tsSymptoms}

`You have not finished or skipped the cluster Quickstart. vSAN Health checks are suppressed.`

After you click **Go to Quickstart**, an informational message is displayed:

`vSAN alarms are supressed until the cluster is fully configured or this Quickstart workflow is skipped.`

These messages are nonissues and do not indicate functional problems.
{: tsCauses}

Click **Skip Quickstart**, and then click **Continue** to resolve the issue.
{: tsResolve}
