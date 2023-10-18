---

copyright:

  years:  2022, 2023

lastupdated: "2023-09-11"

subcollection: vmwaresolutions


---

{{site.data.keyword.attribute-definition-list}}

# Provisioning the Linux hardened repository server
{: #veeam-cr-sag-lhbr}

The Linux® hardened repository server is an {{site.data.keyword.cloud}} bare metal server that is deployed in the {{site.data.keyword.cloud_notm}} account where the vCenter Server instance with the Veeam service is located. The bare metal server is connected to the {{site.data.keyword.cloud_notm}} private network only.

## Assumptions
{: #veeam-cr-sag-lhbr-assumptions}

* The {{site.data.keyword.cloud_notm}} CLI is installed and the required {{site.data.keyword.cloud_notm}} account is targeted.
* Configuration is done through a laptop that has internet connectivity.
* The user has the required privileges in the {{site.data.keyword.cloud_notm}} account to order the required components.

The specification for the {{site.data.keyword.cloud_notm}} bare metal server that is deployed in this solution architecture guide is described as follows. Other bare metal specifications options are also available. The size and number of servers depend on your requirements. For more information, see [Scale-out backup repository](/docs/vmwaresolutions?topic=vmwaresolutions-veeam-cr-sa-components#veeam-cr-sa-components-sobr).

* Dual Intel® Xeon® Gold 5120 (28 Cores, 2.20 GHz)
* 64 GB RAM
* {{site.data.keyword.redhat_full}} Enterprise Linux 8.x
* RAID disk controller
* 2 x 1 TB SATA in RAID 1 for OS
* 8 x 2 TB SATA in RAID 6 for the backup repository
* 10 Gbps redundant private network uplinks
* Redundant power supply

The Dual Intel Xeon Gold 5120 (28 Cores, 2.20 GHz) server has capacity for 12 drives. In the previous example, only 10 drives are used.
{: note}

### Example - Order the bare metal server by using {{site.data.keyword.cloud_notm}} CLI
{: ##veeam-cr-sag-lhbr-exmpl}

The following example uses the {{site.data.keyword.cloud_notm}} CLI to order the bare metal server. However, the following commands are used to capture the required inputs for the bare metal server order:

* `ibmcloud sl hardware create-options` - lists the available options.
* `ibmcloud sl order package-list` - lists the packages available. To find packages that support 12 drives, use `ibmcloud sl order package-list | grep "12 Drives"`. The `Key Name` for the required package is used in a subsequent command.
* `ibmcloud sl order category-list BARE_METAL_SERVER` - defines what is mandated to be ordered. The `Category Code` can be used in the subsequent commands.
* `ibmcloud sl order item-list <Key Name> --category <Category Code>` - lists the options available for each category. For the required bare metal specifications, the following `Key Name` was selected from the available options when the associated `Command` was run:

| Key Name | Description | Command |
|----------|-------------|---------|
| INTEL_INTEL_XEON_5120_2_20 | Dual Intel Xeon Gold 5120 (28 Cores, 2.20 GHz) | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category server` |
| OS_RHEL_8_X_64_BIT_PER_PROCESSOR_LICENSING | Red Hat Enterprise Linux 8.x (64-bit per-processor licensing) | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category os \| grep RHEL` |
| RAM_64_GB_DDR4_2133_ECC_NON_REG | 64 GB RAM | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category ram` |
| DISK_CONTROLLER_RAID | RAID | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category disk_controller` |
| HARD_DRIVE_1_00_TB_SATA_2 | 1.00 TB SATA | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category disk0` |
| HARD_DRIVE_2_00_TB_SATA_2 | 2.00 TB SATA | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category disk3` |
| BANDWIDTH_0_GB  | 0 GB Bandwidth Allotment | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category bandwidth` |
| 10_GBPS_REDUNDANT_PRIVATE_NETWORK_UPLINKS | 10 Gbps Redundant Private Network Uplinks | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category port_speed` |
| REBOOT_KVM_OVER_IP | Restart or KVM over IP | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category remote_management` |
| 1_IP_ADDRESS | 1 IP address | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category pri_ip_addresses` |
| REDUNDANT_POWER_SUPPLY | Redundant Power Supply | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category power_supply` |
| MONITORING_HOST_PING | Host Ping | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category monitoring` |
| NOTIFICATION_EMAIL_AND_TICKET | Email and Ticket| `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category notification` |
| AUTOMATED_NOTIFICATION | Automated notification | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES --category response` |
| UNLIMITED_SSL_VPN_USERS_1_PPTP_VPN_USER_PER_ACCOUNT | Unlimited SSL VPN Users | `ibmcloud sl order item-list 2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES` |
{: caption="Table 1. Bare metal options" caption-side="bottom"}

The order command requires the following additional information:

* `<lhbr_hostname>` - For example, `lhbr01`.
* `<root_domain>` - For example, `test.ibmcloud.local`.
* `<private_vlan_id>` - For example, `3127648`.

Then, the information is incorporated into the order command as shown in the following example:

`"hardware":[{"hostname":"lhbr01","domain":"test.ibmcloud.local","primaryBackendNetworkComponent": {"networkVlan": {"id": 3127648}}}]`

The order command also requires the definition of the disks and RAID for use in `storageGroups`. To get all the Raid Type options, use the following command:

`ibmcloud sl call-api SoftLayer_Configuration_Storage_Group_Array_Type getAllObjects`. A summary of the response of this command is shown in the following table:

| ID | Description |
|----|-------------|
| 1  | RAID 0 |
| 2  | RAID 1 |
| 3  | RAID 5 |
| 4  | RAID 6 |
| 5  | RAID 10 |
| 9  | JBOD |
| 10 | HOT_SPARE |
| 11 | GLOBAL_HOT_SPARE |
| 21 | Straight through connection to the onboard drive controller |
{: caption="Table 2. RAID IDs" caption-side="bottom"}

The specification requires two disks in RAID 1 (disks 0 and 1) and 8 x disks in RAID 6 (disks 2, 3, 4, 5, 6, 7, 8 and 9). The following command is used:

`"storageGroups":[{"arrayTypeId": 2,"arraySize": 1000,"hardDrives": [0,1],"partitionTemplateId": 1},{"arrayTypeId": 4,"arraySize": 12000,"hardDrives": [2,3,4,5,6,7,8,9]}]`

* The `arrayTypeId": 2,"arraySize": 1000` represents the total capacity of 2 x 1 TB drives in RAID 1 in GB.
* The `"arrayTypeId": 4,"arraySize": 12000` represents the total capacity of 8 x 2 TB drives in RAID 6 in GB.

Now, all the required information is in place for the sample order. To verify this example, use the following command:

```text
ibmcloud sl order place \
2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES \
DALLAS10 \
INTEL_INTEL_XEON_5120_2_20,\
OS_RHEL_8_X_64_BIT_PER_PROCESSOR_LICENSING,\
RAM_64_GB_DDR4_2133_ECC_NON_REG,\
DISK_CONTROLLER_RAID,\
HARD_DRIVE_1_00_TB_SATA_2,HARD_DRIVE_1_00_TB_SATA_2,\
HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,\
BANDWIDTH_0_GB,\
10_GBPS_REDUNDANT_PRIVATE_NETWORK_UPLINKS,\
REBOOT_KVM_OVER_IP,\
1_IP_ADDRESS,\
REDUNDANT_POWER_SUPPLY,\
MONITORING_HOST_PING,\
NOTIFICATION_EMAIL_AND_TICKET,\
AUTOMATED_NOTIFICATION,\
UNLIMITED_SSL_VPN_USERS_1_PPTP_VPN_USER_PER_ACCOUNT \
--complex-type SoftLayer_Container_Product_Order_Hardware_Server \
--extras '{"hardware":[{"hostname":"lhbr01","domain":"partner.ibmcloud.local","primaryBackendNetworkComponent": {"networkVlan": {"id": 3127648}}}],"storageGroups":[{"arrayTypeId": 2,"arraySize": 1000,"hardDrives": [0,1],"partitionTemplateId": 1},{"arrayTypeId": 4,"arraySize": 12000,"hardDrives": [2,3,4,5,6,7,8,9]}],"sshKeys": [{"sshKeyIds": [2097510]}]}' \
--billing monthly \
--verify
```
{: codeblock}

The following command is the example of a sample order:

```text
ibmcloud sl order place \
2U_DUAL_INTEL_XEON_PROCESSOR_SCALABLE_FAMILY_12_DRIVES \
DALLAS10 \
INTEL_INTEL_XEON_5120_2_20,\
OS_RHEL_8_X_64_BIT_PER_PROCESSOR_LICENSING,\
RAM_64_GB_DDR4_2133_ECC_NON_REG,\
DISK_CONTROLLER_RAID,\
HARD_DRIVE_1_00_TB_SATA_2,HARD_DRIVE_1_00_TB_SATA_2,\
HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,HARD_DRIVE_2_00_TB_SATA_2,\
BANDWIDTH_0_GB,\
10_GBPS_REDUNDANT_PRIVATE_NETWORK_UPLINKS,\
REBOOT_KVM_OVER_IP,\
1_IP_ADDRESS,\
REDUNDANT_POWER_SUPPLY,\
MONITORING_HOST_PING,\
NOTIFICATION_EMAIL_AND_TICKET,\
AUTOMATED_NOTIFICATION,\
UNLIMITED_SSL_VPN_USERS_1_PPTP_VPN_USER_PER_ACCOUNT \
--complex-type SoftLayer_Container_Product_Order_Hardware_Server \
--extras '{"hardware":[{"hostname":"lhbr01","domain":"partner.ibmcloud.local","primaryBackendNetworkComponent": {"networkVlan": {"id": 3127648}}}],"storageGroups":[{"arrayTypeId": 2,"arraySize": 1000,"hardDrives": [0,1],"partitionTemplateId": 1},{"arrayTypeId": 4,"arraySize": 12000,"hardDrives": [2,3,4,5,6,7,8,9]}],"sshKeys": [{"sshKeyIds": [2097510]}]}' \
--billing monthly \
```
{: codeblock}

The {{site.data.keyword.cloud_notm}} automation provisions the server, which takes approximately 4 hours. When provisioned, if you connect to the server and use the `df -Th` command, you get a response similar to the following output. The `/dev/sdb1` becomes the immutable repository when configured in a subsequent step.

```text
Filesystem     Type      Size  Used Avail Use% Mounted on
devtmpfs       devtmpfs   32G     0   32G   0% /dev
tmpfs          tmpfs      32G     0   32G   0% /dev/shm
tmpfs          tmpfs      32G   42M   32G   1% /run
tmpfs          tmpfs      32G     0   32G   0% /sys/fs/cgroup
/dev/sda3      xfs       929G  9.2G  920G   1% /
/dev/sda1      xfs      1006M  273M  734M  28% /boot
/dev/sdb1      xfs        11T   80G   11T   1% /disk1
tmpfs          tmpfs     6.3G     0  6.3G   0% /run/user/1001
```
{: codeblock}

For more information, see [Understanding and building an order by using the order CLI](https://sldn.softlayer.com/article/understanding-ordering/).

To add a DNS A and PTR record entries in the AD/DNS server for this bare metal server, connect to the AD/DNS server by using RDP and the DNS Manager.

## Related links
{: #veeam-cr-sag-lhbr-related}

* [Cyber recovery with Veeam architecture overview](/docs/vmwaresolutions/?topic=vmwaresolutions-veeam-cr-sa-overview)
