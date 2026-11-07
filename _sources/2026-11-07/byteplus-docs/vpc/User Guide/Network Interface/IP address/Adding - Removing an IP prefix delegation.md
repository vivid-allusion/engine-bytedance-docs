---
title: "Adding/Removing an IP prefix delegation"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Adding_or_removing_an_IP_prefix_delegation"
---

To simplify multi\-IP allocation and improve expansion efficiency, you can configure IP prefix delegation for the network interface to reserve a dedicated subnet in advance for that interface.

## Add IP prefix delegation

### Action notes

* After a network interface is configured with an IP prefix delegation, other network interfaces cannot allocate IP addresses within that prefix; only this network interface can.

* IPv4 prefixes only support /28, and IPv6 prefixes only support /80.

* Each IP prefix occupies one IP address quota of the network interface, so the number of IP prefix delegations that can be added to a network interface is limited by its remaining available IP address count.

* The CIDR block and its IP addresses must not have been assigned to the network interface before configuring IP prefix delegation.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top navigation bar, select the project and region.

4. Click  **··· \> Add IP prefix** to the right of the target network interface.

5. Configure relevant parameters based on the table below.

   |Parameters |Notes |Sample value |
   |---|---|---|
   |IPv4 prefix delegation |Configure IPv4 prefix delegation for the network interface to reserve one or more dedicated IPv4 CIDR blocks for it in advance.<br><br><br>* Do not assign: Do not assign an IPv4 CIDR block to this network interface.<br><br>* Auto assign: After selecting the number of assignments, the system will automatically allocate the corresponding number of available /28 IPv4 CIDR blocks from the subnet to which the network interface belongs.<br><br>* Manual assign: Manually assign one or more available /28 IPv4 CIDR blocks from the subnet to which the network interface belongs as needed. |Custom\-assign, 192.168.1.0/28 |
   |IPv6 prefix delegation |Configure IPv6 prefix delegation for the network interface to reserve one or more dedicated IPv6 CIDR blocks for it in advance.<br><br><br>* Do not assign: Do not assign an IPv6 CIDR block to this network interface.<br><br>* Auto assign: After selecting the number of assignments, the system will automatically allocate the corresponding number of available /80 IPv6 CIDR blocks from the subnet to which the network interface belongs.<br><br>* Manual assign: Manually assign one or more available /80 IPv6 CIDR blocks from the subnet to which the network interface belongs as needed. |Auto\-assign |

6. Click **Add** to complete the action.

## Delete IP prefix delegation

If the network interface has already been assigned IP addresses within an IP prefix, after that prefix is released, it cannot be re\-added.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top navigation bar, select the project and region.

4. Click the name of target Network Interface.

5. On the **Manage IP Addresses** tab, click **Release** to the right of the target IP prefix.

6. Click **Release** to complete the action.
