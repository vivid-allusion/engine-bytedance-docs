---
title: "UpdateHLSConfig"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/updatehlsconfig-zh-CN"
---

调用 `UpdateHLSConfig` API，为指定域名空间添加或更新 HLS 配置，包括分片大小和分片数量，以有效降低延迟并提升直播流兼容性。在 HLS 和低延迟 HLS（LL\-HLS）中，直播流会被切分为 Transport Stream（TS）。每个 TS 都有对应的 URL，在使用 HLS 协议进行直播拉流时，地址会不断变化。

<span id="Requirements"></span>
## 要求


* 前提条件：需要支持 LL\-HLS 的播放器。

* 限制：

   * HLS/LL\-HLS 封装适用于流推送、拉流回源（使用 FLV 和 RTMP）、以及使用 HLS 的拉流。注意，该功能不适用于拉流回源（使用 HLS）。

   * HLS/LL\-HLS 封装配置不仅适用于该域名下的流，还适用于同一域名空间（Vhost）关联的其他域名下的流。

   * HLS/LL\-HLS 封装配置不会应用于启用 [HLS-ABR](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-configuring-an-hls-abr-task) 功能的应用。

   * 封装配置将在 3 到 5 分钟内生效。

      限制：适用于流推送、使用 HLS 的拉流，以及拉流回源（使用 FLV 和 RTMP）。但不适用于拉流回源（使用 HLS）。

* 频率限制：每个账号每秒最多 10 次查询。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=UpdateHLSConfig&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`UpdateHLSConfig` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Vhost |String |是 |`push.example.com` |域名空间。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，获取该域名所属的域名空间。 |
|应用 |String |否 |`live` |直播流 URL 中的 AppName 字段。如未指定，配置将应用于所有 AppName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。 |
|Interval |Float |否 |`3` |HLS 分片时长范围为 1 到 60 秒。<br><br>默认值为 3。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">建议直播流的关键帧间隔（GOP）保持稳定，且分片时长等于或为 GOP 大小的整数倍。</div><br> |
|PlaylistLength |Integer |否 |`3` |m3u8 播放列表中的媒体分片数量。默认值为 3。 |
|FirstPlaylistLength |Integer |否 |`2` |初始播放列表包含的媒体分片数量。可输入整数 `3` 到 `10`。默认值为 `2`。 |
|PartTargetDuration |Float |否 |`1` |每个媒体分片拆分后的部分分片时长。<br><br><br>* 单位为秒。<br><br>* 默认值为 `1`。<br><br>* `0` 表示禁用低延迟 HLS。 |
|InsertPDT |Boolean |否 |`true` |是否在回放文件中插入PDT时间标签，默认不插入，取值及含义如下。<br><br><br>* `true`：插入；<br><br>* `false`：不插入。 |
|PDTInterval |Float |No |`3` |在回放文件中插入PDT（#EXT\-X\-PROGRAM\-DATE\-TIME）时间标签的间隔，单位为秒，取值范围为[0,3600]，默认值为0。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果PDT间隔设置为0或小于分片时长，则每个分片都会插入一个PDT标签。</div><br> |


<span id="Response parameters"></span>
## 返回调用结果参数

该 API 仅在返回结果中返回 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/request-response)。

<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=UpdateHLSConfig&Version=2023-01-01
{
    "Vhost": "push.example.com",
    "App": "live",
    "Interval": 2.6,
    "PlaylistLength": 6,
    "FirstPlaylistLength": 4,
    "PartTargetDuration": 1
}
```


<span id="Sample response"></span>
### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024041106585435BA3A27F267D68D449F",
        "Action": "UpdateCMAFConfig",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    }
}
```
