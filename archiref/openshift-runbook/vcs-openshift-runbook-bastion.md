---

copyright:

  years:  2019, 2024

lastupdated: "2024-06-12"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Red Hat OpenShift Bastion node setup
{: #openshift-runbook-runbook-bastion-intro}

To enable the deployment, a virtual machine (VM) is provisioned to run the {{site.data.keyword.redhat_openshift_full}} installation steps and host an HTTP Server. This VM is known as the bastion node. The bastion node is connected to the {{site.data.keyword.redhat_openshift_notm}} logical switch and the ESG firewall and NAT rules are configured to allow SSH access from the jump-server or remote device.

The bastion node runs {{site.data.keyword.redhat_full}} Enterprise Linux®, and it is used to host the scripts, files, and tools to provision the bootstrap, control-plane, and compute nodes. After the deployment, it is recommended to keep the bastion node as an administrative node for the cluster.

The bastion node setup consists of the following steps:

1. Provision a {{site.data.keyword.redhat_notm}} VM.
2. Register the {{site.data.keyword.redhat_notm}} VM.
3. Install NGINX (HTTP Server).
4. Generate an SSH private key and add it to the agent.

## Provisioning a Red Hat VM
{: #openshift-runbook-runbook-bastion-prov-red-hat}

Provision a {{site.data.keyword.redhat_notm}} VM based on the following specifications. Use the vCenter Server user interface or by using the PowerCLI script that is documented later in this document to provision the VM. Record you NAT address, which is configured in the NSX ESG.

| VM | IP address | Gateway | Disk (GB) | Memory (GB) | vCPU | NAT address |
| --- | --- | --- | --- | --- | --- | --- |
| `bastion` | 192.168.133.8 | 192.168.133.1 | 50 | 2 | 1 | 10.208.59.197 |
{: caption="Red Hat VM - provision" caption-side="bottom"}

Use the following table to record your deployment details:

| Parameter | Example | Your deployment |
| --- | --- | --- |
| vCenter Server IP address | | |
| vCenter Server user | | |
| vCenter Server password | | |
| Logical Switch | `OpenShift-LS` | |
| vCenter Server instance data store | `vsanDatastore` | |
| VM name | `bastion` | | |
| ISO file name | `rhel-8.x-x86_64-dvd.iso` | |
| IP address | 192.168.133.8 | |
| Netmask |255.255.255.0  | |
| Default gateway | 192.168.133.1 | |
{: caption="Red Hat VM deployment" caption-side="bottom"}

Before you begin, create the VM by using the vCenter CLI or the following PowerCLI script.

```psh
# Connect to vCenter
connect-VIserver –server <IP_Address> -User <UserName> -Password '<Password>'

# Create VM
$ls = get-nsxtransportzone | get-nsxlogicalswitch OpenShift-LS | Get-NsxBackingPortGroup | Select-Object Name
$ds = get-datastore -Name vsanDatastore
$vm = New-VM -Name bastion -Datastore $ds -DiskGB 50 -DiskStorageFormat Thin -MemoryGB 2 -NumCpu 1 -Notes "OpenShift Bastion node" -NetworkName $ls.name -GuestId rhel8_64Guest

# Connect a CD Drive loaded with the RHEL ISO
New-CDDrive -VM $vm -IsoPath "[vsanDatastore] ISO\rhel-8.x-x86_64-dvd.iso" -StartConnected

#Start the VM
Start-VM -VM $vm

# Disconnect
Disconnect-NsxServer
```
{: pre}

After the VM starts, connect to the VM by using the web console or remote console and complete the following installation steps. If needed, see the {{site.data.keyword.redhat_notm}} Enterprise Linux documentation.
1. Select the required language.
2. Set the date and time.
3. Configure the network and hostname.
4. Select the installation destination.
5. Set the root password.
6. Create a user.

## Registering the Red Hat VM
{: #openshift-runbook-runbook-bastion-register}

For this step, you require your {{site.data.keyword.redhat_notm}} subscription details:
* Username
* Password
* Subscription Pool

After the bastion node is deployed, you are required to register and subscribe it with the {{site.data.keyword.redhat_notm}} public repositories. From the jump-host or remote device, SSH to connect to the bastion node. Use the `su` command to get root privileges and run the following commands after you replace the username, password, and pool with your variables.

```bash
export rhel_subscription_username=<email address>
export rhel_subscription_password=<password>
sudo subscription-manager register --username=${rhel_subscription_username} --password=${rhel_subscription_password} --force
subscription-manager refresh
subscription-manager attach --pool=<pool>
subscription-manager repos --disable="*"
subscription-manager repos --enable  rhel-8-server-rpms
subscription-manager repos --enable  rhel-8-server-extras-rpms
subscription-manager repos --enable  rhel-server-rhscl-8-rpms
```
{: pre}

## Installing NGINX (HTTP Server)
{: #openshift-runbook-runbook-bastion-http}

The deployment of the {{site.data.keyword.redhat_openshift_notm}} nodes uses Ignition, and this process requires an HTTP Server to be available to download the required configuration. This deployment uses an NGINX instance that runs on the bastion node. To install NGNIX, complete the following steps after you are connected to the bastion node and have root privileges:

1. Use a text editor such as vi to create the following file `vi /etc/yum.repos.d/nginx.repo`.
2. Type `i` to insert and paste the following information into the file:

   ```bash
   [nginx]
   name=nginx repo
   baseurl=http://nginx.org/packages/mainline/rhel/8/$basearch/
   gpgcheck=0
   enabled=1
   ```
   {: pre}

3. Press Esc to get back to command mode and then type `:wq` to save the file and exit vi.
4. Use the `yum` command to install the NGINX package.

   ```bash
   yum update
   yum install -y nginx
   ```
   {: pre}

5. Create the default configuration file `vi /etc/nginx/conf.d/default.conf`.
6. Type `i` to insert and paste the following information into the file:

   ```json
   server {
       listen       80;
       server_name  localhost;

       #charset koi8-r;
       #access_log  /var/log/nginx/host.access.log  main;

       location / {
           root   /usr/share/nginx/html;
           index  index.html index.htm;
       }
   }
   ```
   {: pre}

7. Press Esc to get back to command mode and then type `:wq` to save the file and exit vi.
8. Run the following commands to start NGINX.

   ```bash
   systemctl enable nginx
   systemctl start nginx
   ```
   {: pre}

9. The Linux firewall needs to configured to enable HTTP by using the following firewall-cmd commands:

   ```bash
   firewall-cmd --permanent --zone=public --add-service=http
   firewall-cmd --reload
   ```
   {: pre}

## Generating an SSH private key and add it to the agent
{: #openshift-runbook-runbook-bastion-sshkey}

For the {{site.data.keyword.redhat_openshift_notm}} container platform clusters on which you want to perform installation debugging or disaster recovery, you must provide an SSH key that your ssh-agent process uses to the installer.

You can use this key to SSH into the nodes as the user core. When you deploy the cluster, the key is added to the core user’s `~/.ssh/authorized_keys` list.

You must use a local key.

### Creating the SSH key
{: #openshift-runbook-runbook-sshkey-create}

1. In the SSH session on the bastion node, run the following command, which generates a public or private `rsa` key pair in the directory `/root/.ssh`:

   ```bash
   ssh-keygen -f ~/.ssh/id_rsa -t rsa -b 4096 -N ''
   ```
   {: pre}

   The private key is `/root/.ssh/id_rsa` and the public key is `/root/.ssh/id_rsa.pub`.

2. Start the ssh-agent process as a background task:

   ```bash
   eval "$(ssh-agent -s)"
   ```
   {: pre}

3. Add your SSH private key to the ssh-agent:

   ```bash
   ssh-add /root/.ssh/id_rsa
   ```
   {: .pre}

## Downloading the installation tools
{: #openshift-runbook-runbook-bastion-install-red-hat}

For more information about installing {{site.data.keyword.redhat_openshift_notm}} 4.14, see [Installing a cluster on vSphere with user-provisioned infrastructure](https://docs.openshift.com/container-platform/4.14/installing/installing_vsphere/upi/installing-vsphere.html){: external}.

For more information about how to access the {{site.data.keyword.redhat_openshift_notm}} user provider infrastructure, see [Internet and Telemetry access for {{site.data.keyword.redhat_openshift_notm}} Container Platform](https://docs.openshift.com/container-platform/4.14/installing/installing_vsphere/upi/installing-vsphere.html#cluster-entitlements_installing-vsphere){: external}.

Before you install the {{site.data.keyword.redhat_openshift_notm}} Container Platform, you need to download a number of files onto the bastion node and then extract them. The following actions are completed:
* Download `unzip` to extract the downloaded files.
* Create an installation directory and make it the working directory.
* Download the {{site.data.keyword.redhat_openshift_notm}} installation and client tools.
* Extract the downloaded bundles.
* Move commands to `/usr/local/bin` for ease of use.
* Install Git to download the {{site.data.keyword.redhat_openshift_notm}} installer.
* Clone the installer repository to the bastion node.
* Download and extract Terraform to the `/usr/local/bin` directory for ease of use.

These commands are used in the SSH session to the bastion node that has root privileges. Replace 4.x with the current {{site.data.keyword.redhat_openshift_notm}} version, for example, 4.14.

```bash
# Download unzip
yum install -y wget unzip

# Create an installation directory and make it the working directory
mkdir -p /opt/ocpinstall
cd /opt/ocpinstall

# Download the OpenShift installer and client tools
wget https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest-4.x/openshift-client-linux.tar.gz
wget https://mirror.openshift.com/pub/openshift-v4/clients/ocp/latest-4.x/openshift-install-linux.tar.gz

# Extract the downloaded bundles
tar -xvf openshift-client-linux.tar.gz
tar -xvf openshift-install-linux.tar.gz

# Move commands to /usr/local/bin for ease of use
mv kubectl oc openshift-install /usr/local/bin
mv openshift-install /usr/local/bin

# Install git and clone the OpenShift installer
yum install -y git
git clone -b release-4.x https://github.com/openshift/installer

# Download and extract terraform
wget https://releases.hashicorp.com/terraform/0.11.13/terraform_0.11.13_linux_amd64.zip
unzip terraform_0.11.13_linux_amd64.zip
mv terraform /usr/local/bin
```
{: pre}

The Bastion node is now ready for the steps to install {{site.data.keyword.redhat_openshift_notm}} 4.14, which are described in [{{site.data.keyword.redhat_openshift_notm}} 4.14 user provider infrastructure installation](/docs/vmwaresolutions?topic=vmwaresolutions-openshift-runbook-runbook-install-intro).

## Related links
{: #vcs-openshift-runbook-bastion-related}

* [Installing a cluster on vSphere with user-provisioned infrastructure](https://docs.openshift.com/container-platform/4.14/installing/installing_vsphere/upi/installing-vsphere.html){: external}
* [Using the vi text editor](http://etutorials.org/Linux+systems/red+hat+linux+bible+fedora+enterprise+edition/Part+II+Using+Red+Hat+Linux/Chapter+4+Using+Linux+Commands/Using+the+vi+Text+Editor/){: external}
