---

copyright:

  years:  2022, 2024

lastupdated: "2024-06-05"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Provisioning the jump server
{: #veeam-cr-sag-jmp}

The jump server is a small Microsoft® Windows® Virtual Server Instance (VSI) deployed in the {{site.data.keyword.cloud}} account where the {{site.data.keyword.vcf-auto}} instance with the Veeam® service is located. The VSI is connected to both the {{site.data.keyword.cloud_notm}} private and public networks. The public network interface is protected by a security group that restricts Remote Desktop Protocol (RDP) access to a known remote IP address.

The jump server is used to provide graphical access to the Veeam Backup and replication server, vCenter appliance, and NSX-T Manager. In this step, the following tasks are included:

1. [Order a security group](#veeam-cr-sag-jmp-sg) to protect the jump server.
2. [Order a public VSI](#veeam-cr-sag-jmp-order) running Microsoft Windows for the jump server.

## Prerequisites
{: #veeam-cr-sag-jmp-prereq}

* The {{site.data.keyword.cloud_notm}} CLI is installed and the required {{site.data.keyword.cloud_notm}} account is targeted.
* Configuration is done through a laptop that has internet connectivity.
* The user has the required privileges in the {{site.data.keyword.cloud_notm}} account to order the required components.

## Ordering a security group
{: #veeam-cr-sag-jmp-sg}

This task uses the {{site.data.keyword.cloud_notm}} CLI to order a security group and configures inbound and outbound rules.

* The `<jmp_security_group_name>` is the required name for the security group, such as `sgjump`.
* The `sgid` captures the security group ID for use in subsequent commands.
* The `myip` captures the external IP address of your laptop.
* The inbound rule allows TCP port `3389` to ingress from a known internet IP address.
* The outbound rule allows any protocol to egress to any IP address.
* When the jump server VSI is ordered, it is ordered attached to the security group.

```text
export sgname=<jmp_security_group_name>
ibmcloud sl securitygroup create --name $sgname --description "Allow RDP from known external IP address" 
export sgid=$(ibmcloud sl securitygroup list --output json | jq -r '.[] | select (.name==env.sgn) | .id')
export myip=$(curl -s ifconfig.me)
ibmcloud sl securitygroup rule-add $sgid --remote-ip $myip --direction ingress --port-max 3389 --port-min 3389 --protocol tcp
ibmcloud sl securitygroup rule-add $sgid --remote-ip 0.0.0.0/0 --direction egress
ibmcloud sl securitygroup rule-list $sgid
```
{: codeblock}

## Ordering a public VSI
{: #veeam-cr-sag-jmp-order}

The jump server host is a small Microsoft Windows 2019 public VSI:

* The `ibmcloud sl vlan list` and `ibmcloud sl subnet list` need to be run first so that the IDs of the public and private VLANs and the primary subnets are captured for use in the ordering process.
* The `<js_hostname>` is the required hostname for the jump server, such as `winjs01`.
* The `<root_domain>` the required domain name, such as the matching root-domain name of your {{site.data.keyword.vcf-auto-short}} instance.
* The Linux® server is ordered with 2 vCPU and 4 GB RAM.
* The `<dc_code>` is the code for the data center in which the VSI is provisioned into, such as DAL10.
* The `<public_vlan_number>` and `<private_vlan_number>` are the VLAN numbers of the required public and private VLANs previously captured.
* The `--os WIN_LATEST_64` switch currently installs Windows 2019.
* The `--disk 100 --san` switches orders a 100 GB SAN disk.
* The `--network 1000` orders a 1 Gb NIC for public and private networks.
* The `--public-security-group $sgid` switch connects the VSI to the security group previously ordered and the ID captured in the variable `$sgid`.

```text
export hostname=<js_hostname>
export domain=<root_domain>
export vcpu=2
export mem=4096
export dc=<dc_code>
export pubvlan=<public_vlan_number>
export privlanid=<private_vlan_number>
export privlanid=$(ibmcloud sl vlan list --number $privlan --output json | jq --raw-output '.[] | .id')
export pubvlanid=$(ibmcloud sl vlan list --number $pubvlan --output json | jq --raw-output '.[] | .id')
ibmcloud sl vs create --hostname $hostname --domain $domain --cpu $vcpu --memory $mem --datacenter $dc --os WIN_LATEST_64 --disk 100 --san --network 1000 --vlan-public $pubvlanid --vlan-private $privlanid --public-security-group $sgid
```
{: codeblock}

## Related links
{: #veeam-cr-sag-jmp-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-overview)

