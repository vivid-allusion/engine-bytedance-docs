---
title: "Creating a route table"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

When the system route table cannot meet your business requirements, you can create custom route tables to flexibly manage the network traffic in a Transit Router (TR).

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Click **Create Route Table** to the right of the Route Table List, and configure the route table based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Route table name |Type the name for the route table to be created. |rtb\-set |
   |Tags |A tag consists of a key\-value pair and is used for categorizing and searching resources. [Learn more](https://docs.byteplus.com/en/docs/transitrouter/Tags)<br><br>Click **Add tag**, type the tag key and tag value to add tags to the TR route table. |* Tag key: rtb\-k1<br><br>* Tag value: rtb\-v1 |
   

5. Click **Create** to complete the action.


<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

After a custom route table is created, configure association forwarding and route entries for the table based on [List of routing capabilities](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx6IO95Yqb).

<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[CreateTransitRouterRouteTable](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteTable): Create a custom route table for a TR.
