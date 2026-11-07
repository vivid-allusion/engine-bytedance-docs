---
title: "Adding/Removing a server"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Adding-or-Removing-servers"
---

## Add server

### Action description

* Please deploy services on your ECSs before adding them to a server group. This prevents traffic from being routed to ECSs without deployed services, which could impact business operations.

* Adding ECSs to a server group does not affect existing connections.

* Ensure that the security group for the ECS's primary network interface allows inbound health check traffic from the server group. Specifically, add an inbound rule with the destination CIDR block set to 100.64.0.0/10 and the protocol set to ICMP.

* Server groups only support adding ECSs that reside in the same VPC.

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Server group**.

3. In the top menu bar, select your target Region.

4. In the server group list, click the target server group name.

5. Click **Add server** In the slide\-in panel on the right, select one or multiple servers as needed.

6. Click **Migrate** to complete the action.

## Remove Server

### Action description

* Removing an ECS from the server group will terminate all active connections to that server. Please proceed with caution.

* The Elastic Compute Service (ECS) will not be released after being removed. If you need to release it, see [Deleting an instance](https://docs.byteplus.com/en/docs/ecs/Deleting-ECS-instances).

### Procedures

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Server group**.

3. In the top menu bar, select your target Region.

4. In the server group list, click the target server group name.

5. On the right side of the target server list, click **Remove**.

6. Click **Remove** to complete the actions.

## Related documents

[ModifyInstanceGroupMembers](https://docs.byteplus.com/en/docs/vpc/ModifyInstanceGroupMembers)
