---
title: "CreateTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023"
---

Call the `CreateTranscodePreset` API to create a transcoding configuration, and the system will perform real\-time transcoding on live streams that meet the conditions according to your transcoding configuration.

## Usage scenario

The `CreateTranscodePreset` API supports creating multiple `Vhost + App`\-level transcoding configurations, and different transcoding configurations need to be distinguished by using the transcoding suffix (SuffixName). After creating the transcoding configuration, you can use the transcoding configuration by adding the transcoding suffix to the stream name in the pull\-stream address.

## Requirements

* Billing: For transcoding pricing, please refer to [Transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding).

* Rate limit: 10 queries per second per account.

* Effective description: For adding, updating, and deleting transcoding configurations, you need to re\-push and pull the stream after the adding, updating, and deleting operations (3\-5 minutes) to use the changed configuration.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateTranscodePreset&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateTranscodePreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |Yes |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|SuffixName |String |Yes |`hd` |Suffix of the transcoded stream. This can contain uppercase and lowercase letters（A \- Z, a \- z）, underscores (_), and hyphens (\-). Maximum length: 10 characters. Common suffixes include `_sd`, `_hd`, and `_uhd`. For example, if you set `_hd` as the suffix, the name of the transcoded stream becomes `streamName_hd`. |
|VideoBitrate |Integer |No |`1000000` |Video bitrate in bps. The default value is 1,000,000. 0 means keeping the original video bitrate.<br><br>The range of video bitrates varies depending on the video encoding format (`Vcodec`).<br><br>The valid range varies among the Vcodec values:<br><br><br>* 0–30,000,000 for h264 and h265 |
|Vcodec |String |Yes |`h265` |Video codec.<br><br><br>* `h264`: H.264.<br><br>* `h265`: H.265.<br><br>* `copy`: Does not transcode the video stream. And all the video configurations can not be applied, including video frame rate (`FPS`), video bitrate (`VideoBitrate`), resolution settings (`As`, `Width`, `Height`, `ShortSide`, `LongSide`), `GOP` and `BFrames`, etc. |
|AudioBitrate |Integer |No |`50` |Audio bitrate in Kbps. Valid range: 0\-1000. The default value is 128. 0 means keeping the original bitrate. |
|Acodec |String |No |`aac` |Audio codec. The default value is `aac`. it can take the following values:<br><br><br>* `aac`: AAC.<br><br>* `opus`: OPUS.<br><br>* `copy`: Does not transcode the audio stream. And all the audio configurations can not be applied. Audio codec parameters include audio bitrate (`AudioBitrate`) and so on. |
|FPS |Integer |No |`25` |Video frame rate in fps. The default value is 25. 0 means keeping the original frame rate.<br><br>The valid range varies among the Vcodec values:<br><br><br>* 0–60 for h264 and h265 |
|GOP |Integer |No |`2` |The maximum interval between IDR frames. Unit: second. Valid range: 1–30. |
|Width |Integer |No |`400` |Width of the video in pixel(px). Valid when `Vcodec` is set to h264 and h265 and `As` is set to `0`.<br><br>The range of video width varies among the Vcodec values:<br><br><br>* 150\-1920 for h264 and h265.<br><br>* It does not support setting Width and Height for h266.<br><br><br>> **说明**<br><br><br><br>* > When video resolution auto\-adjust is turned off (`As` value is 0), the video is stretched according to the values of Width and Height.<br><br><br>* > When video resolution auto\-adjust is turned off (`As` value is 0), when either Width or Height is set to 0, the original video dimensions are preserved.<br> |
|Height |Integer |No |`200` |Height of the videoin pixel(px). Valid when Vcodec is set to h264 and h265 and `As` is set to 0.<br><br> <br><br>The range of video width varies among the Vcodec values:<br><br><br>* 150–1920 for h264 and h265<br><br>* It does not support setting Width and Height for h266.<br><br><br>> **说明**<br><br><br><br>* > When video resolution auto\-adjust is turned off (`As` value is 0), the video is stretched according to the values of Width and Height.<br><br><br>* > When video resolution auto\-adjust is turned off (`As` value is 0), when either Width or Height is set to 0, the original video dimensions are preserved.<br> |
|As |String |No |`1` |Whether to auto\-adjust the video dimensions. The default value is 0, it can take the following values:<br><br><br>* `0`: Disables auto\-adjustment;<br><br>* `1`: Enables auto\-adjustment.<br><br><br>> **说明**<br><br><br><br>* > When video resolution auto\-adjust is turned off (`As` value is `0`), the video is stretched according to the values of Width and Height.<br><br><br>* > When video resolution auto\-adjust is turned on (`As` value is `1`), The video resolution of the transcoding is determined according to the priority of the short side length (`ShortSide`), long side length (`LongSide`), video width (`Width`), and video height (`Height`), and the other side is scaled proportionally.<br> |
|ShortSide |Integer |No |`768` |Short side length of the video. When configuring different transcoding types (`Roi`) and video codec (`Vcodec`), the value range of the short side length is as follows.<br><br><br>* When the transcoding type is standard mode (`Roi` value is `false`), the valid range varies among the `Roi` and `Vcodec` values:<br><br>   * 150\-2160 for h264<br><br>   * 150\-4096 for h265<br><br>* When the transcoding type is Low\-bitrate HD mode (`Roi` is `true`)<br><br>   * 0 or 150–1920 for h264 or h265.<br><br><br>> **说明**<br><br><br><br>* > When video resolution auto\-adjust is turned on (`As` value is `1`), the parameter is valid.<br><br><br>* > If you set both `LongSide` and `ShortSide` to 0, the original video dimensions are preserved.<br><br><br>* > If you set both LongSide and `ShortSide` to values other than 0, the video is stretched according to the value of `ShortSide`.<br> |
|LongSide |Integer |No |`500` |Long side length of the video. When configuring different transcoding types (Roi) and video codec (Vcodec), the value range of the long side length is as follows.<br><br><br>* When the transcoding type is standard mode (Roi value is false), the valid range varies among the Roi and Vcodec values:<br><br>   * 150\-4096 for h264<br><br>   * 150\-7680 for h265<br><br>* When the transcoding type is Low\-bitrate HD mode (`Roi` is `true`)<br><br>   * 0 and 150–1920 for h264 and h265.<br><br><br>> **说明**<br><br><br><br>* > When video resolution auto\-adjust is turned on (`As` value is `1`), the parameter is valid.<br><br><br>* > If you set both `LongSide` and `ShortSide` to 0, the original video dimensions are preserved.<br><br><br>* > If you set both `LongSide` and `ShortSide` to values other than 0, the video is stretched according to the value of `ShortSide`.<br> |
|BFrames |Integer |No |`3` |The maximum number of B\-frames between two reference frames. The default value is 3.    0 means removing B\-frames.<br><br>The valid value varies among the Vcodec values:<br><br><br>* [0–7] for h264.<br><br>* {0, 1, 2, 3, 7, 15} for h265. |
|Roi |Boolean |No |`true` |Whether to transcode using low\-bitrate HD mode.<br><br><br>* `true`: Low\-bitrate HD mode.<br><br>* `false`: (default) Standard mode. |
|AutoTransResolution |Integer |No |`1` |Whether to enable the transcoding resolution not to exceed the source stream resolution. After enabling this, when the original stream resolution is lower than transcoding resolution, transcoding is performed according to the source stream resolution.<br><br><br>* `0`: Disable<br><br>* `1`: (default) Enable |
|AutoTransVb |Integer |No |`1` |Whether to enable constrain the transcoding bitrate not to exceed the source stream bitrate. After enabling this, when source stream bitrate is lower than the transcoding bitrate, transcoding is performed to the source stream bitrate<br><br><br>* `0`: Disable<br><br>* `1`: (default) Enable |
|AutoTransVr |Integer |No |`1` |Whether to constrain the transcoding frame rate not to exceed the source frame rate. After enabling this, when source frame rate is lower than the transcoding frame rate, transcoding is performed to the source frame rate.<br><br><br>* `0`: Disable<br><br>* `1`: (default) Enable |
|StopInterval |Integer |No |`60` |The pause duration for the transcoding task, in second.<br><br>Valid when TransType is set to Pull. The valid range of values can be \-1 or an integer between 0 and 300. \-1 means the task does not pause when the stream pulling stops. The default value is 60. |
|TransType |String |No |`Pull` |A transcoding task starts when:<br><br><br>* `Push`: the live stream initiates.<br><br>* `Pull`: (default) the transcoded stream is requested. |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PresetName |String |`preset` |The name of the transcoding template. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateTranscodePreset&Version=2023-01-01
{
    "Vhost":"push.example.com",
    "App":"live",
    "SuffixName":"hd",
    "Vcodec"："h264"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateTranscodePreset",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "PresetName": "preset"
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/20051#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
