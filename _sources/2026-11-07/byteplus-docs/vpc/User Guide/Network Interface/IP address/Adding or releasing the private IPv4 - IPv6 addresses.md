---
title: "Adding or releasing the private IPv4/IPv6 addresses"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address"
---

## Add secondary private IP address

### Action description

* An unmounted secondary network interface can be custom\-assigned up to 9 Secondary Private IPv4 addresses and 10 private IPv6 addresses.

* For the primary network interface or a secondary network interface attached to an ECS instance:

   * The maximum number of secondary private IPv4 addresses that can be assigned is equal to the per\-network interface private IP quota of the ECS [Instance Type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types) minus one (reserved for the primary private IP).

   * The maximum number of private IPv6 addresses that can be assigned is equal to the per\-network interface private IP quota of the ECS [Instance Type](https://docs.byteplus.com/en/docs/ecs/Introduction-to-instance-types).

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top navigation bar, select the project and region.

4. Click  **··· \> Manage IP Addresses** on the right side of the target Network Interface.

5. Click **Add Secondary Private IP**.

6. Configure relevant parameters based on the table below.

   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Secondary Private IPv4 Address |Additionally, assigning secondary private IPv4 addresses to a secondary network interface also supports both Auto\-assign and Custom\-assign.<br><br><br>* Auto\-assign: The system automatically assigns an available IPv4 address from the subnet to which the network interface belongs.<br><br>* Custom\-assign: Manually assign an available IPv4 address from the subnet to which the network interface belongs. |Custom\-assign, 192.XX.XX.5 |
   |Private IPv6 Address |When the subnet to which a network interface belongs supports IPv6 CIDR blocks, you can assign secondary private IPv6 addresses to a secondary network interface.<br><br><br>* Auto\-assign: The system automatically assigns an available IPv6 address from the subnet to which the network interface belongs.<br><br>* Custom\-assign: Manually assign an available IPv6 address from the subnet to which the network interface belongs. |Auto\-assign |

6. Click **Add** to complete the action.

### What to do next

* After adding a private IPv4 address to the network interface, the Elastic Compute Service image cannot recognize this IPv4 address. You must also log in to the cloud server to [configure the secondary private IPv4 address](https://docs.byteplus.com/en/docs/ecs/Configuring-secondary-private-IPv4-addresses-for-ECS-instances) for it to take effect.

* After adding a private IPv6 address to the network interface, some Elastic Compute Service images cannot recognize this IPv6 address. You should refer to [ECS configure private IPv6 address](https://docs.byteplus.com/en/docs/ecs/Configuring-private-IPv6-addresses-for-ECS-instances) to confirm whether configuration is required. Only after configuration, the IPv6 address takes effect.

## Release secondary private IP address

Before releasing a secondary private IP address, please thoroughly evaluate the potential impact on services and proceed with extreme caution. The primary private IPv4 address cannot be released.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top navigation bar, select the project and region.

4. Click  **··· \> Manage IP Addresses** on the right side of the target Network Interface.

5. Click **Release** on the right side of the target secondary private IP address.

6. Click **Release** to complete the action.

## Related documents

* [AssignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/AssignPrivateIpAddresses)

* [UnassignPrivateIpAddresses](https://docs.byteplus.com/en/docs/vpc/UnassignPrivateIpAddresses)

* [AssignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/AssignIpv6Addresses)

* [UnassignIpv6Addresses](https://docs.byteplus.com/en/docs/vpc/UnassignIpv6Addresses)
