---
title: "Deleting a route table"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Deleting-a-route-table"
---

## Scenarios

You can delete a custom route table via this operation when it is no longer required.

> **tip**

> The system route table cannot be manually deleted; it is automatically deleted when the VPC itself is deleted. Refer to [Deleting a Virtual Private Cloud](https://docs.byteplus.com/en/docs/vpc/Deleting-a-VPC) for the operation.

## Prerequisites

* The custom route table is not associated with any subnets. If attached, disassociate it from the subnet first with [Disassociate](https://docs.byteplus.com/en/docs/vpc/Associating-or-disassociating-a-subnet). After disassociation, it automatically attaches to the system route table.

* The gateway route table is not associated with any IPv4 gateways. If attached, disassociate it from the IPv4 gateway first with [Disassociate](https://docs.byteplus.com/en/docs/vpc/Associating-disassociating-an-IPv4-Gateway#rjLQyzMC).

## Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the project and region.

4. In the route table list, click **Delete** to the right of the target route table.

5. Click **OK** to complete the action.

## Related documents

[DeleteRouteTable](https://docs.byteplus.com/en/docs/vpc/DeleteRouteTable)
