---
title: "DeleteTimeShiftPresetV2"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-deletetimeshiftpresetv2-2023-zh-CN"
---

调用 `DeleteTimeShiftPresetV2` API 删除已创建的时移配置。

<span id="Requirements"></span>
## 要求


* 接口行为说明：在添加、更新和删除时移配置后，需要重新推拉流（3\-5分钟），以使用变更后的配置。

* 频率限制：每个账号每秒最多查询1次。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteTimeShiftPresetV2&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Headers"></span>
### Headers


|**参数** |**数据类型** |**是否必填** |**示例值** |**说明** |
|---|---|---|---|---|
|Content\-Type |String |是 |`application/json` |请求体的MIME类型。 |


<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**说明** |
|---|---|---|---|---|
|Action |String |是 |`DeleteTimeShiftPresetV2` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**说明** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用[ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API获取配置的域名空间。 |
|应用 |String |是 |`live` |AppName字段。可调用[ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API获取配置的AppName。 |
|Preset |String |是 |`preset-test` |配置名称。可调用[ListTimeShiftPresetV2](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listtimeshiftpresetv2-2023) API获取配置名称。 |


<span id="Response parameters"></span>
## 返回参数

该API仅在返回调用结果中返回[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteTimeShiftPresetV2&Version=2023-01-01
Content-Type: application/json
{
    "Vhost": "push.example.com",
    "App": "live",
    "Preset": "preset-test"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "Action": "DeleteTimeShiftPresetV2",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "202306041104200100100232280022D31"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**说明** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106958#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无所请求资源（资源包括域名空间、域名、应用、配置、证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无所请求资源（资源包括域名空间、域名、应用、配置、证书）。 |
|403 |RequestForbidden.BillingStatus |AccountID计费情况不可用，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置、证书）。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.VhostNotExist |未找到vhost |未找到域名空间（Vhost）。请检查传入的域名空间是否与实际使用的域名空间一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生了与数据库相关的内部错误，请联系管理员。 |发生了与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.VhostOrDomain |发生了与虚拟主机或域名相关的内部错误，请联系管理员。 |发生了与域名空间（Vhost）或域名（Domain）相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生了内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生了内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
