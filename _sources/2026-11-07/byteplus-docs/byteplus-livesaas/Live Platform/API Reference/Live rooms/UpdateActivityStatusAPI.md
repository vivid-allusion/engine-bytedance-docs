---
title: "UpdateActivityStatusAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-updateactivitystatusapi"
---

Updates the status of a live room. You can restore the live room to the **Preview** status, lock the preview, and unlock the preview.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=UpdateActivityStatusAPI&Version=2020-06-01`

* Method: POST


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateActivityStatusAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. The value is `2020-06-01`. |


<span id="body"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|IsStreamViewEnable |Integer |Yes |`4` |Specifies the operation that you want to perform.<br><br>Valid values:<br><br><br>* `3`: Restore the live room to the **Preview** status.<br><br>* `4`: Lock the preview. The viewing page will be locked in the **Preview** status and will not play live videos or playbacks.<br><br>* `5`: Unlock the preview. The viewing page can then play live videos and playbacks. |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`-` |Deprecated. |
|ActivityIdStr |String |`-` |Deprecated. |
|Status |Integer |`-` |Deprecated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=UpdateActivityStatusAPI&Version=2020-06-01
{    
    "ActivityId": 17218346****,
    "IsStreamViewEnable": 4
}
```


<span id="sample-response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "UpdateActivityStatusAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1696235450
    },
    "Result": {
        "ActivityId": 0,
        "ActivityIdStr": "",
        "Status": 0
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
