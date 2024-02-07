---

copyright:

  years:  2022, 2024

lastupdated: "2024-01-26"

subcollection: vmwaresolutions

---

{{site.data.keyword.attribute-definition-list}}

# Overview
{: #veeam-cr-sag-overview}

The solution guide describes the tasks to create the two cyber-recovery solution architectures, Immutable backup and Isolated recovery environment. It also discusses the use cases for the creation of backups and then making this backup available to cyberadmins.

The solution guide uses:

* {{site.data.keyword.cloud}} CLI commands to deploy the infrastructure.
* Ansible® for operating system configuration.
* PowerShell for the automation of Veeam®.

For a detailed understanding of the two solution architectures, see [Overview of cyber recovery with Veeam architecture](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview).

## Cyber-recovery immutable backup
{: #veeam-cr-sag-overview-ib}

### Assumptions
{: #veeam-cr-sag-overview-immutbckup-assumptions}

* The VMware vCenter Server® instance is already deployed and consists of three hosts in a consolidated cluster that runs VMware NSX-T™ and uses NFS data stores. Your vCenter Server instance might be different, and the step-by-step instructions can accommodate different instances.
* The Veeam service is already deployed and uses the bare metal option. However, the VSI instance is similar from a network perspective with two IP addresses; one on the primary subnet and one on the instance management subnet. The virtual machine (VM) option has a single IP address only on the instance management subnet.

### High-level steps
{: #veeam-cr-sag-overview-immutbckup-highlvlsteps}

* The [Planning the deployment](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-planning) step captures and defines the information that is needed for the subsequent steps.
* [Provisioning the jump server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-jmp) and [Configuring the jump server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-jmpcfg) steps describe the tasks for the jump server. The jump server is a virtual server instance that runs Microsoft® Windows® and has public and private network interfaces. The public network interface is attached to a security group that restricts inbound traffic to MS RDP, TCP 3389, from a known IP address. The jump server provides access to UI consoles, such as vCenter and Veeam console. If you already have remote access to your vCenter Server instance, then you can skip this step.
* [Provisioning the automation server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-as) and [Configuring the automation server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-ascfg) steps define the tasks for an automation server. The automation server is a virtual server instance that runs Ubuntu Linux® and has public and private network interfaces. The public network interface is attached to a security group that restricts inbound traffic to SSH, TCP 22, from a known IP address.
* [Provisioning the Linux hardened repository server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lhbr) step describes the provisioning of the Veeam Linux hardened repository server. The Veeam Linux hardened repository server is an {{site.data.keyword.cloud}} bare metal server that runs Ubuntu Linux or {{site.data.keyword.redhat_full}} Enterprise Linux.
* [Configuring the Veeam backup server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-vbrcfg) step defines the configuration of the Veeam backup server so that it can be accessed by the automation server.
* [Installing and configuring Ansible](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-ansible) step describes the installation of Ansible on the automation server.
* [Configuring the OS of the Linux hardened repository server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lhbrcfg) step describes the Ansible playbook tasks that prepare the server for its role as a Veeam Linux hardened backup server.
* [Configuring the Linux hardened repository server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lhbrmng) step defines the Ansible playbook that adds the Linux hardened backup repository as a Veeam managed server into the Veeam backup infrastructure.
* [Securing the Linux hardened repository server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lhbrsecure) step describes the tasks to secure the Linux hardened repository server.

Optionally, you can use the following information:

* [Instant restore](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-instantrestore) topic describes a use case where a cyberadmin uses a PowerShell script that uses Veeam's ability to do an instant restore of a production VM from the cyberbackup.
* [Creating a Veeam Linux managed server](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-lnxmgdsvr) topic describes a use case where a cyberadmin uses the Veeam data integration API to access the cyberbackup.

## Cyber-recovery isolated recovery environment
{: #veeam-cr-sag-overview-ire}

### Assumptions
{: #veeam-cr-sag-overview-ire-assumptions}

* The vCenter Server instance is already deployed and consists of:
   * A three-host consolidated cluster that runs NSX-T and uses NFS data stores. Your vCenter Server instance might be different, and the step-by-step instructions can accommodate different instances.
   * A gateway cluster that hosts vSRX firewall appliances.
* The Veeam service is already deployed and uses the bare metal option. However, the VSI instance is similar from a network perspective with two IP addresses; one on the primary subnet and one on the instance management subnet. The VM option has a single IP address only on the instance management subnet.

### High-level steps
{: #veeam-cr-sag-overview-ire-highlvlsteps}

Use the same steps as described in [Cyber-recovery immutable backup high-level steps](#veeam-cr-sag-overview-immutbckup-highlvlsteps). In addition, review the following information:

* [Creating the airgap by using Juniper vSRX](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-vsrx) topic describes an approach to create the airgap.
* [Configuring the production environment](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sag-ireprod) topic describes the tasks on the production environment to enable cyber-recovery access.

## Related links
{: #veeam-cr-sag-overview-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
