---
title: "Changing a route table"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Changing-a-route-table-associated-with-a-subnet"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

As your business grows and requires finer\-grained routing control, you can replace the routing table associated with a subnet. This switches the traffic of resources within the subnet from the original routing table to the new one.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The switch takes effect instantly, and all active connections will be disconnected. Proceed with strong caution.</div>


<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

A routing table has been created, and the required route entries for business operations have been added. For related actions, see [Creating a route table](https://docs.byteplus.com/en/docs/vpc/Creating-a-custom-route-table) and [Adding a route entry](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left\-side navigation pane, select **Subnet**.

3. In the top menu bar, select the target project and region.

4. In the subnet list, click **Change route table** on the right of the target subnet.

5. Select the target Route Table.

6. Click **Change** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[AssociateRouteTable](https://docs.byteplus.com/en/docs/vpc/AssociateRouteTable)
