---
title: "StopPushPublicStream"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-113682"
---

If you have already pushed a WTN stream, you can call `StopPushPublicStream` to stop pushing.

<span id="requirements"></span>
## Requirements

The QPS should not exceed 150.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=StopPushPublicStream&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`StopPushPublicStream` |Interface name. The value of this interface: `StopPushPublicStream` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|BusinessId |String |No |`Your_****nessId` |The business identifier for your audio & video app |
|PublicStreamId |String |Yes |`Your_PublicStream` |Public stream ID. |


<span id="response-parameters"></span>
## Response parameters

The return value `Result` only returns "ok" when the request is successful, and returns an error code and related information when failed.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=StopPushPublicStream&Version=2020-12-01
{
    "AppId": "You****pId",
    "BusinessId": "Your_****nessId",
    "PublicStreamId": "PublicStreamId"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "Result": "ok",
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "StopPushPublicStream",
        "Version": "2020-12-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
