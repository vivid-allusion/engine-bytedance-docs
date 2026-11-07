---
title: "Associating/Disassociating a network interface"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-with-a-network-interface"
---

## Scenarios

This topic explains how to associate or disassociate network interfaces for a security group.

> **tip**

> Once a new security group is associated with a network interface, its rules are immediately added to the traffic\-matching queue. For whether the traffic of the network interface matches the rules of this security group, please see the [security group rules matching description](https://docs.byteplus.com/en/docs/vpc/Security-group-overview).

## Limitations

* Each network interface can be associated with up to 5 security groups.

* Each network interface must be associated with at least one security group.

* Each security group can be associated with up to 2,000 network interfaces.

## Associate Network Interface

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the project and region.

4. Click **Associate ENI** on the right side of the target security group.

5. On the **Associate ENI** tab, click **Associate ENI** and select one or more network interfaces.

6. Click **Associate** to complete the action.

## Disassociate Network Interface

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Security Group**.

3. In the top menu bar, select the project and region.

4. Click **Associate ENI** on the right side of the target security group.

5. On the **Associate ENI** tab, select any method to disassociate the associated network interface.

6. Click **Disassociate** on the right side of the target Network Interface.

7. After confirming that the details are correct, click **Disassociate** to complete the actions.

## Related documents

[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes)
