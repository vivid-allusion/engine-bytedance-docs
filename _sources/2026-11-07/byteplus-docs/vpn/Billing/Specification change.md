---
title: "Specification change"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Upgrade-and-downgrade"
---

This topic introduces precautions and related procedures for modifying VPN gateway configurations, such as Bandwidth, SSL Max Connections, Function configuration and other configurations.

<span id=".5Y-Y6YWN5b2x5ZON"></span>
## Impact of modifying instance specifications

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning"><strong>This section contains very important notices. Ignoring them may affect your business. Review and assess carefully before making changes</strong>.</div>



* When Bandwidth of the VPN gateway is changed across specifications, IPsec\-VPN connections and SSL\-VPN connections using this VPN gateway will be temporarily interrupted and will automatically reconnect shortly after.

   The cross\-spec change scenarios are as follows:

   * Upgrade from 200 Mbps or lower specifications (5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps) to 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, or 3 Gbps.

   * Downgrade from 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, or 3 Gbps to 200 Mbps or lower specifications (5 Mbps, 10 Mbps, 20 Mbps, 50 Mbps, 100 Mbps, 200 Mbps).

      <div data-tips="true" data-tips-type="tip" data-tips-is-title="true" data-wrapper-indent="2">tip      </div>
      

      <div data-tips="true" data-tips-type="tip" data-wrapper-indent="2">Currently, VPN gateways in 1 Gbps and 3 Gbps are in the beta stage. Only users who have activated these specifications can use. To request a trial, please contact your account manager.      </div>
      

* When downgrading Bandwidth of the VPN gateway, if the original bandwidth is close to the modified specification, packet loss may occur. Please thoroughly evaluate and select an appropriate Bandwidth.

* Modifying SSL Max Connections (including upgrading and downgrading) and other SSL\-VPN connection configurations may cause temporary interruptions to existing SSL\-VPN connections. But they will automatically reconnect shortly after.

* If SSL Max Connections is downgraded and the existing connections are more than the modified SSL Max Connections, preemption occurs during auto\-reconnecting based on the client\-side reconnection mechanism.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For IPsec\-VPN connections with a dynamic egress IP address on the peer side (i.e., the customer gateway IP address is <code>0.0.0.0/0</code>), the auto\-reconnect mechanism depends on whether the peer gateway supports immediate reconnection.</div>


   * <div data-tips="true" data-tips-type="tip">If the remote gateway supports immediate reconnection, the connection will automatically reconnect right after an interruption.</div>


   * <div data-tips="true" data-tips-type="tip">If the remote gateway does not support immediate reconnection, you need to manually initiate a connection.</div>


* <div data-tips="true" data-tips-type="tip">The automatic reconnection mechanism for SSL\-VPN connections depends on whether the client you are using supports immediate reconnection.</div>


   * <div data-tips="true" data-tips-type="tip">If the client supports immediate reconnection, the connection will automatically reconnect right after an interruption.</div>


   * <div data-tips="true" data-tips-type="tip">If the client does not support immediate reconnection, you must manually initiate the connection.</div>



<span id=".55u45YWz6ZmQ5Yi2"></span>
## Limits

<span id=".5bim5a696ZmQ5Yi2"></span>
### Bandwidth limits


* For an expired Subscription VPN gateway or a Pay\-as\-you\-go VPN gateway that is suspended due to overdue payments, modifying bandwidth is unsupported.

* After the bandwidth of a Subscription VPN gateway is modified successfully, the new specification takes effect immediately. The expiration time remains unchanged. The amount displayed on the interface during specification modification is the difference between the new specification fee and the fee already paid. For more about the modification fees, see [Changing Annual or Monthly Subscription Resource Specifications](https://docs.byteplus.com/en/docs/byteplus-platform/Billing_Rules_for_Resource_Subscription_Change#.5LiA44CB5Y-Y5pu05YyF5bm05YyF5pyI6LWE5rqQ6KeE5qC8).

* After the bandwidth of a Pay\-as\-you\-go VPN gateway is modified successfully, the new specification takes effect immediately. Billing is calculated based on the new specification's price. When modifying the bandwidth of a VPN gateway within a billing cycle, the fee calculation for that billing cycle is: **Old spec unit price × Old usage duration + New spec unit price × New usage duration**.

* If the current VPN gateway version is outdated, you cannot upgrade the specification of the VPN gateway from 200 Mbps and lower specifications to 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, or 3 Gbps, nor downgrade from 300 Mbps, 400 Mbps, 500 Mbps, 1 Gbps, or 3 Gbps to 200 Mbps and lower. If necessary, please update the VPN gateway to the latest version. For more information, see [Upgrading a VPN gateway](https://docs.byteplus.com/en/docs/vpn/Upgrading-a-VPN-gateway).


<span id=".6L-e5o6l6ZmQ5Yi2"></span>
### Connection limit


* For a VPN gateway, you can enable IPsec\-VPN or SSL\-VPN, or both; but you cannot disable the two at the same time.

* The three scenarios differ in billing items based on whether only IPsec\-VPN is enabled, only SSL\-VPN is enabled, or both IPsec\-VPN and SSL\-VPN are enabled. For more information, see [Billing overview](https://docs.byteplus.com/en/docs/vpn/Billing-overview).

* Disabling IPsec\-VPN on a VPN gateway is not allowed if IPsec\-VPN connections exist under it; similarly, SSL\-VPN cannot be disabled if there are SSL\-VPN connections under the gateway.


<span id=".5YW25LuW6ZmQ5Yi2"></span>
### Other limits


* For a yearly Subscription VPN gateway, if its usage duration is less than one year, no annual discount is offered for new billing items incurred by configuration modifications.

* VPN gateways do not support modifying between metering methods. That is, you cannot change the metering method of a VPN gateway from Subscription to Pay\-as\-you\-go, or vice versa.


<span id=".5pON5L2c5q2l6aqk"></span>
## Procedure

For more information, see [Modifying configuration for VPN gateway](https://docs.byteplus.com/en/docs/vpn/Modifying-VPN-gateway-configurations).
