---
title: "ListVhostTransCodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1"
---

Call the `ListVhostTransCodePreset` API to query transcoding configurations or ABR (adaptive bitrate) configurations.

## Requirements

Rate limit：10 queries per second per account.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListVhostTransCodePreset&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListVhostTransCodePreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space, which is the domain name space to which the domain name in the live stream URL belongs. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to get the domain name space to which the domain name in the live stream URL belongs. |
|IsHlsAbr |Boolean |No |`true` |Specifies whether to query ABR configurations for the HLS\-ABR protocol. Default value: `false`. Valid values:<br><br><br>* `true`: Query ABR configurations for the HLS\-ABR protocol.<br><br>* `false`: Do not query ABR configurations for the HLS\-ABR protocol.<br><br><br>> **说明**<br><br><br><br>* > If multiple protocol parameters are set to `true`, the API queries ABR configurations for the specified protocol types. For example, if both `IsHlsAbr` and `IsDashAbr` are set to `true`, the API queries ABR configurations for the HLS\-ABR and DASH\-ABR protocols.<br><br><br>* > If none of `IsHlsAbr`, `IsDashAbr`, and `IsRtmAbr` is set to `true`, the API queries regular transcoding configurations.<br> |
|IsDashAbr |Boolean |No |`true` |Specifies whether to query ABR configurations for the DASH\-ABR protocol. Default value: `false`. Valid values:<br><br><br>* `true`: Query ABR configurations for the DASH\-ABR protocol.<br><br>* `false`: Do not query ABR configurations for the DASH\-ABR protocol.<br><br><br>> **说明**<br><br><br><br>* > If multiple protocol parameters are set to `true`, the API queries ABR configurations for the specified protocol types. For example, if both `IsHlsAbr` and `IsDashAbr` are set to `true`, the API queries ABR configurations for the HLS\-ABR and DASH\-ABR protocols.<br><br><br>* > If none of `IsHlsAbr`, `IsDashAbr`, and `IsRtmAbr` is set to `true`, the API queries regular transcoding configurations.<br> |
|IsRtmAbr |Boolean |No |`true` |Specifies whether to query ABR configurations for the RTM\-ABR protocol. Default value: `false`. Valid values:<br><br><br>* `true`: Query ABR configurations for the RTM\-ABR protocol.<br><br>* `false`: Do not query ABR configurations for the RTM\-ABR protocol.<br><br><br>> **说明**<br><br><br><br>* > If multiple protocol parameters are set to `true`, the API queries ABR configurations for the specified protocol types. For example, if both `IsRtmAbr` and `IsDashAbr` are set to `true`, the API queries ABR configurations for the RTM\-ABR and DASH\-ABR protocols.<br><br><br>* > If none of `IsHlsAbr`, `IsDashAbr`, and `IsRtmAbr` is set to `true`, the API queries regular transcoding configurations.<br> |

## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|CommonPresetList |Array of [TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/7714#transcodepresetvhostapp) |`-` |A list of built\-in configurations that match the query conditions. |
|CustomizePresetList |Array of [TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/7714#transcodepresetvhostapp) |`-` |A list of custom configurations that match the query conditions. |
|AllPresetList |Array of [TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/7714#transcodepresetvhostapp) |`-` |A list of all configurations that match the query conditions, including built\-in and custom configurations. |

### TranscodePresetVhostAPP

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Vhost |String |`push.example.com` |The domain name space. |
|App |String |`live` |The `AppName` field in the live stream URL. |
|TranscodePreset |Object of [TranscodePreset](https://docs.byteplus.com/en/docs/24/7714#transcodepreset) |`-` |Configuration details. |
|CopyParams |Boolean |`true` |Whether all original custom URL parameters in the ABR request URL are copied to each substream URL in the main playlist or manifest. Valid values:<br><br><br>* `true`: Copied.<br><br>* `false`: Not copied.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only for HLS\-ABR and DASH\-ABR.<br> |
|Order |Integer |`0` |The order of substreams in the HLS master playlist. Valid values:<br><br><br>* `0`: Descending by bitrate to list higher\-bitrate substreams first.<br><br>* `1`: Ascending by bitrate to list lower\-bitrate substreams first.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only for HLS\-ABR.<br> |
|URLMode |Integer |`0` |The URL mode of substreams in the HLS master playlist. Valid values:<br><br><br>* `0`: Substream URLs in the master playlist use absolute paths. The HLS\-ABR address example is `https://pull.example.com/live/test/abr.m3u8`.<br><br>* `1`: Substream URLs in the master playlist use relative paths. The HLS\-ABR address example is `https://pull.example.com/live/test_abr.m3u8`.<br><br><br>> **说明**<br><br><br><br>* > This parameter takes effect only for HLS\-ABR.<br><br><br>* > If [URL authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication) is enabled and `URLMode` is `1`, the `StreamName` used for authentication calculation is `{StreamName}_abr`. For example, if the HLS\-ABR address is `https://pull.example.com/live/test_abr.m3u8`, the `StreamName` used for authentication calculation is `test_abr`.<br> |

### TranscodePreset

|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Acodec |String |`aac` |Audio codec.<br><br><br>* `aac`: AAC.<br><br>* `copy`: Does not transcode the audio stream.<br><br>* `opus`: OPUS. |
|As |String |`0` |Whether to auto\-adjust the video dimensions.<br><br><br>* `0`: Disables auto\-adjustment, and stretches the video according to `Width` and `Height`.<br><br>* `1`: Enables auto\-adjustment, and scales the video according to `ShortSide` or `LongSide`. |
|AudioBitrate |Integer |`30` |Audio bitrate. Unit: kbps. |
|AutoTransResolution |Integer |`1` |Whether to constrain the transcoding resolution not to exceed the original stream resolution.<br><br><br>* `0`: Allow<br><br>* `1`: Constrain |
|AutoTransVb |Integer |`1` |Whether to constrain the transcoding bitrate not to exceed the original stream bitrate.<br><br><br>* `0`: Allow<br><br>* `1`: Constrain |
|AutoTransVr |Integer |`1` |Whether to constrain the transcoding frame rate not to exceed the original frame rate.<br><br><br>* `0`: Allow<br><br>* `1`: Constrain |
|BFrames |Integer |`3` |The maximum number of B\-frames between two reference frames. 0 means removing B\-frames. |
|FPS |Integer |`60` |Video frame rate. Unit: fps. |
|GOP |Integer |`2` |The maximum interval between IDR frames. Unit: seconds. |
|Height |Integer |`100` |Video height, in pixels. This parameter is valid when `Vcodec` is set to `h264` or `h265` and `As` is set to `0`.<br><br>> **说明**<br><br><br><br>* > The video is stretched according to Width and Height.<br><br><br>* > When either Width or Height is set to 0, the original video dimensions are preserved.<br> |
|LongSide |Integer |`200` |Long side of the video. This parameter is valid when `As` is set to `1`.<br><br>> **说明**<br><br><br><br>* > If you set both LongSide and ShortSide to 0, the original video dimensions are preserved.<br><br><br>* > If you set both LongSide and ShortSide to values other than 0, the video is stretched according to the value of ShortSide.<br> |
|Preset |String |`preset1` |The configuration name. |
|Roi |Boolean |`true` |Whether to transcode using low\-bitrate HD mode.<br><br><br>* `true`: Low\-bitrate HD mode.<br><br>* `false`: (default) Standard mode. |
|ShortSide |Integer |`100` |Short side of the video. This parameter is valid when `As` is set to `1`.<br><br>> **说明**<br><br><br><br>* > If you set both LongSide and ShortSide to 0, the original video dimensions are preserved.<br><br><br>* > If you set both LongSide and ShortSide to values other than 0, the video is stretched according to the value of ShortSide.<br> |
|StopInterval |Integer |`60` |The pause duration for the transcoding task, in seconds.<br><br>This parameter is valid when `TransType` is set to `Pull`. Valid values are `-1` and integers from 0 to 300. `-1` means the task does not stop when stream pulling stops. The default value is `60`. |
|SuffixName |String |`hd` |The suffix of the transcoded stream or ABR substream. |
|Vcodec |String |`h265` |Video codec.<br><br><br>* `h264`: H.264.<br><br>* `h265`: H.265.<br><br>* `copy`: Does not transcode the video stream. |
|VideoBitrate |Integer |`30` |Video bitrate. Unit: kbps. |
|Width |Integer |`200` |Video width, in pixels. This parameter is valid when `Vcodec` is set to `h264` or `h265` and `As` is set to `0`.<br><br>> **说明**<br><br><br><br>* > The video is stretched according to Width and Height.<br><br><br>* > When either Width or Height is set to 0, the original video dimensions are preserved.<br> |
|TransType |String |`Pull` |A transcoding task starts when:<br><br><br>* `Push`: The live stream starts.<br><br>* `Pull`: The transcoded stream is requested. |

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListVhostTransCodePreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "IsHlsAbr": true
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "2021072818053901022706413520787",
        "Action": "ListVhostTransCodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "AllPresetList": [
            {
                "App": "live01",
                "CopyParams": true,
                "Order": 0,
                "TranscodePreset": {
                    "Acodec": "aac",
                    "As": "1",
                    "AudioBitrate": 128,
                    "AutoTransResolution": 1,
                    "AutoTransVb": 1,
                    "AutoTransVr": 1,
                    "BFrames": 3,
                    "FPS": 25,
                    "GOP": 2,
                    "Height": 0,
                    "LongSide": 0,
                    "Preset": "cieovndlvj",
                    "Roi": false,
                    "ShortSide": 720,
                    "StopInterval": 60,
                    "SuffixName": "_hd",
                    "TransType": "Pull",
                    "Vcodec": "h264",
                    "VideoBitrate": 2048000,
                    "Width": 0
                },
                "URLMode": 0,
                "Vhost": "push.example.com"
            },
            {
                "App": "live",
                "CopyParams": true,
                "Order": 0,
                "TranscodePreset": {
                    "Acodec": "aac",
                    "As": "1",
                    "AudioBitrate": 128,
                    "AutoTransResolution": 1,
                    "AutoTransVb": 1,
                    "AutoTransVr": 1,
                    "BFrames": 3,
                    "FPS": 30,
                    "GOP": 2,
                    "Height": 0,
                    "LongSide": 0,
                    "Preset": "dybebfppng",
                    "Roi": false,
                    "ShortSide": 1080,
                    "StopInterval": 60,
                    "SuffixName": "_uhd",
                    "TransType": "Pull",
                    "Vcodec": "h264",
                    "VideoBitrate": 3200000,
                    "Width": 0
                },
                "URLMode": 0,
                "Vhost": "push.example.com"
            }
        ],
        "CommonPresetList": [],
        "CustomizePresetList": [
            {
                "App": "live",
                "CopyParams": true,
                "Order": 0,
                "TranscodePreset": {
                    "Acodec": "aac",
                    "As": "1",
                    "AudioBitrate": 128,
                    "AutoTransResolution": 1,
                    "AutoTransVb": 1,
                    "AutoTransVr": 1,
                    "BFrames": 3,
                    "FPS": 30,
                    "GOP": 2,
                    "Height": 0,
                    "LongSide": 0,
                    "Preset": "dybebfppng",
                    "Roi": false,
                    "ShortSide": 1080,
                    "StopInterval": 60,
                    "SuffixName": "_uhd",
                    "TransType": "Pull",
                    "Vcodec": "h264",
                    "VideoBitrate": 3200000,
                    "Width": 0
                },
                "URLMode": 0,
                "Vhost": "push.example.com"
            },
            {
                "App": "live01",
                "CopyParams": true,
                "Order": 0,
                "TranscodePreset": {
                    "Acodec": "aac",
                    "As": "1",
                    "AudioBitrate": 128,
                    "AutoTransResolution": 1,
                    "AutoTransVb": 1,
                    "AutoTransVr": 1,
                    "BFrames": 3,
                    "FPS": 25,
                    "GOP": 2,
                    "Height": 0,
                    "LongSide": 0,
                    "Preset": "cieovndlvj",
                    "Roi": false,
                    "ShortSide": 720,
                    "StopInterval": 60,
                    "SuffixName": "_hd",
                    "TransType": "Pull",
                    "Vcodec": "h264",
                    "VideoBitrate": 2048000,
                    "Width": 0
                },
                "URLMode": 0,
                "Vhost": "push.example.com"
            }
        ]
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/7714#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Empty |%s is required |The parameter is missing. Please check if the parameter specified in the error message is passed in. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
