---
title: "Associating/Disassociating an EIP"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-an-EIP"
---

## Scenarios

If a network interface requires multiple EIPs, you can achieve this by associating EIPs to multiple private IPv4 addresses on the Network Interface.

> **tip**

> To associate or disassociate an EIP for the primary private IPv4 address of the primary network interface (that is, the Elastic Compute Service), please go to the [ECS console](https://docs.byteplus.com/en/docs/ecs/associating-an-EIP) or [EIP console](https://docs.byteplus.com/en/docs/eip/Associating-Cloud-Resources-with-an-EIP) to perform the actions.

## Associate an EIP

### Action description

Each private IPv4 address on a network interface can be associated to one EIP.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click  **··· \> Manage IP Addresses** on the right side of the target Network Interface.

5. In the private IP address list, find the row of the target private IPv4 address and click **Associate** in the **EIP** column.

6. In the Select EIP window that appears, select the target EIP, then click **Associate** to complete the actions.

## Disassociate an EIP

### Action description

* After disassociating an EIP, any active connections using that EIP will be terminated immediately.

* In addition to the method below, you can also [Disassociate EIP in the Elastic IP console](https://docs.byteplus.com/en/docs/eip/Disassociating-Cloud-Resource-from-an-EIP).

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Network Interface**.

3. In the top menu bar, select the target project and region.

4. Click  **··· \> Manage IP Addresses** on the right side of the target Network Interface.

5. In the private IP address list, click the **EIP** column in the row of the target private IPv4 address and then click **Disassociate**.

6. Click **Migrate** to complete the action.

## Related documents

* [AssociateEipAddress](https://docs.byteplus.com/en/docs/eip/AssociateEipAddress)

* [DisassociateEipAddress](https://docs.byteplus.com/en/docs/eip/DisassociateEipAddress)
