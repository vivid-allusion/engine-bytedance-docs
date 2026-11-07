---
title: "PresenterChatAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-presenterchatapi"
---

Call this API to sends a comment as the host in a live room.

<span id="459d9053"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="b2acb75e"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=PresenterChatAPI&Version=2020-06-01`

* Method: POST


<span id="5ad3f4d9"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="91ba5468"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`PresenterChatAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="Body parameters"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|Comment |String |Yes |`Hello` |The comment to be sent. |


<span id="e21e2025"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|status |Boolean |`true` |Indicates whether the comment was sent successfully.<br><br><br>* `true`: Successful.<br><br>* `false`: Failed. |


<span id="b574ac21"></span>
## Samples

<span id="3ca901e7"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=PresenterChatAPI&Version=2020-06-01
{
    "ActivityId": 17218346****,
    "Comment": "Hello" 
}
```


<span id="Sample response"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "PresenterChatAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1656067132
    },
    "Result":{
        "status": true
    }
}
```


<span id="6d8a9dad"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
