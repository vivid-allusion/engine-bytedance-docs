---
title: "SetDirectConnectConnectionRenewal - Modifying renewal method for a DC Connection"
product: "Direct Connect"
product_code: "directconnect"
source: "https://docs.byteplus.com/en/docs/directconnect/SetDirectConnectConnectionRenewal"
---

Call SetDirectConnectConnectionRenewal to modify the renewal method for the Direct Connect (DC) Connection.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=SetDirectConnectConnectionRenewal&serviceCode=directconnect&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|mLTudT">必选</span> `Example: SetDirectConnectConnectionRenewal`

The interface name. The current API name is `SetDirectConnectConnectionRenewal`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|BG8ews">必选</span> `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.



**DirectConnectConnectionId ** <span data-label="purple">String </span><span data-api-tag="require|glnRoj">必选</span> `Example: dcc-xnkd823nkd****`

The ID of the DC Connection whose renewal method needs to be modified.

You can call the [DescribeDirectConnectConnections](https://docs.byteplus.com/en/docs/directconnect/DescribeDirectConnectConnections) interface to query the DC Connection ID.



**RenewType ** <span data-label="purple">String </span><span data-api-tag="require|NyMDAm">必选</span> `Example: Auto`

The renewal type.


* Auto: Automatic renewal.

* Manual: Manual renewal.

* NoRenew: Non\-renewal upon expiration.



**RenewPeriod ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Automatic renewal period. Unit: Month.

Values: 1, 2, 3, 6, and 12.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If <code>RenewType</code> is set to <code>Auto</code>, <code>RenewPeriod</code> and <code>RemainRenewTimes</code> must be provided.</div>




**RemainRenewTimes ** <span data-label="purple">Integer </span>`optional` `Example: 1`

The number of automatic renewals available.


* 1–100: The number of automatic renewals.

* \-1: Unlimited renewals.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If <code>RenewType</code> is set to <code>Auto</code>, <code>RenewPeriod</code> and <code>RemainRenewTimes</code> must be provided.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=SetDirectConnectConnectionRenewal&Version=2020-04-01&DirectConnectConnectionId=dcc-xnkd823nkd****&RenewType=Auto&RenewPeriod=1&RemainRenewTimes=1' HTTP/1.1
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
        "Action": "SetDirectConnectConnectionRenewal",
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
|400 |InvalidRemainRenewTimes.Malformed |The specified remain renew times is malformed. Remain renew times only support \-1, 1~100. |The specified number of automatic renewals is invalid. The value for the number of automatic renewals must be \-1 or 1\-100. |
|400 |InvalidRenewPeriodTimes.Malformed |The specified renew period times is malformed. Renew period times only support 1, 2, 3, 6, 12. |The specified automatic renewal cycle is invalid. The value for the automatic renewal cycle must be 1, 2, 3, 6, or 12 months. |
|400 |InvalidRenewType.Malformed |The specified renew type is malformed. Renew type must be Manual, Auto or NoRenew. |The specified renewal type is invalid. The renewal type must be manual renewal, automatic renewal or non\-renewal. |
|404 |InvalidDirectConnectConnection.NotFound |The specified direct connect connection does not exist. |The specified DC Connection does not exist. |
