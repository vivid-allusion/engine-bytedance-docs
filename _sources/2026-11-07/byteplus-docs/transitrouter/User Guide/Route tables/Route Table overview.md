---
title: "Route Table overview"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01"
---

<span id=".566A5LuL"></span>
## Overview

Transit Router (TR) route table consists of a series of route entries and supports association forwarding, route learning, and static routing. This allows quick addition of routes and flexible control of traffic direction in and out of the TR. For details, see [Route planning](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-02).

<span id=".6Lev55Sx57G75Z6L"></span>
## Route type

<span id=".6Lev55Sx6KGo57G75Z6L"></span>
### Route table type

TR route table includes System Route Table and Custom Route Table. After a TR route table is created, it contains no route entries by default. You need to configure route learning and auto publishing for it based on [List of routing capabilities](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-01#.6Lev55Sx6IO95Yqb).

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Route entries are isolated between separate route tables. Route tables do not learn from each other.</div>


The differences between System Route Table and Custom Route Table are shown in the table below.


|Route table type |Creation method |Action description |
|---|---|---|
|System route table |A system\-created route table. It is automatically created by the system when you create a TR instance. |Manual creation and removal are not supported. Other actions on the TR route table are supported. |
|Custom route table |A route table manually created by the user. |Supports all actions related to TR route tables. |


<span id=".6Lev55Sx5p2h55uu57G75Z6L"></span>
### Route entry type

The TR routes include the following three types:


* Blackhole route: This route is manually configured by the user. All traffic matching this route entry will be automatically discarded.

* Static route: This route is manually configured by the user. All traffic matching this route entry will be forwarded to the next hop.

* Auto\-learned route: This route is automatically learned from the network instance through the route learning feature. All traffic matching this route entry will be forwarded to the next hop.


<span id=".6Lev55Sx6IO95Yqb"></span>
## List of routing capabilities

TR offers rich routing capabilities that you can flexibly combine and use. The table below details all routing capabilities.


|Routing capability |Principle description |Configuration procedures |
|---|---|---|
|Custom route table |A route table is manually created by the user. You can use multiple TR route tables to define different interconnectivity scopes for network instances. |[Creating a route table](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-03) |
|Association forwarding |Used to specify the TR route table for the TR instance to forward traffic of a network instance.<br><br>As shown below, vpc01 and vpc02 each establish an attachment with the TR. vpc01 connects and associates with TR Route Table A for forwarding, while vpc02 connects and associates with TR Route Table B for forwarding. The numbered labels indicate the traffic flow when a client in vpc01 accesses a server in vpc02. The traffic flow is similar when vpc02 accesses vpc01.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_24f8da380f797d777c69aad4c7d06ea2.png) </span> |[Create an association forwarding rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-07) |
|Static routes |Manually configure routes on the TR instance side. This applies to scenarios with a small number of routes. |[Create a static route](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05) |
|Route propagation |Used to configure TR\-side routes by route learning. Applicable to scenarios with a large number of network instance routes.<br><br>After configuring route learning, the TR route table automatically generates routes with the next hop set to the attachment. |[Create a route learning rule](https://docs.byteplus.com/en/docs/transitrouter/Route-tables-06) |
|Auto Publish Route |Used to configure routes on the network instance side by auto publishing.<br><br>After enabling auto publishing, the system automatically publishes routes from the TR route table associated with forwarding of the target instance into the route table of that network instance. |[Enable auto publishing](https://docs.byteplus.com/en/docs/transitrouter/Attachments-04) |
|Route policy |Used to filter routes received and sent by the TR, which can change route propagation behavior and selection results.<br><br> |1. [Creating a route policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-routing-policy)<br><br>2. [Configuring a route policy for a TR route table](https://docs.byteplus.com/en/docs/transitrouter/Binding-Unbinding-Modifying-routing-policy-for-TR-route-table) |
|Forwarding policy |Used to specify the TR route table for the TR instance to forward traffic of a CIDR block in the network instance.<br><br>Forwarding policies cannot be used alone and must be configured together with association forwarding. For a single attachment, a forwarding policy takes precedence over association forwarding. As illustrated in the diagram below, two subnets in a VPC run different services. Subnet A forwards traffic based on TR Route Table A. Subnet B forwards traffic to the destination CIDR block (172.16.1.0/24) based on TR Route Table B, while traffic from Subnet B to other destination CIDR blocks still forwards based on TR Route Table A. This can be achieved by configuring forwarding policies.<br><br><span>![图片](https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_c6390654ef7d7dbfaa256fade29cdbc9.png) </span> |1. [Creating a forwarding policy](https://docs.byteplus.com/en/docs/transitrouter/Creating-a-forwarding-policy)<br><br>2. [Configuring a forwarding policy for a network instance attachment](https://docs.byteplus.com/en/docs/transitrouter/Enabling-Disabling-Modifying-forwarding-policy) |


<span id=".6Lev55Sx5LyY5YWI57qn"></span>
## Route matching and synchronization

<span id=".6Lev55Sx5LyY5YWI57qn"></span>
### Route matching

The priority order for route matching in the TR is as follows:


1. Follow the Longest Prefix Match (LPM) principle to prefer the route with the longest mask of the destination CIDR block.

2. For routes with an identical destination CIDR block, the priority order is as follows:

   1. Static routes

   2. Auto\-learned VPC routes

      * For routes that have the same destination CIDR block and learned from multiple VPCs, prefer the earliest learned route. Later learned routes become **not effective**.

      * After the TR forwards traffic to a VPC, the VPC's routing subsystem performs a second route lookup. This lookup queries the route table of the specific subnet where the attachment point resides. The subsystem then applies the Longest Prefix Match (LPM) rule to select the most specific route from that subnet's route table.

   3. Routes that are automatically learned from the TR, Direct Connect (DC) and Virtual Private Network (VPN) instances in the same region and the TR instances across regions.

      1. Prefer the route with the shortest AsPath.

         For DC routes that lack an AsPath attribute, the AsPath length defaults to 0​​. A common example is static routes learned from the DC Gateway.

      2. When the AsPath length is identical, the routing priority order is as follows:

         1. Routes learned from DC Gateways

            Routes from multiple DC Gateways with identical CIDR blocks and AsPath lengths form equal\-cost multi\-path routing (ECMP).

         2. Routes learned from VPNs

            Routes from multiple IPsec\-VPN connections with identical CIDR blocks and AsPath lengths form ECMP.

         3. Routes learned from inter\-region TRs

            Routes from multiple TRs across regions with identical CIDR blocks and AsPath lengths are sorted by the string comparison of peer TR instance IDs, preferring the route with the smallest TR instance ID.


<span id=".6Lev55Sx5L2_55So6ZmQ5Yi2"></span>
### Route synchronization

The logic for TR synchronizing routes to network instances is described in the following table.


|Attachment type |Description |
|---|---|
|VPC attachment |The system injects the TR route as a system route into all the route tables of the VPC. The injected route has the TR instance of the network instance attachment as its next hop.<br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">The system will not synchronize corresponding TR routes to the VPC route tables under the following conflicts:</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The next hop of the TR route is the VPC itself.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The TR route has the exact same destination CIDR block as an existing route in the VPC.</div><br><br><br>   * <div data-tips="true" data-tips-type="warning">The TR route overlaps with an existing subnet route in the VPC, and its mask is longer.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">After deleting the conflicting routes above, the system will resynchronize the TR route to the VPC route table.</div><br> |
|VPN attachment |When the routing propagation mode is dynamic, the system propagates all route entries in the TR route table to the VPN route table. Exceptions are entries where the next hop is this network instance attachment itself.<br><br> |
|DC Gateway attachment |The system propagates all route entries in the TR route table—except those with the next hop being this network instance attachment itself—to the route table of the DC Gateway.<br><br>If multiple ECMP routes from other DC Gateways exist in the TR route table, the system selects the route with the smallest source DC Gateway instance ID for synchronization to this DC Gateway. |
|Intra\-region peering attachment |Route synchronization is enabled by default and cannot be turned off.<br><br>Only when peer route learning is enabled can the peer TR route table learn routes synchronized from the local TR. |
|Inter\-region attachment |Auto Publish Route is enabled by default and cannot be disabled.<br><br>Only when route learning is enabled on the peer can the peer TR route table learn the TR routes synchronized from the local side. |


<span id=".6Lev55Sx5L2_55So6ZmQ5Yi2"></span>
## Route limits


* Each network instance attachment can configure only one TR route table associated with forwarding.

* When creating a cross\-account network instance attachment, if you need to configure association forwarding or route learning simultaneously, you can only select the TR system route table, which can only be modified by the TR instance’s Owner.


For more information, see [Limits](https://docs.byteplus.com/en/docs/transitrouter/Product-Overview-04).
