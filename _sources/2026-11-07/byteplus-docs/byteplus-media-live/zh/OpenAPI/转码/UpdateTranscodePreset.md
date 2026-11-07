---
title: "UpdateTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatetranscodepreset_1-zh-CN"
---

调用 `UpdateTranscodePreset` API 更新已添加的转码配置。如果非必填参数未填写，则对应的参数配置不会发生变化。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 10 次查询。

* 生效说明：对于添加、更新和删除转码配置，需在操作完成后（3\-5 分钟）重新推拉流，才能使用变更后的配置。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateTranscodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateTranscodePreset` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Preset |String |是 |`PresetName` |配置名称。可调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API 获取待更新的配置名称。 |
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API 获取待更新配置的域名空间。 |
|App |String |否 |`live` |AppName 字段。可调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1) API 获取待更新配置的 AppName 字段。 |
|SuffixName |String |否 |`hd` |转码流的后缀。可包含大小写字母、下划线（_）和连字符（\-）。最大长度：10 个字符。常用后缀包括 _sd、_hd 和 _uhd。例如，若设置 _hd 为后缀，转码流名称为 streamName_hd。 |
|VideoBitrate |Integer |否 |`0` |视频码率（bps）。默认值为 1,000,000。0 表示保持原视频码率。<br><br>不同 Vcodec 值对应的支持范围如下：<br><br><br>* h264 和 h265：0–30,000,000<br><br>* h266：0–60,000,000 |
|Vcodec |String |否 |`h265` |视频编码。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `h266`：H.266。<br><br>* `copy`：不转码视频流。且所有视频配置均无法生效。 |
|AudioBitrate |Integer |否 |`30` |音频码率（Kbps）。支持范围：0\-1000。默认值为 128。0 表示保持原码率。 |
|Acodec |String |否 |`aac` |音频编码。<br><br><br>* `aac`：AAC。<br><br>* `copy`：不转码音频流。且所有音频配置均无法生效。<br><br>* `opus`：OPUS。 |
|FPS |Integer |否 |`60` |视频帧率（fps）。默认值为 25。0 表示保持原帧率。<br><br>不同 Vcodec 值对应的支持范围如下：<br><br><br>* h264 和 h265：0–60<br><br>* h266：0–35 |
|GOP |Integer |否 |`2` |IDR 帧最大间隔。单位：秒。支持范围：1–30。 |
|Width |Integer |否 |`1366` |视频宽度（像素 px）。当 Vcodec 设置为 h264 或 h265 且 As 设置为 0 时有效。<br><br>支持范围为 {0,[150–1920]}。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">视频会根据 Width 和 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当 Width 或 Height 任一设置为 0 时，保留原始视频维度。</div><br> |
|Height |Integer |No |`768` |视频高度，单位为像素（px）。当 Vcodec 设置为 h264 和 h265 且 As 设置为 0 时有效。<br><br>支持范围为 {0,[150–1920]}。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">视频将根据 Width 和 Height 拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当 Width 或 Height 任一设置为 0 时，保留原始视频维度。</div><br> |
|As |String |No |`1` |是否自动调整视频维度。<br><br><br>* `0`：关闭自动调整，视频将根据 Width 和 Height 拉伸。请确保 Width 和 Height 在支持范围内。<br><br>* `1`：开启自动调整，视频将根据 ShortSide 或 LongSide 缩放。请确保 ShortSide 和 LongSide 在支持范围内。 |
|ShortSide |Integer |No |`500` |视频短边。当 As 设置为 1 时有效。<br><br>支持范围根据 Roi 和 Vcodec 的取值不同而变化：<br><br><br>* 当 Roi 为 false 时。<br><br>   * h264 的范围为 150\-2160<br><br>   * h265 的范围为 150\-4096<br><br>   * h266 的范围为 150\-720<br><br>* 当 Roi 为 true 时，范围为 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均设置为 0，则保留原始视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均设置为非 0 值，则视频将根据 ShortSide 的值拉伸。</div><br> |
|LongSide |Integer |No |`600` |视频长边。当 As 设置为 1 时有效。<br><br>支持范围根据 Roi 和 Vcodec 的取值不同而变化：<br><br><br>* 当 Roi 为 false 时。<br><br>   * h264 的范围为 150\-4096<br><br>   * h265 的范围为 150\-7680<br><br>   * h266 的范围为 150\-1280<br><br>* 当 Roi 为 true 时，范围为 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均设置为 0，则保留原始视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若 LongSide 和 ShortSide 均设置为非 0 值，则视频将根据 ShortSide 的值拉伸。</div><br> |
|BFrames |Integer |No |`3` |两个参考帧之间允许的最大 B 帧数。默认值为 3。0 表示移除 B帧。<br><br>支持值根据 Vcodec 的取值不同而变化：<br><br><br>* h264 的范围为 [0–7]。<br><br>* h265 和 h266 的取值为 {0, 1, 2, 3, 7, 15}。 |
|Roi |Boolean |No |`true` |是否使用高清低码转码进行转码。<br><br><br>* `true`：高清低码转码。<br><br>* `false`：（默认）标准模式。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 Vcodec 为 H.266 时，不支持高清低码转码。</div><br> |
|AbrMode |Integer |No | |当 IsHlsAbr 设置为 true 时，是否对每路转码流的 I 帧进行对齐：<br><br><br>* `1`：是<br><br>* `0`：（默认）否 |
|AutoTransResolution |Integer |No |`1` |是否限制转码分辨率不超过原始流分辨率。<br><br><br>* `0`：允许<br><br>* `1`：（默认）限制 |
|AutoTransVb |Integer |No |`1` |是否限制转码码率不超过原始流码率。<br><br><br>* `0`：允许<br><br>* `1`：（默认）限制 |
|AutoTransVr |Integer |No |`1` |是否限制转码帧率不超过原始帧率。<br><br><br>* `0`：允许<br><br>* `1`：（默认）限制 |
|StopInterval |Integer |No |`60` |转码任务的暂停时长，单位为秒。<br><br>当 TransType 设置为 Pull 时有效。支持范围为 \-1 或 0 到 300 之间的整数。\-1 表示当流拉取停止时，任务不会暂停。默认值为 60。 |
|TransType |String |No |`Pull` |转码任务在以下情况下启动：<br><br><br>* `Push`：直播流启动时。<br><br>* `Pull`：（默认）请求转码流时。 |


<span id="Response parameters"></span>
## 返回参数

该 API 的返回调用结果仅包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateTranscodePreset&Version=2023-01-01
{
    "Preset": "PresetName",
    "Vhost": "push.example.com",
    "App": "live",
    "SuffixName": "hd"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateTranscodePreset",
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
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107047#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一，%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下无请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
