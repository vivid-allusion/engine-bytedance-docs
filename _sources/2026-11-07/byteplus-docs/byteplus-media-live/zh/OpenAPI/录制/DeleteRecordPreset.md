---
title: "DeleteRecordPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deleterecordpreset-2023-zh-CN"
---

调用 `DeleteRecordPreset` API 删除已创建的录制配置。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 1 次查询。

* 生效说明：添加、更新和删除录制配置后，需在操作完成后（3\-5 分钟）重新推拉流，以使用变更后的配置。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteRecordPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除接口专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteRecordPreset` |API 操作。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |否 |`push.example.com` |域名空间。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待删除配置的域名空间。 |
|应用 |String |否 |`live` |AppName 字段。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待删除配置的 AppName。 |
|流 |String |否 |`example_stream` |StreamName 字段。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待删除配置的 StreamName。 |
|Preset |String |是 |`liverecord` |配置名称。可调用 [ListVhostRecordPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostrecordpresetv2-2023) API 获取待删除配置的名称。 |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 的返回调用结果仅包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteRecordPreset&Version=2023-01-01
{
    "Preset": "liverecord",
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202204081618570101742350380146D011",
        "Action": "DeleteRecordPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106938#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，无法删除 |错误信息中指定的资源正在使用，导致无法删除。请释放资源后重试。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到预设 |未找到配置。请检查传入的配置是否与已创建的配置一致。 |
|429 |RequestLimitExceeded.Exist |%s 已存在 |请求创建的资源（包括域名空间、域名、应用名称、配置、证书）已存在。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
