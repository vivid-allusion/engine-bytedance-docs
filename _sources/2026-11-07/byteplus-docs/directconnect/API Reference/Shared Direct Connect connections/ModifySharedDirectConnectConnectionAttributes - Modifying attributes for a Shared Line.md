---
title: "ModifySharedDirectConnectConnectionAttributes - Modifying attributes for a Shared Line"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/ModifySharedDirectConnectConnectionAttributes"
---

Call ModifySharedDirectConnectConnectionAttributes to modify the port bandwidth of a shared Direct Connect Connection (Shared Line) for a tenant.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=ModifySharedDirectConnectConnectionAttributes&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|1YoHhv">必选</span> `Example: ModifySharedDirectConnectConnectionAttributes`

The interface name. The current API name is `ModifySharedDirectConnectConnectionAttributes`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|obBxhC">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|rCGfat">必选</span> `Example: dcc-e5z1z57glr0g2yjrzamy****`

The ID of the Shared Line.

You can call [DescribeSharedDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeSharedDirectConnectConnections) to query the Shared Line ID.



**ExpectBandwidth** <span data-label="purple">Integer</span> `optional` `Example: 1000`

Expected bandwidth of the Shared Line. Unit: Mbps.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=ModifySharedDirectConnectConnectionAttributes&Version=2020-04-01&DirectConnectConnectionId=dcc-e5z1z57glr0g2yjrzamy****&ExpectBandwidth=1000 HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "202111161611080102121461940900****",
        "Action": "ModifySharedDirectConnectConnectionAttributes",
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
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |InvalidSharedDirectConnectConnection.BandwidthMalformed |The specified bandwidth is malformed. Only support bandwidth of given values: 50, 100, 200, 300, 400, 500, 1000, 2000, 5000, 8000, 10000. |The specified bandwidth value is invalid. Only the following bandwidth values are supported: 50, 100, 200, 300, 400, 500, 1000, 2000, 5000, 8000, and 10000. |
|400 |LimitExceeded.Bandwidth |You've reached the limit on the bandwidth that you can create. |The bandwidth cap has been reached. |
|400 |InvalidDirectConnectConnection.BandwidthMalformed |The specified expect bandwidth is malformed |The specified bandwidth value is invalid. |
|400 |InvalidDirectConnectConnection.InvalidStatus |Operation does not support while the specified direct connect connection's bandwidth in changing progress. |The Direct Connect (DC) specification is being modified. The current action is not supported. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |The maximum bandwidth allocable of the DC Connection has been reached. |
|403 |Forbidden |You are not authorized to create a shared connection on the specified bandwidth. |No permission to create a Shared Line with a specified bandwidth. |
|403 |InvalidDirectConnectConnection.ConnectionType |The specified direct connect connection does not support bandwidth changes. |Dedicated Lines do not support modifying specifications. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
