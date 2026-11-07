---
title: "DescribeHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describehlsconfig"
---

Call the `DescribeHLSConfig` API to query the HLS configuration for a specific domain name space, including segment size, segment number, and more.

<span id="requirements"></span>
## Requirements

Rate limit：10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=DescribeHLSConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`DescribeHLSConfig` |The API operation. |
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
|HLSConfigList |Array of [HLSConfigList](https://docs.byteplus.com/en/docs/24/20097#hlsconfiglist) |`-` |The list of HLS configurations。 |


<span id="hlsconfiglist"></span>
### HLSConfigList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The AppName field. |
|Interval |Float |`3` |HLS segment duration which is measured in seconds. |
|PlaylistLength |Integer |`3` |The number of media segments in a m3u8 playlist. |
|FirstPlaylistLength |Integer |`2` |The number of media segments included in the initial playlist. |
|UpdateTime |String |`2024-04-11 06:30:11` |The time when the configuration was last updated. |
|CreateTime |String |`2024-04-11 06:30:11` |The time when the configuration was created. |
|PartTargetDuration |Float |`1` |The duration of a partial segment which is divided from each media segment.<br><br>It is measured in seconds.<br><br>0 indicates disabling the low\-latency HLS. |
|InsertPDT |Boolean |`true` |Whether to insert the PDT time tag in the playback file, the value and meaning are as follows.<br><br><br>* `true`: insert;<br><br>* `false`: not inserted. |
|PDTInterval |String |`3` |The interval for inserting the PDT (#EXT\-X\-PROGRAM\-DATE\-TIME) time tag in the playback file, in seconds, and the value range is [0,3600], the default value is 0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the PDT interval is set to 0 or a value less than the segment duration, a PDT tag will be inserted for each segment.</div><br> |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=DescribeHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202404120105366DB1CC6291C10149B0EE",
        "Action": "DescribeHLSConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "HLSConfigList": [
            {
                "Vhost": "example.com",
                "App": "",
                "FirstPlaylistLength": 2,
                "Interval": 3,
                "PartTargetDuration": 1,
                "PlaylistLength": 3,
                "CreateTime": "2024-04-11 06:30:11",
                "UpdateTime": "2024-04-11 06:30:11"
            }
        ]
    }
}
```


&nbsp;
