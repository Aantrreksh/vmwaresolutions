---

copyright:

  years: 2023

lastupdated: "2023-12-07"

keywords: direct attached storage, microsoft windows server, requirements for microsoft windows server based repositories, linux server, requirements for linux backup repositories, hardened repository

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Direct attached storage
{: #veeam_repo_dir_storage}

A backup repository is a storage location where Veeam® keeps backup files, VM copies, and metadata for replicated VMs. You can use direct attached storage to configure a backup repository.

You can add virtual and physical servers as backup repositories in Microsoft Windows® server, Linux® server, and hardened repository.

## Microsoft Windows Server
{: #veeam_repo_dir_storage_microsoft}

You can use a Microsoft Windows Server with local or directly attached storage as a backup repository. The storage can be a local disk, directly attached disk-based storage (such as a USB hard disk), or iSCSI SAN LUN in case the server is connected into the SAN fabric. To communicate with a Microsoft Windows-based repository, Veeam Backup and Replication uses two Data Movers that are responsible for data processing and transfer:
* Veeam data mover on a VMware backup proxy
* Veeam data mover on the Microsoft Windows repository

When any job addresses the backup repository, Veeam data mover on the VMware® backup proxy establishes a connection with it on the backup repository, enabling efficient data transfer over LAN or WAN. The Data Mover is installed automatically when you add a server to Veeam Backup and Replication as a managed server. 

### Requirements for Microsoft Windows Server-based repositories
{: #veeam_repo_dir_storage_microsoft_repo}

A machine performs the role of a repository must meet the following requirements:

* The role of the repository can be assigned to a Microsoft Windows machine (physical or virtual). The machine must meet the system requirements. For more information, see [System Requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#limitations-and-recommendations){: external}.
* You must add the machine to the Veeam Backup and Replication console as a managed server.
* If you want to use fast clone in the Microsoft Windows backup repository, the machine must also meet requirements that are listed in the fast clone section. For more information, see [Fast Clone](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage#veeam_repo_man_storage_fast).

## Linux server
{: #veeam_repo_dir_storage_linux}

You can add a Linux server with local, directly attached storage or mounted NFS as a backup repository. The storage can be a local disk, directly attached disk-based storage (such as a USB hard drive), NFS share, or iSCSI SAN LUN in case the server is connected into the SAN fabric. To communicate with a Linux-based repository, Veeam Backup and Replication uses two Veeam data movers that are responsible for data processing and transfer:
* Veeam data mover on the backup proxy
* Veeam data mover on the Linux backup repository

Veeam data mover establishes a connection with the source-side Data Mover on the backup proxy, enabling efficient data transfer over LAN or WAN.

### Requirements for Linux backup repositories
{: #veeam_repo_dir_storage_linux_repo}

A machine performing the role of a repository must meet the following requirements:

* The role of the repository can be assigned to a Linux machine (physical or virtual).The machine must meet the system requirements. For more information, see [System Requirements](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120){: external}.
* You must add the machine to the Veeam Backup and Replication console as a managed server.
* If [Veeam data mover](https://helpcenter.veeam.com/docs/backup/vsphere/veeam_transport_service.html?ver=120){: external} is non-persistent, Veeam Backup and Replication uses the SSH protocol to communicate with Linux backup repositories and requires the SCP utility in Linux repositories. Make sure that the SSH daemon is properly configured and SCP utility is available on the Linux host.
* If you want to use fast clone in the Linux backup repository, the machine must also meet requirements. For more information, see [Fast Clone](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage#veeam_repo_man_storage_fast). 

You can place both repositories (hardened and standard) on one Linux server only if you used single-use credentials when adding the host. Standard repository is a repository added with persistent credentials and disabled immutability. For more hardened repository limitations, see the [Requirements and Limitations](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_dir_storage#veeam_repo_dir_storage_hardened_req).

## Hardened repository
{: #veeam_repo_dir_storage_hardened}

To protect your backup files from loss as a result of malware activity or unplanned actions, you can add to your backup infrastructure a hardened repository based on a Linux server.

The hardened repository supports the following features:

* Immutability: When you add a hardened repository, you specify the time period while backup files must be immutable. During this period, backup files stored in this repository cannot be modified or deleted.
* Single-use credentials: Credentials that are used only once to deploy Veeam data mover, or transport service, while adding the Linux server to the backup infrastructure. These credentials are not stored in the backup infrastructure. Even if the Veeam Backup and Replication server is compromised, the attacker cannot get the credentials and connect to the hardened repository.

### Supported backups
{: #veeam_repo_dir_storage_hardened_sup}

In the hardened repository, you can store the following backups created with backup and backup copy jobs:
* Image-level virtual machine backups and backup copies (VMware, Hyper-V, Cloud Director, Nutanix AHV, RHV)
* Physical machine backups and backup copies (Microsoft Windows, Linux, MacOS, AIX, Solaris)
* Cloud machine backup copies (Microsoft Azure, AWS, Google Cloud Platform)
* NAS backups and backup copies
* Application-aware processing log backups and backup copies (Microsoft SQL transaction log files, Oracle archived log files, PostgreSQL WAL files)
* Enterprise application backups and backup copies (SAP HANA, Oracle RMAN, SAP on Oracle, Microsoft SQL Server).

Furthermore, backups created with VeeamZIP, Copy backup jobs, Move backup jobs, and Export backup jobs are supported.

## Requirements and limitations
{: #veeam_repo_dir_storage_hardened_req}

For the hardened repository, consider the following requirements and limitations.

### Linux server
{: #veeam_repo_dir_storage_hardened_lin}

The role of the hardened repository can be assigned to a Linux machine with local or remotely attached block storage. The machine must meet the [system requirements for backup repository servers](https://helpcenter.veeam.com/docs/backup/vsphere/system_requirements.html?ver=120#repo){: external}.

The Linux distribution must be 64-bit due to the [Veeam data mover requirements](https://helpcenter.veeam.com/docs/backup/vsphere/veeam_transport_service.html?ver=120#requirements-and-limitations-for-veeam-data-movers){: external}.

To reduce the attack surface, use a physical machine with local storage. For RAID configuration, the following recommendations apply:
* For the operating system: RAID 1 on SSDs with at least 100 GB disk space must be used.
* For backup data: RAID 6/60 with write-back cache must be used. At least one disk must be configured for the drive roaming.
* Internal disk cache must be disabled.
* RAID stripe size must be 128 or 256 KB.
* The Linux machine file system must support immutable files and extended attributes modified by the [chattr](https://man7.org/linux/man-pages/man1/chattr.1.html){: external} and [setxattr](https://man7.org/linux/man-pages/man2/setxattr.2.html){: external} commands. We recommend using XFS for performance and space efficiency reasons (block cloning support).
* You must add the Linux machine to the Veeam Backup and Replication console as a managed server. The hardened repository cannot be shared between different Veeam Backup and Replication servers.
* The Linux machine must have redundant network connection.

### Repository
{: #veeam_repo_dir_storage_hardened_repo}

*  To store backup files in a repository, use only a forward incremental backup method with enabled [active full backup](https://helpcenter.veeam.com/docs/backup/vsphere/active_full_backup.html?ver=120){: external} or [synthetic full backup](https://helpcenter.veeam.com/docs/backup/vsphere/synthetic_full_backup.html?ver=120){: external}. Once a backup file becomes immutable, it can be merged or deleted only when the immutability time period expires. For this reason, you cannot select a reverse or a forever forward incremental backup method.
*  For importing a backup, use VBK backup files. Metadata files of a backup chain (.VBM) cannot be immutable because they are updated on every job pass.
*  Hardened repositories do not support rotated drives.

### Immutability feature
{: #veeam_repo_dir_storage_hardened_fet}

*  To use the immutability feature for backup copy jobs, enable the GFS retention policy. 
*  Do not use the immutability feature for a [Nutanix Mine infrastructure](https://helpcenter.veeam.com/docs/nutanixmine/userguide/overview.html?ver=40){: external}. As Mine repositories contain thin-provisioned disks, might come across a case when Veeam Backup and Replication uses full storage capacity of a repository and cannot delete backup files from the file system.

## Preparing Ubuntu Linux Server as hardened repository
{: #veeam_repo_dir_storage_hardened_prep}

This section includes security considerations for installing and configuring the Linux server that will be used as a hardened repository. Recommendations are based on Security
Technical Implementation Guides (STIGs) created and maintained by the Defense Information Systems Agency (DISA) for Ubuntu 20.04 LTS. For more information, see [DISA STIGs Document Library](https://public.cyber.mil/stigs/downloads/){: external}.

### Installing Ubuntu Linux Server
{: #veeam_repo_dir_storage_hardened_instal}

To install Ubuntu 20.04 LTS, download the server install image from the [Ubuntu Releases page](https://releases.ubuntu.com/focal/){: external}. For more information about the installer and options of the installation wizard, see the [official Canonical ubuntu server guide](https://ubuntu.com/server/docs/installation){: external}.

During the installation process, consider the following Veeam recommendations:

<!-- The {: #step-1} tag and the ordered list that has only 1s are intentional. Do not delete. This coding is necessary for proper indentation when the procedure is translated. -->

1. Before you boot the installer, enable UEFI secure boot to prevent unsigned Linux kernel modules from being loaded. {: #step-1}
1. In the **GRUB** menu, select the **Boot and Install** with the HWE kernel option to support the latest hardware.
1. At the welcome screen of the installation wizard, select the language for the installer and the default language for the installed system. For troubleshooting purposes, it is recommended to select the English language.
1. At the **Installer** update available step of the installation wizard, select the **Continue without updating** option.
1. At the **Keyboard configuration** step of the installation wizard, set up the keyboard layout used in your backup infrastructure.
1. At the **Network connections** step of the installation wizard, do the following:
   * If you have several network interface cards, create a bond to provide the network failover in case of connection issues. For the bond mode, select one of the following options:
     * **balance-rr** (if you use EtherChannel without LCAP)
     * **802.3ad** (if you use EtherChannel with LCAP)
     * **active-backup** (for other configurations)
   * If you have only one network interface card and cannot create a bond, assign the static IP address to the network interface to reduce the risk of connection issues, for example, with the DHCP server.
1. At the **Configure proxy** step of the installation wizard, specify the proxy server if required.
1. At the **Configure Ubuntu archive mirror** step of the installation wizard, leave the default mirror address.
1. At the **Storage configuration** step of the installation wizard, follow recommendations from [CIS Benchmarks for Ubuntu Linux 20.04 LTS STIG](https://www.cisecurity.org/benchmark/ubuntu_linux){: external} for partitioning. After you add partitions for all disks, click **Continue** in the **Confirm destructive action** window to apply the changes. Note that all data on the disks will be deleted.
   To be compliant with [DISA STIG UBTU-20-010414](https://www.stigviewer.com/stig/canonical_ubuntu_20.04_lts/2022-12-06/finding/V-238335){: external}, you do not need to enable disk encryption for the operating system. To protect data in backups, use Veeam Backup and Replication built-in encryption instead.
   {: note}

1. At the **Profile setup** step of the installation wizard, specify a hostname and a user account that you will use to connect to the Linux server. Keep in mind that by default it will have `sudo` permissions. After you add a hardened repository to the backup infrastructure, you must remove this user account from the `sudo` group.
1. At the **SSH setup** step of the installation wizard, select the **Install OpenSSH server** check box. The OpenSSH server is required to be compliant with DISA STIG UBTU-20-010042 and for deployment and upgrade of the Veeam data mover.
1. At the **Featured server snaps** step of the installation wizard, do not install any additional packages. Click **Done** to start the installation process.
1. After the installation finishes, remove the installation media and reboot the system. 

### Post-installation
{: #veeam_repo_dir_storage_hardened_post}

For post-installation, consider the following Veeam recommendations:

1. Compliance with DISA STIG UBTU-20-010009

   To be compliant with [DISA STIG UBTU-20-010009](https://www.stigviewer.com/stig/canonical_ubuntu_20.04_lts/2022-12-06/finding/V-238204){: external}, set a password for GRUB. To configure the setting manually, do the following:

   1. Create a password using the grub-mkpasswd-pbkdf2 command:

   ```psh
   grub-mkpasswd-pbkdf2
   Enter password:
   Reenter password:
   PBKDF2 hash of your password is
   grub.pbkdf2.sha512.10000.C0F70D240A8BC5C1BC4E1303EC4F04095
   7C1AF1BB8E99EED573133D3A017BE9B2BB48E52577A141B3A695252
   7A9D1BEF13E2BB29978DA71F2D867EBB03545021.C4E81CAE7B464E
   78B15DF0A578B63BAB3A0CB180C311AFA5A85F6245800D11D40B37
   B817C3F30348EE603AF725B7E09B98A291114B0206D[…]
   ```
   {: pre}

   2. Add a user name and a password hash at the end of the /etc/grub.d/40_custom file:

   ```psh
   set superuser=root
   password_pbkdf2 root
   grub.pbkdf2.sha512.10000.C0F70D240A8BC5F[…]
   ```
   {: pre}

   3. To disable asking for credentials after rebooting the system and require them only when editing boot menu entries, open the /etc/grub.d/10_linux file and add the -- unrestricted parameter to the CLASS variable:

   ```psh
   CLASS="--class gnu-linux --class gnu --class os --unrestricted"
   ```
   {: pre}

   4. Update the GRUB configuration:

   ```psh
   sudo update-grub
   ```
   {: pre}

2. Limit outgoing HTTP traffic

   If you do not use the proxy server and the Linux server which has outgoing HTTP internet, this will limit outgoing HTTP traffic to the Ubuntu servers. You will have to use an internal Ubuntu mirror. To receive Linux security updates, you must have access to the Linux distribution security update servers.

3. User access

   For the separate directory that you created for the backup data, allow access only for the user account you created during the installation. Use the following command:

   1. To assign the directory's owner:

   ```psh
   chown -R owner:group <dir_path>
   ```
   {: pre}

   2. To allow access to the directory only for its owner and the root account:

   ```psh
   chmod 700 <dir_path>
   ```
   {: pre}

   3. To be compliant with DISA STIG UBTU-20-010012, you must have only two users:

      * The root account. Note that by default the root account has a blank password and cannot be used for connection.

      * The user account you created during the installation. This account will be used to connect to the Linux server and deploy required Veeam Backup and Replication components including persistent Veeam data mover, or transport service.

By default, the user account you created during the installation is the member of the sudo group and has enough privileges to deploy and install required Veeam Backup and Replication components. In that case, when you add a Linux server as a hardened repository to the backup infrastructure and specify single-use credentials, you do not need to enter the password for the root account. 

After the repository is added, you must remove the user account from the sudo group to make it a non-root account. To do this, perform the following steps:

1. Allow the user account to reboot and shutdown the operating system:
   ```psh
   sudo bash -c "echo 'user1 ALL = (root) NOEXEC: /usr/sbin/reboot' >>
   /etc/sudoers"
   sudo bash -c "echo 'user1 ALL = (root) NOEXEC: /usr/sbin/shutdown
   ```
   {: pre}

2. Remove the user account from the sudo group:
   ```psh
   sudo deluser user1 sudo
   ```
   {: pre}

The next time you log in with this user account, it will lose sudo permissions. if you need to execute commands as a privileged user, you must boot the operating system into the single user mode.
{: note}

## Adding hardened repository
{: #veeam_repo_dir_storage_hardened_add}

To launch the **New Backup Repository wizard**, complete the following steps:

<!-- The {: #step-2} tag and the ordered list that has only 2s are intentional. Do not delete. This coding is necessary for proper indentation when the procedure is translated. -->

2. Open the **Backup infrastructure view**. In the inventory pane, right-click the **Backup repositories** node and select **Add backup repository**. Alternatively, you can click **Add repository** on the ribbon. {: #step-2}
2. In the **Add backup repository** window, select **Direct attached storage > Linux (Hardened Repository)**.
2. At the **Name** step of the wizard, specify a name and description for the repository. The default description contains information about the user who added the repository, date and time when the repository was added.
2. From the repository server list, select a Linux server that you want to use as a hardened repository. Click **Populate** to see a list of disks connected to the server, their capacity and free space. The repository server list contains only those servers that are added to the backup infrastructure. If the server is not added to the backup infrastructure yet, click **Add New** on the right and follow the wizard:

   2. At the **Name** step of the wizard, specify a full DNS name or IP address and description of the Linux server. The default description contains information about the user who added the server, date and time when the server was added.
   2. At the **SSH Connection** step of the wizard, specify single-use credentials to connect to the Linux server and deploy Veeam data mover. The user account you specified must be a non-root account. Also, it must have the home directory created on the Linux server.

      Veeam Backup and Replication does not store these credentials in the configuration database.
      {: note}

2. The **Elevate account** privileges automatically check box is used by default. If you did not add the user account to the sudoers file, select the Use "su" if "sudo" fails check box and enter the password for the root account.If you want to change default SSH settings, click **Advanced**.

   If you added the user account to the sudoers file, you do not need to select the Use "su" if "sudo" fails check box and specify the root password. But after the server is added, you must remove the user account from the file.
   {: important}

2. At the **Review** step of the wizard, review what Veeam Backup and Replication components are already installed on the server and what components will be installed. Click **Apply** to add the Linux server to the backup infrastructure.
2. At the **Summary** step of the wizard, review details of the Linux server and click **Finish** to exit the wizard.
2. At the **Repository** step of the wizard, specify path and repository settings:

   2. In the **Location** section, specify a path to the directory that you created to store immutable backups when preparing Linux server. Click **Populate** to check capacity and available free space in the selected location.
   2. Select the **Use fast cloning** on XFS volumes check box to enable copy-on-write functionality. For more information, see the [Fast Clone](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_man_storage#veeam_repo_man_storage_fast).
   2. Specify the immutability period.
   2. Specify load control settings to limit the number of concurrent tasks and prevent possible timeouts of storage I/O operations.
   2. If you want to configure additional settings for the repository, click **Advanced**.

2. At the **Mount server** step of the wizard, specify settings for the mount server that you plan to use for file-level and application items restore.
2. At the **Review** step of the wizard, review the hardened repository settings and list of components that will be installed.
    * If the backup repository contains backups that were previously created with Veeam Backup and Replication, select the Search the repository for existing backups and import them automatically check box. Veeam Backup and Replication will scan the backup repository to detect existing backup files and display them in the Veeam Backup and Replication console under the Imported > Backups node.
    * If the backup repository contains guest file system index files that were previously created by Veeam Backup and Replication, select the **Import guest file system index** check box. Index files will be imported with backup files, and you will be able to search for guest OS files inside imported backups.
2. Click **Apply** and wait for Veeam Backup and Replication to install and configure all required components. At the **Summary** step of the wizard, review details of the added hardened repository and click Finish to exit the wizard.
2. To maximize the repository security and protect your data from different attacks, after the deployment of Veeam data mover, change file permissions for authentication certificates, so that only the user account you specified to connect to the Linux server and the root account can read the certificate files. Use the following commands:

   ```psh
   chown owner:group /opt/veeam/transport/certs
   chmod 700 /opt/veeam/transport/certs
   ```
   {: pre}

Both owner and group must be the user account that you specified to connect to the Linux server. You can also use `chmod 770` to add the same permissions to the group.
{: note}

The SSH connection is necessary only for the deployment and upgrade of Veeam data mover. For security purposes, after you add the hardened repository, disable SSH connection for the user account that you used to connect to the Linux server. If you can work with the server from the console, disable the SSH connection for the server itself.
{: important}

## Managing hardened repository
{: #veeam_repo_dir_storage_hardened_manage}

If you want to update hardened repository components or remove a hardened repository from the backup infrastructure, ensure that the SSH connection is enabled. Consider that
you also need to specify single-use credentials that you use to connect to the Linux server and deploy Veeam data mover.

## Migrating Linux Repository to hardened repository
{: #veeam_repo_dir_storage_hardened_migrating}

If you have a Linux server added to the backup infrastructure as a backup repository and want to use it as a hardened repository, perform the following steps:

1. On the Linux server, change permissions for the directory where backups are stored. Both owner and group must be the account with non-root permissions you use to connect to the Linux server.

   ```psh
   chown -R owner:group <dir_path>
   ```
   {: pre}

2. Go to the Veeam Backup and Replication console and perform the following steps:

   1. Open the **Backup infrastructure** view and select **Managed servers** in the navigation pane. Right-click the Linux server, select **Properties**, go to the SSH Connection step of the wizard, and specify the account with non-root permissions you use to connect to the Linux server. 
   
   These credentials must be single-use.
   {: note}

   2. Remove backup files stored on the Linux repository from the backup configuration. To do this, go to the **Backups > Disk node and select the backup file**. Hold `[Ctrl]` and right-click the file. Then click **Remove** from configuration.

   3. Add the same Linux server to the backup infrastructure as a hardened repository using the **New backup repository wizard**. At the **Review** step of the wizard, select the **Search the repository for existing backups** and import them automatically check box to detect existing backup files and display them in the Veeam Backup and Replication console under the **Imported >Backups node**. For more information, see [Adding Hardened Repository](https://helpcenter.veeam.com/docs/backup/vsphere/hardened_repository_add.html?ver=120){: external}.

   4. Go to the **Jobs node** and edit the job associated with the Linux repository. At the **Storage** step of the wizard, select the **hardened repository** from the **Backup repository list.**

   5. Click **Map** backup and specify imported backups from the previous step. Finish the wizard to apply changes.

   6. Open the **Backup infrastructure** view and remove the Linux backup repository from the backup infrastructure.

## Related links
{: #veeam_repo_dir_storage-links}

* [Network attached storage](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_net_storage)
* [Create backup repository](/docs/vmwaresolutions?topic=vmwaresolutions-veeam_repo_create)
