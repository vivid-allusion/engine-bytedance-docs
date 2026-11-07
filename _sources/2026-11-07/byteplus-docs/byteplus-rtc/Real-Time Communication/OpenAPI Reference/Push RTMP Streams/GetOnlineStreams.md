---
title: "GetOnlineStreams"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-139262"
---

You can use this interface to query the list of online WTN streams.

<span id="http-request"></span>
## HTTP request


* Method: GET

* Endpoint: https://open.byteplusapi.com?Action=GetOnlineStreams&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

The following table only lists the request parameters specific to this interface and some common parameters. For more information, please see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetOnlineStreams` |API name. The value of this interface: `GetOnlineStreams`。 |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01`。 |
|AppId |String |Yes |`661****543cf` |Application ID. |
|SourceProtocol |String |Yes |`RTMP` |Streaming protocol. Currently only `RTMP` is supported. |
|Limit |String |No |`200` |The maximum number of data entries returned in a single query. The value range is `(0,500]`, and the default value is `200`.<br><br>If the entered value is greater than `500`, it will be automatically adjusted to `500`. If the entered value is of a non\-numeric type, it will be automatically adjusted to `200`. |
|Cursor |String |No |`1` |The starting position of this query. Start from `0`.<br><br>The default value is empty. |


<span id="response-parameters"></span>
## Response parameters

The following table only lists the return parameters specific to this interface. For the common return parameters, please refer to [Return Structure](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#response).


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|HasMore |Boolean |`true` |Whether there is a next page. |
|Cursor |String |`20` |The starting position of the next page query. |
|Streams |Array of String |`["stream1","stream2"]` |List of stream IDs. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
GET https://open.byteplusapi.com?Action=GetOnlineStreams&Version=2023-11-01&AppId=&SourceProtocol=&Limit=&Cursor=
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetOnlineStreams",
        "Version": "2023-11-01",
        "Service": "wtn",
        "Region": "cn-north-1"
    },
    "Result": {
        "HasMore": true,
        "Cursor": "3",
        "Streams": [
            "stream1",
            "stream2"
        ]
    }
}
```


&nbsp;
