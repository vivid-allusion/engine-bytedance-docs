---
title: "CreateTranscodePresetBatch"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023-zh-CN"
---

调用 `CreateTranscodePresetBatch` API 批量创建 ABR 子流转码配置。

<span id="Requirements"></span>
## 使用要求


* 通过对原始流进行转码为不同分辨率和码率，可以创建子流，此过程会产生转码费用。有关价格详情，请参阅[转码](https://docs.byteplus.com/docs/byteplus-media-live/docs-transcoding)。

* 更新转码配置将在 3 到 5 分钟后生效。

* 更新和移除转码配置不会影响正在进行的流。您必须停止并重新启动流以应用更改。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateTranscodePresetBatch&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |字符串 |是 |`CreateTranscodePresetBatch` |API 操作。 |
|Version |字符串 |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Type |字符串 |是 |`hls-abr` |选择批量创建 ABR 配置的协议类型。有效值：<br><br><br>* `hls-abr`：创建已开启 HLS\-ABR 的 ABR 配置。<br><br>* `dash-abr`：创建已开启 DASH\-ABR 的 ABR 配置。<br><br>* `rtm-abr`：创建已开启 RTM\-ABR 的 ABR 配置。<br><br>* `abr`：创建同时已开启 HLS\-ABR 和 DASH\-ABR 的 ABR 配置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">该参数可与<code>IsRtmAbr</code>结合使用，以同时启用 RTM\-ABR 与其他 ABR 协议类型：</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">将该参数设置为<code>hls-abr</code>，并将<code>IsRtmAbr</code>设置为<code>true</code>，即可同时启用 HLS\-ABR 和 RTM\-ABR。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">将该参数设置为<code>dash-abr</code>，并将<code>IsRtmAbr</code>设置为<code>true</code>，即可同时启用 DASH\-ABR 和 RTM\-ABR。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">将该参数设置为<code>abr</code>，并将<code>IsRtmAbr</code>设置为<code>true</code>，即可同时启用 HLS\-ABR、DASH\-ABR 和 RTM\-ABR。</div><br> |
|CopyParams |布尔值 |否 |`true` |将用户请求的 URL 参数复制到子流请求 URL。<br><br><br>* `true`：是；<br><br>* `false`：否。 |
|PresetList |[PresetList](https://docs.byteplus.com/en/docs/24/106955#presetlist) 数组 |是 |`-` |子流转码配置的详细参数。 |


<span id="presetlist"></span>
### PresetList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |字符串 |是 |`push.example.com` |域名空间。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在 BytePlus MediaLive 控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取该域名所属的域名空间。 |
|App |字符串 |是 |`live` |直播流 URL 中的 AppName 字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。 |
|SuffixName |字符串 |是 |`hd` |转码流的后缀，支持由大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）和连字符（\-）组成，长度为 1 到 10 个字符。<br><br>转码后缀通常以流名称后缀的形式使用。常见标识包括 `sd`、`hd`、`uhd`。例如，若转码配置的标识为 `hd`，拉流时转码流的流名称为 `原始流名称_hd`。 |
|VideoBitrate |整数 |是 |`1000000` |视频码率，单位为 bps，取值范围为 [0,30000000]。 |
|Vcodec |字符串 |是 |`h265` |视频编码格式：<br><br><br>* `h264`：使用 H.264 编码格式；<br><br>* `h265`：使用 H.265 编码格式；<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一流下所有 ABR 子流应配置相同的视频编码格式。</div><br> |
|AudioBitrate |整数 |否 |`50` |音频码率，单位为 kbps。 |
|Acodec |字符串 |否 |`acc` |音频编码格式。默认格式为 AAC，支持以下 3 种类型：<br><br><br>* `aac`：使用 AAC 编码格式；<br><br>* `copy`：不进行转码，所有音频编码参数均无效；<br><br>* `opus`：使用 Opus 编码格式。 |
|FPS |整数 |否 |`25` |视频帧率，以 fps（每秒帧数）为单位，取值范围为 [0,60]，默认值为 25fps。帧率越高，视频回放越流畅。 |
|GOP |整数 |是 |`2` |IDR 帧的最大间隔，单位为秒，取值范围为 [1,30]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一流下所有 ABR 子流的 GOP 配置必须保持一致。</div><br> |
|Width |整数 |是 |`1000` |视频宽度，取值范围为 [150, 1920]。 |
|Height |整数 |是 |`500` |视频高度，取值范围为 [150,1920]。 |
|Roi |布尔值 |否 |`true` |是否使用极智超清模式进行转码。<br><br><br>* `true`：高清低码转码。<br><br>* `false`：（默认）标准模式。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一流下所有 ABR 子流应配置为相同的转码方式。</div><br> |
|AutoTransResolution |整数 |否 |`1` |是否开启转码分辨率不超过源流分辨率，默认值 `1` 表示已开启。开启后，若源流分辨率低于转码配置分辨率（即源流的宽和高均低于转码配置的宽和高），则按源流视频分辨率进行转码。<br><br><br>* `0`：未开启；<br><br>* `1`：已开启。 |
|AutoTransVb |整数 |否 |`1` |仅在码率不超过源流码率时进行转码。默认值 `1` 表示该功能已开启。开启后，若源流码率低于配置的转码码率，则按源流视频码率进行转码。<br><br><br>* `0`：未开启；<br><br>* `1`：已开启。 |
|AutoTransVr |整数 |否 |`1` |开启后，转码帧率不超过源流帧率，默认值为 `1`，表示已开启。开启后，若源流帧率低于转码配置帧率，则按源流视频帧率进行转码。<br><br><br>* `0`：未开启；<br><br>* `1`：已开启。 |
|TranscodeStruct |[TranscodeStruct](https://docs.byteplus.com/en/docs/24/106955#transcodestruct) 对象 |否 |`-` |转码信息。 |


<span id="transcodestruct"></span>
### TranscodeStruct


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Type |字符串 |否 |`Pull` |转码任务在以下情况下启动：<br><br><br>* `Push`：直播流启动时。<br><br>* `Pull`：（默认）请求转码流时。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">同一流下所有 ABR 子流的类型应配置为一致。</div><br> |
|IsRtmAbr |布尔值 |否 |`false` |创建 ABR 配置时是否启用 RTM\-ABR。默认值：`false`。有效值：<br><br><br>* `true`：启用 RTM\-ABR。<br><br>* `false`：不启用 RTM\-ABR。 |


<span id="Response parameters"></span>
## 返回调用结果

该 API 的返回调用结果仅包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateTranscodePresetBatch&Version=2023-01-01
{
    "Type": "hls-abr",
    "CopyParams": true,
    "PresetList": [
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SuffixName": "hd",
            "VideoBitrate": 1000000,
            "Vcodec": "h265",
            "FPS": 25,
            "GOP": 2,
            "Width": 1000,
            "Height": 500,
            "AudioBitrate": 50,
            "Acodec": "acc",
            "AutoTransResolution": 1,
            "AutoTransVb": 1,
            "AutoTransVr": 1,
            "Roi": true,
            "TranscodeStruct": {
                "Type": "Pull"
            },
        {
            "Vhost": "push.example.com",
            "App": "live",
            "SuffixName": "ld",
            "VideoBitrate": 500000,
            "Vcodec": "h265",
            "FPS": 25,
            "GOP": 2,
            "Width": 1000,
            "Height": 500,
            "AudioBitrate": 50,
            "Acodec": "acc",
            "AutoTransResolution": 1,
            "AutoTransVb": 1,
            "AutoTransVr": 1,
            "Roi": true,
            "TranscodeStruct": {
                "Type": "Pull"
            }
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
        "Action": "CreateTranscodePresetBatch",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下是与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106955#request-parameters)的接口行为进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.OutOfRange |%s 应为 {[%s]} 之一，%s 应在 %d 到 %d 之间 |参数超出允许范围。请检查错误信息中指定参数的值是否超出取值范围。 |
|403 |RequestForbidden |*  |由于当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权访问对应资源，请检查请求参数。 |由于当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |未开通视频直播流服务或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与服务或账单相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
