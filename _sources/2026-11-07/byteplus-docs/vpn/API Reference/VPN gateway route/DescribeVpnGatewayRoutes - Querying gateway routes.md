---
title: "DescribeVpnGatewayRoutes - Querying gateway routes"
product: "Virtual Private Network"
product_code: "vpn"
source: "https://docs.byteplus.com/en/docs/vpn/DescribeVpnGatewayRoutes"
---

Call DescribeVpnGatewayRoutes to query destination routes of a VPN gateway based on the specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeVpnGatewayRoutes&serviceCode=vpn&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** `String` <span data-api-tag="require|kubWma">必选</span> Example: `DescribeVpnGatewayRoutes`

The action that you want to perform. Value: DescribeVpnGatewayRoutes.



**Version ** `String` <span data-api-tag="require|Yn9gtT">必选</span> Example: `2020-04-01`

The API version.



**VpnGatewayId ** `String` `optional` Example: `vgw-3tehy13n2l4c6c0v****`

The ID of the VPN gateway instance. You can call [DescribeVpnGateways](https://docs.byteplus.com/en/docs/vpn/DescribeVpnGateways) to query the ID of the VPN gateway.



**VpnGatewayRouteIds.N ** `String` `optional` Example: `vgr-1cwd2lwd4c8cnh****`

ID of the VPN gateway route.


* N represents the sequence number of a route ID.

* Separate multiple IDs with ampersands (&).



**PageSize ** `Integer` `optional` Example: `20`

The number of rows per page for paginated queries. Maximum: 100. Default: 20.



**PageNumber ** `Integer` `optional` Example: `1`

Page number for pagination query.


* If you specify this parameter, it must be a non\-negative integer.

* If you omit it or set it to 0, the value defaults to 1.



**NextHopId ** `String` `optional` Example: `vgc-3tex2x1cwd4c6c0v****`

ID of the IPsec\-VPN connection that will be set as the route's next hop. You can call [DescribeVpnConnections](https://docs.byteplus.com/en/docs/vpn/DescribeVpnConnections) to query the ID of the IPsec\-VPN connection.



**DestinationCidrBlock ** `String` `optional` Example: `192.XX.XX.0/24`

The destination CIDR block of the VPN gateway route.



**RouteType ** `String` `optional` Example: `Static`

The route type.


* Static: Static route

* BGP: BGP route

* Cloud: VPC route


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Route types synchronized from TR are currently unsupported for display.</div>




**Status ** `String` `optional` Example: `Available`

The status of the VPN gateway route.


* Creating

* Deleting

* Pending: ​​Configuration in progress.

* Available: The route is effective and preferred.

* Conflicted: The route is ineffective and non\-preferred.


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">When route prefixes are identical, the route priority order is Cloud route \> Static route \> BGP route. Therefore, multiple routes with the same prefix may have some marked as <code>Available</code> and others as <code>Conflicted</code>.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** `String` `optional` Example: `20220322145233010225243081016A****`

Request ID.



**PageSize ** `Integer` `optional` Example: `20`

The number of rows on the current page.



**PageNumber ** `Integer` `optional` Example: `1`

Current page number.



**TotalCount ** `Integer` `optional` Example: `33`

Total number of qualified route entries.



**VpnGatewayRoutes ** `Object[]` `optional` Example: `-`

Details of the route entry.


**VpnGatewayRouteId ** `String` `optional` Example: `vgr-3tex2c6c0v844c****`

ID of the VPN gateway route.



**VpnGatewayId ** `String` `optional` Example: `vgw-3tehy13n2l4c6c0v****`

The instance ID of the VPN gateway.



**DestinationCidrBlock ** `String` `optional` Example: `192.XX.XX.0/24`

The destination CIDR block of the VPN gateway route.



**NextHopId ** `String` `optional` Example: `vgc-3tex2x1cwd4c6c0v****`

ID of the IPsec\-VPN connection set as the next hop. If `RouteType` is `Cloud`, this parameter returns an empty string.



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
GET /?Action=DescribeVpnGatewayRoutes&Version=2020-04-01&VpnGatewayRouteIds.1=vgr-3tex2c6c0v844c**** HTTP/1.1
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
        "Action": "DescribeVpnGatewayRoutes",
        "Version": "2020-04-01",
        "Service": "vpn",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220322145233010225243081016A****",
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1,
        "VpnGatewayRoutes": [
            {
                "VpnGatewayId":"vgw-3tehy13n2l4c6c0v****",
                "VpnGatewayRouteId": "vgr-3tex2c6c0v844c****",
                "DestinationCidrBlock":"172.XX.XX.0/24",
                "NextHopId":"vgc-3tex2x1cwd4c6c0v****",
                "CreationTime": "2022-03-16T17:05:42+08:00",
                "UpdateTime": "2021-04-09T09:30:40+08:00",
                "RouteType":"BGP",
                                        "AsPath":[
                                          {
                                            "Type":"Sequence",
                                            "Numbers":[
                                                65533
                                             ]
                                           }
                                         ],
                "Status": "Available"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/vpn/Public-error-codes).


|**Status code** |**Error codes** |**Error message** |**Description** |
|---|---|---|---|
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |LimitExceeded.VpnGatewayRouteId |You've reached the limit on the number of VPN gateway route IDs that you can describe. |You have reached the maximum number of route IDs that can be queried for the VPN gateway. |
