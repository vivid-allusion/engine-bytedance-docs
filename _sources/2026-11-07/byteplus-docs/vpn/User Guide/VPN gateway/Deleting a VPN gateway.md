---
title: "Deleting a VPN gateway"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Deleting-a-VPN-gateway"
---

<span id="x19Rs3Q5"></span>
## Scenarios

If you no longer need to use the VPN attachment service, you can delete the VPN gateway to release network resources. When you delete the VPN gateway, the gateway’s egress IP address will be deleted simultaneously and will not be retained.

<span id=".5YmN5o-Q5p2h5Lu2"></span>
## Prerequisites


* Subscription VPN gateways cannot be deleted before expiration. If you no longer need the VPN gateway afterward, go to the **Billing center** to unsubscribe. For details, see [Unsubscription](https://docs.byteplus.com/en/docs/6269/81013).

* The VPN gateway to be deleted cannot contain any IPsec\-VPN connections or SSL\-VPN servers. If any exist, first delete all IPsec\-VPN connections and SSL\-VPN servers under the VPN gateway, then delete the VPN gateway. For procedure, see [Deleting an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Deleting-an-IPsec-VPN-connection) and [Deleting an SSL-VPN server](https://docs.byteplus.com/en/docs/vpn/Deleting-an-SSL-server).


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to the [VPN Gateway console](https://console.byteplus.com/vpn/vpnGateway).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click **Delete** to the right of the target VPN gateway.

4. In the pop\-up dialog, confirm the VPN gateway information to be deleted.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteVpnGateway](https://docs.byteplus.com/en/docs/vpn/DeleteVpnGateway)
