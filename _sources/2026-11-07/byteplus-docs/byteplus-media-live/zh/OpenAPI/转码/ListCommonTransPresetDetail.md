---
title: "ListCommonTransPresetDetail"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listcommontranspresetdetail-2023-zh-CN"
---

调用 `ListCommonTransPresetDetail` API 查询通用转码配置的详细信息。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListCommonTransPresetDetail&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了特定 API 参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListCommonTransPresetDetail` |API 操作。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|PresetList |String 数组 |否 |`["preser1","preset2"]` |转码模版列表。若未指定，则会查询所有通用转码模版。 |


<span id="Response parameters"></span>
## 返回参数

关于唯一的 API 特定返回参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|NarrowBandHDPresetDetail |[PresetDetail](https://docs.byteplus.com/en/docs/24/107009#presetdetail) 数组 |`-` |极智超清模版详情。 |
|StandardPresetDetail |[PresetDetail](https://docs.byteplus.com/en/docs/24/107009#presetdetail) 数组 |`-` |标准模版详情。 |


<span id="presetdetail"></span>
### PresetDetail


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|SuffixName |String |`hd` |转码流的后缀。 |
|VideoBitrate |Integer |`1000000` |视频码率。单位：Kbps。 |
|Vcodec |String |`h265` |视频编码。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `copy`：不转码视频流。 |
|AudioBitrate |Integer |`30` |音频码率。单位：Kbps。 |
|Acodec |String |`aac` |音频编码。<br><br><br>* `aac`：AAC。<br><br>* `copy`：不转码音频流。<br><br>* `opus`：OPUS。 |
|FPS |Integer |`60` |视频帧率。单位：fps。 |
|GOP |Integer |`2` |IDR 帧的最大间隔。单位：秒。 |
|Width |Integer |`100` |视频宽度（像素 px）。当 Vcodec 设置为 h264 和 h265 且 As 设置为 0 时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">视频会根据 Width 和 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当 Width 或 Height 任意一个为 0 时，保留原视频维度。</div><br> |
|Height |Integer |`50` |视频高度（像素 px）。当 Vcodec 设置为 h264 和 h265 且 As 设置为 0 时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">视频会根据 Width 和 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当 Width 或 Height 任意一个为 0 时，保留原视频维度。</div><br> |
|As |String |`1` |是否自动调整视频维度。<br><br><br>* `0`：关闭自动调整，视频会根据 `Width` 和 `Height` 拉伸。<br><br>* `1`：开启自动调整，视频会根据 `ShortSide` 或 `LongSide` 缩放。 |
|ShortSide |Integer |`100` |视频短边（像素 px）。当 As 设置为 1 时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均为 0，则保留原视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均不为 0，则视频会根据 ShortSide 的值拉伸。</div><br> |
|LongSide |Integer |`200` |视频长边（像素 px）。当 As 设置为 1 时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均为 0，则保留原视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均不为 0，则视频会根据 ShortSide 的值拉伸。</div><br> |
|BFrames |整数 |`3` |两个参考帧之间最多允许的B帧数量。0表示移除B帧。 |
|Roi |布尔值 |`true` |是否采用高清低码转码进行转码。<br><br><br>* `true`：高清低码转码。<br><br>* `false`：（默认）标准模式。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListCommonTransPresetDetail&Version=2023-01-01
{
    "PresetList": [
        "preset1",
        "preset2"
    ]
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestID": "20220426203705010211197144119377C1",
        "Action": "ListCommonTransPresetDetail",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "StandardPresetDetail": [],
        "NarrowBandHDPresetDetail": []
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107009#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s应为{[%s]}之一%s应在%d到%d之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |因当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |该AccountID无权限访问对应资源，请检查请求参数 |因当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该AccountID计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
