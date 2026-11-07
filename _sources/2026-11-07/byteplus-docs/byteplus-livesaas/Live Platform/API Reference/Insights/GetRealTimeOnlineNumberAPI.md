---
title: "GetRealTimeOnlineNumberAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getrealtimeonlinenumberapi"
---

Call this API to get the number of online viewers, including virtual popularity, in a specific live room. The data is updated once every minute.

<span id="a5e47365"></span>
## Requirements

Quota: 120 requests per minute per account

<span id="b64eac6a"></span>
## HTTP request


* Method: GET

* Endpoint: `https://livesaas.byteplusapi.com/?Action=GetRealTimeOnlineNumberAPI&Version=2020-06-01`


<span id="3f1a15e7"></span>
## Request parameters

<span id="f6822206"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="ce9592c2"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetRealTimeOnlineNumberAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`178398****301234` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="21aa01c9"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|RealPopularity |Integer |`1` |The actual number of viewers in the live room. |
|FakePopularity |Integer |`2` |The virtual popularity in the live room. |


<span id="e910ff53"></span>
## Samples

<span id="9fe44dd6"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetRealTimeOnlineNumberAPI&Version=2020-06-01&ActivityId=178398****301234
```


<span id="6ff71fa6"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202201201826170101501312091D1C09D2",
        "Action": "GetRealTimeOnlineNumberAPI",
        "Version": "2020-06-01",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "SystemTime": 1681979936
    },
    "Result": {
        "RealPopularity": 1,
        "FakePopularity": 2
    }
}
```


<span id="9ccfe9d9"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
