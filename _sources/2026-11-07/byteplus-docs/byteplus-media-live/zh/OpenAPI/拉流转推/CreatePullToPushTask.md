---
title: "CreatePullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createpulltopushtask-2023-zh-CN"
---

调用 `CreatePullToPushTask` API 创建拉流转推任务，从直播流源或点播视频拉取内容。

<span id="Requirements"></span>
## 要求


* 计费情况：关于拉流转推价格，请参阅 [Relay](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-relay-1)。

* 请求频率限制：每个账号每秒最多 1 次查询。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=CreatePullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreatePullToPushTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|GroupName |String |否 |`default` |任务所属的分组名称。可调用 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 获取分组名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">主账号调用时，该字段为可选项。默认归属于 <code>default</code> 分组。若 <code>default</code> 分组不存在，将自动创建并绑定至 <code>default</code> 项目。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">子账号调用时，该字段为必填项。</div><br> |
|Title |String |否 |`task001` |拉流转推任务名称。可包含中文、英文字符及数字。最大长度：20 个字符。 |
|StartTime |Integer |是 |`1640891476` |拉流转推任务的开始时间，单位为秒。UNIX 时间戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">拉流转推任务最长时长为 7 天。</div><br> |
|EndTime |Integer |是 |`1640841476` |拉流转推任务的结束时间，单位为秒。UNIX 时间戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">拉流转推任务最长时长为 7 天。</div><br> |
|CallbackURL |String |否 |`http://example.mtime.cn/live/example/callbackapi` |用于接收拉流转推任务事件的回调地址。最大长度：512 个字符。 |
|Type |Integer |是 |`0` |素材类型。有效值包括：<br><br><br>* `0`：内容从直播流源拉取。<br><br>* `1`：内容从点播视频拉取。 |
|CycleMode |Integer |否 |`-1` |当 `Type` 设置为 `1` 时，可设置点播视频的循环播放模式。取值及含义如下。<br><br><br>* `-1`：列表无限循环播放<br><br>* 大于 0 的整数表示循环播放次数。 |
|DstAddr |String |否 |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|Domain |String |否 |`example.mtime.cn` |推流域名。当推流地址（DstAddr）为空时必须传递，否则该参数无效。 |
|App |String |否 |`live` |直播流 URL 中的 AppName 字段。当推流地址（DstAddr）为空时必须传递，否则该参数无效。 |
|Stream |String |否 |`stream-123` |直播流 URL 中的 StreamName 字段。当推流地址（DstAddr）为空时必须传递，否则该参数无效。 |
|SrcAddr |String |否 |`http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |当 `Type` 设置为 `0` 时，必须设置直播视频的拉流地址。最大长度：1,000 字符。 |
|SrcAddrS |字符串数组 |否 |`["https://pull.example.com/live/stream-123"]` |当你将 `Type` 设置为 `1` 时，必须设置点播视频列表。 |
|水印 |[水印](https://docs.byteplus.com/en/docs/24/107032#watermark) 对象 |否 |`-` |为拉流转推视频添加的水印配置信息。 |
|PullRequestHeaders |[PullRequestHeaders](https://docs.byteplus.com/en/docs/24/107032#pullrequestheaders) 对象 |否 |`-` |拉流请求中包含的 HTTP 请求头。如果直播源或点播源会校验拉流请求中的 Referer 或 User\-Agent 请求头，可以通过该参数配置所需的请求头。 |


<span id="watermark"></span>
### 水印


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|图片 |字符串 |是 |`data:image/png;base64,iVBORw0KGg****mCC` |水印图片的 Data URL。允许的图片文件大小范围为 100 B 到 2 MB。最大分辨率：1080×1080 像素。Data URL 格式：`data:[<mediatype>];[base64],<data>`，例如 `data:png;base64,iVBORw0KGg****mCC`。<br><br><br>* `mediatype`：图片格式，包括 `png`、`jpg` 和 `jpeg`。<br><br>* `data`：图片的 Base64 字符串。 |
|RelativePosX |浮点型 |是 |`0.1` |水平偏移，即水印左边缘与转码视频左边缘之间距离与视频宽度的比例。支持范围：0–1。 |
|RelativePosY |浮点型 |是 |`0.1` |垂直偏移，即水印上边缘与转码视频上边缘之间距离与视频高度的比例。支持范围：0–1。 |
|Ratio |浮点型 |是 |`0.1` |水印宽度与转码视频宽度的比例。支持范围：0–1。水印高度会自动调整为与宽度一致。 |


<span id="pullrequestheaders"></span>
### PullRequestHeaders


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Referer |字符串 |否 |`http://test.com` |拉流请求中包含的 Referer 请求头。如果直播源或点播源会校验请求来源，请指定所需的 Referer。 |
|UserAgent |字符串 |否 |`example-agent` |拉流请求中包含的 User\-Agent 请求头。如果直播源或点播源要求拉流请求携带特定的 User\-Agent，请指定所需的 User\-Agent。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关 API 专属返回调用结果参数，请参见下表。更多详情请参阅 [请求与返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|任务Id |字符串 |`8fde6aa0281d9f6e15e6059a6e242365` |任务的唯一标识符。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreatePullToPushTask&Version=2023-01-01
{
    "Title": "task001",
    "StartTime": 1640891476,
    "EndTime": 1640841476,
    "CallbackURL": "http://example.com/live/callback",
    "Type": 0,
    "DstAddr": "rtmp://push.example.com/live/example_stream",
    "SrcAddr": "http://pull.example.com/live/example_stream.mp4",
    "PullRequestHeaders": {
        "Referer": "http://test.com",
        "UserAgent": "user-agent"
    }
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202112311457430101742350380352BCB2",
        "Action": "CreatePullToPushTask",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TaskId": "8fde6aa0281d*******9a6e242365"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107032#request-parameters) 接口行为进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号存在欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |请求创建的资源（包括域名空间、域名、应用、配置、证书）超出限制。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
