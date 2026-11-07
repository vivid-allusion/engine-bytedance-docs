---
title: "UpdateHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig"
---

Call the `UpdateHLSConfig` API to add or update the HLS configuration for a specific domain space, including segment size, and segment number to effectively reduce latency and improve compatibility in live streaming. In HTTP Live Streaming (HLS) and Low\-Latency HLS (LL\-HLS), a live stream is sliced into Transport Stream (TS). Each TS has a corresponding URL, and the address changes constantly when using the HLS protocol for live pull streaming.

<span id="requirements"></span>
## Requirements


* Prerequisites：A player supporting LL\-HLS is required.

* Limitations：

   * The HLS/LL\-HLS encapsulation is applicable for stream pushing, origin pull using FLV and Real\-Time Messaging Protocol (RTMP), and stream pulling using HLS. Note that it does not apply to origin pull using HLS.

   * The HLS/LL\-HLS encapsulation configuration will apply not only to streams under this domain name but also to streams under other domain names associated with the same domain name space (Vhost).

   * The HLS/LL\-HLS encapsulation configuration will not apply to the application which enables the [HLS-ABR](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) feature.

   * The encapsulation configuration takes effect in 3 minutes to 5 minutes.

      Limitations：Applicable for stream pushing, stream pulling using HLS, and origin pull using FLV and Real\-Time Messaging Protocol (RTMP). But not for origin pull using HLS.

* Rate limit：10 queries per second per account.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateHLSConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateHLSConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |No |`live` |The AppName field in the live stream URL. If unspecified, the configuration will apply to all the AppNames. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Interval |Float |No |`3` |HLS segment duration ranging from 1 to 60 seconds.<br><br>The default value is 3.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that the group of pictures (GOP) size of the live stream is stable and that the segment duration is equal to or an integer multiple of the GOP size.</div><br> |
|PlaylistLength |Integer |No |`3` |The number of media segments in an m3u8 playlist. The default value is 3. |
|FirstPlaylistLength |Integer |No |`2` |The number of media segments included in the initial playlist. You can enter an integer from `3` to `10`. The default value is `2`. |
|PartTargetDuration |Float |No |`1` |The duration of a partial segment which is divided from each media segment.<br><br><br>* It is measured in seconds.<br><br>* The default value is `1`.<br><br>* `0` indicates disabling the low\-latency HLS. |
|InsertPDT |Boolean |No |`true` |Whether to insert the PDT time tag in the playback file, the default is not inserted, the value and meaning are as follows.<br><br><br>* `true`: insert;<br><br>* `false`: not inserted. |
|PDTInterval |Float |No |`3` |The interval for inserting the PDT (#EXT\-X\-PROGRAM\-DATE\-TIME) time tag in the playback file, in seconds, and the value range is [0,3600], the default value is 0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the PDT interval is set to 0 or a value less than the segment duration, a PDT tag will be inserted for each segment.</div><br> |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Interval": 2.6,
    "PlaylistLength": 6,
    "FirstPlaylistLength": 4,
    "PartTargetDuration": 1
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024041106585435BA3A27F267D68D449F",
        "Action": "UpdateCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
