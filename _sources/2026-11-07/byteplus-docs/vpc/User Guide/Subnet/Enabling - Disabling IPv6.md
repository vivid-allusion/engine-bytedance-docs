---
title: "Enabling/Disabling IPv6"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-subunet"
---

## Scenarios

For cloud resources (such as ECSs) to use an IPv6 address, the subnet they reside in must have IPv6 enabled before an IPv6 address can be assigned to them.

> **tip**

> VPC's IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.

## Enable IPv6

### Prerequisites

The VPC to which the subnet belongs has IPv6 enabled. If not enabled, please [Enable IPv6 for VPC](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-VPC).

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Subnet**.

3. In the top menu bar, select the target project and region.

4. Click **Enable IPv6** in the **IPv6 CIDR** column of the target subnet row.

5. Select the target IPv6 subnet from the dropdown. The subnet mask for the IPv6 network segment defaults to /64. You can customize the last 8 bits of the subnet's IPv6 network segment by entering a decimal number from 0 to 255, e.g., 2408:XXXX:0:a60 1::/64.

6. Click **Enable** to complete the action.

### What to do next

To allocate IPv6 addresses to Elastic Compute Service instances, see [Allocate IPv6 Address](https://docs.byteplus.com/en/docs/vpc/Adding-or-releasing-a-private-IP-address).

## Disable IPv6

### Prerequisites

There are no cloud resources within the subnet that have been assigned an IPv6 address.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Subnet**.

3. In the top menu bar, select the target project and region.

4. Click **Disable IPv6** in the **IPv6 CIDR** column of the target subnet row.

5. Click **Confirm** to complete the action.

## Related documents

[ModifySubnetAttributes](https://docs.byteplus.com/en/docs/vpc/ModifySubnetAttributes)
