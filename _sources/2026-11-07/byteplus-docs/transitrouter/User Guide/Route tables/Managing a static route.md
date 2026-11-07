---
title: "Managing a static route"
product: "Transit Router"
product_code: "transitrouter"
source: "https://docs.byteplus.com/en/docs/transitrouter/Route-tables-05"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

To flexibly control traffic flow through the Transit Router (TR), create or delete a static route in the route table associated with a network instance attachment or an inter\-region attachment. When the number of route entries is large, you can use prefix lists to create static routes, thereby simplifying route configuration.

<span id="3428c225"></span>
## Prerequisites

To create static routes through a prefix list, ensure you have [created the prefix list](https://docs.byteplus.com/en/docs/vpc/Creating-a-prefix-list).

<span id="gT1BKfqN"></span>
## Create a static route


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table and click the **Route entry** tab.

5. Click **Create static route**, and configure the static route based on the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Route name |Name of the static route to be created. |Example route |
   |Destination CIDR |Set the destination CIDR block to be accessed. IPv4/IPv6 CIDR and Prefix list are supported.<br><br><br>* When Destination CIDR is set to **IPv4/IPv6 CIDR**:<br><br>   * Destination CIDR cannot be identical to that of any existing route entry in the route table.<br><br>   * The destination CIDR block must not be a multicast CIDR (`224.0.0.0–239.255.255.255` or `FF00::/8`).<br><br>   * After enabling IPv6, IPv6 CIDR blocks are supported when the next hop is a TR attachment with IPv6 enabled.<br><br>      <div data-tips="true" data-tips-type="default" data-tips-is-title="true" data-wrapper-indent="2">tip      </div><br>      <br><br>      <div data-tips="true" data-tips-type="default" data-wrapper-indent="2">The IPv6 feature of TR is in the beta stage. If you need a trial, please contact your account manager.      </div><br>      <br><br>* When Destination CIDR is set to **Prefix list**:<br><br>   * The number of route entry quota consumed by this static route is equal to the maximum entries of the prefix list. For example, if a prefix list has a maximum of 100 entries (with 10 entries configured), it will consume 100 route entries in the TR route table.<br><br>   * You cannot select a prefix list that would cause the number of route entries in the TR route table to exceed its quota limit.<br><br>   * To modify a prefix list entry, see [Adding or deleting a prefix list entry](https://docs.byteplus.com/en/docs/vpc/Managing-entries-in-the-prefix-list). |192.168.22.0/24 |
   |Black hole routing |Specify whether the static route to be created is a blackhole route.<br><br><br>* Yes: All traffic pointing to this route will be discarded.<br><br>* No: All traffic pointing to this route will be forwarded to the next hop. This option requires you to specify the next hop for this route. |No |
   |Next Hop type |Select the next hop for this static route. Options: Intra\-region attachment and Inter\-region attachment. |Intra\-region attachment |
   |Next Hop |Select the next hop for this static route. Routes from the destination CIDR block will be forwarded to the specified next hop.<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">This parameter is not required when Blackhole routing is set to <strong>Yes</strong>.</div><br> |attach\-vpc |
   

6. Click **Create** to complete the action.


<span id=".5Yig6Zmk6Z2Z5oCB6Lev55Sx"></span>
## Delete a static route


1. Log in to [the Transit Router console](https://console.byteplus.com/tr/transitRouter).

2. Click the name of the target TR instance.

3. In the zone below **Basic information**, select the **Route Table** tab.

4. Select the target route table and delete static routes as needed.

   * **Single delete**: Click **Delete** to the right of the target static route and confirm the resource information.

   * **Batch delete**: Check all static routes to be deleted, click **Delete route entry** and confirm the resource information.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documentation


* [CreateTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/CreateTransitRouterRouteEntry): Add a static route to a specified TR route table.

* [DeleteTransitRouterRouteEntry](https://docs.byteplus.com/en/docs/transitrouter/DeleteTransitRouterRouteEntry): Delete a specified static route.
