---
title: "UpdatePullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023"
---

Call the `UpdatePullToPushTask` API to update the information of a Relay task.

<span id="requirements"></span>
## Requirements

Rate limit: 1 query per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=UpdatePullToPushTask&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`UpdatePullToPushTask` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|TaskId |String |Yes |`8fde6aa0281*********59a6e242365` |The task ID. You can call the [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) API to obtain the task ID. |
|Title |String |No |`task001` |The name of the relay task is composed of 1 to 20 Chinese characters, upper and lower case letters and numbers. By default, it is empty, indicating that the task name is not modified. |
|StartTime |Integer |Yes |`1640891476` |The start time of the relay task, in seconds. UNIX timestamp.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum duration of a relay task is 7 days.</div><br> |
|EndTime |Integer |Yes |`1640891976` |The end time of the relay task, in seconds. UNIX timestamp.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The maximum duration of a relay task is 7 days.</div><br> |
|CallbackURL |String |No |`http://example.mtime.cn/live/example/callbackapi` |The callback address for receiving relay task events. Maximum length: 512 characters. |
|Type |Integer |Yes |`0` |The stream source type. Valid values include:<br><br><br>* `0`: The streamed content is pulled from a live\-stream source.<br><br>* `1`: The streamed content is pulled from on\-demand videos. |
|CycleMode |Integer |No |`-1` |When you set `Type` as `1`, you can set the loop playback mode of on\-demand videos. Values and meanings are as follows.<br><br><br>* `-1`: Infinite list loop<br><br>* An integer greater than 0 indicates the number of times of loop playback. |
|DstAddr |String |No |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |The push stream address. |
|Domain |String |No |`push.example.com` |Domain name for stream pushing. It must be passed when the push streaming address (DstAddr) is empty; otherwise, this parameter does not take effect. |
|App |String |No |`live` |Appname field stream pushing. It must be passed when the push streaming address (DstAddr) is empty; otherwise, this parameter does not take effect. |
|Stream |String |No |`stream-123` |StreamName field stream pushing. It must be passed when the push streaming address (DstAddr) is empty; otherwise, this parameter does not take effect. |
|SrcAddr |String |No |`http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |When you set `Type` as `0`, you must set the pull stream address of live video. Maximum length: 1,000 characters. |
|SrcAddrS |Array of String |No |`["http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |When you set `Type` as `1`, you must set the list of on\-demand video. |
|Watermark |Object of [Watermark](https://docs.byteplus.com/en/docs/24/27475#watermark) |No |`-` |The watermark configuration information added for the relay video. |
|GroupName |String |No | |The group name to which the task belongs. You can call the [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API to obtain the group name.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When using the main account to call, it is not a required field and will be defaulted to joining the <code>default</code> group by default. When the <code>default</code> group does not exist, it will be created by default and bound to the <code>default</code> project.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">When using the sub\-account to call, it is a required field.</div><br> |


<span id="watermark"></span>
### Watermark


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Picture |String |Yes |`data:image/png;base64,iVBORw0KGg****mCC` |Data URL of the watermark image. The allowed image file size ranges from 100 B to 2 MB. Maximum resolution: 1080×1080 pixels. Data URL format: `data:[<mediatype>];[base64],<data>`, for example `data:png;base64,iVBORw0KGg****mCC`.<br><br><br>* `mediatype`: Image format, including `png`, `jpg`, and `jpeg`.<br><br>* `data`: Base64 string of the image. |
|RelativePosX |Float |Yes |`0.1` |Horizontal offset, which is the ratio of the distance between the left edge of the watermark and the left edge of the transcoded video to the width of the video. Valid range: 0–1. |
|RelativePosY |Float |Yes |`0.1` |Vertical offset, which is the ratio of the distance between the top edge of the watermark and the top edge of the transcoded video to the height of the video. Valid range: 0–1. |
|Ratio |Float |Yes |`0.1` |The ratio of the width of the watermark to that of the transcoded video. Valid range: 0–1. The height of the watermark will be auto\-adjusted to its width. |


<span id="response-parameters"></span>
## Response parameters

This API only returns [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/request-response) in the response.

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=UpdatePullToPushTask&Version=2023-01-01
{
    "Type": 0,
    "DstAddr": "rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4",
    "EndTime": 1640891476,
    "SrcAddr": "http://example.mtime.cn/Video/2003/02/04/mp4/190204084208765161.mp4",
    "TaskId": "8fde6aa0281d9f6e15e6059a6e242365",
    "StartTime": 1640841476,
    "Title": "suexample007",
    "CallbackURL": "http://example.mtime.cn/live/example/callbackapi"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311522300102252431180946DD57",
        "Action": "UpdatePullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|200 |CommonErr |\- |Uncategorized error. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Format |%s format error |The parameter format is incorrect. Please check if there are illegal characters or URL format errors in the specified parameter in the error message. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllow |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|429 |RequestLimitExceeded |\- |The resource (including domain name space, domain name, app name, configuration, certificate) requested to be created exceeds the limit. |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
