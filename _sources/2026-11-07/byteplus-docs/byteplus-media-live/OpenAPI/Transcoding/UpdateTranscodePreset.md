---
title: "UpdateTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1"
---

Call the `UpdateTranscodePreset` API to update the added transcoding configuration. If the non\-required parameters are not filled in, the corresponding parameter configuration will not change.

## Requirements

* Rate limit: 10 queries per second per account.

* Effective description: For adding, updating, and deleting transcoding configurations, you need to re\-push and pull the stream after the adding, updating, and deleting operations (3\-5 minutes) to use the changed configuration.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdateTranscodePreset&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdateTranscodePreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Preset |String |Yes |`PresetName` |The name of configuration. You can call the [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API to obtain the name of configuration to be updated. |
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API to obtain the domain name space of configuration to be updated. |
|App |String |No |`live` |The AppName field. You can call the [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API to obtain the AppName field of configuration to be updated. |
|SuffixName |String |No |`hd` |Suffix of the transcoded stream. This can contain uppercase and lowercase letters, underscores (_), and hyphens (\-). Maximum length: 10 characters. Common suffixes include _sd, _hd, and _uhd. For example, if you set _hd as the suffix, the name of the transcoded stream becomes streamName_hd. |
|VideoBitrate |Integer |No |`0` |Video bitrate in bps. The default value is 1,000,000. 0 means keeping the original video bitrate.<br><br>The valid range varies among the Vcodec values:<br><br><br>* 0–30,000,000 for h264 and h265<br><br>* 0–60,000,000 for h266 |
|Vcodec |String |No |`h265` |Video codec.<br><br><br>* `h264`: H.264.<br><br>* `h265`: H.265.<br><br>* `h266`: H.266.<br><br>* `copy`: Does not transcode the video stream. And all the video configurations can not be applied. |
|AudioBitrate |Integer |No |`30` |Audio bitrate in Kbps. Valid range: 0\-1000. The default value is 128. 0 means keeping the original bitrate. |
|Acodec |String |No |`aac` |Audio codec.<br><br><br>* `aac`: AAC.<br><br>* `copy`: Does not transcode the audio stream. And all the audio configurations can not be applied.<br><br>* `opus`: OPUS. |
|FPS |Integer |No |`60` |Video frame rate in fps. The default value is 25. 0 means keeping the original frame rate.<br><br>The valid range varies among the Vcodec values:<br><br><br>* 0–60 for h264 and h265<br><br>* 0–35 for h266 |
|GOP |Integer |No |`2` |The maximum interval between IDR frames. Unit: second. Valid range: 1–30. |
|Width |Integer |No |`1366` |Width of the video in pixel(px). Valid when Vcodec is set to h264 and h265 and As is set to 0.<br><br>The valid range is {0,[150–1920]}.<br><br>> **说明**<br><br><br><br>* > The video is stretched according to Width and Height.<br><br><br>* > When either Width or Height is set to 0, the original video dimensions are preserved.<br> |
|Height |Integer |No |`768` |Height of the videoin pixel(px). Valid when Vcodec is set to h264 and h265 and As is set to 0.<br><br> <br><br>The valid range is {0,[150–1920]}.<br><br>> **说明**<br><br><br><br>* > The video is stretched according to Width and Height.<br><br><br>* > When either Width or Height is set to 0, the original video dimensions are preserved.<br> |
|As |String |No |`1` |Whether to auto\-adjust the video dimensions.<br><br><br>* `0`: Disables auto\-adjustment, and stretches the video according to Width and Height. Ensure Width and Height are within the valid range.<br><br>* `1`: Enables auto\-adjustment, and scales the video according to ShortSide or LongSide. Ensure ShortSide and LongSide are within the valid range. |
|ShortSide |Integer |No |`500` |Short side of the video. Valid when As is set to 1.<br><br>The valid range varies among the Roi and Vcodec values:<br><br><br>* When Roi is false.<br><br>   * 150\-2160 for h264<br><br>   * 150\-4096 for h265<br><br>   * 150\-720 for h266<br><br>* 150–1920 when Roi is true.<br><br><br>> **说明**<br><br><br><br>* > If you set both LongSide and ShortSide to 0, the original video dimensions are preserved.<br><br><br>* > If you set both LongSide and ShortSide to values other than 0, the video is stretched according to the value of ShortSide.<br> |
|LongSide |Integer |No |`600` |Long side of the video. Valid when As is set to 1.<br><br>The valid range varies among the Roi and Vcodec values:<br><br><br>* When Roi is false.<br><br>   * 150\-4096 for h264<br><br>   * 150\-7680 for h265<br><br>   * 150\-1280 for h266<br><br>* 150–1920 when Roi is true.<br><br><br>> **说明**<br><br><br><br>* > If you set both LongSide and ShortSide to 0, the original video dimensions are preserved.<br><br><br>* > If you set both LongSide and ShortSide to values other than 0, the video is stretched according to the value of ShortSide.<br> |
|BFrames |Integer |No |`3` |The maximum number of B\-frames between two reference frames. The default value is 3.    0 means removing B\-frames.<br><br>The valid value varies among the Vcodec values:<br><br><br>* [0–7] for h264.<br><br>* {0, 1, 2, 3, 7, 15} for h265 and h266. |
|Roi |Boolean |No |`true` |Whether to transcode using low\-bitrate HD mode.<br><br><br>* `true`: Low\-bitrate HD mode.<br><br>* `false`: (default) Standard mode.<br><br><br>> **说明**<br><br><br>> When the Vcodec is H.266, the transcoding does not support low\-bitrate HD mode.<br> |
|AutoTransResolution |Integer |No |`1` |Whether to constrain the transcoding resolution not to exceed the original stream resolution.<br><br><br>* `0`: Allow<br><br>* `1`: (default) Constrain |
|AutoTransVb |Integer |No |`1` |Whether to constrain the transcoding bitrate not to exceed the original stream bitrate.<br><br><br>* `0`: Allow<br><br>* `1`: (default) Constrain |
|AutoTransVr |Integer |No |`1` |Whether to constrain the transcoding frame rate not to exceed the original frame rate.<br><br><br>* `0`: Allow<br><br>* `1`: (default) Constrain |
|StopInterval |Integer |No |`60` |The pause duration for the transcoding task, in second.<br><br>Valid when TransType is set to Pull. The valid range of values can be \-1 or an integer between 0 and 300. \-1 means the task does not pause when the stream pulling stops. The default value is 60. |
|TransType |String |No |`Pull` |A transcoding task starts when:<br><br><br>* `Push`: the live stream initiates.<br><br>* `Pull`: (default) the transcoded stream is requested. |

## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdateTranscodePreset&Version=2023-01-01
{
    "Preset": "PresetName",
    "Vhost": "push.example.com",
    "App": "live",
    "SuffixName": "hd"
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateTranscodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7716#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the database occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
