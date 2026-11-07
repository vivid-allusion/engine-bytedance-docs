---
title: "CreateWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-createwatermarkpreset-2023-zh-CN"
---

调用 `CreateWatermarkPreset` API，为转码流或 ABR（自适应码率）子流添加水印配置。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多 1 次查询。

* 前提条件：

   * 你已在目标域名空间下为指定的 `AppName` 添加了转码配置或 ABR 配置，并希望在该空间添加水印配置。更多信息，请参见 [CreateTranscodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/createtranscodepresetv2023) 或 [CreateTranscodePresetBatch](https://docs.byteplus.com/en/docs/byteplus-media-live/CreateTranscodePresetBatch-2023)。

   * 准备一个 JPG 或 PNG 图片作为水印。图片大小不得超过 2 MB，分辨率不得超过 1080 × 1080 像素。PNG 图片可包含透明通道。

* 生效时间：添加、更新或删除水印配置后，变更将在 3 到 5 分钟内生效。变更生效后生成的转码流或 ABR 子流将使用最新的水印配置。变更生效前已生成的转码流或 ABR 子流不会自动应用更新。若变更前不存在转码流或 ABR 子流，请等待配置生效。若变更前已存在转码流或 ABR 子流且需使用更新后的配置，请在配置添加、更新或删除后等待 3 到 5 分钟，然后重新推流。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=CreateWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`CreateWatermarkPreset` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间，即直播流 URL 中域名所属的域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取域名所属的域名空间。 |
|App |String |是 |`live` |直播流 URL 中的 `AppName` 字段。可包含大写和小写字母（A \- Z，a \- z）、数字（0 \- 9）、下划线（_）、连字符（\-）和点（.）。长度要求为 1 到 30 个字符。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 `StreamName` 字段。可包含大写和小写字母（A \- Z，a \- z）、数字（0 \- 9）、下划线（_）、连字符（\-）和点（.）。长度要求为 1 到 100 个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">留空此参数，则水印配置将应用于指定 <code>AppName</code> 下的所有转码流和 ABR 子流。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若指定 <code>StreamName</code>，则水印配置仅应用于指定 <code>AppName</code> 下指定的 <code>StreamName</code>。</div><br> |
|Orientation |String |否 |`vertical` |水印视频的方向。有效值：<br><br><br>* `vertical`：竖屏。<br><br>* `horizontal`：横屏。 |
|图片 |字符串 |否 |`data:image/png;base64,iVBORw0KGg****mCC` |编码后的水印图片字符串。图片大小不能超过 2 MB，最小为 100 字节，分辨率不能超过 1080 × 1080 px。图片数据 URL 格式为：`data:[<mediatype>];[base64],<data>`。<br><br><br>* `mediatype`：图片类型。支持 `png`、`jpg` 和 `jpeg` 格式。<br><br>* `data`：Base64 编码的图片字符串。 |
|PosX |浮点型 |否 |`0` |水平偏移，表示水印左边缘与转码流或 ABR 子流图片左边缘之间的距离。采用相对比例。支持范围：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 <code>WatermarkMode</code> 设置为 <code>static</code> 时，该参数为必填。</div><br> |
|PosY |浮点型 |否 |`1.0` |垂直偏移，表示水印上边缘与转码流或 ABR 子流图片上边缘之间的距离。采用相对比例。支持范围：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 <code>WatermarkMode</code> 设置为 <code>static</code> 时，该参数为必填。</div><br> |
|RelativeWidth |浮点型 |否 |`1.0` |水印宽度相对值，即水印宽度与转码流或 ABR 子流图片宽度的比例。支持范围：[0,1]。水印高度会随宽度等比缩放。 |
|WatermarkMode |字符串 |否 |`dynamic` |水印类型。默认值为 `static`。有效值：<br><br><br>* `static`：静态水印。水印固定在指定位置。<br><br>* `dynamic`：动态水印。水印在回放过程中移动，增加了非法录屏和滥用的难度。 |
|DynamicMode |字符串 |否 |`dynamic_move_curve` |动态水印效果。有效值：<br><br><br>* `dynamic_move_curve`：动态曲线移动。水印持续移动，遇到视频边缘时会改变方向。<br><br>* `dynamic_blink`：动态闪烁。水印会以指定频率在视频中随机新位置出现。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当 <code>WatermarkMode</code> 设置为 <code>dynamic</code> 时，该参数为必填。</div><br> |
|DynamicSpeedLevel |整型 |否 |`1` |动态速度。默认值为 `1`。支持范围为 1 到 10 的整数，值越大变化越快。<br><br><br>* 当 `DynamicMode` 设置为 `dynamic_move_curve` 时，该速度控制水印的移动速度。<br><br>* 当 `DynamicMode` 设置为 `dynamic_blink` 时，该速度控制水印位置变化的频率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>WatermarkMode</code> 设置为 <code>dynamic</code> 时，该参数生效。</div><br> |
|TransSuffixs |字符串 |否 |`_hd,_uhd` |水印配置适用的转码流或 ABR 子流后缀。默认情况下，水印配置适用于当前 `AppName` 下所有转码流或 ABR 子流后缀。可指定 1\-20 个后缀，多个后缀用英文逗号（,）分隔。<br><br>可调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)，并从返回参数 `SuffixName` 获取转码流或 ABR 子流后缀。 |


<span id="Response parameters"></span>
## 返回调用结果参数

如需了解该 API 特有的专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|ID |整型 |`1234567` |水印模版 ID。 |
|PresetName |字符串 |`preset` |水印模版名称。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=CreateWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Orientation": "vertical",
    "RelativeWidth": 0.185,
    "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
    "WatermarkMode": "dynamic",
    "DynamicMode": "dynamic_move_curve",
    "DynamicSpeedLevel": 1,
    "TransSuffixs": "_hd,_uhd"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "Action": "CreateWatermarkPreset",
        "Region": "ap-singapore-1",
        "RequestId": "20230604110420****100232280022D31",
        "Service": "live",
        "Version": "2023-01-01"
    },
    "Result": {
        "ID": 1234567,
        "PresetName": "preset"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。若仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106973#request-parameters)描述进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|400 |InvalidParam.Empty |%s为必填项 |缺少参数。请检查错误信息中指定的参数是否已传入。 |
|403 |RequestForbidden |*  |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.AccountIDNotAllowed |该AccountID无权访问对应资源，请检查请求参数 |由于当前账号下不存在请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|403 |RequestForbidden.BillingStatus |该AccountID的计费情况不可用，请开通服务或充值。 |未开启视频直播流服务或账号欠费，导致账单不可用。请检查服务开通状态及账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
