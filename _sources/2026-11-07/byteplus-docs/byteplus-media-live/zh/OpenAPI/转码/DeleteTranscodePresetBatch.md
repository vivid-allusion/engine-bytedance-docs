---
title: "DeleteTranscodePresetBatch"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DeleteTranscodePresetBatch-2023-zh-CN"
---

调用 `DeleteTranscodePresetBatch` API，批量删除 ABR 子流的转码配置。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DeleteTranscodePresetBatch&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了需传递 API 专属参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DeleteTranscodePresetBatch` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Type |String |是 |`hls-abr` |请选择要删除的 ABR 配置的协议类型。有效值：<br><br><br>* `hls-abr`：HLS\-ABR<br><br>* `dash-abr`：DASH\-ABR<br><br>* `rtm-abr`：RTM\-ABR<br><br>* `abr`：HLS\-ABR 和 DASH\-ABR<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若删除已开启多协议类型的 ABR 配置，请使用如下<code>Type</code>值：</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">对于已开启 HLS\-ABR 和 RTM\-ABR 的配置，请使用<code>hls-abr</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">对于已开启 DASH\-ABR 和 RTM\-ABR 的配置，请使用<code>dash-abr</code>。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">对于已开启 HLS\-ABR、DASH\-ABR 和 RTM\-ABR 的配置，请使用<code>abr</code>。</div><br> |
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/106948#presetlist) 数组 |是 |`-` |要删除 ABR 子流转码配置信息，可调用[ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)查看需删除的 ABR 类型转码配置。 |


<span id="presetlist"></span>
### PresetList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Preset |String |是 |`asdq12ed` |删除配置中的 Preset 值。 |
|Vhost |String |是 |`push.example.com` |待删除配置中的 Vhost 值。 |
|App |String |是 |`live` |删除配置中的 App 值。 |


<span id="Response parameters"></span>
## 返回调用结果

该 API 的返回调用结果仅包含[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DeleteTranscodePresetBatch&Version=2023-01-01
{
    "Type": "hls-abr",
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "Preset": "asdq12ed"
        },
        {
            "Vhost": "push.example.com",
            "App": "live",
            "Preset": "d2asda2e"
        }
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DeleteTranscodePresetBatch",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106948#request-parameters)描述进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.StillUsing |%s 仍在使用中，无法删除 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、App、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，当前账号下无请求资源（资源包括域名空间、域名、App、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未已开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
