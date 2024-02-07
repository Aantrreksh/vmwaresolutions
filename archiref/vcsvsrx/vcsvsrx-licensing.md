---

copyright:

  years:  2019, 2024

lastupdated: "2024-02-02"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# vSRX base and advanced licensing
{: #vcsvsrx-licensing}

The vSRX is ordered and deployed with the necessary license keys to operate. Advanced licensing is only available directly from Juniper Networks®. Licenses can be procured from the Juniper Networks License Management System (LMS).

For more information, see [Licensing guide](https://www.juniper.net/documentation/us/en/software/license/juniper-licensing-user-guide/index.html){: external}.

## Adding license keys from the CLI
{: #vcsvsrx-licensing-add-new}

You can add a license key from a local file, from a remote URL, or from the terminal.

To install a license from the CLI, use the `request system license add` operational mode command. You can add the license from a local file or from a remote URL that contains the license key, or you can paste the license key in the terminal.

```text
user@vsrx> `request system license add terminal`

  [Type ^D at a new line to end input,
 enter blank line between each license key]

 E413XXXX57  aaaaaa bbbbbb cccccc dddddd eeeeee ffffff
 cccccc bbbbbb dddddd aaaaaa ffffff aaaaaa
aaaaaa bbbbbb cccccc dddddd eeeeee ffffff
cccccc bbbbbb dddddd aaaaaa ffffff

  E413XXXX57: successfully added

  add license complete (no errors)
```

You can save the license key to a file and upload the file to the vSRX file system through FTP or Secure Copy. Then, you can use the `request system license add file-name` command to install the license.
{: note}

Optionally, use the `show system license` command to view details of the licenses.
```sh
    root@host> `show system license`
```

The license key is installed and activated on the vSRX instance.

## Related links
{: #vcsvsrx-licensing-related}

* [Getting started with {{site.data.keyword.cloud_notm}} Juniper vSRX](/docs/vsrx?topic=vsrx-getting-started)
* [Understand vSRX Virtual Firewall with VMware](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/concept/security-vsrx-vmware-overview.html){: external}
* [Requirements for vSRX Virtual Firewall on VMware](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/concept/security-vsrx-vmware-system-requirement.html){: external}
* [Install vSRX Virtual Firewall with VMware vSphere Web Client](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-vmware/topics/task/security-vsrx-vsphere-client-installing.html){: external}
* [Configure a vSRX Virtual Firewall Chassis Cluster in Junos OS](https://www.juniper.net/documentation/us/en/software/vsrx/vsrx-consolidated-deployment-guide/vsrx-hyper-v/topics/task/security-vsrx-chassis-cluster-configuring.html){: external}
* [Configure ECMP on VMware NSX](https://letsv4real.com/2016/09/23/configure-ecmp-on-vmware-nsx/){: external}
