---
title: "API release notes"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/API-change-records"
---

This article introduces change information for the VPN connection OpenAPI.

<span id="k60gJRKv"></span>
## July 2026


|API |Release note |Associated features |
|---|---|---|
|CreateVpnGateway |Added new error code: SslEnabled. |VPN Gateway |
|* CreateSslVpnServer<br><br>* ModifySslVpnServer |Added new error code: ClientCertSessionPolicy、SsoAuthEnabled、SamlData. |SSL VPN Server |
|DescribeSslVpnServers |Added request parameters: SsoAuthEnabled. ||
|DescribeSslVpnServerSamlData |New interfaces added. ||


<span id="jrGFf8Xh"></span>
## September 2025


|API |Release note |Associated features |
|---|---|---|
|CreateVpnGatewayRoute<br><br> |Added new error code: InvalidVpnRouteCidr.Conflict. |VPN Gateway Route<br><br> |
|ModifySslVpnServer |Add error code: InvalidParameter.ClientCertSessionPolicy. |<div style="text-align: center"><br>SSL VPN Server</div><br> |
|DescribeSslVpnServers |* Added response parameter: ClientCertSessionPolicy.<br><br>* Added error code: Forbidden.ClientCertSessionPolicyNotGranted. ||
|CreateSslVpnServer |Added new error codes: Forbidden.ClientCertSessionPolicyNotGranted,<br><br>InvalidParameter.ClientCertSessionPolicy。 ||
|CreateVpnGateway |* Added request parameters: DualTunnelEnabled, SecondarySubnetId.<br><br>* Added error codes: InvalidSecondarySubnet.Conflict, InvalidSubnet.ZoneShouldDifferent, InvalidVpnGateway.BGPSupport, InvalidVpnGateway.SslNotSupport, Forbidden.DualTunnelVpnPermissionNotGranted, InvalidSecondarySubnet.NotFound.<br><br>* Removed error code: InvalidVpnGateway.BGPSupport. |VPN Gateway<br><br> |
|DescribeVpnGatewayAttributes |Add response parameters: DualTunnelEnabled, SecondaryIpAddress, SecondarySubnetId. ||
|DescribeVpnGateways |||
|ModifyVpnGatewayAttributes |* Added error codes: InvalidVpnGateway.BGPSupport, InvalidVpnGateway.SslNotSupport.<br><br>* Removed error code: InvalidVpnGateway.BGPSupport. ||
|CreateVpnConnection<br><br> |* Added 20 new request parameters related to dual tunnels, including TunnelOptions.N.CustomerGatewayId.<br><br>* Added new error codes: InvalidTunnelOptionRole.Malformed, InvalidVpnConnection.DualTunnelConfigNotSupported, InvalidVpnConnection.SingleTunnelConfigNotSupported, InvalidVpnTunnelRemoteId.Conflict. ||
|DescribeVpnConnectionAttributes |Added response parameters: EnableTunnelsBgp, TunnelBgpInfo, DualTunnelEnabled, TunnelOptions structure.<br><br> ||
|DescribeVpnConnections |||
|ModifyVpnConnectionAttributes |* Added request parameters: TunnelOptions.N.CustomerGatewayId and 20 other parameters related to dual tunnels.<br><br>* Added error codes: InvalidVpnConnection.DualTunnelConfigNotSupported, InvalidVpnConnection.SingleTunnelConfigNotSupported, InvalidVpnTunnelRemoteId.Conflict, InvalidTunnel.NotFound, InvalidCustomerGateway.InvalidASN, InvalidHealthCheckConfig.IpNotInTrafficSelector, InvalidVpnGateway.InvalidASN, InvalidVpnGatewayRouteType.Malformed.<br><br>* Removed error code: InvalidVpnConnection.MoidfyCustomerGatewayNotSupport. ||
|ModifyVpnConnectionTunnelAttributes |Added the interface to modify parameters unique to Dual\-tunnel IPsec connection. ||
|ResetVpnConnection |* Added new request parameter: TunnelId.<br><br>* Added new error code: InvalidTunnel.NotFound. ||
|DescribeVpnGatewayRouteAttributes |Added response parameter: NextTunnelId. |VPN Gateway Route |
|DescribeVpnGatewayRoutes |||


