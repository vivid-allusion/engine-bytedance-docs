---
title: "UpdateCMAFConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig"
---

In Dynamic Adaptive Streaming over HTTP (DASH) and Low\-Latency DASH (LL\-DASH), a live stream is sliced into Common Media Application Format (CMAF) segments. Call the `UpdateCMAFConfig` API, you can adjust the duration and segment number settings to effectively reduce the latency and improve compatibility in live streaming under the specified domain name space (Vhost).

<span id="requirements"></span>
## Requirements


* Prerequisites：

   * A player supporting DASH is required.

   * iOS 10.0, macOS 10.12, and tvOS 10.0 or later OS versions support CMAF content.

* Limitations：

   * The DASH encapsulation is applicable for stream pushing, origin pull using HLS, FLV and Real\-Time Messaging Protocol (RTMP), and stream pulling using DASH over CMAF.

   * The DASH encapsulation configuration will apply not only to this domain name but also to other domain names associated with the same domain name space (Vhost).

   * The encapsulation configuration takes effect in 3 minutes to 5 minutes.

* Rate limit：10 queries per second per account


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateCMAFConfig&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateCMAFConfig` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`Arctic` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |No |`Far` |The AppName field in the live stream URL. If unspecified, the configuration will apply to all the AppNames. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Interval |Float |No |`2` |CMAF segment duration ranging from `1` to `60` seconds. The default value is `2`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">We recommend that the group of pictures (GOP) size of the live stream is stable and that the segment duration is equal to or an integer multiple of the GOP size.</div><br> |
|PlaylistLength |Integer |No |`6` |The number of media segments included in a playlist. You can enter an integer from `3` to `10`. The default value is `3`. |
|DisableLowLatency |Boolean |No |`true` |Whether to disable Low\-latency DASH. Low\-Latency DASH extends the protocol to enable low\-latency video streaming while maintaining scalability. The default values is `false`.<br><br><br>* `true`: Disable;<br><br>* `false`:Enable. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateCMAFConfig&Version=2023-01-01
{
    "Vhost": "example",
    "App": "liveShow",
    "Interval": 3,
    "PlaylistLength": 6,
    "DisableLowLatency": true
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024041105461468A8B53B2CE41BAA7E87",
        "Action": "UpdateCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
