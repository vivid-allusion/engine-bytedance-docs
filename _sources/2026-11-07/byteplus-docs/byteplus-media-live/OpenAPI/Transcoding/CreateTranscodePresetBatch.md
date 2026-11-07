---
title: "CreateTranscodePresetBatch"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023"
---

Call the `CreateTranscodePresetBatch` API to batch create ABR substream transcoding configurations.

## Requirements

* Substreams are created by transcoding original streams to different resolutions and bitrates, and this process incurs transcoding fees. For pricing details, please refer to [Transcoding](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding).

* Updating a transcoding configuration will take effect in 3\-5 minutes.

* Updating and removing a transcoding configuration will not affect the ongoing streams. You must stop and restart the streams to apply the change.

## HTTP request

* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateTranscodePresetBatch&Version=2023\-01\-01

## Request parameters

### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

### Query

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateTranscodePresetBatch` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |

### Body parameters

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |Yes |`hls-abr` |Select the protocol type for batch creation of ABR configurations. Valid values:<br><br><br>* `hls-abr`: Create ABR configurations with HLS\-ABR enabled.<br><br>* `dash-abr`: Create ABR configurations with DASH\-ABR enabled.<br><br>* `rtm-abr`: Create ABR configurations with RTM\-ABR enabled.<br><br>* `abr`: Create ABR configurations with both HLS\-ABR and DASH\-ABR enabled.<br><br><br>> **说明**<br><br><br>> This parameter can be combined with `IsRtmAbr` to enable RTM\-ABR together with other ABR protocol types:<br><br><br><br>* > Set this parameter to `hls-abr` and `IsRtmAbr` to `true` to enable HLS\-ABR and RTM\-ABR.<br><br><br>* > Set this parameter to `dash-abr` and `IsRtmAbr` to `true` to enable DASH\-ABR and RTM\-ABR.<br><br><br>* > Set this parameter to `abr` and `IsRtmAbr` to `true` to enable HLS\-ABR, DASH\-ABR, and RTM\-ABR.<br> |
|CopyParams |Boolean |No |`true` |Whether to copy all original custom URL parameters in the ABR request URL to each substream URL in the main playlist or manifest.<br><br>For example, if the HLS\-ABR request URL is `https://pull.example.com/live/test/abr.m3u8?uid=10001&scene=live_home`, with the parameter value set to `true`, the substream URLs in the main M3U8 playlist carry the same parameters, such as `/live/test_hd/index.m3u8?uid=10001&scene=live_home` and `/live/test_sd/index.m3u8?uid=10001&scene=live_home`.<br><br>Valid values:<br><br><br>* `true`: Copy.<br><br>* `false`: Do not copy.<br><br><br>> **说明**<br><br><br><br>* > This parameter takes effect only for HLS\-ABR and DASH\-ABR.<br><br><br>* > You cannot set this parameter to `true` if time shifting is enabled.<br> |
|PresetList |Array of [PresetList](https://docs.byteplus.com/en/docs/24/35785#presetlist) |Yes |`-` |Detailed parameters of ABR substream transcoding configurations. |
|Order |Integer |No |`0` |The order of substreams in the HLS master playlist. Default value: `0`. Valid values:<br><br><br>* `0`: Descending by bitrate to list higher\-bitrate substreams first.<br><br>* `1`: Ascending by bitrate to list lower\-bitrate substreams first.<br><br><br>> **说明**<br><br><br>> This parameter takes effect only when you contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable this feature and set `Type` to `hls-abr` or `abr`.<br> |
|URLMode |Integer |No |`0` |The URL mode of substreams in the HLS master playlist. Default value: `0`. Valid values:<br><br><br>* `0`: Substream URLs in the master playlist use absolute paths. The HLS\-ABR address example is `https://pull.example.com/live/test/abr.m3u8`.<br><br>* `1`: Substream URLs in the master playlist use relative paths. The HLS\-ABR address example is `https://pull.example.com/live/test_abr.m3u8`.<br><br><br>> **说明**<br><br><br><br>* > This parameter takes effect only when you contact [technical support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980) to enable this feature and set `Type` to `hls-abr` or `abr`.<br><br><br>* > If [URL authentication](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication) is enabled and `URLMode` is set to `1`, the `StreamName` used for authentication calculation is `{StreamName}_abr`. For example, if the HLS\-ABR address is `https://pull.example.com/live/test_abr.m3u8`, the `StreamName` used for authentication calculation is `test_abr`.<br> |

### PresetList

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name space which the domain belongs. |
|App |String |Yes |`live` |The AppName field in the live stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|SuffixName |String |Yes |`hd` |The suffix of the transcoding stream, which supports characters consisting of uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), and hyphens (\-), and has a length of 1 to 10 characters.<br><br>The transcoding suffix is typically used in the form of a stream name suffix. Common identifiers include `sd`, `hd`, `uhd`. For example, if the identifier for the transcoding configuration is `hd`, the stream name for the transcoded stream when pulled would be `original stream name_hd`. |
|VideoBitrate |Integer |Yes |`1000000` |Video bitrate, measured in bps, with a value range of [0,30000000]. |
|Vcodec |String |Yes |`h265` |Video Codec Formats:<br><br><br>* `h264`: Use the H.264 encoding format;<br><br>* `h265`: Use the H.265 encoding format;<br><br><br>> **说明**<br><br><br>> All ABR substreams within the same stream should have the same video codec format configured.<br> |
|AudioBitrate |Integer |No |`50` |Audio bitrate, measured in kbps. |
|Acodec |String |No |`aac` |Audio Encoding Formats. The default format is AAC, and the following 3 types are supported:<br><br><br>* `aac`: Uses AAC encoding format;<br><br>* `copy`: Does not transcode, all audio encoding parameters are ineffective;<br><br>* `opus`: Uses Opus encoding format. |
|FPS |Integer |No |`25` |Video frame rate, measured in fps (frames per second), ranges from [0,60], with a default setting of 25fps. The higher the frame rate, the smoother the video playback. |
|GOP |Integer |Yes |`2` |The maximum interval between IDR frames, measured in seconds, ranges from [1,30].<br><br>> **说明**<br><br><br>> The GOP configuration must be the same for all ABR substreams within the same stream.<br> |
|Width |Integer |Yes |`1000` |Video width, ranging from [150, 1920]. |
|Height |Integer |Yes |`500` |Video height, the value range is [150,1920]. |
|Roi |Boolean |No |`true` |Whether to transcode using low\-bitrate HD mode.<br><br><br>* `true`: Low\-bitrate HD mode.<br><br>* `false`: (default) Standard mode.<br><br><br>> **说明**<br><br><br>> All ABR substreams of the same stream should be configured with the same transcoding method.<br> |
|AutoTransResolution |Integer |No |`1` |Whether to enable transcoding to not exceed the source stream resolution, the default value of `1` means enabled. When enabled, if the source stream resolution is lower than the transcoding configuration resolution (i.e., both the width and height of the source stream are lower than those of the transcoding configuration), the transcoding will be conducted at the source stream video resolution.<br><br><br>* `0`: Disabled;<br><br>* `1`: Enabled. |
|AutoTransVb |Integer |No |`1` |Enable transcoding only at a bitrate that does not exceed the source stream's bitrate. The default value, `1`, indicates that this feature is enabled. When enabled, if the source stream's bitrate is lower than the configured transcoding bitrate, the transcoding will be performed at the source stream's video bitrate.<br><br><br>* `0`: Disable;<br><br>* `1`: Enable. |
|AutoTransVr |Integer |No |`1` |Enable transcoding frame rate not to exceed the source stream frame rate, the default value is `1` indicating it is enabled. When enabled, if the source stream frame rate is lower than the transcoding configuration frame rate, transcoding will be performed according to the source stream video frame rate.<br><br><br>* `0`: Disabled;<br><br>* `1`: Enabled. |
|TranscodeStruct |Object of [TranscodeStruct](https://docs.byteplus.com/en/docs/24/35785#transcodestruct) |No |`-` |Transcoding Information. |

### TranscodeStruct

|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Type |String |No |`Pull` |A transcoding task starts when:<br><br><br>* `Push`: the live stream initiates.<br><br>* `Pull`: (default) the transcoded stream is requested.<br><br><br>> **说明**<br><br><br>> The type should be configured the same for all ABR substreams of the same stream.<br> |
|IsRtmAbr |Boolean |No |`false` |Whether to enable RTM\-ABR when creating the ABR configuration. Default value: `false`. Valid values:<br><br><br>* `true`: Enable RTM\-ABR.<br><br>* `false`: Do not enable RTM\-ABR. |

## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

## Samples

### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateTranscodePresetBatch&Version=2023-01-01
{
    "Type": "hls-abr",
    "CopyParams": true,
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SuffixName": "hd",
            "VideoBitrate": 1000000,
            "Vcodec": "h265",
            "FPS": 25,
            "GOP": 2,
            "Width": 1000,
            "Height": 500,
            "AudioBitrate": 50,
            "Acodec": "aac",
            "AutoTransResolution": 1,
            "AutoTransVb": 1,
            "AutoTransVr": 1,
            "Roi": true,
            "TranscodeStruct": {
                "Type": "Pull"
            }
        },
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SuffixName": "ld",
            "VideoBitrate": 500000,
            "Vcodec": "h265",
            "FPS": 25,
            "GOP": 2,
            "Width": 1000,
            "Height": 500,
            "AudioBitrate": 50,
            "Acodec": "aac",
            "AutoTransResolution": 1,
            "AutoTransVb": 1,
            "AutoTransVr": 1,
            "Roi": true,
            "TranscodeStruct": {
                "Type": "Pull"
            }
        }
    ]
}
```

### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "CreateTranscodePresetBatch",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```

## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).

|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request parameters](https://docs.byteplus.com/en/docs/24/35785#request-parameters) section. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |The internal service timed out. Please [contact support](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980). |
