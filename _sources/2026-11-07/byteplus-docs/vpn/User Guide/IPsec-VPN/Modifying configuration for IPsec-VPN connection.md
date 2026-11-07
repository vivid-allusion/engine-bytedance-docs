---
title: "Modifying configuration for IPsec-VPN connection"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Modifying-IPsec-VPN-connection-configurations"
---

<span id=".5pON5L2c5Zy65pmv"></span>
## Scenarios

You can modify the configuration of an IPsec\-VPN connection, such as the name, description, routing mode, route propagation mode, customer gateway, pre\-shared key, local subnet, remote subnet, IKE Config, IPsec Config, NAT traversal, and Dead Peer Detection (DPD).

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Pre\-Shared Key is for IKE negotiation between VPN devices on both sides. Ensure the configuration on both sides of the VPN Connect is identical. This information is crucial. Keep it secure.</div>


<span id=".5pON5L2c6K-05piO"></span>
## Instructions

**Any modifications to an IPsec\-VPN connection will clear the established IKE SA, except modifying its name or description**. After modification is completed, the IPsec\-VPN connection will initiate a connection instantly or re\-establish the connection upon receiving new traffic based on your negotiation setting.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To enable dynamic routing for IPsec\-VPN connections via Transit Router (TR) that were created before September 30, 2024, you need to <a href="https://console.byteplus.com/workorder/create?step=3&SubProductID=P00000249&FlowKey=NGhBLLYotsiBMSgHMvCt">submit a ticket</a>.</div>


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure


1. Log in to [the VPN Connection console](https://console.byteplus.com/vpn/vpnConnect).

2. In the top menu bar, select the project and region to which the target resource belongs.

3. Click **Modify** to the right of the target IPsec\-VPN connection and modify its configuration as needed. For more parameters, see [Creating an IPsec-VPN connection](https://docs.byteplus.com/en/docs/vpn/Creating-an-IPsec-VPN-connection1).

4. Click **OK** to complete the action.


<span id=".55u45YWz5paH5qGj"></span>
## Related documents


* [ModifyVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes): Modify configuration for an IPsec\-VPN connection, including parameters common to both single\- and dual\- tunnel modes and parameters specific to single tunnel mode.

* [ModifyVpnConnectionTunnelAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes): Modify parameters specific to dual\-tunnel IPsec\-VPN connections.
