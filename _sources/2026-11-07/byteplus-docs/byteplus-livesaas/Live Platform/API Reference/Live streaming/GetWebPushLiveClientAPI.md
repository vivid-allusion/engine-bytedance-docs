---
title: "GetWebPushLiveClientAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getwebpushliveclientapi"
---

Gets the URL for the live streaming page of a live room, allowing the host to start a live stream from a web browser without the need for logging in.

<span id="d1ad3925"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="a61cce88"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientAPI&Version=2020-06-01`

* Method: GET


<span id="11dd5e64"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="4e52a872"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetWebPushLiveClientAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="c917226e"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Url |String |`http://livesaas.example.com/***` |The URL for the live streaming page. A host can open this URL in a web browser to start streaming without needing to log in. |


<span id="7d9b305a"></span>
## Samples

<span id="2c69e10f"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientAPI&Version=2020-06-01&ActivityId=17218312****
```


<span id="59f3352f"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetWebPushLiveClientAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656067132 
    }, 
    "Result": {
        "Url": "http://livesaas.example.com/***"
    }
}
```


<span id="cb06ddde"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
