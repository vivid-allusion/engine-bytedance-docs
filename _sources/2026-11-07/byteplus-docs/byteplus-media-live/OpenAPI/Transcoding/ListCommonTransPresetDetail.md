---
title: "ListCommonTransPresetDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023"
---

Call the `ListCommonTransPresetDetail` API to query the detailed of the default transcoding configuration.

<span id="requirements"></span>
## Requirements

Rate limit: 10 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=ListCommonTransPresetDetail&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCommonTransPresetDetail` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PresetList |Array of String |No |`["preser1","preset2"]` |A list of transcoding templates. If unspecified, all default transcoding templates will be queried. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|NarrowBandHDPresetDetail |Array of [PresetDetail](https://docs.byteplus.com/en/docs/24/27420#presetdetail) |`-` |Details of a low\-bitrate HD template. |
|StandardPresetDetail |Array of [PresetDetail](https://docs.byteplus.com/en/docs/24/27420#presetdetail) |`-` |Details of a standard template. |


<span id="presetdetail"></span>
### PresetDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|SuffixName |String |`hd` |Suffix of the transcoded stream. |
|VideoBitrate |Integer |`1000000` |Video bitrate. Unit: Kbps. |
|Vcodec |String |`h265` |Video codec.<br><br><br>* `h264`: H.264.<br><br>* `h265`: H.265.<br><br>* `copy`: Does not transcode the video stream. |
|AudioBitrate |Integer |`30` |Audio bitrate. Unit: Kbps. |
|Acodec |String |`aac` |Audio codec.<br><br><br>* `aac`: AAC.<br><br>* `copy`: Does not transcode the audio stream.<br><br>* `opus`: OPUS. |
|FPS |Integer |`60` |Video frame rate. Unit: fps. |
|GOP |Integer |`2` |The maximum interval between IDR frames. Unit: second. |
|Width |Integer |`100` |Width of the video in pixel(px). Valid when Vcodec is set to h264 and h265 and As is set to 0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The video is stretched according to Width and Height.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When either Width or Height is set to 0, the original video dimensions are preserved.</div><br> |
|Height |Integer |`50` |Height of the video in pixel(px). Valid when Vcodec is set to h264 and h265 and As is set to 0.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">The video is stretched according to Width and Height.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When either Width or Height is set to 0, the original video dimensions are preserved.</div><br> |
|As |String |`1` |Whether to auto\-adjust the video dimensions.<br><br><br>* `0`: Disables auto\-adjustment, and stretches the video according to `Width` and `Height`.<br><br>* `1`: Enables auto\-adjustment, and scales the video according to `ShortSide` or `LongSide`. |
|ShortSide |Integer |`100` |Short side of the video in pixel(px). Valid when As is set to 1.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both LongSide and ShortSide to 0, the original video dimensions are preserved.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both LongSide and ShortSide to values other than 0, the video is stretched according to the value of ShortSide.</div><br> |
|LongSide |Integer |`200` |Long side of the video in pixel(px). Valid when As is set to 1.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both LongSide and ShortSide to 0, the original video dimensions are preserved.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both LongSide and ShortSide to values other than 0, the video is stretched according to the value of ShortSide.</div><br> |
|BFrames |Integer |`3` |The maximum number of B\-frames between two reference frames. 0 means removing B\-frames. |
|Roi |Boolean |`true` |Whether to transcode using low\-bitrate HD mode.<br><br><br>* `true`: Low\-bitrate HD mode.<br><br>* `false`: (default) Standard mode. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=ListCommonTransPresetDetail&Version=2023-01-01
{
    "PresetList": [
        "preset1",
        "preset2"
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestID": "20220426203705010211197144119377C1",
        "Action": "ListCommonTransPresetDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "StandardPresetDetail": [],
        "NarrowBandHDPresetDetail": []
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27420#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the service or bill occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
