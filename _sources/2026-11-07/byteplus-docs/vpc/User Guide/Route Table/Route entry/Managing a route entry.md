---
title: "Managing a route entry"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry"
---

## Add route entry

### **Action notes**

* The destination CIDR block of a route cannot be the same as that of an existing route entry.

* The Subnet route table destination CIDR block of a route cannot be a subset of the CIDR block of a subnet in the VPC to which it belongs.

* The newly added route entry will take effect immediately. Both existing persistent connections and subsequently established new connections will be affected by the new route.

### **Procedures**

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the project and region.

4. Click the target route table name.

5. On the **Route entry \> Custom route** tab, click **Add route**.

6. Different types of route tables have different parameter values, as detailed below:

   * **Subnet route table**

      |Parameters |Notes |Sample value |
      |---|---|---|
      |Destination CIDR |Set the destination CIDR block for traffic routing. Supports IPv4 CIDR, IPv6 CIDR, and prefix lists.<br><br><br>* A prefix list consists of a set of CIDR blocks and can be reused across multiple route tables, simplifying route entry configuration. When a prefix list is modified, all associated route tables are updated synchronously. [Learn more](https://docs.byteplus.com/en/docs/vpc/Prefix-list-overview)<br><br>* The maximum number of routes a route table can hold must be greater than or equal to the maximum number of entries in the target prefix list. |0.0.0.0/0 |
      |Next Hop type |Select a resource type for the next hop of the route entry.<br><br><br>* IPv4: Supports selection of ECS, NAT Gateway, Secondary ENI, VPN Gateway, High Availability Virtual IP, Transit Router, IPv4 Gateway, Gateway Load Balancer Endpoint, and Server Group.<br><br>* IPv6: Supports selection of ECS, Secondary ENI, Transit Router, IPv6 Gateway, and Gateway Load Balancer Endpoint.<br><br><br>> **tip**<br><br><br><br>* > When the next hop type is IPv6 Gateway, the destination CIDR block is fixed to `::/0` and cannot be modified.<br><br><br>* > IPv4 gateway and IPv6 Gateway are in beta stage. If you need a trial, please contact your account manager.<br> |NAT |
      |Next Hop |Select resources from the drop\-down menu based on the next hop type. |NAT\-1 |

      * **Gateway** ** route table**

      |Parameters |Notes |Sample value |
      |---|---|---|
      |Destination CIDR |Set the destination CIDR block for traffic routing. Enter an IPv4 CIDR block, and the destination CIDR block must be within the CIDR block of the current VPC. |192.168.1.0/24 |
      |Next Hop type |Select a resource type for the next hop of the route entry. Supports Secondary ENI and Gateway Load Balancer Endpoint. |Secondary network interface |
      |Next Hop |Select resources from the drop\-down menu based on the next hop type. |ENI\-1 |

7. Click **Create** to complete configuration.

## Modify the next hop of a route

When traffic switching is required by business needs, modifying the next hop of a route entry minimizes the interruption duration compared to reconfiguring routes.

### **Action notes**

* Only subnet route tables can be modified. Gateway route tables do not support modifications.

* Route entries for an IPv6 gateway can only be added, not modified.

* The modifications take effect immediately. Therefore, please choose an appropriate time to make these changes to minimize the impact of route propagation and switching on your services.

### **Procedures**

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the project and region.

4. Click the target route table name.

5. In the **Route Entry \> Custom route** tab, click **Edit** on the right side of the target route entry.

6. Select the new next hop Type and resource from the drop\-down menu, and click **Confirm** to complete the actions.

## Delete route entry

System route entries cannot be deleted. You can delete custom route entries.

> **warning**

> Deleting a route entry will immediately interrupt traffic forwarded through it. Proceed with caution.

1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Route Table**.

3. In the top menu bar, select the project and region.

4. Click the target route table name.

5. In the **Route Entry \> Custom route** tab, click **Delete** to the right of the target route entry.

6. Click **Remove** to complete the action.

## Related documents

* [CreateRouteEntry](https://docs.byteplus.com/en/docs/vpc/CreateRouteEntry)

* [ModifyRouteEntry](https://docs.byteplus.com/en/docs/vpc/ModifyRouteEntry)

* [DeleteRouteEntry](https://docs.byteplus.com/en/docs/vpc/DeleteRouteEntry)
