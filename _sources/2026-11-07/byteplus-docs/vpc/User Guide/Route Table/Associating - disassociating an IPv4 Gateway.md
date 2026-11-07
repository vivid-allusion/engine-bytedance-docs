---
title: "Associating/disassociating an IPv4 Gateway"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Associating-disassociating-an-IPv4-Gateway"
---

## Attach IPv4 Gateway

### Prerequisites

The target IPv4 Gateway is associated with a VPC (where the gateway route table resides) and is activated. If no association exists, see [Associate a VPC and activate](https://docs.byteplus.com/en/docs/vpc/Associating-Disassociating-a-VPC), [Activate IPv4 Gateway](https://docs.byteplus.com/en/docs/vpc/Disabling-Enabling-an-IPv4-Gateway).

### Action description

Routes in the gateway route table take effect immediately after associating the IPv4 Gateway.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click **Associate IPv4 Gateway** on the right side of the target custom route table.

5. Select the associated IPv4 Gateway, click **Associate** to complete the operation.

## Detach IPv4 Gateway

### Action description

After disassociation, incoming IPv4 internet traffic to the VPC will no longer be routed to the firewall or gateway node for security protection. Proceed with extreme caution.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the target project and region.

4. Click **Disassociate IPv4 Gateway** to the right of the target custom route table.

5. Click **Migrate** to complete the action.

## Related documents

* [AssociateRouteTable](https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable)

* [DisassociateRouteTable](https://docs.byteplus.com/en/docs/vpc/DisassociateRouteTable)
