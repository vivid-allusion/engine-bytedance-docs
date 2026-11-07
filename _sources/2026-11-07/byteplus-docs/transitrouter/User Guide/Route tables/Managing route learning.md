---
title: "Managing route learning"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

By creating route learning, the route table automatically generates routes with the next hop set to the specified network instance. This means you no longer have to manually create and manage a large number of static routes, significantly streamlining Transit Router (TR) configuration.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* A TR route table can establish route learning with multiple network instances. A network instance can also establish route learning with multiple TR route tables. After route learning is established, the routes learned by the TR route table from different network instances vary, as shown in the table below.

   
   |Attachment type |Attached network instance type |Auto\-learned routes |
   |---|---|---|
   |Network instance attachment |Virtual Private Cloud (VPC) |* Automatically learn subnet routes by default, specifically all routes in the VPC system route table whose destination CIDR block matches a subnet CIDR block.<br><br>* If the learning granularity feature is enabled, the auto\-learned routes vary according to the configured granularity.<br><br>   * **Set learning granularity to Subnet CIDR**: Subnet routes will be automatically learned, specifically all routes in the VPC system route table whose destination CIDR block matches a subnet CIDR block.<br><br>   * **Set learning granularity to VPC CIDR**: Routes of VPC CIDR blocks will be automatically learned by summarizing all subnet routes based on VPC CIDR blocks (including the primary CIDR block and the IPv4/IPv6 secondary CIDR block).<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">Enabling route learning at the VPC CIDR granularity will forward traffic belonging to the VPC CIDR block but not to any subnet within that VPC to the TR, causing changes in traffic forwarding paths. Carefully assess and decide.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After enabling route learning at the VPC CIDR granularity, the TR route table learns/withdraws the related routes when you enable/disable VPC IPv6 CIDR and add/delete secondary CIDR blocks on the VPC side.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">Once the learning granularity is configured, it cannot be modified. You can only delete the current route learning configuration and set up a new one.</div><br> |
   ||Direct Connect Gateway |Routes in the DC Gateway with the destination CIDR block set to the on\-premises CIDR block. |
   ||Virtual Private Network (VPN) |Routes whose destination CIDR blocks are on\-premises CIDR blocks connected through the IPsec\-VPN connection. |
   |Inter\-region attachment |Transit Router |All routes in the peer TR route table, except those with the next hop being the inter\-region attachment itself. |
   

* TR discards routes coming from attachments under the following conditions:

   * The AsPath of the route contains the TR's own ASN.

   * The route's AsPath length exceeds 30.

   * A route whose destination CIDR block is a multicast CIDR block (`224.0.0.0 to 239.255.255.255` or `FF00::/8`).


<span id=".5Yib5bu66Lev55Sx5a2m5Lmg"></span>
## Create a route learning rule


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table and click the **Route learning** tab.

5. Click **Create route learning** and select the attachment type.

   <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="default" data-wrapper-indent="1">If you select a VPC attachment, configure <strong>Learning granularity</strong> as needed. For more descriptions and limits, see <a href="https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06">Instructions</a>.   </div>
   

6. Click **Create** to complete the action.


<span id=".5Yig6Zmk6Lev55Sx5a2m5Lmg"></span>
## Delete a route learning rule

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">After a route learning rule is deleted, TR routes learned from this network instance will be automatically withdrawn.</div>



1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table and click the **Route learning** tab.

5. Click **Delete** to the right of the target route learning rule, and confirm resource information.

6. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [DescribeTransitRouterRouteTablePropagations](https://docs.byteplus.com/en/docs/transitrouter/DescribeTransitRouterRouteTablePropagations): Query route learning rules created in a specified route table.

* [DisableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/DisableTransitRouterRouteTablePropagation): Delete a specified route learning rule.

* [EnableTransitRouterRouteTablePropagation](https://docs.byteplus.com/en/docs/transitrouter/EnableTransitRouterRouteTablePropagation): Create a route learning rule.
