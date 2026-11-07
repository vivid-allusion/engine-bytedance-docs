---
title: "API overview"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/VPN-API-overview"
---

This topic describes the VPN Connect\-related APIs and their functions.

<span id=".VlBO572R5YWz"></span>
## VPN gateway


|API name |Feature |
|---|---|
|[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway) |Create a new VPN gateway. |
|[DeleteVpnGateway](https://docs.byteplus.com/en/docs/vpn/DeleteVpnGateway) |Delete a specified VPN gateway. |
|[ModifyVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes) |Modify the name and description of a VPN gateway. |
|[DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) |Filter VPN gateways by conditions. |
|[DescribeVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayAttributes) |Query information of a specified VPN gateway. |
|[RenewVpnGateway](https://docs.byteplus.com/en/docs/vpn/RenewVpnGateway) |Renew a Subscription VPN gateway. |
|[SetVpnGatewayRenewal](https://docs.byteplus.com/en/docs/vpn/SetVpnGatewayRenewal) |Modify renewal method for a VPN gateway. |
|[DescribeVpnGatewaysBilling](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewaysBilling) |Query billing information of a specified VPN gateway. |


<span id=".55So5oi3572R5YWz"></span>
## Customer gateway


|API name |Feature |
|---|---|
|[CreateCustomerGateway](https://docs.byteplus.com/en/docs/vpn/CreateCustomerGateway) |Create a customer gateway. |
|[DeleteCustomerGateway](https://docs.byteplus.com/en/docs/vpn/DeleteCustomerGateway) |Delete a customer gateway. |
|[ModifyCustomerGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyCustomerGatewayAttributes) |Modify the name and description of a customer gateway. |
|[DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) |Query customer gateway details by conditions. |
|[DescribeCustomerGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGatewayAttributes) |Query information of a specified customer gateway. |


<span id=".SVBzZWPov57mjqU="></span>
## IPsec\-VPN connection


|API name |Feature |
|---|---|
|[CreateVpnConnection](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnection) |Create a new IPsec\-VPN connection. |
|[DeleteVpnConnection](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnection) |Delete an IPsec\-VPN connection. |
|[ModifyVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes) |Modify information of an IPsec\-VPN connection. |
|[ModifyVpnConnectionTunnelAttributes](https://docs.byteplus.com/en/docs/6455/1554704) |Modify the specific configuration of a dual\-tunnel IPsec\-VPN connection. To modify parameters shared with a single\-tunnel connection, such as name and description, call [ModifyVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes). |
|[DescribeVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnectionAttributes) |Query a specified IPsec\-VPN connection. |
|[DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) |Query IPsec\-VPN connections that meet specified conditions. |
|[ResetVpnConnection](https://docs.byteplus.com/en/docs/vpn/ResetVpnConnection) |Reset an IPsec\-VPN connection. |


<span id=".5YGl5bq35qOA5p-l"></span>
## Health check


|API name |Feature |
|---|---|
|[CreateVpnConnectionHealthCheckers](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnectionHealthCheckers) |Create health check for an IPsec\-VPN connection. |
|[DeleteVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnectionHealthChecker) |Delete health check for an IPsec\-VPN connection. |
|[ModifyVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionHealthChecker) |Modify the health check information of an IPsec\-VPN connection. |


<span id=".U1NM5pyN5Yqh56uv"></span>
## SSL\-VPN server


|API name |Feature |
|---|---|
|[CreateSslVpnServer](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnServer) |Create an SSL\-VPN server. |
|[ModifySslVpnServer](https://docs.byteplus.com/en/docs/vpn/ModifySslVpnServer) |Modify the basic information of an SSL\-VPN server. |
|[DeleteSslVpnServer](https://docs.byteplus.com/en/docs/vpn/DeleteSslVpnServer) |Delete a specified SSL\-VPN server. |
|[DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) |Query information about SSL\-VPN servers. |
|[DescribeSslVpnServerSamlData](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServerSamlData) |Query identity provider (IdP) metadata. |


<span id=".U1NM5a6i5oi356uv"></span>
## SSL\-VPN client certificate


|API name |Feature |
|---|---|
|[CreateSslVpnClientCert](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnClientCert) |Create an SSL\-VPN client certificate. |
|[ModifySslVpnClientCert](https://docs.byteplus.com/en/docs/vpn/ModifySslVpnClientCert) |Modify basic information of an SSL\-VPN client certificate. |
|[DeleteSslVpnClientCert](https://docs.byteplus.com/en/docs/vpn/DeleteSslVpnClientCert) |Delete a specified SSL\-VPN client certificate. |
|[DescribeSslVpnClientCertAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCertAttributes) |Query the details of a specified SSL\-VPN client certificate. |
|[DescribeSslVpnClientCerts](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCerts) |Query detailed information of SSL\-VPN client certificates meeting the conditions. |


<span id=".VlBO572R5YWz6Lev55Sx"></span>
## VPN gateway route


|API name |Feature |
|---|---|
|[CreateVpnGatewayRoute](https://docs.byteplus.com/en/docs/vpn/CreateVpnGatewayRoute) |Add a destination route to a VPN gateway. |
|[DeleteVpnGatewayRoute](https://docs.byteplus.com/en/docs/vpn/DeleteVpnGatewayRoute) |Delete a destination route of a VPN gateway. |
|[DescribeVpnGatewayRouteAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRouteAttributes) |Query routes of a specified VPN gateway. |
|[DescribeVpnGatewayRoutes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRoutes) |Filter destination routes of a VPN gateway by conditions. |


<span id="X502VyDD"></span>
## Tag


|API name |Feature |
|---|---|
|[TagResources](https://docs.byteplus.com/en/docs/vpn/TagResources) |Add a custom tag to a resource. |
|[UntagResources](https://docs.byteplus.com/en/docs/vpn/UntagResources) |Remove a custom tag from a resource. |
|[ListTagsForResources](https://docs.byteplus.com/en/docs/vpn/ListTagsForResources) |Query tags meeting the specified conditions. |
