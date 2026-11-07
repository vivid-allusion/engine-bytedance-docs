---
title: "ListVhostTransCodePreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1-zh-CN"
---

调用 `ListVhostTransCodePreset` API 查询转码配置列表。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多查询 10 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListVhostTransCodePreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`ListVhostTransCodePreset` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |此 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名所属的域名空间。 |
|IsHlsAbr |Boolean |否 |`true` |是否查询 DASH 协议 ABR 子流的转码配置，默认为空。<br><br><br>* `true`：是<br><br>* `false`：否<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 <code>IsHlsAbr</code> 和 <code>IsDashAbr</code> 均为 <code>true</code> 时，表示同时查询基于 HLS 协议和 DASH 协议的 ABR 子流转码配置。</div><br> |
|IsDashAbr |Boolean |否 | |是否查询 DASH 协议 ABR 子流的转码配置，默认为空。<br><br><br>* `true`：是<br><br>* `false`：否<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 <code>IsHlsAbr</code> 和 <code>IsDashAbr</code> 均为 <code>true</code> 时，表示同时查询基于 HLS 协议和 DASH 协议的 ABR 子流转码配置。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|CommonPresetList |[TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/106918#transcodepresetvhostapp) 数组 |`-` |通用转码配置列表。 |
|CustomizePresetList |[TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/106918#transcodepresetvhostapp) 数组 |`-` |自定义转码配置列表。 |
|AllPresetList |[TranscodePresetVhostAPP](https://docs.byteplus.com/en/docs/24/106918#transcodepresetvhostapp) 数组 |`-` |全部转码配置列表。 |


<span id="transcodepresetvhostapp"></span>
### TranscodePresetVhostAPP


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`live` |应用名称字段。 |
|TranscodePreset |[TranscodePreset](https://docs.byteplus.com/en/docs/24/106918#transcodepreset) 对象 |`-` |模版详细信息。 |


<span id="transcodepreset"></span>
### TranscodePreset


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|AbrMode |Integer |`1` |当 `IsHlsAbr` 设置为 `true` 时，是否对每个转码流的 I 帧进行对齐：<br><br><br>* `1`：是<br><br>* `0`：否 |
|Acodec |String |`aac` |音频编码格式。<br><br><br>* `aac`：AAC。<br><br>* `copy`：不转码音频流。<br><br>* `opus`：OPUS。 |
|As |String |`0` |是否自动调整视频维度。<br><br><br>* `0`：关闭自动调整，按 `Width` 和 `Height` 拉伸视频。<br><br>* `1`：开启自动调整，按 `ShortSide` 或 `LongSide` 缩放视频。 |
|AudioBitrate |Integer |`30` |音频码率。单位：Kbps。 |
|AutoTransResolution |Integer |`1` |是否限制转码分辨率不超过原始流分辨率。<br><br><br>* `0`：允许<br><br>* `1`：限制 |
|AutoTransVb |Integer |`1` |是否限制转码码率不超过原始流码率。<br><br><br>* `0`：允许<br><br>* `1`：限制 |
|AutoTransVr |Integer |`1` |是否限制转码帧率不超过原始帧率。<br><br><br>* `0`：允许<br><br>* `1`：限制 |
|BFrames |Integer |`3` |两参考帧之间最多的 B帧 数量。0 表示移除 B帧。 |
|FPS |Integer |`60` |视频帧率。单位：fps。 |
|GOP |整数 |`2` |IDR帧之间的最大间隔。单位：秒。 |
|Height |整数 |`100` |视频的高度，单位为像素（px）。当Vcodec设置为h264和h265且As设置为0时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">视频会根据Width和Height进行拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当Width或Height设置为0时，保留原视频维度。</div><br> |
|LongSide |整数 |`200` |视频的长边。当As设置为1时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若LongSide和ShortSide均设置为0，则保留原视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若LongSide和ShortSide均设置为非0值，则视频会根据ShortSide的值进行拉伸。</div><br> |
|Preset |字符串 |`preset1` |转码配置的名称。 |
|Roi |布尔值 |`true` |是否使用高清低码转码模式进行转码。<br><br><br>* `true`：高清低码转码模式。<br><br>* `false`：（默认）标准模式。 |
|ShortSide |整数 |`100` |视频的短边。当As设置为1时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若LongSide和ShortSide均设置为0，则保留原视频维度。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若LongSide和ShortSide均设置为非0值，则视频会根据ShortSide的值进行拉伸。</div><br> |
|StopInterval |整数 |`60` |转码任务的暂停时长，单位为秒。<br><br>当TransType设置为Pull时有效。支持范围为\-1或0到300之间的整数。\-1表示拉流停止时任务不暂停。默认值为60。 |
|SuffixName |字符串 |`hd` |转码流的后缀。 |
|Vcodec |字符串 |`h265` |视频编码格式。<br><br><br>* `h264`：H.264。<br><br>* `h265`：H.265。<br><br>* `copy`：不转码视频流。 |
|VideoBitrate |整数 |`30` |视频码率。单位：Kbps。 |
|Width |整数 |`200` |视频的宽度，单位为像素（px）。当Vcodec设置为h264和h265且As设置为0时有效。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">视频会根据Width和Height进行拉伸。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当Width或Height设置为0时，保留原视频维度。</div><br> |
|TransType |字符串 |`Pull` |转码任务在以下情况下启动：<br><br><br>* `Push`：直播流发起。<br><br>* `Pull`：请求转码流。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST
{
    "Vhost": "push.example.com"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestID": "2021072818053901022706413520787",
        "Action": "ListVhostTransCodePreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "CommonPresetList": [],
        "CustomizePresetList": []
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106918#request-parameters)接口行为进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Empty |%s为必填项 |参数缺失。请检查错误信息中指定的参数是否已传入。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该账号的计费情况不可用，请开通服务或充值。 |视频直播服务尚未开启或账号存在欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
