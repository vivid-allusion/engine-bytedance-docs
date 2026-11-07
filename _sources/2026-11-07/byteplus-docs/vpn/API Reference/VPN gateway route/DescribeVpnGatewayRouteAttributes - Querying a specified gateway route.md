---
title: "DescribeVpnGatewayRouteAttributes - Querying a specified gateway route"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRouteAttributes"
---

Call DescribeVpnGatewayRouteAttributes to query the information of a specified VPN gateway route.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnGatewayRouteAttributes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|R7Opbq">必选</span> Example: `DescribeVpnGatewayRouteAttributes`

The action that you want to perform. Value: DescribeVpnGatewayRouteAttributes.



**Version ** `String` <span data-api-tag="require|Fpr5B7">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayRouteId ** `String` <span data-api-tag="require|GxnR8i">必选</span> Example: `vgr-3tex2c6c0v844c****`

ID of the VPN gateway route. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRoutes) to query the ID of the VPN gateway route.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `20220322145233010225243081016A****`

Request ID.



**VpnGatewayRouteId ** `String` `optional` Example: `vgr-3tex2c6c0v844c****`

ID of the VPN gateway route.



**VpnGatewayId ** `String` `optional` Example: `vgw-3tehy13n2l4c6c0v****`

The instance ID of the VPN gateway.



**DestinationCidrBlock ** `String` `optional` Example: `192.XX.XX.0/24`

The destination CIDR block of the VPN gateway route.



**NextHopId ** `String` `optional` Example: `vgc-3tex2x1cwd4c6c0v****`

The ID of the IPsec\-VPN connection associated with the VPN gateway. If `RouteType` is `Cloud`, this parameter returns an empty string.



**CreationTime ** `String` `optional` Example: `2021-04-09T08:36:47+08:00`

The time when the VPN gateway route is created.



**UpdateTime ** `String` `optional` Example: `2021-04-09T09:30:40+08:00`

The time when the route of the VPN gateway is modified.



**Status ** `String` `optional` Example: `Available`

The status of the VPN gateway route.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available: The route is effective and preferred.

* Conflicted: The route is ineffective and non\-preferred.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When route prefixes are identical, the route priority order is Cloud route \> Static route \> BGP route. Therefore, multiple routes with the same prefix may have some marked as <code>Available</code> and others as <code>Conflicted</code>.</div>




**RouteType ** `String` `optional` Example: `Static`

The route type.


* Static: Static route

* BGP: BGP route

* Cloud: VPC route


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Route types synchronized from TR are currently unsupported for display.</div>




**NextTunnelId ** `String` `optional` Example: `tun-bp18h6dgapdbs1l7p****`

ID of the tunnel that will be set as the next hop.

This parameter is returned only for VPN gateways in dual\-tunnel mode.



**AsPath ** `Object[]` `optional` Example: `-`

The AS path traversed by the BGP route.


**Type ** `String` `optional` Example: `Sequence`

The type for AS path.


* Sequence: Original sequence

* Set: Aggregated sequence



**Numbers ** `Integer[]` `optional` Example: `[65533]`

The sequence for AS path.


* If the type of AS path is Sequence, the response will be the original ASN sequence, such as [65533].

* If the type of AS path is Set, indicating that the AS path is aggregated, the response will be the aggregated ASN sequence, such as [4,5].




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?Action=DescribeVpnGatewayRouteAttributes&Version=2020-04-01&VpnGatewayRouteId=vgr-3tex2c6c0v844c**** HTTP/1.1
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
        "Action": "DescribeVpnGatewayRouteAttributes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220322145233010225243081016A****",
        "VpnGatewayId": "vgw-3tehy13n2l4c6c0v****",
        "VpnGatewayRouteId": "vgr-3tex2c6c0v844c****",
        "DestinationCidrBlock": "172.XX.XX.0/24",
        "NextHopId": "vgc-3tex2x1cwd4c6c0v****",
        "CreationTime": "2022-03-16T17:05:42+08:00",
        "UpdateTime": "2021-04-09T09:30:40+08:00",
        "RouteType": "BGP",
        "AsPath": [
            {
                "Type": "Sequence",
                "Numbers": [
                    65533
                ]
            }
        ],
        "Status": "Available"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|404 |InvalidVpnGatewayRoute.NotFound |The specified VPN gateway route does not exist. |The specified VPN gateway route does not exist. |
