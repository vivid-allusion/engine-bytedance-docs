---
title: "DescribeDirectConnectGatewayRouteAttributes - Querying a specified DC Gateway route"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayRouteAttributes"
---

Call DescribeDirectConnectGatewayRouteAttributes to query the detailed information of a specified Direct Connect (DC) Gateway route.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectGatewayRouteAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters.](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters)



**Action ** <span data-label="purple">String </span><span data-api-tag="require|MlOgnr">必选</span> `Example: DescribeDirectConnectGatewayRouteAttributes`

The interface name. The current API name is `DescribeDirectConnectGatewayRouteAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|SSz8MI">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayRouteId ** <span data-label="purple">String </span><span data-api-tag="require|y6PnVI">必选</span> `Example: dcr-2752hzaqrwfeo7f****`

The ID of the DC Gateway to be queried.

You can call [DescribeDirectConnectGatewayRoutes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayRoutes) to query the ID of the static route for the DC Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

The ID of the account to which the DC Gateway route belongs.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway.



**DirectConnectGatewayRouteId ** <span data-label="purple">String </span>`Example: dcr-2752hzaqrwfeo7f****`

The ID of the DC Gateway route.



**DestinationCidrBlock ** <span data-label="purple">String </span>`Example: 172.XX.XX.0/24`

The destination CIDR block of the DC Gateway route.



**NextHopId ** <span data-label="purple">String </span>`Example: dcv-13fszmm1xdssg3n6nu4x9****`

The ID of the next hop instance for the DC Gateway route.



**NextHopType ** <span data-label="purple">String </span>`Example: VIF`

The type of the next hop instance for the DC Gateway route. Values:


* VIF: DC Virtual Interface

* CEN: Cloud Enterprise Network

* TransitRouter: Transit Router (TR)



**RouteType ** <span data-label="purple">String </span>`Example: Static`

The type of the DC Gateway route. Values:


* BGP: BGP dynamic route

* Static: Static route

* CEN: CEN route. The routes synchronized from a CEN after a DC Gateway are attached to it.



**CreationTime ** <span data-label="purple">String </span>`Example: 2021-04-09T08:36:47+08:00`

The time when the DC Gateway route is created.



**Status ** <span data-label="purple">String </span>`Example: Available`

The status of the DC Gateway route.


* Creating

* Deleting

* Pending: In the configuring process.

* Available



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribeDirectConnectGatewayRouteAttributes&Version=2020-04-01&DirectConnectGatewayRouteId=dcr-2752hzaqrwfeo7f**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2021111616110801021214619****",
        "Action": "DescribeDirectConnectGatewayRouteAttributes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021111616110801021214619****",
        "AccountId": "210000****",
        "DirectConnectGatewayId": "dcg-7qthudw0ll6jmc****",
        "DirectConnectGatewayRouteId": "dcr-2752hzaqrwfeo7f****",
        "DestinationCidrBlock": "172.XX.XX.0/24",
        "NextHopId": "dcv-13fszmm1xdssg3n6nu4x9****",
        "NextHopType": "VIF",
        "RouteType": "Static",
        "CreationTime": "2021-12-15T17:05:42+08:00",
        "Status": "Available"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For more information, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|404 |InvalidDirectConnectGatewayRoute.NotFound |The specified direct connect gateway route does not exist. |The specified DC Gateway route does not exist. |
