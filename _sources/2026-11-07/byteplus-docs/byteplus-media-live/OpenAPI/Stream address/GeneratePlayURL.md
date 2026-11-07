---
title: "GeneratePlayURL"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generateplayurl-2023"
---

Call the `GeneratePlayURL` API to generate the pull stream addresses for a specified stream.

<span id="requirements"></span>
## Requirements


* Rate limit: 25 queries per second per account.

* Prerequisites:

   * To generate the pull stream address of the transcoded stream, you must complete the [transcoding configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-transcoding) of the corresponding `AppName` first.

   * To generate the ABR pull stream address, you must complete the [ABR configuration](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) of the corresponding `AppName` and select the corresponding protocol type first.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=GeneratePlayURL&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GeneratePlayURL` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Domain |String |Yes |`pull.example.com` |The domain name for stream pulling. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|App |String |Yes |`live` |The AppName field in the push stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Stream |String |Yes |`test` |The StreamName field in the pull stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters. |
|Type |String |No |`fcdn` |The CDN type. Valid values:<br><br><br>* `fcdn`: (Default) BytePlus MediaLive CDN.<br><br>* `3rd`: Third\-party CDN. If you are using the [relay](https://docs.byteplus.com/byteplus-media-live/docs/relay) feature and want to get a third\-party pull stream address, set `Type` to `3rd`. |
|Suffix |String |No |`5` |The suffix of the transcoded stream, which is empty by default. If the configuration is not empty, it is the pull stream address for generating the transcoded stream. You can call [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) to query existing transcoding templates and their corresponding suffixes. |
|ValidDuration |Integer |No |`5` |The addresses expire after the length of time specified by `ValidDuration`, starting from the moment the addresses are generated. Unit: second. Valid range: \> 0. Default value: 604800 (seven days).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When an M3U8 pull stream address expires, stream pulling will stop immediately. For other types of addresses, the ongoing stream pulling will not be affected if the address expires.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both <code>ValidDuration</code> and <code>ExpiredTime</code>, only the setting of <code>ExpiredTime</code> takes effect.</div><br> |
|ExpiredTime |String |No |`2022-08-19T16:07:25+08:00` |Expiration time (Local time in RFC 3339 format with second precision) of the addresses, in seconds. The default expiration time is seven days after the addresses are generated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When an M3U8 pull stream address expires, stream pulling will stop immediately. For other types of addresses, the ongoing stream pulling will not be affected if the address expires.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both <code>ValidDuration</code> and <code>ExpiredTime</code>, only the setting of <code>ExpiredTime</code> takes effect.</div><br> |
|StreamType |String |Yes |`source` |The generated address type, with the following values:<br><br><br>* `source`: Generate the source stream address.<br><br>* `transcode`: Generate the transcoded stream address.<br><br>* `abr`: Generate the ABR address. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|URLList |Array of [URLList](https://docs.byteplus.com/en/docs/24/27414#urllist) |`-` |A list of pull stream addresses. |
|AuthType |String |`TypeB` |The URL authentication type used to generate pull stream addresses. If the value is empty, it indicates that URL authentication is not configured for the current domain.<br><br><br>* `TypeA`: Type A.<br><br>* `TypeB`: Type B.<br><br>* `TypeC`: Type C.<br><br>* `TypeCustom`: Custom type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on type A, B, or C, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>.</div><br> |


<span id="urllist"></span>
### URLList


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|URL |String |`https://pull.example.com/live/test.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70` |The pull stream address. |
|Type |String |`pull` |The address type.<br><br><br>* `pull`: A pull stream address<br><br>* `3rd_play(replay_source)`: A third\-party pull stream address for origin pull<br><br>* `3rd_play(relay_sink)`: A third\-party pull stream address for relay |
|CDN |String |`fcdn` |The CDN type.<br><br><br>* `fcdn`: (Default) BytePlus Video Cloud CDN;<br><br>* `3rd`: Third\-party CDN. |
|Protocol |String |`udp` |Streaming protocol. Valid values:<br><br><br>* `hls`: HLS pull stream address.<br><br>* `flv`: FLV pull stream address.<br><br>* `rtmp`: RTMP pull stream address.<br><br>* `udp`: RTM pull stream address for client SDKs (BytePlus MediaLive Player SDKs for iOS, Android, React Native, and Flutter) and other players.<br><br>* `udp_websdk`: RTM pull stream address for the BytePlus MediaLive Player SDK for Web.<br><br>* `cmaf`: CMAF pull stream address.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><br>* <div data-tips="true" data-tips-type="warning">If you cannot get the RTM pull stream address for the BytePlus MediaLive Player SDK for Web, contact <a href="https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980">technical support</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">The RTM pull stream address for the BytePlus MediaLive Player SDK for Web supports automatic transcoding, including B\-frame removal and AAC\-to\-Opus audio conversion. For more information, see <a href="https://docs.byteplus.com/docs/byteplus-media-live/docs-generating-live-stream-addresses">Generating live\-stream addresses</a>.</div><br><br><br>* <div data-tips="true" data-tips-type="warning">When the value of <code>StreamType</code> is <code>abr</code>, the RTM\-ABR pull stream address whose <code>Protocol</code> value is <code>udp</code> currently supports the BytePlus MediaLive Player SDKs for iOS and Android, and other players.</div><br> |
|SubStreamURL |Array of [SubStreamURL](https://docs.byteplus.com/en/docs/24/27414#substreamurl) |`-` |The sub\-stream address. Returned only when `StreamType` is `abr`. |


<span id="substreamurl"></span>
### SubStreamURL


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Suffix |String |`_ld` |The substream transcoding suffix. |
|Tag |String |`LL-HLS` |The address label, such as `drm`, `hls encryption`. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=GeneratePlayURL&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "test",
    "StreamType": "source",
    "ExpiredTime": "2022-08-19T16:07:25Z"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GeneratePlayURL",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "URLList": [
            {
                "URL": "https://pull.example.com/live/test.sdp?auth_key=1779891783-0-0-873bca4ce****e85f357be5434067b70",
                "CDN": "fcdn",
                "Protocol": "udp",
                "Type": "pull"
            }
        ],
        "AuthType": "TypeB"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27414#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Format |%s format error |The parameter format is incorrect. Please check if there are illegal characters or URL format errors in the specified parameter in the error message. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|400 |InvalidParam.TimeLogic |startTime later than endTime, etc. |The passed\-in time parameter does not conform to the logic of time. Please check if the following problems exist:The start time is later than the end time.The expiration time is earlier than the current time. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |An internal error related to the domain name space (Vhost) or domain name (Domain) occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
