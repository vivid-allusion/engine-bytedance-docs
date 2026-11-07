---
title: "Enabling/Disabling IPv6"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-VPC"
---

## Scenarios

This topic introduces how to enable/disable IPv6 for a Virtual Private Cloud (VPC).

> **tip**

> VPC's IPv6 is currently in Beta stage. If you need a trial, please contact your account manager.

## Enable IPv6 for VPC

### Action description

* After enabling the IPv6 for a VPC, the system automatically creates an [IPv6 Gateway](https://docs.byteplus.com/en/docs/IPv6/What_is_IPv6_Gateway) and associates it with the VPC.

* After enabling the IPv6 for a VPC, IPv6 rules are added automatically to all security groups and network ACLs within the VPC. See [Network ACL overview](https://docs.byteplus.com/en/docs/vpc/Network-ACL-overview) and [Security group overview](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) for details.

### Procedures

1. Log in to the VPC consoleVPC console.

2. In the top menu bar, select the target project and region.

3. Click **Enable IPv6** next to the target VPC.

4. Select the ISP from the dropdown menu to automatically assign an IPv6 CIDR block of that type to the VPC, such as `2408:XXXX:0:a600::/56`.

   > **tip**

 has **Auto\-assign**, and the type is BGP (Multi\-ISP).

5. Click **Enable** to complete the action.

### What to do next

After enabling IPv6 for the VPC, you must also enable IPv6 for subnets to use IPv6 features. For details, see [Enabling IPv6 for a subnet](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-subunet).

## Disable IPv6 for VPC

### Prerequisites

* All subnets in the VPC have IPv6 disabled. If any subnet is still enabled, see [Disable IPv6 for subnet](https://docs.byteplus.com/en/docs/vpc/Enabling-or-disabling-IPv6-for-a-subunet).

* The VPC has no associated IPv6 Gateway. If associated, see [Delete IPv6 Gateway Instance](https://docs.byteplus.com/en/docs/IPv6/Deleting_an_IPv6_gateway_instance).

### Procedures

1. Log in to the VPC consoleVPC console.

2. In the top menu bar, select the target project and region.

3. Click the **IPv6 CIDR** column in the target VPC, then click **Disable IPv6**.

4. Click **Confirm** to complete the action.

## Related documents

[ModifyVpcAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyVpcAttributes)
