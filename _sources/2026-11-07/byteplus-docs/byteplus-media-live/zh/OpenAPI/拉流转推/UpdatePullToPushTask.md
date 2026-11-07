---
title: "UpdatePullToPushTask"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023-zh-CN"
---

调用 `UpdatePullToPushTask` API，更新拉流转推任务的信息。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 1 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=UpdatePullToPushTask&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdatePullToPushTask` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|TaskId |String |是 |`8fde6aa0281*********59a6e242365` |任务 ID。可调用 [ListPullToPushTask](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushtask-2023) API 获取任务 ID。 |
|Title |String |否 |`task001` |拉流转推任务名称由 1 到 20 个汉字、大小写字母和数字组成。默认为空，表示任务名称不修改。 |
|StartTime |Integer |是 |`1640891476` |拉流转推任务的开始时间，单位为秒。UNIX 时间戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">拉流转推任务最大时长为 7 天。</div><br> |
|EndTime |Integer |是 |`1640891976` |拉流转推任务的结束时间，单位为秒。UNIX 时间戳。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">拉流转推任务最大时长为 7 天。</div><br> |
|CallbackURL |String |否 |`http://example.mtime.cn/live/example/callbackapi` |用于接收拉流转推任务事件的回调地址。最大长度：512 个字符。 |
|Type |Integer |是 |`0` |流素材类型。有效值包括：<br><br><br>* `0`: 拉取直播流作为素材。<br><br>* `1`: 拉取点播视频作为素材。 |
|CycleMode |Integer |否 |`-1` |当 `Type` 设置为 `1` 时，可设置点播视频的循环播放模式。取值及含义如下。<br><br><br>* `-1`: 列表无限循环播放<br><br>* 大于 0 的整数表示循环播放次数。 |
|DstAddr |String |否 |`rtmp://example.mtime.cn/Video/2022/02/04/mp4/190204084208765161.mp4` |推流地址。 |
|Domain |String |否 |`push.example.com` |推流域名。当推流地址（DstAddr）为空时必须传递，否则该参数无效。 |
|App |String |否 |`live` |应用字段推流。当推流地址（DstAddr）为空时必须传递，否则该参数无效。 |
|Stream |String |否 |`stream-123` |StreamName 字段推流。当推流地址（DstAddr）为空时必须传递，否则该参数无效。 |
|SrcAddr |String |否 |`http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4` |当 `Type` 设置为 `0` 时，必须设置直播视频的拉流地址。最大长度：1,000 个字符。 |
|SrcAddrS |Array of String |否 |`["http://example.cn/Video/2003/02/04/mp4/190204084208765161.mp4"]` |当 `Type` 设置为 `1` 时，必须设置点播视频列表。 |
|水印 |[水印](https://docs.byteplus.com/en/docs/24/106975#watermark) 对象 |否 |`-` |为拉流转推视频添加的水印配置信息。 |
|GroupName |String |否 | |任务所属的分组名称。可调用 [ListPullToPushGroup](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listpulltopushgroup-2023) API 获取分组名称。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">使用主账号调用时，该字段为非必填项，默认加入<code>default</code>分组。当<code>default</code>分组不存在时，将默认创建并绑定到<code>default</code>项目。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">使用子账号调用时，该字段为必填项。</div><br> |


<span id="watermark"></span>
### 水印


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|图片 |字符串 |是 |`data:image/png;base64,iVBORw0KGg****mCC` |水印图片的数据 URL。允许的图片文件大小范围为 100 B 到 2 MB。最大分辨率：1080×1080 像素。数据 URL 格式：`data:[<mediatype>];[base64],<data>`，例如`data:png;base64,iVBORw0KGg****mCC`。<br><br><br>* `mediatype`：图片格式，包括`png`、`jpg`和`jpeg`。<br><br>* `data`：图片的 Base64 字符串。 |
|RelativePosX |浮点型 |是 |`0.1` |水平偏移，即水印左边缘与转码后视频左边缘之间距离与视频宽度的比例。支持范围：0–1。 |
|RelativePosY |浮点型 |是 |`0.1` |垂直偏移，即水印上边缘与转码后视频上边缘之间距离与视频高度的比例。支持范围：0–1。 |
|Ratio |浮点型 |是 |`0.1` |水印宽度与转码后视频宽度的比例。支持范围：0–1。水印高度会根据宽度按比例自动调整。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

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


<span id="Sample response"></span>
### 返回示例

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


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatepulltopushtask-2023#request-parameters)的说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.Format |%s 格式错误 |参数格式不正确。请检查错误信息中指定参数是否存在非法字符或 URL 格式错误。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一，%s 应在 %d 到 %d 之间 |参数超出支持范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|429 |RequestLimitExceeded |*  |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）已超出限制。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
