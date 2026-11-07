---
title: "ListWatermarkPreset"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listwatermarkpreset-2023-zh-CN"
---

调用 `ListWatermarkPreset` API 查询水印配置的信息。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每分钟最多查询 5 次。

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=ListWatermarkPreset&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Action |String |是 |`ListWatermarkPreset` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |本 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API，通过 `Vhost` 参数值获取该配置的域名空间。 |
|App |String |是 |`live` |直播流 URL 中的 `AppName` 字段。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API，通过 `App` 参数值获取该配置的 `AppName`。 |
|Stream |String |否 |`example_stream` |直播流 URL 中的 `StreamName` 字段。可调用 [ListVhostWatermarkPreset](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listvhostwatermarkpreset-2023) API，通过 `Stream` 参数值获取该配置的 `StreamName`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">此参数留空时，将查询指定 <code>AppName</code> 下所有流的配置。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">指定流名称时，将查询该流在指定 <code>AppName</code> 下的配置。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|Preset |[Preset](https://docs.byteplus.com/en/docs/24/107043#preset) 对象 |`-` |水印配置。 |


<span id="preset"></span>
### Preset


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|ID |Integer |`1234567` |水印模版 ID。 |
|AccountID |String |`****1` |BytePlus 账号 ID。 |
|Vhost |String |`push.example.com` |域名空间。 |
|App |String |`example_app` |`AppName`。 |
|Stream |String |`test-stream` |`StreamName`。 |
|Picture |String |`data:image/png;base64,iVBORw0KGg****mCC` |编码后的水印图片字符串。 |
|PictureKey |String |`testtesttest.png` |水印图片文件名。 |
|Orientation |String |`vertical` |水印视频的方向。支持值：<br><br><br>* `vertical`：竖屏。<br><br>* `horizontal`：横屏。 |
|PosX |Float |`1.0` |水平偏移，表示水印左边缘与转码流或 ABR（自适应码率）子流图片左边缘之间的距离。采用相对比例。支持范围：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>WatermarkMode</code> 设置为 <code>static</code> 时，此参数才有值。</div><br> |
|PosY |Float |`1.0` |垂直偏移，表示水印上边缘与转码流或 ABR 子流图片上边缘之间的距离。采用相对比例。支持范围：[0,1]。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当 <code>WatermarkMode</code> 设置为 <code>static</code> 时，此参数才有值。</div><br> |
|RelativeWidth |Float |`1.0` |水印的相对宽度，即水印宽度与转码流或 ABR 子流图片宽度的比例。支持范围：[0,1]。水印高度会随宽度等比例缩放。 |
|WatermarkMode |String |`dynamic` |水印类型。支持值：<br><br><br>* `static`：静态水印。水印固定在指定位置。<br><br>* `dynamic`：动态水印。水印在回放过程中移动，从而增加了未经授权的屏幕录制和滥用的难度。 |
|DynamicMode |String |`dynamic_move_curve` |动态水印效果。有效值：<br><br><br>* `dynamic_move_curve`：动态曲线移动。水印会持续移动，并在到达视频边缘时改变方向。<br><br>* `dynamic_blink`：动态闪烁。水印会以指定频率在视频中随机出现于新的位置。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>WatermarkMode</code>设置为<code>dynamic</code>时，该参数才有值。</div><br> |
|TransSuffixs |String |`_hd,_uhd` |水印配置适用的转码流或 ABR 子流后缀。后缀以逗号（,）分隔。 |
|DynamicSpeedLevel |Integer |`1` |动态速度。有效值为 1 到 10 的整数。值越大，变化越快。<br><br><br>* 当`DynamicMode`设置为`dynamic_move_curve`时，该速度控制水印的移动速度。<br><br>* 当`DynamicMode`设置为`dynamic_blink`时，该速度控制水印变换位置的频率。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>WatermarkMode</code>设置为<code>dynamic</code>时，该参数才有值。</div><br> |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=ListWatermarkPreset&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live"
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "Action": "ListWatermarkPreset",
        "Region": "ap-singapore-1",
        "Service": "live",
        "Version": "2023-01-01",
        "RequestId": "20230604110420****100232280022D31"
    },
    "Result": {
        "Preset": {
            "App": "example_app",
            "Orientation": "vertical",
            "Picture": "data:image/png;base64,iVBORw0KGg****mCC",
            "RelativeWidth": 1.0,
            "AccountID": "****1",
            "PictureKey": "testtesttest.png",
            "ID": 1****67,
            "Vhost": "push.example.com",
            "Stream": "test-stream",
            "WatermarkMode": "dynamic",
            "DynamicMode": "dynamic_move_curve",
            "TransSuffixs": "_hd,_uhd",
            "DynamicSpeedLevel": 1
        }
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**描述** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107043#request-parameters)描述进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllowed |该 AccountID 无权限访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播流服务未开启或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍然返回错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|404 |ResourceNotFound.PresetNotExist |未找到预设 |未找到配置。请检查传入的配置是否与已创建的配置一致。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.Preset |发生与预设相关的内部错误，请联系管理员。 |发生与预设相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
