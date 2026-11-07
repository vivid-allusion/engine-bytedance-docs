---
title: "CreateDirectConnectGatewayRoute - Creating a DC Gateway route"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateDirectConnectGatewayRoute"
---

Call CreateDirectConnectGatewayRoute to add a static route to a Direct Connect (DC) Gateway.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateDirectConnectGatewayRoute&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|pjhw0f">必选</span> `Example: CreateDirectConnectGatewayRoute`

The interface name. The current API name is `CreateDirectConnectGatewayRoute`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|Oiwph2">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayId ** <span data-label="purple">String </span><span data-api-tag="require|o8vxkE">必选</span> `Example: dcg-2fe3zsmkshs59g****`

The ID of the DC Gateway.

You can call [DescribeDirectConnectGateways](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGateways) to query the DC Gateway ID.



**DestinationCidrBlock ** <span data-label="purple">String </span><span data-api-tag="require|pAYlwk">必选</span> `Example: 172.XX.XX.0/24`

The destination CIDR block of the DC Gateway route.



**NextHopId ** <span data-label="purple">String </span><span data-api-tag="require|kFj1Rz">必选</span> `Example: dcv-7qthudw0ll6jmc****`

The ID of the DC Virtual Interface which is the next hop for the DC Gateway route.

You can call [DescribeDirectConnectVirtualInterfaces](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectVirtualInterfaces) to query the ID of the DC Virtual Interface.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**DirectConnectGatewayRouteId** <span data-label="purple">String</span> `Example: dcr-7qthudw0ll6jmc****`

The ID of the newly added static route.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateDirectConnectGatewayRoute&Version=2020-04-01&DirectConnectGatewayId=dcg-2fe3zsmkshs59g****&DestinationCidrBlock=172.XX.XX.0/24&NextHopId=dcv-7qthudw0ll6jmc**** HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "CreateDirectConnectGatewayRoute",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****",
        "DirectConnectGatewayRouteId": "dcr-2752hzaqrwfeo7f****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |QuotaExceeded.DirectConnectGatewayRoute |You've reached the limit on the number of routes per direct connect gateways that you can create. |You have reached the maximum number of routes that can be created per DC Gateway. |
|400 |InvalidDirectConnectGatewayRoute.InvalidVirtualInterfaceRouteType |The specified next hop does not support. |The specified next hop route type is not supported for creating this DC Gateway route. |
|400 |InvalidRouteCidr.Malformed |The specified CIDR is malformed. |The specified CIDR block is invalid. |
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectConnection.InvalidBusinessStatus |The specified direct connect connection is not in the correct status for the request. The specified direct connect connection is in freeze. |The specified DC Connection cannot respond to this request due to its status. The current DC Connection is frozen. |
|400 |InvalidDirectConnectGateway.InvalidBusinessStatus |The specified direct connect gateway is not in the correct status for the request. The specified direct connect gateway is in freeze. |The specified DC Gateway cannot respond to this request due to its status. The current DC Gateway is frozen. |
|400 |InvalidCen.InvalidStatus |The CEN attached by the specified direct connect gateway is not in the correct status for the request. |The CEN instance to which the specified DC Gateway attached cannot respond to this request due to the CEN's status. Retry later. |
|400 |InvalidCidr.Malformed |The specified cidr block is malformed. |The format of the specified CIDR block is invalid. |
|400 |InvalidDirectConnectGatewayRoute.IpVersionMismatch |The specified direct connect virtual interface has no IPv6 address. |No IPv6 address exists on the specified DC Virtual Interface. |
|400 |InvalidDirectConnectVirtualInterface.InvalidStatus |The specified direct connect virtual interface is not in the correct status for the request. |The specified DC Virtual Interface cannot respond to this request due to its status. |
|403 |Forbidden.IPv6 |You are not authorized to operate IPv6 functions. |No permission to operate IPv6. |
|403 |InvalidOperation.NotSupport |The operation is not supported. |This action is not supported. |
|404 |InvalidDirectConnectGateway.NotFound |The specified direct connect gateway does not exist. |The specified DC Gateway does not exist. |
|404 |InvalidDirectConnectVirtualInterface.NotFound |The specified direct connect virtual interface does not exist. |The specified DC Virtual Interface does not exist. |
|404 |InvalidDirectConnectGatewayRoute.InvalidNextHop |The specified virtual interface does not belong to the specified direct connect gateway. |The specified next hop does not belong to the specified DC Gateway. |
|409 |InvalidRouteCidr.Conflict |There is conflict between the specified route and existed routes. |The specified route conflicts with an existing route. |
