---
title: "WithdrawAward"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/WithdrawAward"
---

Call `WithdrawAward` to withdraw a real\-time lucky draw from a live room. Note that a withdrawn lucky draw cannot be sent again or updated.

<span id="Requirements"></span>
## Requirements


* Rate limit: 10 requests per second per account

* Prerequisite: A BytePlus account or an IAM user with **Live control** \> **Edit** permission. For more information on how to add IAM users, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="HTTP request"></span>
## HTTP request


* Method：POST

* Endpoint：https://livesaas.byteplusapi.com/?Action=WithdrawAward&Version=2023\-08\-01


<span id="Request parameters"></span>
## Request parameters

<span id="Common parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="Query"></span>
### Query


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`WithdrawAward` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="Body parameters"></span>
### Body parameters


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|ActivityId |Integer |Yes |17218346\*\*\*\* |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|Id |Integer |Yes |36576 |The real\-time lucky draw ID to be withdrawn. You can obtain the ID by calling the ListAwardConfigs API.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When withdrawing a real\-time lucky draw, make sure the lucky draw status is "In progress" or "Completed". You can call this API to withdraw the real\-time lucky draw when the value of the <code>Status</code> parameter returned by the <code>ListAwardConfigs</code> API is <code>2</code> or <code>4</code>.</div><br> |


<span id="Response parameters"></span>
## Response parameters


|**Parameter** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|Status |Boolean |`true` |Whether the lucky draw is successfully withdrawn. Return `true` if successful. |


<span id="Samples"></span>
## Samples

<span id="Sample request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=WithdrawAward&Version=2023-08-01
{
    "ActivityId": 17218346****,
    "Id": 36576
}
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "WithdrawAward",
        "Version": "2023-08-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1697446406
    },
    "Result": {
        "Status": true
    }
}
```


<span id="Error codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
