---
title: "GeneratePushURL"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-generatepushurl-2023-zh-CN"
---

调用`GeneratePushURL` API，为指定流生成推流地址。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多25次请求。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=GeneratePushURL&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 在调用时，除需传入 API 专属参数外，还需传入[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`GeneratePushURL` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |推流域名。可通过调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面获取域名。 |
|应用 |String |是 |`live` |推流地址中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1~30个字符。 |
|Stream |String |是 |`example_stream` |推流地址中的 StreamName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1~100个字符。 |
|ValidDuration |Integer |否 |`5000` |推流地址自生成时刻起，经过`ValidDuration`指定的时长后失效。单位：秒。支持范围：\> 0。默认值：604800（七天）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">推流地址过期后，正在进行的推流不会受到影响。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同时设置<code>ValidDuration</code>和<code>ExpiredTime</code>，仅<code>ExpiredTime</code>生效。</div><br> |
|ExpiredTime |String |否 |`2023-08-19T16:07:25Z` |推流地址的过期时间（本地时间，RFC 3339 格式，精确到秒），单位为秒。默认过期时间为推流地址生成后七天。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">推流地址过期后，正在进行的推流不会受到影响。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同时设置<code>ValidDuration</code>和<code>ExpiredTime</code>，仅<code>ExpiredTime</code>生效。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

关于 API 专属的返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PushURLList |Array of String |`["rtmp://push.example.com/live/example_stream"]` |RTMP 推流地址。 |
|PushURLListDetail |Array of [PushURLListDetail](https://docs.byteplus.com/en/docs/24/107039#pushurllistdetail) |`-` |RTMP 推流地址详情。 |
|TsOverSrtURLList |Array of String |`["srt://push.example.com:9000?streamid=#!::h=push.example.com,r=live/example_stream,m=publish"]` |TS over SRT 推流地址。 |
|RtmpOverSrtURLList |Array of String |`["rtmp://push.example.com:1999/live/example_stream"]` |RTMP over SRT 推流地址。 |
|RtmURLList |Array of String |`["http://push.example.com/live/example_stream.sdp"]` |RTM 推流地址。 |
|AuthType |String |`TypeB` |用于生成推流地址的 URL 鉴权类型。若该值为空，表示当前域名未配置 URL 鉴权。<br><br><br>* `TypeA`：A 类型。<br><br>* `TypeB`：B 类型。<br><br>* `TypeC`：C 类型。<br><br>* `TypeCustom`：自定义类型。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">关于 A、B、C 类型的更多信息，请参见<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/docs-url-authentication">配置 URL 鉴权</a>。</div><br> |


<span id="pushurllistdetail"></span>
### PushURLListDetail


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|URL |String |`rtmp://live.push.example.com/live/example_stream` |RTMP 推流地址。 |
|DomainApp |字符串 |`rtmp://push.example.com/live/` |OBS 推流地址。 |
|StreamSign |字符串 |`example_stream` |OBS 流密钥。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

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


<span id="Sample response"></span>
### 返回示例

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


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107039#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|400 |InvalidParam.TimeLogic |startTime 晚于 endTime 等。 |传入的时间参数不符合时间逻辑。请检查是否存在以下问题：开始时间晚于结束时间。过期时间早于当前时间。 |
|403 |RequestForbidden |*  |因当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |因当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 未开通计费情况，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致计费情况不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生与 vhost 或域名相关的内部错误，请联系管理员。 |发生与域名（`Domain`）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
