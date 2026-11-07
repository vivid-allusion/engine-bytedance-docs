---
title: "Creating a secondary network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-a-secondary-network-interface"
---

## Scenarios

Only the creation of secondary network interfaces (ENI) is supported. The primary network interface is created by default with the Elastic Compute Service (ECS) instance and cannot be created separately.

## Procedure

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click **Create ENI**.

5.  Configure relevant parameters based on the table below.

   |Parameter |Description |Sample value |
   |---|---|---|
   |Name |Enter the name of the secondary ENI. |eni\-01 |
   |VPC |Select the VPC where the secondary ENI resides. After selection, this ENI can only be associated with or bound to cloud resources such as security groups and ECS instances within the same VPC. |vpc\-01 |
   |Subnet |Select the subnet where the secondary ENI resides. Subnets assign private IPv4 addresses to secondary ENIs. Ensure sufficient available IPv4s exist in the subnet.​​ |subnet\-01 |
   |Primary private IPv4 address |Assigning secondary private IPv4 addresses to a secondary ENI also supports both Auto\-assign and Custom\-assign.<br><br><br>* Auto\-assign: The system automatically assigns an available IPv4 address from the selected subnet.<br><br>* Custom\-assign: Manually assign an available IPv4 address from the subnet to which the ENI belongs. |192.168.2.5 |
   |Secondary private IPv4 address |Configure secondary private IPv4 addresses for the ENI as needed, with support for assigning up to 9 addresses.<br><br><br>* Do Not Assign for Now: Temporarily skip assigning a Secondary Private IPv4 Address.<br><br>* Auto assign: Specify the number of secondary private IPv4 addresses to assign automatically. The system will allocate the corresponding number of unused IPv4 addresses from the selected subnet.<br><br>* Custom\-assign: Manually assign an available IPv4 address from the subnet to which the ENI belongs. |192.168.2.6 |
   |Private IPv6 address |If the subnet has IPv6 enabled, you can configure secondary private IPv6 addresses for the ENI as needed, with support for assigning up to 10 addresses.<br><br><br>* Do Not Assign for Now: Temporarily skip assigning a private IPv6 address.<br><br>* Auto\-assign: Specify the number of secondary private IPv6 addresses to assign automatically. The system will allocate the corresponding number of unused IPv6 addresses from the selected subnet.<br><br>* Custom\-assign: Manually assign an available IPv6 address from the subnet to which the ENI belongs.<br><br><br>> **tip**<br><br><br>> VPC's IPv6 is currently in the invite\-only Beta stage. If you need a trial, please contact your account manager.<br> |Not assigned |
   |Security group |Select the security group to associate with the secondary ENI. The interface will be protected by the rules of this security group. Each ENI can be associated with up to 5 security groups.<br><br>After creating the secondary network interface, if you need to modify its security group policy, see [Changing the network interface security group](https://docs.byteplus.com/en/docs/vpc/Updating-the-security-group-of-a-network-interface). |Default |
   |Project |Select the project to which the ENI belongs. For more information, see [Project management](https://docs.byteplus.com/en/docs/vpc/Managing-projects). |default |
   |Tag |Add one or more custom tags to the secondary ENI as needed. A tag consists of a key\-value pair and is used for categorizing and searching resources.<br><br>Click the add icon, then select or enter the tag key and tag value to add tags to the ENI. |* Tag key: eni\-key<br><br>* Tag value: eni\-v1 |
   |Established TCP connection timeout period |Configure the TCP connection idle timeout period. This specifies the maximum length of time a TCP connection can be retained without data transmission. When the timeout is reached, the connection is automatically disconnected and session resources are released.<br><br><br>* Value range: 30\-7200 seconds.<br><br>* Default: 910 seconds. |910 |
   |TCP wait and close timeout period |Configure TCP connection close timeout. This specifies the maximum length of time to wait for responses during the TCP four\-way handshake termination process. If the handshake is not completed before the timeout, the connection is forcibly disconnected and session resources are released.<br><br><br>* Value range: 3 to 15 seconds.<br><br>* Default: 3 seconds. |3 |
   |UDP flow timeout period |Configure UDP stream timeout. This specifies the maximum idle retention duration for a bidirectional UDP session with no round\-trip traffic. When the timeout is reached, the session is automatically deleted and resources are released.<br><br><br>* Value range: 10\-180 seconds.<br><br>* Default: 32 seconds. |32 |
   |IPv4 prefix delegation |Configure IPv4 prefix delegation for the ENI to reserve one or more dedicated IPv4 CIDR blocks for it in advance. For constraints and limits, see [IP prefix delegation configuration](https://docs.byteplus.com/en/docs/vpc/Adding_or_removing_an_IP_prefix_delegation).<br><br><br>* Do not assign: Do not assign an IPv4 CIDR block to this ENI.<br><br>* Auto assign: After selecting the number of assignments, the system will automatically allocate the corresponding number of available /28 IPv4 CIDR blocks from the subnet to which the ENI belongs.<br><br>* Manual assign: Manually assign one or more available /28 IPv4 CIDR blocks from the subnet to which the ENI belongs as needed. |Auto\-assign |
   |IPv6 prefix delegation |Configure IPv6 prefix delegation for the ENI to reserve one or more dedicated IPv6 CIDR blocks for it in advance. For constraints and limits, see [IP prefix delegation configuration](https://docs.byteplus.com/en/docs/vpc/Adding_or_removing_an_IP_prefix_delegation).<br><br><br>* Do not assign: Do not assign an IPv6 CIDR block to this ENI.<br><br>* Auto assign: After selecting the number of assignments, the system will automatically allocate the corresponding number of available /80 IPv6 CIDR blocks from the subnet to which the ENI belongs.<br><br>* Manual assign: Manually assign one or more available /80 IPv6 CIDR blocks from the subnet to which the ENI belongs as needed. |Auto\-assign |

6. Click **Create** to complete the operation.

### What to do next

After creating a secondary network interface, you need to [Attach it to an ECS instance](https://docs.byteplus.com/en/docs/vpc/Loading-or-unloading-a-secondary-network-interface#.5oyC6L296L6F5Yqp572R5Y2h) and see [Configuring a secondary network interface](https://docs.byteplus.com/en/docs/vpc/Configuring-a-network-interface-and-a-private-address) to determine whether further configuration is required. If so, the interface will only become functional after you complete the configuration.

## Related documents

[CreateNetworkInterface](https://docs.byteplus.com/en/docs/vpc/CreateNetworkInterface)
