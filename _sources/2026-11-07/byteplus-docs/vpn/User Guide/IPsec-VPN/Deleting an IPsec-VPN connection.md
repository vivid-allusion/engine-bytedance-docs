---
title: "Deleting an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Deleting-an-IPsec-VPN-connection"
---

This topic describes how to delete an unused IPsec\-VPN connection to release the network resources.

<span id=".5pON5L2c6ZmQ5Yi2"></span>
## Limits


* Deleting an IPsec\-VPN connection also removes all route entries in the VPN gateway whose next hop is this IPsec\-VPN connection.

* IPsec\-VPN connections attached to a Transit Router (TR) cannot be deleted directly. First delete the IPsec\-VPN connection instance on the TR side by [deleting an intra-region attachment](https://docs.byteplus.com/en/docs/transitrouter/Attachments-03).


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Once deleted, the IPsec\-VPN connection becomes immediately invalid. This may affect your ongoing services. Proceed with caution.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect). 

2. In the top menu bar, select the target project and region.

3. Click **Delete** on the right side of the target IPsec\-VPN connection.

4. In the popup dialog box, confirm the information of the IPsec\-VPN connection to be deleted.

5. Click **Delete** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[DeleteVpnConnection](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnection): Delete the specified IPsec\-VPN connection.
