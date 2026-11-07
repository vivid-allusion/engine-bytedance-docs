---
title: "DeleteDirectConnectGatewayRoute - Deleting a DC Gateway route"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/DeleteDirectConnectGatewayRoute"
---

Call DeleteDirectConnectGatewayRoute to delete a specified static route of a Direct Connect (DC) Gateway.

<span id=".5L2_55So6K-05piO"></span>
## Instructions

Entries of "System route" and "BGP routes" cannot be deleted.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DeleteDirectConnectGatewayRoute&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|7AqBnv">必选</span> `Example: DeleteDirectConnectGatewayRoute`

The interface name. The current API name is `DeleteDirectConnectGatewayRoute`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|XwPd2Z">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectGatewayRouteId ** <span data-label="purple">String </span><span data-api-tag="require|sGfsDw">必选</span> `Example: dcr-2752hzaqrwfeo7f****`

The ID of the static route to be deleted.

You can call [DescribeDirectConnectGatewayRoutes](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectGatewayRoutes) to query the ID of the static route for the DC Gateway.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DeleteDirectConnectGatewayRoute&Version=2020-04-01&DirectConnectGatewayRouteId=dcr-7qthudw0ll6jmc**** HTTP/1.1
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
        "Action": "DeleteDirectConnectGatewayRoute",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "202111161611080102121461940900****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDirectConnectGateway.InvalidStatus |The specified direct connect gateway is not in the correct status for the request. |The specified DC Gateway cannot respond to this request due to its status. |
|400 |InvalidDirectConnectGatewayRoute.InUse |The specified direct connect gateway route can not be deleted while in use. |The specified static route is being processed and cannot be deleted. |
|400 |InvalidCen.InvalidStatus |The CEN attached by the specified direct connect gateway is not in the correct status for the request. |The CEN instance to which the specified DC Gateway attached cannot respond to this request due to the CEN's status. Retry later. |
|403 |Forbidden |You are not authorized to perform operations on the specified route entry. The specified route entry is a system route entry. |No sufficient permissions to perform this operation on the specified route entry. The specified route entry is a system route entry. |
|404 |InvalidDirectConnectGatewayRoute.NotFound |The specified direct connect gateway route does not exist. |The specified DC Gateway route does not exist. |
|404 |InvalidDirectConnectGateway.NotFound |The specified direct connect gateway does not exist. |The specified DC Gateway does not exist. |
