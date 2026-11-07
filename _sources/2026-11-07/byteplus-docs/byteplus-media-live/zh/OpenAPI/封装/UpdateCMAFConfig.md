---
title: "UpdateCMAFConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatecmafconfig-zh-CN"
---

在动态自适应HTTP流媒体（DASH）和低延迟DASH（LL\-DASH）中，直播流会被切分为Common Media Application Format（CMAF）片段。调用`UpdateCMAFConfig` API，可以调整时长和片段数量设置，从而有效降低延迟并提升直播流在指定域名空间（Vhost）下的兼容性。

<span id="Requirements"></span>
## 要求


* 前提条件：

   * 需要支持DASH的播放器。

   * iOS 10.0、macOS 10.12 和 tvOS 10.0 或更高版本操作系统支持CMAF内容。

* 限制：

   * DASH封装适用于推流、通过HLS、FLV和RTMP拉流回源，以及通过DASH over CMAF拉流。

   * DASH封装配置不仅适用于当前域名，还会应用于同一域名空间（Vhost）下关联的其他域名。

   * 封装配置将在3分钟至5分钟内生效。

* 频率限制：每个账号每秒最多10次查询


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateCMAFConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateCMAFConfig` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`Arctic` |域名空间。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取域名所属的域名空间。 |
|应用 |String |否 |`Far` |直播流URL中的AppName字段。如未指定，配置将应用于所有AppName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至30个字符。 |
|Interval |Float |否 |`2` |CMAF片段时长范围为`1`至`60`秒。默认值为`2`。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建议直播流的关键帧间隔（GOP）大小保持稳定，且片段时长等于或为关键帧间隔的整数倍。</div><br> |
|PlaylistLength |Integer |否 |`6` |播放列表中包含的媒体片段数量。可输入`3`至`10`的整数。默认值为`3`。 |
|DisableLowLatency |Boolean |否 |`true` |是否禁用低延迟DASH。低延迟DASH扩展协议以实现低延迟视频流，同时保持可扩展性。默认值为`false`。<br><br><br>* `true`：禁用；<br><br>* `false`：启用。 |


<span id="Response parameters"></span>
## 返回参数

该API仅在返回调用结果中返回[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateCMAFConfig&Version=2023-01-01
{
    "Vhost": "example",
    "App": "liveShow",
    "Interval": 3,
    "PlaylistLength": 6,
    "DisableLowLatency": true
}
```


<span id="Sample response"></span>
### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024041105461468A8B53B2CE41BAA7E87",
        "Action": "UpdateCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
