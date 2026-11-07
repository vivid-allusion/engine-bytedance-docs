---
title: "UpdateLatencyConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatelatencyconfig"
---

Call the `UpdateLatencyConfig` API to reduce the live streaming latency by configuring server GOP cache for streams under the specified domain name used in stream pulling.

<span id="requirements"></span>
## Requirements


* Limitations: This feature is applicable for stream pulling over Flash Video(FLV) and Real\-Time Messaging Protocol (RTMP).

* Rate limit: 10 queries per second per account.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateLatencyConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateLatencyConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Domain |String |Yes |`pull.example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|GopCacheSize |Integer |Yes |`2000` |The cache size of an edge server refers to the amount of storage allocated for temporarily storing the group of picture (GOP).<br><br><br>* The cache size is measured in milliseconds.<br><br>* Valid range: 500\-20,000.<br><br>* The default value is `2000`. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateLatencyConfig&Version=2023-01-01
{
    "GopCacheSize": 2000,
    "Domain": "pull.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240412014133DA1BD20A355B07FE66F5",
        "Action": "UpdateLatencyConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
