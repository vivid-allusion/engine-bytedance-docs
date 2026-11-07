---
title: "Creating/Deleting a server group"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/Creating-or-deleting-a-server-group"
---

<span id=".5Yib5bu65pyN5Yqh5Zmo57uE"></span>
## Creating a server group


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select your target Region.

4. In the server group list, click **Create Server Group**.

5. Configure relevant parameters based on the table below.

   
   |Parameter |Explanation |Sample value |
   |---|---|---|
   |Name |Enter server group name |InstanceGroup\-1 |
   |VPC |Select the server group's VPC from the dropdown. |VPC\-01 |
   

6. Click **Create** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
### What to do next


1. [Add server](https://docs.byteplus.com/en/docs/vpc/Adding-or-Removing-servers#.5re75Yqg5pyN5Yqh5Zmo): Add servers with deployed services to a server group.

2. [Add route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry): Add a route entry that directs traffic to the server group.


<span id=".5Yig6Zmk5pyN5Yqh5Zmo57uE"></span>
## Deleting a server group

<span id=".5YmN5o-Q5p2h5Lu2"></span>
### Prerequisites

The server group has no servers. If servers have been added, first [Move out Server](https://docs.byteplus.com/en/docs/vpc/Adding-or-Removing-servers#.56e75Ye65pyN5Yqh5Zmo).

<span id=".5pON5L2c6K-05piO"></span>
### Action description

After a server group is deleted, the routing entries pointing to it in the route table will be automatically removed.

<span id=".5pON5L2c5q2l6aqk"></span>
### Procedures


1. Log in to the [VPC console](https://console.byteplus.com/vpc/vpc).

2. In the left navigation pane, select **Server Group**.

3. In the top menu bar, select your target Region.

4. In the server group list, click **Delete** on the right side of the target server group.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [CreateInstanceGroup](https://docs.byteplus.com/en/docs/vpc/CreateInstanceGroup)

* [DeleteInstanceGroup](https://docs.byteplus.com/en/docs/vpc/DeleteInstanceGroup)