<span id="l0LqOvZD"></span>
## July 2025


|API |Release note |Associated features |
|---|---|---|
|DescribeVpnConnections<br><br> |Modified request parameter: Spec added value field xlarge, representing 3G specification. |IPsec\-VPN Connection<br><br> |
|CreateVpnConnectionHealthCheckers |Added error codes: InvalidHealthCheckConfig.IpNotInTrafficSelector, QuotaExceeded.TRIPsecHealthCheckers. |Health Check |
|DeleteVpnConnectionHealthChecker |Added new error code: InvalidVpnConnection.NotFound. ||
|ModifyVpnConnectionHealthChecker<br><br> |Added error codes: InvalidHealthCheckConfig.IpNotInTrafficSelector and InvalidVpnConnection.NotFound. ||


<span id="l0LqOvZD"></span>
## May 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|z2nDYo">更新</span>[CreateCustomerGateway](https://docs.byteplus.com/en/docs/vpn/CreateCustomerGateway) |Deleted Error code: Forbidden.VpnBgpPermissionNotGranted. |Customer Gateway<br><br> |
|<span data-api-tag="update\|X2Iaj4">更新</span>[ModifyVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes) ||<div style="text-align: center"><br></div><br><br><br>VPN Gateway |
|<span data-api-tag="update\|y0WSwn">更新</span>[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway) |* Add error code: InvalidVpn.ServiceRoleNotAuthorized.<br><br>* Remove error code: Forbidden.VpnBgpPermissionNotGranted. ||
|<span data-api-tag="update\|sdAvP3">更新</span>[CreateVpnConnection](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnection)<br><br> |* Change request parameters: CustomerGatewayId and IkeConfig.Psk from mandatory to optional.<br><br>* Remove error code: Forbidden.VpnBgpPermissionNotGranted. |IPsec\-VPN Connection |
|<span data-api-tag="update\|oELqgh">更新</span>[CreateVpnGatewayRoute](https://docs.byteplus.com/en/docs/vpn/CreateVpnGatewayRoute) |Added error codes: IncorrectVpnConnectionStatus, QuotaExceeded.SystemRouteEntry. |VPN Gateway Route |


<span id=".MjAyNOW5tDEy5pyI"></span>
## March 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|aX58zF">更新</span>[CreateVpnGatewayRoute](https://docs.byteplus.com/en/docs/vpn/CreateVpnGatewayRoute)<br><br> |Added new error codes: InvalidGatewayRouteTablePrefixList.Malformed and InvalidRouteNextHop.Malformed. |VPN Gateway |


&nbsp;

<span id=".MjAyNOW5tDEy5pyI"></span>
## January 2025


|API |Release note |Associated features |
|---|---|---|
|<span data-api-tag="update\|PkNB8w">更新</span>[CreateCustomerGateway](https://docs.byteplus.com/en/docs/vpn/CreateCustomerGateway) |* Added request parameters: Tags.N.Key, Tags.N.Value.<br><br>* Added error codes: InvalidTag.Disorder, InvalidTagKey.Malformed, InvalidTagValue.Malformed, LimitExceeded.TagOperation. |Customer Gateway |
|<span data-api-tag="update\|jvISWq">更新</span>[DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) |* Added request parameters: TagFilters.N.Key, TagFilters.N.Values.M.<br><br>* Added response parameter: Tags structure.<br><br>* Added new error codes: InvalidTagFilter.Disorder, InvalidTagFilterKey.Malformed, InvalidTagFilterValue.Malformed, LimitExceeded.TagFilterKey, LimitExceeded.TagFilterValue. ||
|<span data-api-tag="update\|BtdTQ6">更新</span>[DescribeCustomerGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGatewayAttributes) |Add response parameter: Tags structure. ||
|<span data-api-tag="update\|wmpScU">更新</span>[CreateVpnConnection](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnection) |* Added request parameters: Tags.N.Key, Tags.N.Value.<br><br>* Added error codes: InvalidTag.Disorder, InvalidTagKey.Malformed, InvalidTagValue.Malformed, LimitExceeded.TagOperation, InvalidCustomerGateWay.SameVpcWithVpnGateway. |IPsec\-VPN Connection |
|<span data-api-tag="update\|tzzOCn">更新</span>[ModifyVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes) |||
|<span data-api-tag="update\|nayQ3N">更新</span>[DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) |* Added request parameters: TagFilters.N.Key, TagFilters.N.Values.M.<br><br>* Added response parameter: Tags structure.<br><br>* Added error codes: InvalidTagFilter.Disorder, InvalidTagFilterKey.Malformed, InvalidTagFilterValue.Malformed, LimitExceeded.TagFilterKey, LimitExceeded.TagFilterValue. ||
|<span data-api-tag="update\|snOdlX">更新</span>[DescribeVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnectionAttributes) |Added response parameter: Tags structure. ||
|<span data-api-tag="update\|yiRQZX">更新</span>[CreateSslVpnServer](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnServer) |* Added request parameters: Tags.N.Key, Tags.N.Value.<br><br>* Added error codes: InvalidTag.Disorder, InvalidTagKey.Malformed, InvalidTagValue.Malformed, LimitExceeded.TagOperation. |SSL VPN Server |
|<span data-api-tag="update\|BLF68s">更新</span>[DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) |* Add request parameters: TagFilters.N.Key, TagFilters.N.Values.M.<br><br>* Add response parameter: Tags structure.<br><br>* Add error codes: InvalidTagFilter.Disorder, InvalidTagFilterKey.Malformed, InvalidTagFilterValue.Malformed, LimitExceeded.TagFilterKey, LimitExceeded.TagFilterValue. ||
|<span data-api-tag="update\|xYrbbr">更新</span>[CreateSslVpnClientCert](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnClientCert) |* Added request parameters: Tags.N.Key, Tags.N.Value.<br><br>* Added error codes: InvalidTag.Disorder, InvalidTagKey.Malformed, InvalidTagValue.Malformed, LimitExceeded.TagOperation. |SSL VPN Client Certificate |
|<span data-api-tag="update\|sE0Vrx">更新</span>[DescribeSslVpnClientCertAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCertAttributes) |Add response parameter: Tags structure. ||
|<span data-api-tag="update\|AnpFuu">更新</span>[DescribeSslVpnClientCerts](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnClientCerts) |* Add request parameters: TagFilters.N.Key, TagFilters.N.Values.M.<br><br>* Add response parameters: Tags structure.<br><br>* Added new error codes: InvalidTagFilter.Disorder, InvalidTagFilterKey.Malformed, InvalidTagFilterValue.Malformed, LimitExceeded.TagFilterKey, LimitExceeded.TagFilterValue. ||


<span id=".MjAyNOW5tDEy5pyI"></span>
## December 2024


|API |Released on |Release note |Associated features |
|---|---|---|---|
|<span data-api-tag="update\|uNJJKU">更新</span>[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway) |December 06, 2024 |Added new error code: InvalidVpnGateway.IPv6OnlySubnet. |VPN Gateway |
|<span data-api-tag="update\|dvNz5U">更新</span>[DeleteVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnectionHealthChecker) ||Added new request parameter: `VpnConnectionId`. |Health Check |
|<span data-api-tag="update\|H5WdwJ">更新</span>[ModifyVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionHealthChecker) ||Add request parameter: `VpnConnectionId`. ||
|<span data-api-tag="update\|FAMG1G">更新</span>[ModifySslVpnServer](https://docs.byteplus.com/en/docs/vpn/ModifySslVpnServer) ||Removed error code: Forbidden. |SSL VPN Server |


<span id=".MjAyNOW5tDA55pyI"></span>
## September 2024


|**API** |**Release Date** |**Change History** |**Associated Features** |
|---|---|---|---|
|[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway) |18 September 2024 |* Added a request parameter: Asn.<br><br>* Added Error codes: InvalidVpnGateway. InvalidASN, Forbidden. VpnBgpPermissionNotGranted, InvalidZoneId. NotFound. |VPN Gateway |
|[ModifyVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes) ||* Added a request parameter: Asn.<br><br>* Added Error codes: InvalidVpnGateway. InvalidASN, InvalidVpnGatewayAsn ASNAlreadyConfigured, Forbidden VpnBgpPermissionNotGranted. ||
|[DescribeVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayAttributes) ||Added a response parameter: Asn. ||
|[DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) ||Added a response parameter: Asn. ||
|[DescribeVpnGatewayRouteAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRouteAttributes) ||* Added Response parametersRouteType and AsPath.<br><br>* Response parameters Status Added value Conflicted. |VPN Gateway Route |
|[DescribeVpnGatewayRoutes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRoutes) ||* Added Request parametersRouteType.<br><br>* Added Response parametersRouteType and AsPath.<br><br>* Response parameters Status Added value Conflicted. ||
|[CreateCustomerGateway](https://docs.byteplus.com/en/docs/vpn/CreateCustomerGateway) ||* Added a request parameter: Asn.<br><br>* Added Error codes: InvalidCustomerGateway. InvalidASN, Forbidden. VpnGatewayBgpPermissionNotGranted. |Customer Gateway |
|[DescribeCustomerGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGatewayAttributes) ||Added a response parameter: Asn. ||
|[DescribeCustomerGateways](https://docs.byteplus.com/en/docs/vpn/DescribeCustomerGateways) ||Added a response parameter: Asn. ||
|[CreateVpnConnection](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnection) ||* Added Request parametersBgpConfig. EnableBgp , BgpConfig. TunnelCidr , BgpConfig. LocalBgpIp.<br><br>* Added Error codes: InvalidVpnConnectionBgpLocalIp. Malformed, InvalidVpnConnectionBgpTunnelCidr. Malformed, InvalidCustomerGateWay. ASNNotConfigured, InvalidVpnConnectionBgpTunnelCidr. Conflict, InvalidVpnGateway. ASNNotConfigured, InvalidVpnGateway.CustomerGateWayASNDuplicated, Forbidden. VpnBgpPermissionNotGranted.<br><br>* Error codes InvalidVpnConnection. RegionNotSupport update error information. |IPsec\-VPN Connection |
|[ModifyVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes) ||* Added Request parameters BgpConfig. EnableBgp , BgpConfig. TunnelCidr , BgpConfig. LocalBgpIp, CustomerGatewayId.<br><br>* Added Error codes: InvalidVpnConnectionBgpLocalIp. Malformed, InvalidVpnConnectionBgpTunnelCidr. Malformed, InvalidCustomerGateWay. ASNNotConfigured, InvalidCustomerGateway. InvalidStatus, InvalidVpnConnection. MoidfyCustomerGatewayNotSupport, InvalidVpnConnectionBgpTunnelCidr. Conflict, InvalidVpnGateway. ASNNotConfigured, InvalidVpnGateway.CustomerGateWayASNDuplicated, InvalidVpnGateway. InvalidStatus, Forbidden. VpnBgpPermissionNotGranted. ||
|[DescribeVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnectionAttributes) ||Added Response parameters BgpInfo structure. ||
|[DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) ||Added Response parameters BgpInfo structure. ||
|All ||Added public Error codes InvalidOperation. Conflict. |All |


<span id=".MjAyNOW5tDA35pyI"></span>
## July 2024


|API |Released on |Release note |Associated features |
|---|---|---|---|
|<span data-api-tag="update\|MpCTGS">更新</span>[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway) |July 19 & 17, 2024 |Added error code Forbidden.SharedVpc. |VPN Gateway |


<span id=".MjAyNOW5tDA15pyI"></span>
## May 2024


|**API** |**Release Date** |**Change History** |**Associated Features** |
|---|---|---|---|
|[CreateVpnConnectionHealthCheckers](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnectionHealthCheckers) |28 May 2024 |Added new API. |Health Check |
|[DeleteVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/DeleteVpnConnectionHealthChecker) ||Added new API. ||
|[ModifyVpnConnectionHealthChecker](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionHealthChecker) ||Added new API. ||
|[CreateVpnGateway](https://docs.byteplus.com/en/docs/vpn/CreateVpnGateway) ||* Added new error code Forbidden.<br><br>* Delete error code InvalidServiceStatus.TemporaryUnavailable. |VPN Gateway |
|[ModifyVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnGatewayAttributes) ||* Delete error codes InvalidVpnGateway. Outdated, InvalidServiceStatus TemporaryUnavailable.<br><br>* Added new error codes Forbidden, InvalidSslMaxConnections ClientIpPoolNotEnough, Forbidden.VpnGatewayBlocked. ||
|[DescribeVpnGatewayAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayAttributes) ||Added new response parameter IsBlocked. ||
|[DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) ||Added new response parameter IsBlocked. ||
|[CreateVpnConnection](https://docs.byteplus.com/en/docs/vpn/CreateVpnConnection) ||Added new error codes InsufficientResource.VpnGateway, InvalidVpnConnection.RegionNotSupport, InvalidVpn.ServiceRoleNotAuthorized, Forbidden.VpnGatewayBlocked. |IPsec\-VPN Connection |
|[ModifyVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/ModifyVpnConnectionAttributes) ||Added new error codes Forbidden.VpnConnectionBlocked, Forbidden.VpnGatewayBlocked. ||
|[DescribeVpnConnectionAttributes](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnectionAttributes) ||Added new response parameters HealthCheckers structure, IsBlocked. ||
|[DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) ||Added new response parameters HealthCheckers structure, IsBlocked. ||
|[ResetVpnConnection](https://docs.byteplus.com/en/docs/vpn/ResetVpnConnection) ||Added new API. ||
|[CreateSslVpnServer](https://docs.byteplus.com/en/docs/vpn/CreateSslVpnServer) ||* Added new request parameter Port.<br><br>* Added new error codes InvalidClientIpPool.NotEnough, InvalidSslVpnServerPort.Malformed, QuotaExceeded.VpcRouteEntry, InvalidSslVpnServerVpcRouteEntry.Conflict, Forbidden.VpnGatewayBlocked.<br><br>* Request parameters Protocol the default value was changed from UDP to TCP.<br><br>* Request parameters LocalSubnets.N supplementary quantity limit.<br><br>* Delete error codes InvalidRouteCidr.Malformed、QuotaExceeded.RouteEntry、InvalidSslVpnServer.VpcRouteEntryConflict. |SSL VPN Server |
|[ModifySslVpnServer](https://docs.byteplus.com/en/docs/vpn/ModifySslVpnServer) ||* Added new request parameters Auth,Cipher,ClientIpPool,Compress,LocalSubnets.N,Port,Protocol.<br><br>* Added new error codes InvalidCidr. Malformed~ QuotaExceeded. VpcRouteEntry, Forbidden, InvalidVpnGateway. NotFound, InvalidRouteCidr. Conflict, InvalidSslVpnServerVpcRouteEntry. Conflict, InvalidVpnGateway. Expired, Forbidden.VpnGatewayBlocked. ||
|[DescribeSslVpnServers](https://docs.byteplus.com/en/docs/vpn/DescribeSslVpnServers) ||Added new Request parameters Port and IsBlocked. ||


<span id=".MjAyNOW5tDA05pyI"></span>
## April 2024


|**API** |**Release Date** |**Changelog** |**Related Feature** |
|---|---|---|---|
|addAll |24 April 2024 |Open APIs for the VPN connection were released for the first time. |VPN connection |
