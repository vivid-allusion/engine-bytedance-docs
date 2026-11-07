---
title: "Updating a network interface security group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Updating-the-security-group-of-a-network-interface"
---

## Scenarios

As your business evolves, security group policies may become increasingly complex. This operation allows you to switch or add associated security groups for a network interface to adapt to changing business requirements.

> **tip**

> If a network interface is associated with multiple security groups, please be sure to review [the security group rule matching guideline](https://docs.byteplus.com/en/docs/vpc/Security-group-overview) to understand how inbound and outbound traffic is matched against security group rules. This helps prevent potential service disruptions caused by updates to the network interface's associated security groups.

![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5f8b4bae66e0d783e025edd66550fd77.png)

## Action description

* Changes to security groups take effect immediately. Both existing persistent connections and newly established connections are governed by the updated security group rules.

* Each network interface must be associated with at least one security group and can be associated with up to five.

* A network interface can only be associated with security groups within the same VPC.

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click  **··· \> Update Security Group Policy** on the right side of the target Network Interface.

5. On the **Associated Security Groups** page, click **Change Security Group** on the right side of the associated security group.

   * Select: Add associated security groups to the network interface.

   * Deselect: Remove associated security groups from the network interface.

6. Click **OK** to complete the action.

## Related documents

[ModifyNetworkInterfaceAttributes](https://docs.byteplus.com/en/docs/vpc/ModifyNetworkInterfaceAttributes)
