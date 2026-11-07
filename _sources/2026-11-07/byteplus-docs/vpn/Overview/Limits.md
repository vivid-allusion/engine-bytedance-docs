---
title: "Limits"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/Limits"
---

<span id=".6YWN6aKd6ZmQ5Yi2"></span>
## Quota limits

The following table introduces the default quotas for resources related to VPN Connect. If you need additional quota beyond the default allocation, you can go to Quota Center to increase the corresponding quota. For procedure, see [Quota management](https://docs.byteplus.com/en/docs/vpn/Quota-management).

<span id=".VlBO572R5YWz"></span>
### VPN gateway


|Quota parameter |Description |Default quota |Increaseable |Maximum quota |
|---|---|---|---|---|
|VPNGateway |The maximum number of VPN gateways per account per region<br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">The maximum number of VPN gateways is not dependent on​ the number of VPC instances.</div><br><br><br><br>* <div data-tips="true" data-tips-type="default">If you create a VPN gateway for one VPC instance, you can create up to 5 VPN gateways for this VPC.</div><br><br><br>* <div data-tips="true" data-tips-type="default">If you create a VPN gateway for multiple VPC instances, you can create up to 5 VPN gateways for all VPCs in the same region.</div><br> |5 |Yes |15 |
|VPNGateway/RouteEachVPNGateway |The maximum number of routes per VPN gateway (including static routes and auto publish routes) |200 |Yes |500 |
|VPNGateway/HealthChecksEachVPNGateway |The maximum number of health checks per VPN gateway<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">That is, the total number of health check entries that you can add to all IPsec\-VPN connections under the same VPN gateway.</div><br> |10 |Yes |25 |


<span id="IPsec VPN"></span>
### IPsec VPN


|Quota parameter |Description |Default quota |Increasable |Maximum quota |
|---|---|---|---|---|
|VPNGateway/VpnConEachVPNGateway |The maximum number of IPsec\-VPN connections per VPN gateway |10 |Yes |50 |
|\- |The maximum number of IPsec\-VPN connections that can be **associated with a TR later​**  per account |50 |Yes |\- |
|\- |The maximum number of IPsec\-VPN connections that you can create by using the same VPN gateway and the same Remote ID |1 |No |\- |
|* VPNGateway/Ipsec/LocCIDREachVpnConIkeV1<br><br>* VPNGateway/Ipsec/LocCIDREachVpnConIkeV2 |The maximum number of local subnets per IPsec\-VPN connection |5 |Yes<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of increasing this quota is in the beta stage. To request a trial, please contact your account manager.</div><br> |\- |
|* VPNGateway/Ipsec/RemCIDREachVpnConIkeV1<br><br>* VPNGateway/Ipsec/RemCIDREachVpnConIkeV2 |The maximum number of remote subnets per IPsec\-VPN connection |5 |Yes<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The feature of increasing this quota is in the beta stage. To request a trial, please contact your account manager.</div><br> |\- |
|\- |The maximum number of dynamic routes that a single IPsec\-VPN connection with an associated VPN gateway can learn from the peer |100 |Yes |\- |


<span id="SSL VPN"></span>
### SSL VPN

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">The SSL\-VPN feature is not supported for VPN gateways with 3 Gbps bandwidth or dual\-tunnel VPN gateways.</div>



|Quota parameter |Limit item |Default quota |Increasable |Maximum quota |
|---|---|---|---|---|
|\- |The maximum number of SSL\-VPN servers per VPN gateway |1 |No |\- |
|SslVpnServer/SslVpnClientCertEachSslVpnServer |The maximum number of SSL client certificates per SSL\-VPN server<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum number of SSL client certificates is not limited by the client IP pool. That is, separate certificates can initiate connections using the same client IP at different time periods. If IP addresses in the client IP pool are used up by connections from different SSL client certificates, new connection requests will be rejected.</div><br> |10 |Yes |50 |
|\- |The maximum number of local subnets per SSL VPN gateway |5 |Yes |50 |


<span id=".5Yqf6IO957qm5p2f"></span>
## Feature limits


|Limit item |Description |
|---|---|
|VPN Connect transitivity |Currently, VPN Connect does not support transitive routing.<br><br>For example, if a VPC connected to an on\-premises data center via VPN is attached to a Cloud Enterprise Network (CEN) instance, other network instances on that CEN cannot reach the peer CIDR block in the data center through that VPN Connect. |


<span id=".VlBO572R5YWz5bim5a696ZmQ5Yi2"></span>
## VPN gateway bandwidth limits

VPN gateway bandwidth limits are categorized as outbound bandwidth (from a local VPC to a peer VPC or on\-premises data center) and inbound bandwidth (from a peer VPC or on\-premises data center to a local VPC). The specific bandwidth limits are as follows:

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">When using VPN Connect, the VPN gateway charges only the outbound bandwidth fee. The inbound bandwidth is free.</div>


* <div data-tips="true" data-tips-type="tip">The bandwidth limit applies to encapsulated encrypted packets. To configure alarm strategies in Cloud Monitor to monitor VPN gateway metrics, select monitoring metrics including packet encapsulation overhead for trigger conditions, such as VPN gateway outbound/inbound bandwidth utilization.</div>


* **Outbound bandwidth limits**

   The VPN gateway outbound bandwidth cap is consistent with the bandwidth of the VPN gateway you purchased. This value is the bandwidth shared for all IPsec\-VPN and SSL\-VPN connections created on this VPN gateway. That is, the total bandwidth of all IPsec\-VPN and SSL\-VPN connections cannot exceed the bandwidth of the VPN gateway.

* **Inbound bandwidth limits**

   The inbound bandwidth of the VPN gateway depends on the bandwidth you purchased for the VPN gateway.

   * If the bandwidth you purchased for the VPN gateway is ≤ 10 Mbps, the platform allocates 10 Mbps of inbound bandwidth for you by default. That is, the inbound bandwidth cap is 10 Mbps.

   * If the bandwidth you purchased for the VPN gateway is \> 10 Mbps, the inbound bandwidth cap equals the bandwidth of the VPN gateway.


<span id=".VlBO572R5YWz6Lev55Sx6ZmQ5Yi2"></span>
## VPN gateway route limits


* Equal\-cost multi\-path routing (ECMP) is not supported across multiple VPN gateways.

* Multiple VPN gateways within the same Virtual Private Cloud (VPC) cannot be interconnected via IPsec\-VPN connection.

* You cannot add a static route whose destination CIDR block is the same as that of an existing route in a VPN gateway.

* VPN gateways in different BGP routing modes may contain routes to the same destination CIDR block. When these routes are propagated to the same VPC, the VPC prioritizes the propagated routes according to their order of arrival.


<span id=".6Leo5aKD6L-e5o6l6ZmQ5Yi2"></span>
## Cross\-border connection limits

**VPN Connect only provides services within the scope of compliance with Chinese laws and regulations. Only supports establishing non\-cross\-border connections via VPN Connect. Cross\-border connections are not supported.** 

For more information, see [Regions](https://docs.byteplus.com/en/docs/vpn/Regions).


|VPN Connect type |Cross\-border connection scenario |Non\-cross\-border connection scenario |
|---|---|---|
|IPsec\-VPN connection |In the process of establishing IPsec\-VPN, it is considered a cross\-border connection if the regions of the on\-premises data center or peer VPC and the IPsec\-VPN connection meet any of the following conditions.<br><br><br>* The on\-premises data center or peer VPC resides in the China Mainland, while the IPsec\-VPN connection resides in a region outside the China Mainland.<br><br>* The on\-premises data center or peer VPC resides in a region outside the China Mainland, while the IPsec\-VPN connection resides in the China Mainland. |In the process of establishing IPsec\-VPN, it is considered a non\-cross\-border connection if the regions of the on\-premises data center or peer VPC and the IPsec\-VPN connection meet any of the following conditions.<br><br><br>* The on\-premises data center or peer VPC resides in the China Mainland, and the IPsec\-VPN connection is in the China Mainland.<br><br>* The on\-premises data center or peer VPC resides in a region outside the China Mainland, and the IPsec\-VPN connection is in a region outside the China Mainland. |
|SSL\-VPN connection |In the process of establishing SSL\-VPN, it is considered a cross\-border connection if the regions of the client and the SSL\-VPN server meet any of the following conditions.<br><br><br>* The SSL\-VPN client resides in the China Mainland, while the SSL\-VPN server resides in a region outside the China Mainland.<br><br>* The SSL\-VPN client resides in a region outside the China Mainland, while the SSL\-VPN server resides in the China Mainland. |In the process of establishing SSL\-VPN, it is considered a non\-cross\-border connection if the regions of the SSL\-VPN client and the SSL\-VPN server meet any of the following conditions.<br><br><br>* The SSL\-VPN client resides in the China Mainland, and the SSL\-VPN server is in the China Mainland.<br><br>* The SSL\-VPN client resides in a region outside the China Mainland, and the SSL\-VPN server is in a region outside the China Mainland. |


<span id=".572R5YWzVENQIE1TU-mZkOWItg=="></span>
## Gateway TCP MSS limits

Maximum Segment Size (MSS) is the maximum length of a packet segment. MSS is used to negotiate the maximum data length each TCP segment can carry during TCP connection establishment.

To encapsulate and transfer packets efficiently, we recommend setting TCP MSS to **1360** bytes on the on\-premises VPN gateway.
