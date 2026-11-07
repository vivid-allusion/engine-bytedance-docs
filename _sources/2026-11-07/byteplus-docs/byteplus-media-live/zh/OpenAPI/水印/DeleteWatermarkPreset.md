---
title: "DeleteWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletewatermarkpreset-2023-zh-CN"
---

调用 `DeleteWatermarkPreset` API 删除已有的水印配置。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒 1 次查询。

* 生效时间：添加、更新或删除水印配置后，变更将在 3 至 5 分钟内生效。变更生效后生成的转码流或 ABR（自适应码率）子流将使用最新的水印配置。变更生效前已生成的转码流或 ABR 子流不会自动应用更新。若变更前不存在转码流或 ABR 子流，请等待配置生效。若变更前已存在转码流或 ABR 子流且需使用更新后的配置，请在配置添加、更新或删除后等待 3 至 5 分钟，然后重新推流。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了特定参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`DeleteWatermarkPreset` |API 操作名。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 获取配置的域名空间作为 `Vhost` 参数值。 |
|App |String |是 |`live` |直播流 URL 中的 `AppName` 字段。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 获取配置的 `AppName` 作为 `App` 参数值。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 `StreamName` 字段。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 获取配置的 `StreamName` 作为 `Stream` 参数值。 |


<span id="Response parameters"></span>
## 返回参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DeleteWatermarkPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106926#request-parameters) 描述进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，无法删除 |错误信息中指定的资源正在使用，导致无法删除。请释放资源后重试。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID 的计费情况不可用，请激活服务或充值。 |视频直播流服务尚未开启或账户存在欠费，导致账单不可用。请检查服务激活状态和账户欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到预设。 |未找到配置。请检查传入的配置是否与已创建的配置一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
