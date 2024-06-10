---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Configuring the automation server
{: #veeam-cr-sag-ascfg}

The automation server is used to host Ansible®. The following architecture describes Ansible:

* **One Ansible control node** - The Ansible control node is the place where Ansible is installed, and can access the Ansible Linux® hosts over Secure Shell (SSH), and Ansible Windows® hosts that are configured with Windows Remote Management (WinRM). The following items are required by Ansible:
   * A nonroot user with sudo privileges.
   * An SSH key pair associated with this user.
   * An inventory file that contains information about the Ansible hosts to be managed with Ansible.
   * A playbook that details the tasks to be carried out on the Ansible hosts.
   * Optionally, Ansible Vault can be used to create encrypted files to hold sensitive parameters, such as passwords.
* **One or more Ansible hosts** - An Ansible host is any virtual machine (VM) that your Ansible control node is configured to automate.
   * For Linux, Ansible control node’s SSH public key that is added to the authorized keys of a system user is required. The user can be either root or a regular user with sudo privileges.
   * For Windows, Ansible hosts that are configured with WinRM need to be operative.

A Virtual Server Instance (VSI) is selected here for ease of deployment and external connectivity. However, if a VM is preferred, then a number of these tasks are still applicable.
{: note}

You can connect to the automation server that was ordered in the previous step from your laptop on the public IP address. Next, you must follow these tasks:

1. [Update the OS packages](#veeam-cr-sag-ascfg-os).
2. [Change the DNS](#veeam-cr-sag-ascfg-dns).
3. [Configure the Network Time Protocol (NTP)](#veeam-cr-sag-ascfg-ntp).
4. [Create two user accounts](#veeam-cr-sag-ascfg-user), one for you to use, and another called _ansible_ that can be used by Ansible.
5. [Create an SSH key pair on the VSI for the _ansible_ user account](#veeam-cr-sag-ascfg-sakey) to connect to Ansible Linux hosts.
6. [Create an SSH key pair on your laptop](#veeam-cr-sag-ascfg-userkey), and copy your public key to the Ansible server so that you can access the server without passwords.
7. [Harden the SSH](#veeam-cr-sag-ascfg-ssh).
8. [Install Ansible](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-ansible).

## Updating OS packages
{: #veeam-cr-sag-ascfg-os}

The `apt update` command downloads package information from all configured sources. The system knows which packages are available for upgrade, and where to retrieve that software. The `apt upgrade` command uses this information and upgrades all installed packages to their most recent versions.

1. From your laptop, connect to the automation server by using the IP address and the root credentials from the {{site.data.keyword.cloud}} console `ssh root@<public_ip_address>`
2. At the command line, use command `apt update && apt upgrade -y` to update and upgrade the OS packages.

## Changing DNS
{: #veeam-cr-sag-ascfg-dns}

After provisioning, the VSI is configured to use the {{site.data.keyword.cloud_notm}} DNS resolvers: `10.0.80.11 and 10.0.80.12`, and not your {{site.data.keyword.vcf-auto}} instance - Active Directory™ DNS (AD/DNS) servers. You can change this configuration by using the following commands, and changing `<addns_1>` and `<addns_2>` to the IP addresses of your AD/DNS servers. Replace `<root_domain>` with your {{site.data.keyword.vcf-auto-short}} instance domain. For example, `test.ibmloud.local`

```text
sudo sed -i 's/10.0.80.11/<addns_1>/g' /etc/netplan/50-cloud-init.yaml
sudo sed -i 's/10.0.80.12/<addns_2>/g' /etc/netplan/50-cloud-init.yaml
sudo sed -i 's/search: \[\]/search: \[<root_domain>\]/g' /etc/netplan/50-cloud-init.yaml
sudo netplan apply
```
{: codeblock}

Use the following commands for verification.

```text
systemd-resolve --status | grep 'DNS Servers' -A2
resolvectl status
```
{: codeblock}

## Configuring NTP
{: #veeam-cr-sag-ascfg-ntp}

The following commands install NTP, configure `servertime.service.softlayer.com` as the NTP time source, remove the `ubuntu.pool.ntp.org` servers, and then restart the NTP service.

```text
apt install ntp -y
sudo sed -i 's/pool 0.ubuntu.pool.ntp.org iburst/#pool 0.ubuntu.pool.ntp.org iburst/g' /etc/ntp.conf
sudo sed -i 's/pool 1.ubuntu.pool.ntp.org iburst/#pool 1.ubuntu.pool.ntp.org iburst/g' /etc/ntp.conf
sudo sed -i 's/pool 2.ubuntu.pool.ntp.org iburst/#pool 2.ubuntu.pool.ntp.org iburst/g' /etc/ntp.conf
sudo sed -i 's/pool 3.ubuntu.pool.ntp.org iburst/#pool 3.ubuntu.pool.ntp.org iburst/g' /etc/ntp.conf
sudo sed -i 's/pool ntp.ubuntu.com/#pool ntp.ubuntu.com/g' /etc/ntp.conf
sudo sed -i '/^# Specify one or more NTP servers./a # IBM Cloud NTP\nserver servertime.service.softlayer.com prefer iburst' /etc/ntp.conf
sudo service ntp restart
```
{: codeblock}

The command `ntpq -p` is used to verify NTP. The line `remote is 10.0.77.54` is shown in the output, which is the IP address of `servertime.service.softlayer.com`

## Creating the users
{: #veeam-cr-sag-ascfg-user}

Two users are created on the server. The first user is an account that you can use to connect to the server, as in a subsequent step SSH as root is removed. The second user is an account that is used by Ansible.

1. Using the IP address and the root credentials of the {{site.data.keyword.cloud_notm}} console, from your laptop, connect to the Linux server `ssh root@<public_ip_address>`
2. At the command line, enter the following commands and supply a password when prompted.

```text
adduser <your_username>
usermod -aG sudo <your_username>
adduser ansible
usermod -aG sudo ansible
```
{: codeblock}

## Creating the key pair for the Ansible user
{: #veeam-cr-sag-ascfg-sakey}

1. At the command line, switch to the ansible user with `su - ansible`.
2. To create a key pair, enter `ssh-keygen -b 4096`, and follow the prompts. A passphrase complicates the use of the SSH key in automation.

## Creating the key pair for your user
{: #veeam-cr-sag-ascfg-userkey}

Suppose that you are using a Mac or Linux laptop to create an SSH key pair and create or update an SSH config file.

1. Log out of the SSH session of the automation server.
2. If you do not have a key pair on your laptop, create one with the command `ssh-keygen -b 4096`. A passphrase is recommended here.
3. Transfer the public key to the automation server: `ssh-copy-id <your_username@<bastion_host_public_ip_address>`.
4. Create or update your local user SSH config file by using a text editor, for example `vi ~/.ssh/config`. The `<short_name>` is the name that you want to use at the SSH command, such as `ssh <short_name>`.

```text
Host *
    Port 22
    StrictHostKeyChecking no
    UserKnownHostsFile /dev/null
    ServerAliveInterval 60
    ServerAliveCountMax 30

Host <short_name>
    HostName <automation_server_public_ip_address>
    User <your_user_name>
    IdentityFile <private_key_e.g._~/.ssh/key01>
```
{: codeblock}

Save the file by pressing `Esc` and `wq`. Then, you can access the automation server by using the command `ssh <short_name>`.

## Hardening SSH
{: #veeam-cr-sag-ascfg-ssh}

1. Connect to the automation server: `ssh <short_name>`. This time SSH uses the config file, your username, the IP address, and the private key to connect to the automation server.
2. At the prompt, enter your passphrase if you used one.
3. Use the following command to disable password authentication: `sudo sed -i 's/PasswordAuthentication yes/PasswordAuthentication no/g' /etc/ssh/sshd_config`.
4. Use the following command to disable root login: `sudo sed -i 's/#PermitRootLogin prohibit-password/PermitRootLogin no/g' /etc/ssh/sshd_config`.
5. Restart SSH with command `sudo systemctl restart ssh`.

## Related links
{: #veeam-cr-sag-ascfg-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
