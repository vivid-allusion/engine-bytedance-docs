---
title: "Deleting a VPN gateway route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Deleting-a-VPN-gateway-route"
---

This topic describes how to delete a route entry that is no longer in use to release the network resource.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions

The route entries to be deleted are no longer needed. If the route to be deleted is still in use, deleting it may cause network disruption.

<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [ VPN Gateway console.](https://console.byteplus.com/vpn/vpnGateway). 

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click the name of target VPN Gateway.

4. Select the **Routing information** tab, then click **Delete** on the right side of target route entry.

5. In the pop\-up dialog box, confirm the information of route to be deleted.

6. After confirming the information is correct, click **Delete** to complete the action.


<span id=".5pON5L2c57uT5p6c"></span>
## Results

After a VPN gateway route is deleted, the route entry is also removed from the route tables of the associated Virtual Private Cloud (VPC).

<span id=".55u45YWz5paH5qGj"></span>
## Related documents

DeleteVpnGatewayRoute: Delete a route entry.
