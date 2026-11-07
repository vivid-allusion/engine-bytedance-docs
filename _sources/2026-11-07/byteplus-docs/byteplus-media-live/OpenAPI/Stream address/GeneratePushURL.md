---
title: "GeneratePushURL"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023"
---

Call the `GeneratePushURL` API to generate the push stream addresses for a specified stream.

<span id="requirements"></span>
## Requirements

Rate limit: 25 queries per second per account.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com/?Action=GeneratePushURL&Version=2023\-01\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters) in addition to API\-specific parameters.

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GeneratePushURL` |The API operation. |
|Version |String |Yes |`2023-01-01` |The version of this API operation. Current version: 2023\-01\-01. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Domain |String |Yes |`push.example.com` |The domain name for stream pushing. You can call the [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API or visit the [Domains](https://console.byteplus.com/live/main/domain/list) page in the BytePlus MediaLive console to obtain the domain name. |
|App |String |Yes |`live` |The AppName field in the push stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 30 characters. |
|Stream |String |Yes |`example_stream` |The StreamName field in the push stream URL. It can include uppercase letters (A\-Z), lowercase letters (a\-z), numbers (0\-9), underscores (_), hyphens (\-), and periods (.), with a length ranging from 1 to 100 characters. |
|ValidDuration |Integer |No |`5000` |The addresses expire after the length of time specified by `ValidDuration`, starting from the moment the addresses are generated. Unit: second. Valid range: \> 0. Default value: 604800 (seven days).<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When a push stream address expires, the ongoing stream pushing will not be affected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both <code>ValidDuration</code> and <code>ExpiredTime</code>, only the setting of <code>ExpiredTime</code> takes effect.</div><br> |
|ExpiredTime |String |No |`2023-08-19T16:07:25Z` |Expiration time (Local time in RFC 3339 format with second precision) of the addresses, in seconds. The default expiration time is seven days after the addresses are generated.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">When a push stream address expires, the ongoing stream pushing will not be affected.</div><br><br><br>* <div data-tips="true" data-tips-type="tip">If you set both <code>ValidDuration</code> and <code>ExpiredTime</code>, only the setting of <code>ExpiredTime</code> takes effect.</div><br> |


<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PushURLList |Array of String |`["rtmp://push.example.com/live/example_stream"]` |The RTMP push stream address. |
|PushURLListDetail |Array of [PushURLListDetail](https://docs.byteplus.com/en/docs/24/27413#pushurllistdetail) |`-` |The details of the RTMP push stream address. |
|TsOverSrtURLList |Array of String |`["srt://push.example.com:9000?streamid=#!::h=push.example.com,r=live/example_stream,m=publish"]` |The TS over SRT push stream address. |
|RtmpOverSrtURLList |Array of String |`["rtmp://push.example.com:1999/live/example_stream"]` |The RTMP over SRT push stream address. |
|RtmURLList |Array of String |`["http://push.example.com/live/example_stream.sdp"]` |The RTM push stream address. |
|AuthType |String |`TypeB` |The URL authentication type used to generate push stream addresses. If the value is empty, it indicates that URL authentication is not configured for the current domain.<br><br><br>* `TypeA`: Type A.<br><br>* `TypeB`: Type B.<br><br>* `TypeC`: Type C.<br><br>* `TypeCustom`: Custom type.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">For more information on type A, B, or C, see <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">Configuring URL authentication</a>.</div><br> |


<span id="pushurllistdetail"></span>
### PushURLListDetail


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|URL |String |`rtmp://live.push.example.com/live/example_stream` |The RTMP push stream address. |
|DomainApp |String |`rtmp://push.example.com/live/` |OBS push stream address. |
|StreamSign |String |`example_stream` |OBS stream key. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com/?Action=GeneratePushURL&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ValidDuration": 5000,
    "ExpiredTime": "2023-08-19T16:07:25Z"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GeneratePushURL",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "PushURLList": [
            "rtmp://push.example.com/live/example_stream"
        ],
        "PushURLListDetail": [
            {
                "URL": "rtmp://live.push.example.com/live/example_stream",
                "DomainApp": "rtmp://push.example.com/live/",
                "StreamSign": "example_stream"
            }
        ],
        "TsOverSrtURLList": [
            "srt://push.example.com:9000?streamid=#!::h=push.example.com,r=live/example_stream,m=publish"
        ],
        "RtmpOverSrtURLList": [
            "rtmp://push.example.com:1999/live/example_stream"
        ],
        "RtmURLList": [
            "http://push.example.com/live/example_stream.sdp"
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
|400 |InvalidParam |\- |The input parameters are invalid or do not meet the requirements. Please refer to the [Request Parameters](https://docs.byteplus.com/en/docs/24/27413#request-parameters) description for inspection. |
|400 |InvalidParam.BindError |Request parameter error, please check input data |The parameter failed validation. Please check if the data type is correct. |
|400 |InvalidParam.Format |%s format error |The parameter format is incorrect. Please check if there are illegal characters or URL format errors in the specified parameter in the error message. |
|400 |InvalidParam.OutOfRange |%s should be one of {[%s]}%s should be between %d and %d |The parameter exceeds the allowable range. Please check if the value of the specified parameter in the error message exceeds the value range. |
|400 |InvalidParam.TimeLogic |startTime later than endTime, etc. |The passed\-in time parameter does not conform to the logic of time. Please check if the following problems exist:The start time is later than the end time.The expiration time is earlier than the current time. |
|403 |RequestForbidden |\- |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.AccountIDNotAllowed |this AccountID does not have permission to access the corresponding resource, please check the request parameters |The request is rejected because there are no requested resources under the current account (resources include domain name space, domain name, app name, configuration, and certificate). |
|403 |RequestForbidden.BillingStatus |Billing status is not available for the AccountID, please activate the service or recharge. |The video live streaming service has not been enabled or the account is in arrears, resulting in an unavailable bill. Please check the service activation status and account arrears status. |
|404 |ResourceNotFound |\- |The resource (including domain name space, domain name, app name, configuration, and certificate) was not found. It is recommended to retry. If the error code is still returned, please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|500 |InternalError.VhostOrDomain |an internal error related to vhost or domain occurred, please contact the administrator. |An internal error related to the domain name (`Domain`) occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |An internal error occurred. Please [contact support](https://console.byteplus.com/workorder/create). |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |Internal Service is timeout. Please [contact support](https://console.byteplus.com/workorder/create). |


&nbsp;
