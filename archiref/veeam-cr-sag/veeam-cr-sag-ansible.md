---

copyright:

  years:  2023, 2024

lastupdated: "2024-08-08"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Installing and configuring Ansible
{: #veeam-cr-sag-ansible}

The automation server is provisioned and the initial operating system configuration is completed in the previous step. In this step, the following tasks are implemented:

1. [Installing Ansible](#veeam-cr-sag-ansible-install).
2. [Adding Ansible collections](#veeam-cr-sag-ansible-collections).
3. [Creating an Ansible inventory file](#veeam-cr-sag-ansible-inv).
4. [Using Ansible vault to encrypt files](#veeam-cr-sag-ansible-vault).
5. [Testing connections](#veeam-cr-sag-ansible-test).

An optional step is included to [install the Ansible NSX-T collections](#veeam-cr-sag-ansible-nsxt). The optional step is needed only if Ansible® is used to create sandboxes.

## Installing Ansible
{: #veeam-cr-sag-ansible-install}

At a command line on the automation server, run the following commands.

```text
sudo apt update
sudo apt install ansible -y
sudo apt install python3-pip -y
ansible --version
```
{: codeblock}

These commands are used for the following items:

* Refresh the system’s package index.
* Install the Ansible® software.
* Install the pip package that is required for the use if WinRM with Ansible.
* Verify that Ansible is installed.

## Adding Ansible collections
{: #veeam-cr-sag-ansible-collections}

Ansible collections are extra modules. In this deployment, use the following commands to add the required collections:

```text
ansible-galaxy collection install ansible.posix
ansible-galaxy collection install community.general
ansible-galaxy collection install ansible.windows
ansible-galaxy collection install community.windows
ansible-galaxy collection install juniper.device
ansible-galaxy collection install junipernetworks.junos
```
{: codeblock}

The `juniper.device` and `junipernetworks.junos` collections are required only if you are building an isolated recovery environment.

## Creating an Ansible inventory file
{: #veeam-cr-sag-ansible-inv}

1. Create a directory structure for the Ansible files and create an initial inventory file to test Ansible connections to the Ansible hosts. Use the following commands, when connected as the ansible user:

   ```text
   sudo mkdir /swlib
   sudo mkdir /swlib/ansible
   ```
   {: codeblock}

2. Create an inventory file called `hosts` that has two groups: [LHBR] and [VBR], with the IP addresses or FQDN of the Linux® hardened repository and Veeam® backup server: 

   ```text
   touch /swlib/ansible/hosts
   vi /swlib/ansible/hosts
   ```
   {: codeblock}

### Examples
{: #veeam-cr-sag-ansible-inv-exmpls}

A `hosts` file for the immutable backup.

```text
[lhbr]
lhbr01.test.ibmcloud.local ansible_user=root

[vbr]
prodbackup ansible_host=10.38.207.157 ansible_user=sa-ansible ansible_connection=winrm ansible_winrm_server_cert_validation=ignore
```
{: codeblock}

A `hosts` file for the isolated recovery environment.

```text
[lhbr]
lhbr01.test.ibmcloud.local ansible_user=root

[vbr]
prodbackup ansible_host=10.38.207.157 ansible_user=sa-ansible ansible_connection=winrm ansible_winrm_server_cert_validation=ignore

[vsrx]
gateway01 ansible_host=10.5.37.138 ansible_user=sa-ansible
```
{: codeblock}

## Using Ansible vault to encrypt files
{: #veeam-cr-sag-ansible-vault}

Ansible vault allows the encryption of values and data structures to secure sensitive data that is necessary to successfully run Ansible plays, but are not publicly visible, like passwords or private keys. Ansible automatically decrypts vault-encrypted content at run time when the key is provided.

Vault is implemented with file-level granularity, which means the files are either entirely encrypted or unencrypted. It uses the AES256 algorithm to provide symmetric encryption that is keyed to a user-supplied password. The same password is used to encrypt and decrypt content. The `ansible-vault` command is used to initially encrypt files, and then is used to view, edit, or decrypt the data.

* Create an Ansible configuration file that details the location of the `hosts` file and vault password file.
* Create and encrypt a file, called `group_vars/vbr.yml`, that holds the password for the `sa-ansible` user to access the Veeam backup server. The reason that the password for the Veeam backup server is placed here is so that the `ansible vbr -m win_ping` commands works.
* Create and encrypt a file that is called `vault` that holds the passwords for the hardened backup repository and optionally the vSRX appliance.

The use of the `vault_pass` file is an optional task, which creates and protects a file that holds the password to the vault. If you choose not to do this task, then you need to enter your password at the prompt when you run Ansible commands.
{: note}

1. To allow us not to be prompted for the vault password, enter the following commands:

   ```text
   touch ~/.vault_pass
   vi ~/.vault_pass
   ```
   {: codeblock}

2. Enter the password that you want to use for the vault, and save the file.
3. Change the permissions so that only the ansible user can read or write `chmod 600 ~/.vault_pass`.
4. Create the Ansible configuration file:

   ```text
   cd /swlib/ansible
   touch ansible.cfg
   vi ansible.cfg
   ```
   {: codeblock}

5. Then, use the following text in the file:

   ```text
   [defaults]
   inventory = /swlib/ansible/hosts
   vault_password_file = ~/.vault_pass
   ```
   {: codeblock}

6. We need to place the Windows® server password in an encrypted file. Ansible automatically reads files that contain variables from directories, called group_vars and host_vars, and associate them with the groups and hosts by file name. The following command creates an encrypted file, called `vbr.yml`, that matches the vbr group [vbr] in the inventory file.

   ```text
   mkdir group_vars
   ansible-vault create group_vars/vbr.yml
   ```
   {: codeblock}

7. In the editor, enter the password:

   ```text
   ansible_password: <password>
   ```
   {: codeblock}

8. Exit by pressing `Esc` and `:wq`.
9. The following commands can be used to modify the file when needed:

   * `ansible-vault edit group_vars/vbr.yml` - The command edits the file.
   * `ansible-vault decrypt group_vars/vbr.yml` - The command decrypts the file so it can be viewed or changed by using another editor, for example, `nano`.
   * `ansible-vault encrypt group_vars/vbr.yml` - The command encrypts the file after it is viewed or changed.

10. The following command creates an encrypted file called `vault`: `ansible-vault create vault`.
11. In the editor, enter the following command, where `<lhbr_password>` and `<sa_ansible_password>` are the passwords that are defined in the planning stage.

    ```text
    vault_lhbr_password: <lhbr_password>
    vault_sa_ansible_password: <sa_ansible_password>
    ```
    {: codeblock}

12. Exit by pressing `Esc` and `:wq`.

## Testing connections
{: #veeam-cr-sag-ansible-test}

Use the following commands to test connections:

```text
ansible lhbr -m ping
ansible vbr -m win_ping
```
{: codeblock}

If successful, the output shows `SUCCESS` for each command.

## Installing the Ansible NSX-T collections
{: #veeam-cr-sag-ansible-nsxt}

This step is optional, and is required only if Ansible is used for configuring sandboxes.

1. Connect to the Ansible control node as the ansible user.
2. Install Python: `sudo pip3 install --upgrade pyvmomi pyvim requests`.
3. Run the following commands to complete the following tasks:
   * Create a folder for the download.
   * Clone the Git repo.
   * Build the Ansible collection.
   * Install the locally built collection.

   ```text
   cd /swlib
   mkdir downloads
   cd downloads
   git clone https://github.com/vmware/ansible-for-nsxt.git
   cd ansible-for-nsxt
   ansible-galaxy collection build
   ansible-galaxy collection install vmware-ansible_for_nsxt-1.0.0.tar.gz
   ```
   {: codeblock}

## Related links
{: #veeam-cr-sag-ansible-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
