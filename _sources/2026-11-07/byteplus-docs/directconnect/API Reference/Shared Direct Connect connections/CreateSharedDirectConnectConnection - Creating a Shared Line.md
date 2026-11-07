---
title: "CreateSharedDirectConnectConnection - Creating a Shared Line"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/CreateSharedDirectConnectConnection"
---

Call CreateSharedDirectConnectConnection to create a new shared Direct Connect Connection (Shared Line).

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=CreateSharedDirectConnectConnection&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|SJFusL">必选</span> `Example: CreateSharedDirectConnectConnection`

The interface name. The current API name is `CreateSharedDirectConnectConnection`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|iiN27l">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|oH6KeZ">必选</span> `Example: dcc-3tehy13n2l4c6c0v****`

The ID of the Direct Connect (DC) Connection on which the Shared Line is created. You can call [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) to query the DC Connection ID.



**UserAccountId ** <span data-label="purple">String </span><span data-api-tag="require|3MWG41">必选</span> `Example: 20******1011`

Root account ID of the account that accepts the Shared Line. You can access the BytePlus console and view account information under "Account management".



**VlanId ** <span data-label="purple">Integer </span><span data-api-tag="require|PKprnu">必选</span> `Example: 1123`

VLAN ID for the Shared Line. Valid range: 1–2999. VLAN IDs for multiple Shared Lines under the same DC Connection must be unique.



**Bandwidth** <span data-label="purple">Integer</span> <span data-api-tag="require|3dJHi3">必选</span> `Example: 50`

The bandwidth for the Shared Line. Unit: Mbps. Values: 50, 100, 200, 300, 400, 500, and 1000.



**SharedDirectConnectConnectionName ** <span data-label="purple">String </span>`optional` `Example: test-name`

Name of the Shared Line.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), underscores (_), and hyphens (\-).

* Must be 1 to 128 characters.

* If you do not provide this parameter or leave it empty, it defaults to the ID of the Shared Line.



**Description ** <span data-label="purple">String </span>`optional` `Example: test-desc`

The description of the Shared Line.


* Must start with a Chinese character, letter, or number. May include Chinese characters, letters, numbers, periods (.), spaces ( ), underscores (_), hyphens (\-), equals signs (=), commas (,), Chinese commas (，), and Chinese periods (。).

* Must be 0 to 255 characters.

* If you do not provide this parameter or leave it unset, it defaults to an empty string.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

The following only details response parameters specific to this API. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**SharedDirectConnectConnectionId ** <span data-label="purple">String </span>`Example: dcc-e5z1z57glr0g2yjrzamy****`

The ID of the newly created Shared Line.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=CreateSharedDirectConnectConnection&Version=2020-04-01&DirectConnectConnectionId=dcc-3tehy13n2l4c6c0v****&UserAccountId=20******1011&VlanId=1123&Bandwidth=50&SharedDirectConnectConnectionName=test-name&Description=test-desc HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20220419155310010225243081****",
        "Action": "DeleteDirectConnectConnection",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220419155310010225243081****",
        "SharedDirectConnectConnectionId": "dcc-e5z1z57glr0g2yjrzamy****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |InvalidDescription.Malformed |The specified description is malformed. |The format of specified description is invalid. Correct the description format and retry. |
|400 |InvalidDescription.Malformed |The specified description is malformed. Ensure the maximum length of description is 255. |The format of specified description is invalid. A description must not exceed 255 characters. |
|400 |InvalidName.Malformed |The specified name is malformed. Ensure the maximum length of name is 128. |The format of specified name is invalid. A name must not exceed 128 characters in length. |
|400 |InvalidName.Malformed |The specified name is malformed. |The format of the specified name is invalid. Correct the name format and retry. |
|400 |QuotaExceeded.SharedConnectionPerConnection |You've reached the limit on the number of shared connections per direct connect connection that you can create. |You have reached the maximum number of Shared Lines that can be created per DC Connection. |
|400 |InvalidSharedDirectConnectConnection.UserAccountIdMalformed |The specified user account ID is malformed. |The format of the specified user account ID is invalid. |
|400 |InvalidSharedDirectConnectConnection.ConnectionMismatch |The specified connection is a shared connection. It is not supported to create a new shared connection based on it. |The specified DC Connection is a Shared Line, which does not support creating a new Shared Line based on it. |
|400 |InvalidSharedDirectConnectConnection.VlanIdMalformed |The specified Vlan ID is malformed. It must be in 1 \- 2999. |The specified VLAN ID is invalid. It must be between 1 and 2999. |
|400 |InvalidSharedDirectConnectConnection.ConnectionIsExclusive |The specified connection is exclusive. You can not create another shared connection on it. |The specified connection is exclusively occupied via VLAN 0 and cannot be used to create a new Shared Line. |
|400 |InvalidSharedDirectConnectConnection.BandwidthMalformed |The specified bandwidth is malformed. Only support bandwidth of given values: 50, 100, 200, 300, 400, 500, 1000, 2000, 5000, 8000, 10000. |The specified bandwidth value is invalid. Only the following bandwidth values are supported: 50, 100, 200, 300, 400, 500, 1000, 2000, 5000, 8000, and 10000. |
|400 |InvalidSharedDirectConnectConnection.BandwidthExceeded |The specified bandwidth exceeds the remaining available bandwidth of physical connection. |The specified Shared Line bandwidth exceeds the remaining available bandwidth of the DC Connection. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|400 |LimitExceeded.PhysicalLineBandwidth |You’ve reached the bandwidth limit on the number of physical line. |You have reached the maximum bandwidth allocable to the DC Connection. |
|403 |Forbidden |You are not authorized to perform operations on the specified shared connection. |No permission to perform actions on the specified Shared Line. |
|403 |Forbidden |You are not authorized to create a shared connection on the specified bandwidth. |No permission to create a Shared Line with a specified bandwidth. |
|404 |InvalidSharedDirectConnectConnection.ConnectionNotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|404 |InvalidProject.NotFound |The specified Project does not exist. |The specified project does not exist. |
|409 |InvalidSharedDirectConnectConnection.VlanIdConflict |The specified Vlan ID already exists. |The specified VLAN ID already exists. |
|409 |InvalidSharedDirectConnectConnection.UserAccountIdConflict |The specified user account ID is equal to current user. |The specified user account ID is the same as the current account ID. |
