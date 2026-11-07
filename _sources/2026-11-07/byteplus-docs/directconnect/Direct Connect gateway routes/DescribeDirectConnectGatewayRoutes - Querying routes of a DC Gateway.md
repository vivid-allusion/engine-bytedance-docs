---
title: "DescribeDirectConnectGatewayRoutes - Querying routes of a DC Gateway"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayRoutes"
---

Call the DescribeDirectConnectGatewayRoutes API to query the details of Direct Connect (DC) Gateway routes that meet the specified conditions.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* If the `DirectConnectGatewayRouteIds` request parameter is not specified, the system queries based on the other parameters provided and returns the qualified DC Gateway routes.

* If you do not provide any optional request parameters, the system queries based on the currently logged\-in account and returns all DC Gateway routes under that account.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeDirectConnectGatewayRoutes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|Mq2VPU">必选</span> `Example: DescribeDirectConnectGatewayRoutes`

The interface name. The current API name is `DescribeDirectConnectGatewayRoutes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|AR6eoD">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayRouteIds.N ** <span data-label="purple">String </span>`optional` `Example: dcr-4jhsdn0nekil****`

The ID of the DC Gateway route.


* N represents the sequence number of a DC Gateway route ID. You can call a maximum of 100 IDs per request.

* Separate multiple DC Gateway route IDs with ampersands (&).



**DirectConnectGatewayId ** <span data-label="purple">String </span>`optional` `Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway.

You can call [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) to query the DC Gateway ID.



**DestinationCidrBlock ** <span data-label="purple">String </span>`optional` `Example: 172.XX.XX.0/24`

The destination CIDR block of the DC Gateway route.



**NextHopId ** <span data-label="purple">String </span>`optional` `Example: dcv-13fszmm1xdssg3n6nu4x9****`

The ID of the next hop instance for the DC Gateway route.

You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the instance ID for which the next hop is a DC Virtual Interface.



**NextHopType ** <span data-label="purple">String </span>`optional` `Example: VIF`

The type of the next hop instance for the DC Gateway route. Values:


* VIF: DC Virtual Interface

* CEN: Cloud Enterprise Network

* TransitRouter: Transit Router (TR)



**RouteType ** <span data-label="purple">String </span>`optional` `Example: BGP`

The type of the DC Gateway route. Values:


* BGP: BGP dynamic route

* Static: Static route

* CEN: CEN route. The routes synchronized from a CEN after a DC Gateway are attached to it.



**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The page number of the list.


* Set a non\-negative integer to this parameter.

* If left blank or set to 0, it defaults to 1.



**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TotalCount ** <span data-label="purple">Integer </span>`Example: 10`

The total number of DC Gateway routes that meet the specified conditions.



**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.



**PageSize ** <span data-label="purple">Integer </span>`Example: 20`

Number of entries per page in the current pagination.



**DirectConnectGatewayRoutes ** <span data-label="purple">Object[] </span>`Example: -`

The details of the DC Gateway routes.


**AccountId ** <span data-label="purple">String </span>`Example: 21000*****`

The ID of the account to which the DC Gateway route belongs.



**DirectConnectGatewayId ** <span data-label="purple">String </span>`Example: dcg-7qthudw0ll6jmc****`

The ID of the DC Gateway.



**DirectConnectGatewayRouteId ** <span data-label="purple">String </span>`Example: dcr-4jhsdn0nekil****`

The ID of the DC Gateway route.



**DestinationCidrBlock ** <span data-label="purple">String </span>`Example: 172.XX.XX.0/24`

The destination CIDR block of the DC Gateway route.



**NextHopId ** <span data-label="purple">String </span>`Example: dcv-13fszmm1xdssg3n6nu4x9****`

The ID of the next hop instance for the DC Gateway route.



**NextHopType ** <span data-label="purple">String </span>`Example: VIF`

The type of the next hop instance for the DC Gateway route.


* VIF: DC Virtual Interface

* CEN: Cloud Enterprise Network



**RouteType ** <span data-label="purple">String </span>`Example: BGP`

The type of the DC Gateway route.


* BGP: BGP dynamic route

* Static: Static route

* CEN: CEN route



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
GET /?Action=DescribeDirectConnectGatewayRoutes&Version=2020-04-01&DirectConnectGatewayIds.1=dcg-7qthudw0ll6jmc****&PageNumber=1&PageSize=20 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20211222112033010224****",
        "Action": "DescribeDirectConnectGatewayRoutes",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20211222112033010224****",
        "PageNumber": 1,
        "PageSize": 20,
        "TotalCount": 1,
        "DirectConnectGatewayRoutes": [
            {
                "AccountId": "210000****",
                "DirectConnectGatewayId": "dcg-7qthudw0ll6jmc****",
                "DirectConnectGatewayRouteId": "dcr-4jhsdn0nekil****",
                "DestinationCidrBlock": "172.XX.XX.0/24",
                "NextHopId": "dcv-13fszmm1xdssg3n6nu4x9****",
                "NextHopType": "VIF",
                "RouteType": "BGP",
                "CreationTime": "2021-12-15T17:05:42+08:00",
                "Status": "Available"
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |LimitExceeded.DirectConnectGatewayRouteId |You've reached the limit on the number of direct connect gateway route IDs that you can describe. |You have reached the maximum number of DC Gateway route IDs that can be queried. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
