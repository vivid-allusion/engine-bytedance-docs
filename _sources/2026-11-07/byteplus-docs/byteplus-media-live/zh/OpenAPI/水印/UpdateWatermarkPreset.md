---
title: "UpdateWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-updatewatermarkpreset-2023-zh-CN"
---

调用 `UpdateWatermarkPreset` API 以更新现有水印配置。

<span id="Usage scenario"></span>
## 使用场景

请根据以下规则传递可选参数：


* 要更新动态水印配置，或将静态水印更新为动态水印，必须传递 `WatermarkMode`、`DynamicMode` 和 `DynamicSpeedLevel`。

* 要将动态水印更新为静态水印，必须传递 `PosX` 和 `PosY`。

* 仅在需要更新相关配置时，才传递其他可选参数。如果未传递这些参数，则使用原有水印配置值。


<span id="Requirements"></span>
## 要求


* 请求频率限制：每个账号每秒最多 1 次查询。

* 生效时间：添加、更新或删除水印配置后，变更将在 3 到 5 分钟内生效。变更生效后生成的转码流或 ABR（自适应码率）子流将使用最新的水印配置。变更生效前生成的现有转码流或 ABR 子流不会自动应用更新。若变更前不存在转码流或 ABR 子流，请等待配置生效。若变更前已存在转码流或 ABR 子流且需要使用更新后的配置，请在配置添加、更新或删除后等待 3 到 5 分钟，然后重新推流。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 除了特定参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### Query


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`UpdateWatermarkPreset` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 获取配置的域名空间，作为 `Vhost` 参数的值。 |
|App |String |是 |`live` |直播流 URL 中的 `AppName` 字段。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 获取配置的 `AppName`，作为 `App` 参数的值。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 `StreamName` 字段。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API 获取配置的 `StreamName`，作为 `Stream` 参数的值。 |
|Orientation |String |否 |`vertical` |水印视频的方向。有效值：<br><br><br>* `vertical`：竖屏。<br><br>* `horizontal`：横屏。 |
|Picture |String |否 |`data:image/png;base64,iVBORw0KGg****mCC` |编码后的水印图片字符串。图片大小不得超过 2 MB，最小为 100 字节，分辨率不得超过 1080 × 1080 px。PNG 图片可包含透明通道。图片数据 URL 格式为：`data:[<mediatype>];[base64],<data>`。<br><br><br>* `mediatype`：图片类型。支持 `png`、`jpg` 和 `jpeg` 格式。<br><br>* `data`：base64 编码的图片字符串。<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">若水印图片未更新，更新配置时请勿传递此参数。否则水印可能无法显示。</div><br> |
|PosX |Float |否 |`1.0` |水平偏移，表示水印左边缘与转码流或 ABR 子流图像左边缘之间的距离。使用相对比例。支持范围：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅对静态水印生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当将动态水印更新为静态水印时，必须填写该参数。</div><br> |
|PosY |Float |否 |`1.0` |垂直偏移，表示水印上边缘与转码流或 ABR 子流图像上边缘之间的距离。使用相对比例。支持范围：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">该参数仅对静态水印生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当将动态水印更新为静态水印时，必须填写该参数。</div><br> |
|RelativeWidth |Float |否 |`1.0` |水印的相对宽度，即水印宽度与转码流或 ABR 子流图像宽度的比例。支持范围：[0,1]。水印高度会随宽度同比例缩放。 |
|WatermarkMode |String |否 |`dynamic` |水印类型。支持的取值：<br><br><br>* `static`：静态水印。水印固定在指定位置。<br><br>* `dynamic`：动态水印。水印在回放过程中移动，可增加非法录屏和滥用的难度。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当更新动态水印配置或将静态水印更新为动态水印时，必须填写该参数。</div><br> |
|DynamicMode |String |否 |`dynamic_move_curve` |动态水印效果。支持的取值：<br><br><br>* `dynamic_move_curve`：动态曲线移动。水印持续移动，遇到视频边缘时改变方向。<br><br>* `dynamic_blink`：动态闪烁。水印会以指定频率在视频中随机新位置出现。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当更新动态水印配置或将静态水印更新为动态水印时，必须填写该参数。</div><br> |
|DynamicSpeedLevel |Integer |否 |`1` |动态速度。支持的取值为 1 到 10 的整数，值越大变化越快。<br><br><br>* 当 `DynamicMode` 设置为 `dynamic_move_curve` 时，该速度控制水印的移动速度。<br><br>* 当 `DynamicMode` 设置为 `dynamic_blink` 时，该速度控制水印位置变化的频率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">当更新动态水印配置或将静态水印更新为动态水印时，必须填写该参数。</div><br> |
|TransSuffixs |String |是 |`_hd,_uhd` |水印配置适用的转码流或 ABR 子流后缀。可指定 1\-20 个后缀，多个后缀用英文逗号（,）分隔。<br><br>可调用 [ListVhostTransCodePreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhosttranscodepreset_1)，并从返回参数 `SuffixName` 获取转码流或 ABR 子流后缀。 |


<span id="Response parameters"></span>
## 返回参数

该 API 仅在返回调用结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateWatermarkPreset&Version=2023-01-01
{
    "App": "live",
    "Vhost": "push.example.com",
    "WatermarkMode": "dynamic",
    "DynamicMode": "dynamic_move_curve",
    "DynamicSpeedLevel": 1,
    "TransSuffixs": "_hd,_uhd"
}
```


<span id="Sample response"></span>
### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "UpdateWatermarkPreset",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106960#request-parameters)描述进行排查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|400 |InvalidParam.Length |%s 不应超过 %d |参数长度不正确。请检查错误信息中指定参数的长度是否超出限制。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权访问对应资源，请检查请求参数。 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务尚未开启或账号欠费，导致账单不可用。请检查服务已开启状态和账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到预设 |未找到配置。请检查传入的配置是否与已创建的配置一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
