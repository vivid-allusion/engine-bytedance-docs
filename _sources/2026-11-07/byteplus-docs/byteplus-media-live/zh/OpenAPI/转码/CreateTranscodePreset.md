---
title: "CreateTranscodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023-zh-CN"
---

调用 `CreateTranscodePreset` API 创建转码配置，系统会根据你的转码配置对符合条件的在线流进行实时转码。

<span id="Usage scenario"></span>
## 使用场景

`CreateTranscodePreset` API 支持创建多个 `Vhost + 应用` 级别的转码配置，不同的转码配置需通过转码后缀（SuffixName）进行区分。创建转码配置后，你可以通过在拉流地址的流名称中添加转码后缀来使用该转码配置。

<span id="Requirements"></span>
## 使用要求


* 计费情况：关于转码价格，请参考 [Transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* 频率限制：每个账号每秒最多查询 10 次。

* 接口行为：添加、更新和删除转码配置后，需要重新推流和拉流（3\-5 分钟）以使用变更后的配置。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateTranscodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递接口专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`CreateTranscodePreset` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取该域名所属的域名空间。 |
|应用 |String |是 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。 |
|SuffixName |String |是 |`hd` |转码流的后缀。可包含大写字母、小写字母（A\-Z、a\-z）、下划线（_）和连字符（\-）。最大长度：10 个字符。常用后缀包括 `_sd`、`_hd` 和 `_uhd`。例如，若设置 `_hd` 为后缀，转码流名称为 `streamName_hd`。 |
|VideoBitrate |Integer |否 |`1000000` |视频码率（bps）。默认值为 1,000,000。0 表示保持原视频码率。<br><br>视频码率的范围取决于视频编码格式（`Vcodec`）。<br><br>不同 Vcodec 值支持范围如下：<br><br><br>* h264 和 h265 支持范围为 0–30,000,000 |
|Vcodec |String |是 |`h265` |视频编码格式。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `copy`：不转码视频流。此时所有视频配置均不可用，包括视频帧率（`FPS`）、视频码率（`VideoBitrate`）、分辨率设置（`As`、`Width`、`Height`、`ShortSide`、`LongSide`）、`GOP` 和 `BFrames` 等。 |
|AudioBitrate |Integer |否 |`50` |音频码率（Kbps）。支持范围：0\-1000。默认值为 128。0 表示保持原码率。 |
|Acodec |String |否 |`aac` |音频编码格式。默认值为 `aac`。可取值如下：<br><br><br>* `aac`：AAC。<br><br>* `opus`：OPUS。<br><br>* `copy`：不会对音频流进行转码。且所有音频配置均无法生效。音频编码格式参数包括音频码率（`AudioBitrate`）等。 |
|FPS |整数 |否 |`25` |视频帧率，单位为 fps。默认值为 25。0 表示保持原始帧率。<br><br>支持范围因 Vcodec 值而异：<br><br><br>* h264 和 h265 的范围为 0–60 |
|GOP |整数 |否 |`2` |IDR 帧的最大间隔。单位：秒。支持范围：1–30。 |
|Width |整数 |否 |`400` |视频宽度，单位为像素（px）。当 `Vcodec` 设置为 h264 和 h265 且 `As` 设置为 `0` 时有效。<br><br>视频宽度的支持范围因 Vcodec 值而异：<br><br><br>* h264 和 h265 的范围为 150\-1920。<br><br>* h266 不支持设置 Width 和 Height。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整关闭（<code>As</code> 值为 0）时，视频会根据 Width 和 Height 的值进行拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整关闭（<code>As</code> 值为 0）时，若 Width 或 Height 任一设置为 0，则保留原始视频维度。</div><br> |
|Height |整数 |否 |`200` |视频高度，单位为像素（px）。当 Vcodec 设置为 h264 和 h265 且 `As` 设置为 0 时有效。<br><br>视频高度的支持范围因 Vcodec 值而异：<br><br><br>* h264 和 h265 的范围为 150–1920<br><br>* h266 不支持设置 Width 和 Height。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整关闭（<code>As</code> 值为 0）时，视频会根据 Width 和 Height 的值进行拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整关闭（<code>As</code> 值为 0）时，若 Width 或 Height 任一设置为 0，则保留原始视频维度。</div><br> |
|As |字符串 |否 |`1` |是否自动调整视频维度。默认值为 0，可取以下值：<br><br><br>* `0`：关闭自动调整；<br><br>* `1`：开启自动调整。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整关闭（<code>As</code> 值为 <code>0</code>）时，视频会根据 Width 和 Height 的值进行拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整开启（<code>As</code> 值为 <code>1</code>）时，转码的视频分辨率会根据短边长度（<code>ShortSide</code>）、长边长度（<code>LongSide</code>）、视频宽度（<code>Width</code>）和视频高度（<code>Height</code>）的优先级确定，另一边按比例缩放。</div><br> |
|ShortSide |整数 |否 |`768` |视频短边长度。配置不同转码类型（`Roi`）和视频编码格式（`Vcodec`）时，短边长度的支持范围如下。<br><br><br>* 当转码类型为标准模式（`Roi` 值为 `false`）时，支持范围因 `Roi` 和 `Vcodec` 值而异：<br><br>   * h264 的范围为 150\-2160<br><br>   * h265 的范围为 150\-4096<br><br>* 当转码类型为高清低码转码模式（`Roi` 为 `true`）<br><br>   * h264 或 h265 的范围为 0 或 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当视频分辨率自动调整开启（<code>As</code> 值为 <code>1</code>）时，该参数有效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若同时将 <code>LongSide</code> 和 <code>ShortSide</code> 设置为 0，则保留原始视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果同时将 LongSide 和 <code>ShortSide</code> 设置为非 0 的值，视频会根据 <code>ShortSide</code> 的值进行拉伸。</div><br> |
|LongSide |整数 |否 |`500` |视频的长边长度。配置不同转码类型（Roi）和视频编码格式（Vcodec）时，长边长度的支持范围如下。<br><br><br>* 当转码类型为标准模式（Roi 值为 false）时，支持范围会根据 Roi 和 Vcodec 的值有所不同：<br><br>   * h264 支持范围为 150\-4096<br><br>   * h265 支持范围为 150\-7680<br><br>* 当转码类型为高清低码转码模式（`Roi` 为 `true`）<br><br>   * h264 和 h265 支持范围为 0 和 150–1920。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当开启视频分辨率自动调整（<code>As</code> 值为 <code>1</code>）时，该参数有效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果同时将 <code>LongSide</code> 和 <code>ShortSide</code> 设置为 0，则保留原视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">如果同时将 <code>LongSide</code> 和 <code>ShortSide</code> 设置为非 0 的值，视频会根据 <code>ShortSide</code> 的值进行拉伸。</div><br> |
|BFrames |整数 |否 |`3` |两参考帧之间的最大 B帧 数。默认值为 3。0 表示移除 B帧。<br><br>有效值会根据 Vcodec 的值有所不同：<br><br><br>* h264 支持范围为 [0–7]。<br><br>* h265 支持范围为 {0, 1, 2, 3, 7, 15}。 |
|Roi |布尔值 |否 |`true` |是否使用高清低码转码模式进行转码。<br><br><br>* `true`：高清低码转码模式。<br><br>* `false`：（默认）标准模式。 |
|AbrMode |整数 |否 |`1` |当 IsHlsAbr 设置为 true 时，是否对每路转码流的 I 帧进行对齐：<br><br><br>* `1`：是<br><br>* `0`：（默认）否 |
|AutoTransResolution |整数 |否 |`1` |是否启用转码分辨率不超过源流分辨率。启用后，当原流分辨率低于转码分辨率时，将按照源流分辨率进行转码。<br><br><br>* `0`：关闭<br><br>* `1`：（默认）开启 |
|AutoTransVb |整数 |否 |`1` |是否启用转码码率不超过源流码率。启用后，当源流码率低于转码码率时，将按照源流码率进行转码。<br><br><br>* `0`：关闭<br><br>* `1`：（默认）开启 |
|AutoTransVr |整数 |否 |`1` |是否限制转码帧率不超过源帧率。启用后，当源帧率低于转码帧率时，将按照源帧率进行转码。<br><br><br>* `0`：关闭<br><br>* `1`：（默认）开启 |
|StopInterval |整数 |否 |`60` |转码任务的暂停时长，单位为秒。<br><br>当 TransType 设置为 Pull 时有效。支持范围为 \-1 或 0 到 300 之间的整数。\-1 表示拉流停止时任务不暂停。默认值为 60。 |
|TransType |字符串 |否 |`Pull` |转码任务在以下情况下启动：<br><br><br>* `Push`：直播流发起时。<br><br>* `Pull`：（默认）请求转码流时。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于接口专属的返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|PresetName |字符串 |`preset` |转码模版名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateTranscodePreset&Version=2023-01-01
{
    "Vhost":"push.example.com",
    "App":"live",
    "SuffixName":"hd",
    "Vcodec"："h264"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "Action": "CreateTranscodePreset",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "PresetName": "preset"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106977#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据。 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权访问对应资源，请检查请求参数。 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务尚未开启或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费情况。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
