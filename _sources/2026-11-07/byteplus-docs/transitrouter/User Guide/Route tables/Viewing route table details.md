---
title: "Viewing route table details"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-08"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

After configuring a route table, you can view its detailed information as needed, including all route entries in the table and the configured association forwarding and route learning.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table, then switch tabs to view related information of the route table.

   
   |Tab |Description |
   |---|---|
   |Basic information |This tab displays the basic information of the target route table, such as the name, description and creation time. |
   |Route entry |This tab displays all routes in the target route table, including static routes and routes auto\-learned from network instances. For details, see [Route types](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx5p2h55uu57G75Z6L). The routes in a TR can be in one of the following statuses:<br><br><br>* Available: The route is valid and used.<br><br>* Not effective: The route is valid but not used due to a lower priority than other routes in the TR route table.<br><br>* Conflict: The route's CIDR block conflicts with an existing route in the table. |
   |Association forwarding |This tab displays the status and information of all association forwarding rules configured in the target route table. |
   |Route learning |This tab displays the status and information of all route learning rules configured in the target route table. |
   


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation

[DescribeTransitRouterRouteEntries](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteEntries): Query route entries that meet the specified conditions.
