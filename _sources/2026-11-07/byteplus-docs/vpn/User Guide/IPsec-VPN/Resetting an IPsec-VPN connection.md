---
title: "Resetting an IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Reset-IPsec-VPN-connection"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

IPsec\-VPN tunnels may experience packet loss after prolonged connectivity. If the tunnel suddenly becomes unreachable or health check fails, you can reset the IPsec\-VPN connection.

<span id=".5pON5L2c6K-05piO"></span>
## Instructions


* You can reset IPsec\-VPN tunnels only for existing connections. This action is unsupported for connections without being attached to a Transit Router (TR).

* Resetting IPsec\-VPN connection may interrupt the current data transmission through the tunnel. To avoid impacting business operations, perform this action at off\-peak hours.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the target project and region.

3. In the IPsec\-VPN connection list, click **Reset connection** in the operations column of the target IPsec\-VPN connection.

   <div data-tips="true" data-tips-type="warning" data-tips-is-title="true" data-wrapper-indent="1">warning   </div>
   

   <div data-tips="true" data-tips-type="warning" data-wrapper-indent="1">Clicking <strong>Reset connection</strong> will reset all tunnels of the IPsec\-VPN connection. For example, after resetting an IPsec\-VPN connection in Protected Data Flows mode, all tunnels individually established between different local and peer CIDR blocks will be reset. Proceed with caution.   </div>
   

4. In the pop\-up dialog box, click **OK**. The IPsec\-VPN connection will restore to the initial state and immediately initiate the connection or wait for the peer to initiate it according to your IPsec\-VPN connection configuration.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents

[ResetVpnConnection](https://docs.byteplus.com/en/docs/vpn/ResetVpnConnection): Reset tunnel for an IPsec\-VPN connection.
