---

copyright:

  years:  2016, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# HCX troubleshooting
{: #hcxclient-troubleshooting}

Review the following information for common HCX™ issues and fixes.

## HCX Client user interface issues
{: #hcxclient-troubleshooting-hcx-client-issues}

### HCX user interface token timeout
{: #hcxclient-troubleshooting-hcx-ui-issues}

Typically, if the {{site.data.keyword.vcf-auto}} user interface has been opened for some time you might encounter a timeout in the HCX™ user interface, because the login token to the HCX Manager server timed out. Log out of the vSphere web user interface and back in to refresh the token.

### HCX Client user interface displaying “NaN” for all metrics on the dashboard screen
{: #hcxclient-troubleshooting-nan-display}

This issue is related to the permissions of the currently logged in vCenter account. Ensure that the Enterprise Administrator group is set in the HCX cloud side appliance manager user interface.

## Migration issues
{: #hcxclient-troubleshooting-mig-issues}

Migration issues in the current versions of HCX are usually in three categories: licensing, cloud gateway networking connectivity, and destination hardware compatibility.

### Licensing
{: #hcxclient-troubleshooting-licensing}

If a migration fails because of a licensing issue, current versions of HCX clearly display this issue in the error message with the client web user interface within the vCenter user interface.

### Network (WAN) connectivity
{: #hcxclient-troubleshooting-wan-connect}

If you have any WAN connectivity issues, always check the **Interconnect -> HCX Components** screen within the HCX user interface for tunnel status. The fleet components typically do not need to be reset or rebooted. If WAN connectivity is restored, they reconnect automatically.

If any fixes and updates were applied to the HCX managers (Client and Cloud) and those updates also patch issues with the fleet components, you must redeploy the Cloud Gateway and any L2Cs deployed. It is possible to do further tunnel status debugging, by connecting to HCX Manager through an SSH client such as `ccli`.

1. SSH to HCX Manager by using the admin account and the supplied password.
2. Run the `su –` command and enter the password of the `root` user (same as admin password) to change to root.
3. Change the directory to `/opt/vmware/bin` and run the `./ccli` command. If this attempt is not successful because the environment is not set up for root, run the `./ccliSetup.pl` command.
4. Run the `list` command within the `ccli` shell to list the fleet components registered with HCX Manager.
5. Specify the fleet ID for the `ccli` by typing the ID listed for the fleet component. For example, `go 8`.
6. Run the `debug remoteaccess enable` command to connect by using SSH to the wanted fleet component.
7. Exit `ccli` and connect by using SSH to the IP address of the SSH-enabled fleet component.
8. Continue to troubleshoot.
9. Return to the `ccli` and disable the `ssh` service for the component.
10. If necessary, use the `hc` ccli command to run a health check on the components.

## Destination hardware compatibility issues
{: #hcxclient-troubleshooting-hw-compatibility}

vMotion migration can be an issue when the client source side is of newer hardware version and vSphere release than the cloud. Since replication-based migration copies data to a newly built virtual machine (VM) on the destination side, changing the migration type to “Bulk Migration” allows the migration to succeed in most cases.

## Stretched L2 Concentrator issues
{: #hcxclient-troubleshooting-stretched-l2}

If the L2C loses connectivity it reconnects automatically after the network connectivity is restored. Use the ccli shell to check health and operation. After SSH is enabled and the L2C is connected, run the `ip tunnel` and `ip link |grep t_` commands to view the status of the tunnels.

## Related links
{: #hcxclient-troubleshooting-related}

* [Glossary of HCX components and terms](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-components)
* [Preparing the installation environment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-planning-prep-install)
* [HCX Client deployment](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-client-deployment)
* [HCX on-premises Service Mesh](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-vcs-mesh-deployment)
* [VMware Hybrid Cloud migrations](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-migrations)
* [Monitoring parameters and components](/docs/vmwaresolutions?topic=vmwaresolutions-hcxclient-monitoring)
