---
title: "Adding a static route"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/Adding-a-static-route-entry"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

If a Virtual Interface associated with a Direct Connect (DC) Gateway uses "Static" routes, you need to add a static route at the on\-premises data center side for the DC Gateway to interconnect the network between the data center and the DC Gateway.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* You have created a DC Gateway with basic features and a Virtual Interface using **static** routes.


<span id=".6ZmQ5Yi25p2h5Lu2"></span>
## Limits

DC Gateways with the status of "Suspended" do not support adding static routes.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [Direct Connect Gateway console](https://console.byteplus.com/dc/DirectConnectGateway).

2. In the top menu bar, select your target region.

3. Click the name of the target DC Gateway.

4. Select the **Routing Information** tab, click **Add static route entry**, and configure the route based on the table below.

   
   |Parameter |Description |Sample value |
   |---|---|---|
   |Network type |Select the network type for the static route. It is IPv4 by default. If you enable IPv6 for DC Gateway, you can add static routes of IPv6 type. |IPv4 |
   |Destination CIDR |Based on the selected network type, enter the private CIDR block and its mask of your on\-premises data center. Ensure this CIDR block does not conflict with the private CIDR block of the Virtual Private Cloud (VPC) to be interconnected.<br><br> |192.168.22.0/24 |
   |Next Hop type |Select the next hop type for the route. It is fixed as **Virtual Interface**. |Virtual Interface |
   |Next Hop |Select the Virtual Interface that is associated with the current DC Gateway and configured with a route type of **Static**. |VIF\-ad3hu |
   

5. Click **Add** to add the route.

   <span id="C1hBDJFo"></span>
   ## Related documentation

[CreateDirectConnectGatewayRoute](https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGatewayRoute): Add a static route for a DC Gateway.
