---

copyright:

  years:  2019, 2024

lastupdated: "2024-02-06"

keywords: Red Hat OpenShift for VMware, manage OpenShift, OpenShift operations

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Managing Red Hat OpenShift for VMware
{: #ocp_managing}

Review the following information to manage your {{site.data.keyword.redhat_openshift_full}} for VMware® service after deployment.

## Rotating the Red Hat OpenShift certificates (required)
{: #ocp_managing-cert-rotation}

{{site.data.keyword.redhat_openshift_notm}} for VMware uses kubelet client certificates that must be rotated periodically for security purposes. {{site.data.keyword.redhat_openshift_notm}} mainly automates the rotation process, but requires manual approval of certificate signing requests (CSRs). Therefore, it is important that you understand the {{site.data.keyword.redhat_openshift_notm}} certificate rotation schedule to avoid expired certificates.  

The initial certificates that are created during installation expire 24 hours after they are created. IBM's automation process, which installs {{site.data.keyword.redhat_openshift_notm}}, handles the approval of the CSRs for this initial rotation, which is done by running a script on the bastion for the first 30 hours. The script is named `/root/approve-csr.sh` and its log file is named `/root/approve-csr.log`. 

For the script to run successfully, the initial `kubeadmin` credentials must be the same until the initial certificate rotation is complete. Do not change the kubeadmin credentials for the first 24 hours. If the credentials are changed, you must monitor and approve the CSRs for the initial certificate rotation. For more information, see [Approving the CSRs for your machines](https://docs.openshift.com/container-platform/4.14/installing/installing_vsphere/installing-vsphere.html#installation-approve-csrs_installing-vsphere){: external}.

Do not restart any of the {{site.data.keyword.redhat_openshift_notm}} cluster virtual machines (VMs) or the bastion VM until the first certificate rotation is done.
{: attention}

After the initial certificate rotation, certificates are renewed every 30 days. You must establish a process to approve the CSRs for every certificate rotation. According to {{site.data.keyword.redhat_full}}, you can approve CSRs when they reach 80% of their expiration period, which is approximately 25 days into the lifespan of the CSRs.

If you do not approve CSRs in time and the certificates expire, you can recover from expired control plane certificates and get the {{site.data.keyword.redhat_openshift_notm}} cluster operational again. For more information, see [Recovering from expired control plane certificates](https://docs.openshift.com/container-platform/4.14//backup_and_restore/control_plane_backup_and_restore/disaster_recovery/scenario-3-expired-certs.html){: external}.

## Resizing your Red Hat OpenShift VMs post-deployment
{: #ocp_managing-resize}

1. Log in to the bastion VM by using SSH.
2. Become the `root` user: `sudo -i`
3. Shut down the target VM: `ssh core@<vm-ip> sudo shutdown -h 0`
4. After the VM is powered off, resize the VM in vCenter Server.
5. Power on the VM.
6. In the {{site.data.keyword.redhat_openshift_notm}} console, go to **Compute > Nodes** and wait for the VM that was restarted to be back in a **Ready** state.
7. Complete the previous steps for all VMs.

## Changing the SSH key on the Red Hat OpenShift bastion VM
{: #ocp_managing-change-ssh-key}

The SSH key pair that is generated during installation is on the {{site.data.keyword.redhat_openshift_notm}} bastion VM. The location of the SSH key pair is displayed on the {{site.data.keyword.redhat_openshift_notm}} service details page. This SSH key was installed on all cluster VMs to allow SSH logins from the bastion without requiring a password.

It is recommended that a new SSH key pair is generated and used to replace the existing key. To generate a new
SSH key pair, use the instructions in [How to update ssh keys after installation in Openshift 4](https://access.redhat.com/solutions/3868301){: external}. You must run the commands from the bastion VM. For more information about logging in to the bastion, see [Bastion details](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview#ocp_overview-bastion).

## Expanding Red Hat OpenShift cluster with more workers
{: #ocp_managing-expand-cluster}

To expand your {{site.data.keyword.redhat_openshift_notm}} cluster by adding more worker VMs, complete the following steps:

1. Create a worker VM from the RHCOREOS template:
   1. Ensure that the VM is connected to the same network as the other {{site.data.keyword.redhat_openshift_notm}} worker VMs.
   2. Do not power on this VM yet because more configuration steps are required.

2. Prepare a worker ignition file on the bastion:
   1. For more information about logging in to the bastion, see [Bastion details](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview#ocp_overview-bastion).
   2. In the installation directory on the bastion, locate the worker ignition file named `worker.ign`. Create a base64 version of this file by using the command `base64 -w0 worker.ign > worker.ign.b64`. You will use the contents of the newly created `worker.ign.b64` file in the next step.

3. Set the VM attributes:
   1. Before you start, power off the VM. Then, go to the Configuration Parameters window, select the new worker VM, and click **Actions > Edit Settings**.
   2. In the Edit Settings window, click the **VM Options** tab. On the left, click **Advanced** to expand the **Advanced** section in the window. Then, scroll down to **Configuration Parameters** on the left. Click **Edit Configuration**.
   3. The Configuration Parameters window might have a long list of existing parameters for the VM. To add a value, click **Add Configuration Params**. Two empty fields that are labeled **Name** and **Value** are displayed for you to complete. Use this process for the following 3 steps.
   4. Create a value named `guestinfo.ignition.config.data` and set it to the contents of the base64-encoded ignition config file `worker.ign.b64` that was created earlier.
   5. Create a value named `guestinfo.ignition.config.data.encoding` and set it to the string `base64`.
   6. Create a value named `disk.EnableUUID` and set it to the string `TRUE`.
   7. After you create the new parameters, click **OK** twice to close the opened windows.

4. Create a DHCP binding for the worker VM:
   1. Log in to NSX-T™.
   2. Go to **Networking > Segments**.
   3. Edit the `ocp-internal` segment.
   4. Expand **DHCP Static Bindings** and click **Set** to open the Set Static Bindings window.
   5. Review the list of existing bindings and make a note of the next available IP address.
   6. Examine one of the existing worker bindings to look at information that you need later. Make a note of the gateway address and the DHCP options. To view the DHCP options, click **Set** next to **DHCP Options**. On the Options window, select **Generic Options** from the **Select DHCP Option** list. Make a note of the options that are set.
   7. Close the existing binding that you were examining to return to the Set Static Bindings window.
   8. Click **Add IPV4 Static Binding**. Complete the details for the new worker, including the DHCP options that you previously noted.
   9. When you are done, click **Save** to commit the changes.

5. Add a worker to the Load Balancer pools:
   1. Go to **Networking > Load Balancer > Server Pools**.
   2. Edit the server pool `ocp-apps`.
   3. In the edit window, under **Members/Group**, click the blue numerical link. The default is 3.
   4. When the Configure Server Pool Members window opens, click **Add Member**.
   5. Enter the new worker's name and IP address. Leave the port number empty.
   6. Click **Save** and then click **Apply**.

6. Create DNS records for the new worker:
   1. Log in to the AD NS server for your vCenter Server instance.
   2. Using the DNS Manager, add a new A record to the corresponding `ocp` zone. When you create the A record, ensure that the option to create associated PTR record is selected.

7. Approve any certificate signing requests (CSRs) from the bastion. During the provisioning of the new worker, you might have to [approve CSRs](https://docs.openshift.com/container-platform/4.14/installing/installing_vsphere/installing-vsphere.html#installation-approve-csrs_installing-vsphere){: external} from the bastion:
   1. Log in to the bastion as the `root` user and change to the bastion installation directory. For more information, see [Bastion details](/docs/vmwaresolutions?topic=vmwaresolutions-ocp_overview#ocp_overview-bastion).
   2. Before you can run any commands, you must authenticate to {{site.data.keyword.redhat_openshift_notm}}:
      * If authentication is not configured and you are using the default `kubeadmin` account and password, run the command `export KUBECONFIG=auth/kubeconfig` and verify that you are authenticated by running the command `./oc whoami`.
      * If other backends or users are authenticated, log in by using one of those accounts as explained in the {{site.data.keyword.redhat_openshift_notm}} documentation, for example, by running the command `./oc login`.
   3. Run `./oc get nodes` to see the new worker. If it is not in the **Ready** state, check repeatedly for pending CSRs by using the command `./oc get csr`, and then approve the CSRs by using the command `./oc adm certificate approve <csr_name>`. Continue to check until the configuration is complete and the new worker is in the **Ready** state.

      After the new worker is in **Ready** state, it can be used by {{site.data.keyword.redhat_openshift_notm}}.

8. Power on the VM:
   * After the VM is powered on, you can monitor the VM to see whether a problem exists. The VM gets an IP address, then processes the ignition file, and then opens a login prompt. 
   * After the login prompt is shown, it might be covered by console log messages. If required, press Enter a few times on the console. If the login prompt is present but covered with console log messages, press Enter to display the login prompt again. 
   * If the login prompt does not display, it is possible that:
      * The VM is not getting an IP address. Check the network that the VM is connected to. Also, check the DHCP binding settings.
      * The base64 value from `worker.ign.64` is not correct. It might be missing some characters or it has extra characters. Check the value to confirm.

      If you must change any settings because the VM didn't display a login prompt, power off the VM, change the necessary settings, and power it back on.

## Considerations when you delete Red Hat OpenShift for VMware
{: #ocp_overview-consid-remove}

* Before you delete {{site.data.keyword.redhat_openshift_notm}} for VMware, you must remove any additional VMs that you created in the `ocp` directory on VMware. The VMware Solutions automation removes only the items that were deployed during the initial installation of {{site.data.keyword.redhat_openshift_notm}} (VMs, storage, and NSX). Any node that is deployed after the installation is not cleaned up.
* The VXLAN, DLR, and the Edge Gateway that were created during the initial deployment of {{site.data.keyword.redhat_openshift_notm}} for VMware is deleted. The VMs that you deployed on VXLAN will lose connectivity after the removal of {{site.data.keyword.redhat_openshift_notm}} for VMware starts.
* If your cluster uses NFS storage, deleting {{site.data.keyword.redhat_openshift_notm}} deletes the NFS data store that was added during installation.
* If you are using a vSAN datastore, delete any persistent volumes that you no longer need before you uninstall {{site.data.keyword.redhat_openshift_notm}}. Any volumes that are not deleted will remain in the vSAN storage after the {{site.data.keyword.redhat_openshift_notm}} uninstallation.
* Before you delete the service, you must remove any personal VMs that were deployed with this service from the storage. {{site.data.keyword.redhat_openshift_notm}} only orders personal VMs if it’s not vSAN.

## Related links
{: #ocp_managing-related}

* [Ordering services for vCenter Server instances](/docs/vmwaresolutions?topic=vmwaresolutions-vc_addingservices)
* [Getting help and support](/docs/vmwaresolutions?topic=vmwaresolutions-trbl_support)
* [FAQ](/docs/vmwaresolutions?topic=vmwaresolutions-faq-vmwaresolutions)
