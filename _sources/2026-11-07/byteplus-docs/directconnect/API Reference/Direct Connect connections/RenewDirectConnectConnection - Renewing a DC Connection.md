---
title: "RenewDirectConnectConnection - Renewing a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/RenewDirectConnectConnection"
---

Call RenewDirectConnectConnection to renew a Direct Connect (DC) Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=RenewDirectConnectConnection&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|VLvnIN">必选</span> `Example: RenewDirectConnectConnection`

The interface name. The current API name is `RenewDirectConnectConnection`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|aE2mvw">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|FVeGk1">必选</span> `Example: dcc-xnkd823nkd****`

The ID of the DC Connection to be renewed.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) API to query the DC Connection ID.



**PeriodUnit ** <span data-label="purple">String </span>`optional` `Example: Month`

The duration unit for the Subscription DC Connection. Values:


* Month (default)

* Year



**Period ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The purchase duration for the Subscription DC Connection. Default: 1.


* When `PeriodUnit` is set to `Month`, the valid range for `Period` is 1 to 11.

* When `PeriodUnit` is set to `Year`, the valid range for `Period` is 1 to 3.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=RenewDirectConnectConnection&Version=2020-04-01&DirectConnectConnectionId=dcc-8njk2nl32bd232b****&Period=1&PeriodUnit=Month' HTTP/1.1
Host: directconnect.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/directconnect/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20220627103212010225145152058*****",
        "Action": "RenewDirectConnectConnection",
        "Version": "2020-04-01",
        "Service": "directconnect",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "20220627103212010225145152058*****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below describes the error codes for this API that are associated with business logic. For details, see [Common error codes](https://docs.byteplus.com/en/docs/directconnect/Public-error-codes).


|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |OrderError |Failed to create an order in one step. |Failed to create and pay for the order. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account balance and available vouchers are less than 100 yuan in total. |The action request on this instance is rejected because the sum of both account balance and available coupons are less than USD 100. |
|400 |UnsupportedOperation |The request on the specified instance is denied due to the account in arrears status. |The action request on this instance is denied because the account is in arrears. |
|400 |InvalidDirectConnectConnection.InvalidStatus |The specified direct connect connection is not in the correct status for the request. |The specified DC Connection cannot respond to this request due to its status. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
|404 |InvalidEip.GetInstanceDetail |Get instance detail failed. |Failed to obtain instance information. |
