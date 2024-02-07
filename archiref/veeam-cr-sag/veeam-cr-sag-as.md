---

copyright:

  years:  2022, 2024

lastupdated: "2024-01-26"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Provisioning the automation server
{: #veeam-cr-sag-as}

The automation server is a small Linux® Virtual Server Instance (VSI) deployed in the {{site.data.keyword.cloud}} account where the VMware vCenter Server® instance with the Veeam® service is located. The VSI is connected to both the {{site.data.keyword.cloud_notm}} private and public networks. The public network interface is protected by a security group that restricts SSH access to a known remote IP address. This server can be removed after the builds or kept for ongoing use cases.

The automation server can be a virtual machine (VM) hosted on the vCenter Server instance. However, external connectivity requires extra configuration that is not discussed here.
{: note}

The automation server is used to host Ansible®. Ansible is used to automate many of the manual steps to configure the Linux hardened repository server after they are provisioned for applications, such as the Veeam backup server. In this step, the following tasks are included:

1. [Order a security group](#veeam-cr-sag-as-sg) to protect the automation server.
2. [Order a public VSI](#veeam-cr-sag-as-order) running Ubuntu for the automation server.

## Assumptions
{: #veeam-cr-sag-as-assumptions}

* The VSI is an Ubuntu VSI.
* The {{site.data.keyword.cloud_notm}} CLI is installed and the required {{site.data.keyword.cloud_notm}} account is targeted.
* Configuration is done through a laptop that has internet connectivity.
* The user has the required privileges in the {{site.data.keyword.cloud_notm}} account to order the required components.

## Ordering a security group
{: #veeam-cr-sag-as-sg}

The {{site.data.keyword.cloud_notm}} CLI is used to order a security group and configure inbound and outbound rules.

* The `<as_security_group_name>` is the required name for the security group, such as `sgauto`.
* The `sgid` captures the security group ID for use in subsequent commands.
* The `myip` captures the external IP address of your laptop.
* The inbound rule allows TCP port `22` to ingress from a known internet IP address.
* The outbound rule allows any protocol to egress to any IP address.
* When the jump server VSI is ordered, it is ordered attached to the security group.

```text
export sgname=<as_security_group_name>
ibmcloud sl securitygroup create --name $sgname --description "Allow SSH from known external IP address" 
export sgid=$(ibmcloud sl securitygroup list --output json | jq -r '.[] | select (.name==env.sgn) | .id')
export myip=$(curl -s ifconfig.me)
ibmcloud sl securitygroup rule-add $sgid --remote-ip $myip --direction ingress --port-max 22 --port-min 22 --protocol tcp
ibmcloud sl securitygroup rule-add $sgid --remote-ip 0.0.0.0/0 --direction egress
ibmcloud sl securitygroup rule-list $sgid
```
{: codeblock}

## Ordering a public VSI
{: #veeam-cr-sag-as-order}

The {{site.data.keyword.cloud_notm}} CLI is used to order an Ubuntu public VSI.

* The `ibmcloud sl vlan list` and `ibmcloud sl subnet list` need to be run first so that the IDs of the public and private VLANs and the primary subnets that are captured for use in the ordering process.
* The `<as_hostname>` is the required hostname for the automation server, such as `lnxas01`.
* The `<root_domain>` is the required domain name, such as the matching root-domain name of your vCenter Server instance.
* The Linux server is ordered with 2 vCPU and 4 GB RAM.
* The `<dc_code>` is the code for the data center in which the VSI is provisioned into, such as DAL10.
* The `<public_vlan_number>` and `<private_vlan_number>` are the VLAN numbers of the required public and private VLANs previously captured.
* The `--os UBUNTU_LATEST_64` switch currently installs Ubuntu 20.04 LTS.
* The `--disk 100 --san` switches orders a 100 GB SAN disk.
* The `--network 1000` orders a 1 Gb NIC for public and private networks.
* The `--public-security-group $sgid` switch connects the VSI to the security group previously ordered and the ID captured in the variable `$sgid`.

```text
export hostname=<hostname> 
export domain=<root_domain>
export vcpu=2
export mem=4096
export dc=<dc_code>
export pubvlan=<public_vlan_number>
export privlanid=<private_vlan_number>
export privlanid=$(ibmcloud sl vlan list --number $privlan --output json | jq --raw-output '.[] | .id')
export pubvlanid=$(ibmcloud sl vlan list --number $pubvlan --output json | jq --raw-output '.[] | .id')
ibmcloud sl vs create --hostname $hostname --domain $domain --cpu $vcpu --memory $mem --datacenter $dc --os UBUNTU_LATEST_64 --disk 100 --san --network 1000 --vlan-public $pubvlanid --vlan-private $privlanid --public-security-group $sgid
```
{: codeblock}

## Related links
{: #veeam-cr-sag-as-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)
