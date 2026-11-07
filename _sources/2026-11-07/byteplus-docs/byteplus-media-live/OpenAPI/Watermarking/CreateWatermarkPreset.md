---
title: "CreateWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023"
---

Call the `CreateWatermarkPreset` API to add a watermark configuration for transcoded streams or ABR (adaptive bitrate) substreams.

<span id="requirements"></span>
## Requirements


* Rate limit: 1 query per second per account.

* Prerequisites:

   * You have added a transcoding configuration or ABR configuration for the specified `AppName` under the domain name space where you want to add the watermark configuration. For more information, see [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023) or [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023).

   * Prepare a JPG or PNG image as the watermark. The image size cannot exceed 2 MB, and the resolution cannot exceed 1080 × 1080 px. PNG images can contain transparency.

* Effective time: After you add, update, or delete a watermark configuration, the change takes effect in 3 to 5 minutes. Transcoded streams or ABR substreams generated after the change takes effect use the latest watermark configuration. Existing transcoded streams or ABR substreams generated before the change takes effect do not automatically apply the update. If no transcoded stream or ABR substream exists before the change, wait for the configuration to take effect. If a transcoded stream or ABR substream already exists before the change and you need to use the updated configuration, wait 3 to 5 minutes after the configuration is added, updated, or deleted, and then push the stream again.


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=CreateWatermarkPreset&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`CreateWatermarkPreset` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Vhost |String |Yes |`push.example.com` |The domain name space, which is the domain name space to which the domain name in the live stream URL belongs. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to get the domain name space to which the domain name belongs. |
|App |String |Yes |`live` |The `AppName` field in the live stream URL. It can contain uppercase and lowercase letters (A \- Z, a \- z), digits (0 \- 9), underscores (_), hyphens (\-), and periods (.). The length must be 1 to 30 characters. |
|Stream |String |No |`example_stream` |The `StreamName` field in the live stream URL. It can contain uppercase and lowercase letters (A \- Z, a \- z), digits (0 \- 9), underscores (_), hyphens (\-), and periods (.). The length must be 1 to 100 characters.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">Leave this parameter empty to apply the watermark configuration to all transcoded streams and ABR substreams under the specified <code>AppName</code>.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you specify a <code>StreamName</code>, the watermark configuration applies only to the specified <code>StreamName</code> under the specified <code>AppName</code>.</div><br> |
|Orientation |String |No |`vertical` |Orientation of the watermarked video. Valid values:<br><br><br>* `vertical`: Portrait.<br><br>* `horizontal`: Landscape. |
|Picture |String |No |`data:image/png;base64,iVBORw0KGg****mCC` |The encoded watermark image string. The image size cannot exceed 2 MB, the minimum size is 100 bytes, and the resolution cannot exceed 1080 × 1080 px. The image data URL format is: `data:[<mediatype>];[base64],<data>`.<br><br><br>* `mediatype`: The image type. `png`, `jpg`, and `jpeg` formats are supported.<br><br>* `data`: The base64\-encoded image string. |
|PosX |Float |No |`0` |Horizontal offset, which indicates the distance between the left edge of the watermark and the left edge of the transcoded stream or ABR substream image. A relative ratio is used. Valid range: [0,1].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when <code>WatermarkMode</code> is set to <code>static</code>.</div><br> |
|PosY |Float |No |`1.0` |Vertical offset, which indicates the distance between the top edge of the watermark and the top edge of the transcoded stream or ABR substream image. A relative ratio is used. Valid range: [0,1].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when <code>WatermarkMode</code> is set to <code>static</code>.</div><br> |
|RelativeWidth |Float |No |`1.0` |The relative watermark width, which is the ratio of the watermark width to the transcoded stream or ABR substream image width. Valid range: [0,1]. The watermark height scales proportionally with the width. |
|WatermarkMode |String |No |`dynamic` |The watermark type. The default value is `static`. Valid values:<br><br><br>* `static`: Static watermark. The watermark is fixed at the specified position.<br><br>* `dynamic`: Dynamic watermark. The watermark moves during playback, which increases the difficulty of unauthorized screen recording and misuse. |
|DynamicMode |String |No |`dynamic_move_curve` |The dynamic watermark effect. Valid values:<br><br><br>* `dynamic_move_curve`: Dynamic curve movement. The watermark moves continuously and changes direction when it reaches the video edges.<br><br>* `dynamic_blink`: Dynamic blinking. The watermark appears at a new random position in the video at the specified frequency.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter is required when <code>WatermarkMode</code> is set to <code>dynamic</code>.</div><br> |
|DynamicSpeedLevel |Integer |No |`1` |The dynamic speed. The default value is `1`. Valid values are integers from 1 to 10. A larger value indicates faster changes.<br><br><br>* When `DynamicMode` is set to `dynamic_move_curve`, this speed controls the movement speed of the watermark.<br><br>* When `DynamicMode` is set to `dynamic_blink`, this speed controls the frequency at which the watermark changes position.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This parameter takes effect only when <code>WatermarkMode</code> is set to <code>dynamic</code>.</div><br> |
|TransSuffixs |String |No |`_hd,_uhd` |The transcoded stream or ABR substream suffixes to which the watermark configuration applies. By default, the watermark configuration applies to all transcoded stream or ABR substream suffixes under the current `AppName`. You can specify 1\-20 suffixes, separated by commas (,).<br><br>You can call [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) and obtain the transcoded stream or ABR substream suffixes from the returned parameter `SuffixName`. |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ID |Integer |`1234567` |The watermark template ID. |
|PresetName |String |`preset` |The watermark template name. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=CreateWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Orientation": "vertical",
    "RelativeWidth": 0.185,
    "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
    "WatermarkMode": "dynamic",
    "DynamicMode": "dynamic_move_curve",
    "DynamicSpeedLevel": 1,
    "TransSuffixs": "_hd,_uhd"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "Action": "CreateWatermarkPreset",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "ID": 1234567,
        "PresetName": "preset"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27461#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Empty |%s is required |The parameter is missing. Please check if the parameter specified in the error message is passed in. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.Preset |an internal error related to preset occurred, please contact the administrator. |An internal error related to the preset occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |
