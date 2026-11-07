---
title: "DescribeCMAFConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describecmafconfig"
---

Call the `DescribeCMAFConfig` API to query the duration and segment number settings for the streaming under the specified domain name space.

<span id="requirements"></span>
## Requirements

Rate limit：10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeCMAFConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeCMAFConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CMAFConfigList |Array of [CMAFConfigList](https://docs.byteplus.com/en/docs/24/20099#cmafconfiglist) |`-` |The list of CMAF configurations。 |


<span id="cmafconfiglist"></span>
### CMAFConfigList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`Arctic` |The domain name space. |
|App |String |`Far` |The AppName field. |
|Interval |Float |`2.6` |CMAF segment duration ranging from 1 to 60. |
|PlaylistLength |Integer |`6` |The number of media segments included in a playlist. Integer from 3 to 10. |
|DisableLowLatency |Boolean |`true` |Whether the Low\-latency DASH is disabled. Low\-Latency DASH extends the protocol to enable low\-latency video streaming while maintaining scalability.<br><br><br>* `true`: Disable;<br><br>* `false`: Enable. |
|CreateTime |String |`2024-02-23T07:51:15Z` |The UTC time in RFC 3339 format when the configuration was created. |
|UpdateTime |String |`2024-02-23T07:51:15Z` |The UTC time in RFC 3339 format when the configuration was last updated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeCMAFConfig&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240411060546FAFDB99137DFD66F1D02",
        "Action": "DescribeCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CMAFConfigList": [
            {
                "Vhost": "example.com",
                "App": "",
                "DefaultLatency": 3,
                "DisableLowLatency": false,
                "Interval": 2,
                "PlaylistLength": 3,
                "CreateTime": "2024-03-18T05:47:44Z",
                "UpdateTime": "2024-03-18T05:47:44Z"
            }
        ]
    }
}
```


&nbsp;
