---
title: "Adding a  VPN gateway route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Adding-a-VPN-gateway-route"
---

If the IPsec\-VPN connection uses static routing, you must manually add route entries from the VPN gateway to the customer gateway after completing the IPsec\-VPN connection configuration.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites

You have created an IPsec\-VPN connection. For procedure, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1).

<span id=".57qm5p2f6ZmQ5Yi2"></span>
## Limits

You cannot add route entries that conflict with existing routes in the VPN gateway's private network route table.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">The project must match the project of the VPN gateway for which the route is being added. VPN gateway routes are sub\-resources of the VPN gateway. Their project attribute matches the VPN gateway’s and follows the VPN gateway during project migration. VPN gateway routes cannot be migrated independently.   </div>
   

3. Click the name of target VPN gateway.

4. Select the **Routing information** tab, then click **Add route**.

5. Configure routing according to the table below.

   
   |Parameter |Description |Example |
   |---|---|---|
   |Destination CIDR |Enter the private CIDR block of the data center or the CIDR block of another Virtual Private Cloud (VPC) accessed by a VPC via the IPsec\-VPN connection. |192.168.3.0/24 |
   |Next Hop type |Fixed to IPsec\-VPN connection. |IPsec\-VPN connection |
   |Next Hop |Select the created IPsec\-VPN connection. |IPsecVPN\-jym1\-tp2v |
   

6. Click **OK** to add the route.

   After the route is added, the system automatically published the route to the system route table of the VPC associated with the VPN gateway.

   <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="1">tip   </div>
   

   <div data-tips="true" data-tips-type="tip" data-wrapper-indent="1">Routes configured on the VPN gateway side are only distributed to the system route table of its associated VPC. If your VPC has a custom route table and the subnet traffic linked to this table needs to be forwarded to the VPN gateway, follow these steps: Manually add a route to the custom route table. Set the Destination CIDR block to the Remote Subnet. Set the Next Hop type to <strong>VPN gateway</strong> to forward subnet traffic to the VPN gateway.   </div>
   

<span id=".5ZCO57ut5pON5L2c"></span>
## What to do next

If the added VPN gateway route conflicts with the destination CIDR block of an existing route in the VPC system route table, you need to manually modify the destination CIDR block of the VPN gateway route. Alternatively, you can delete the conflicting route in the VPC system route table. For procedure, see [Delete route](https://docs.byteplus.com/en/docs/vpc/Managing-a-route-entry#.5Yig6Zmk6Lev55Sx5p2h55uu).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[CreateVpnGatewayRoute](https://docs.byteplus.com/en/docs/vpn/CreateVpnGatewayRoute): Add a destination\-based route for a VPN gateway.
