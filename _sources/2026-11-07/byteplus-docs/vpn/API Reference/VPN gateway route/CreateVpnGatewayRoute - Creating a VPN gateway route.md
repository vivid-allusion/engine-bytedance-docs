---
title: "CreateVpnGatewayRoute - Creating a VPN gateway route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/CreateVpnGatewayRoute"
---

Call CreateVpnGatewayRoute to add a destination route for a VPN gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

You cannot add routes that conflict with existing routes in the route table of the Virtual Private Cloud (VPC) to which the VPN gateway belongs. For more about VPN gateway routes, see [Route overview](https://docs.byteplus.com/en/docs/vpn/Overview).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateVpnGatewayRoute&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|XWpK9T">必选</span> Example: `CreateVpnGatewayRoute`

The action that you want to perform. Value: CreateVpnGatewayRoute.



**Version ** `String` <span data-api-tag="require|TnylKt">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayId ** `String` <span data-api-tag="require|Nbyo13">必选</span> Example: `vgw-3tehy13n2l4c6c0v****`

The ID of the VPN gateway to which you want to add the route.



**DestinationCidrBlock ** `String` <span data-api-tag="require|FxJ_HT">必选</span> Example: `192.XX.XX.0/24`

The destination CIDR block of the VPN gateway route.



**NextHopId ** `String` <span data-api-tag="require|BxprHM">必选</span> Example: `vgc-3tex2x1cwd4c6c0v****`

ID of the IPsec\-VPN connection that will be set as the route's next hop. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `20220322145233010225243081016A****`

Request ID.



**VpnGatewayRouteId ** `String` `optional` Example: `vgr-3tex2c6c0v844c****`

ID of the new VPN gateway route.



<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=CreateVpnGatewayRoute&Version=2020-04-01&VpnGatewayId=vgw-12bfa2du7fojk17q7y1rk****&DestinationCidrBlock=172.XX.XX.0/24&NextHopId=vgc-7qthudw0ll6jmc**** HTTP/1.1
Host: vpn.cn-beijing.byteplusapi.com.cn
X-Date: 20251029T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251029/cn-beijing/vpn/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20220322145233010225243081016A****",
        "Action": "CreateVpnGatewayRoute",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220322145233010225243081016A****",
        "VpnGatewayRouteId": "vgr-3tex2c6c0v844c****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format specified for the CIDR block is invalid. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |InvalidVpnGateway.InvalidStatus |The specified VPN gateway is not in the correct status for the request. |The specified VPN gateway cannot respond to this request due to its status. |
|400 |QuotaExceeded.RouteEachVPNGateway |You've reached the limit on the number of route entries per VPN gateway that you can create. |You have reached the maximum of routes that you can create per VPN gateway. |
|400 |QuotaExceeded.RouteEntry |Route entry of a route table number exceeded quota. |You have reached the maximum number of routes that can be created. |
|400 |InvalidVpnGatewayRoute.SslVpnClientIpPoolConflict |The specified vpn gateway route conflicts with that of existing SSL server client ip pool. |The specified VPN gateway route conflicts with the remote CIDR of the existing SSL VPN server. |
|400 |InvalidGatewayRouteTablePrefixList.Malformed |The specified gateway route table does not support prefix list. |The specified gateway route table does not support Prefix List. |
|400 |InvalidRouteNextHop.Malformed |The specified next hop is malformed. |The specified next hop is invalid. |
|400 |IncorrectVpnConnectionStatus |The operation is not supported by the current vpn connection. |This action is unsupported. Retry later. |
|400 |QuotaExceeded.SystemRouteEntry |You've reached the limit on the number of system route entries per route table. |The maximum number of system routes that you can create has been reached. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|404 |InvalidVpnGatewayRoute.InvalidNextHop |The specified connection does not belong to the specified VPN gateway. |The specified next hop does not belong to the specified VPN gateway. |
|404 |InvalidVpnConnection.NotFound |The specified IPSec connection does not exist. |The specified IPsec\-VPN connection does not exist. |
|404 |InvalidVpnGateway.NotFound |The specified VPN gateway does not exist. |The specified VPN gateway does not exist. |
|404 |InvalidRouteTable.NotFound |The specified route table does not exist. |The specified route table does not exist. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in your route table. |The specified CIDR block conflicts with another rule's CIDR block in the associated route table. |
|409 |InvalidRouteCidr.Conflict |The specified CIDR block conflicts with that of another subnet in your VPC. |The specified CIDR block conflicts with the CIDR block of another subnet in the associated VPC. |
|409 |InvalidVpnRouteCidr.Conflict |The specified CIDR block conflicts with that of another route in vpc of VPN gateway. |The specified CIDR block conflicts with the CIDR block for the VPN gateway VPC’s route. |
|412 |InvalidVpnGateway.Expired |The specified VPN gateway has expired. |The specified VPN gateway is expired. |
