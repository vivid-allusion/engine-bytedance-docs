---
title: "DescribeLiveSourceStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcestreammetrics-zh-CN"
---

调用 `DescribeLiveSourceStreamMetrics` API，查询指定时间范围内单个源流的监控数据（如音视频帧率和码率），以评估源流的健康状况。

<span id="Requirements"></span>
## 要求


* 限制：支持查询指定域下源流的历史监控数据（包括已删除域）。

* 频率限制：每个账号每秒最多查询 30 次

* 数据延迟：30 秒


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSourceStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还必须包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSourceStreamMetrics` |API 操作名称。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流域名。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面，查看用于直播拉流的域名。 |
|应用 |String |是 |`live` |直播流地址中 `AppName` 字段的值。可包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。 |
|流 |String |是 |`example_stream` |直播流地址中的 `StreamName` 字段。可包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 100 个字符。 |
|StartTime |String |是 |`2021-08-16T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">单次查询的最大时间跨度为 1 天，历史查询的最大时间范围为 366 天。</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |否 |`30` |数据聚合的颗粒度以秒为单位，当前接口仅支持 `30` 秒的数据聚合间隔。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参考 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |String |`pull.example.com` |拉流域名。 |
|应用 |String |`live` |直播流 URL 中的 AppName 字段。 |
|流 |String |`example_stream` |直播流 URL 中的 StreamName 字段。 |
|StartTime |String |`2021-08-16T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |String |`2021-08-16T00:01:59Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |`30` |数据颗粒度，单位为秒。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/106988#metriclist) 数组 |`-` |每个颗粒度下的全部数据。 |


<span id="metriclist"></span>
### MetricList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个颗粒度的起始时间，格式为 RFC3339 UTC 时间，精确到秒。 |
|码率 |Float |`20` |当前数据聚合时间颗粒度内的最大视频码率，单位为 kbps。 |
|帧率 |浮点型 |`20` |当前数据聚合时间颗粒度内的最大视频帧率，单位为 fps。 |
|音频帧率 |浮点型 |`20` |当前数据聚合时间颗粒度内的最大音频帧率，单位为 fps。 |
|音频码率 |浮点型 |`20` |当前数据聚合时间颗粒度内的最大音频码率，单位为 kbps。 |
|音频PTS |双精度型 |`1651831909` |当前数据聚合时间颗粒度内最后一个音频帧的显示时间戳（PTS），单位为毫秒。 |
|视频PTS |双精度型 |`1651831910` |当前数据聚合时间颗粒度内最后一个视频帧的显示时间戳（PTS），单位为毫秒。 |
|PTS差值 |浮点型 |`1` |当前数据聚合时间颗粒度内所有音频帧和视频帧的显示时间戳最大差值，即所有音频PTS与视频PTS的最大差值，单位为毫秒。 |
|音频帧间隔 |浮点型 |`20` |当前数据聚合时间颗粒度内相邻音频帧显示时间戳的最大差值，单位为毫秒。 |
|视频帧间隔 |浮点型 |`20` |当前数据聚合时间颗粒度内相邻视频帧显示时间戳的最大差值，单位为毫秒。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceStreamMetrics&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 30
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveSourceStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 30,
        "MetricList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bitrate": 20,
                "Framerate": 20,
                "AudioFramerate": 20,
                "AudioBitrate": 20,
                "AudioPts": 1651831909,
                "VideoPts": 1651831910,
                "PtsDelta": 1,
                "AudioFrameGap": 20,
                "VideoFrameGap": 20
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106988#request-parameters)说明进行检查。 |
|403 |RequestForbidden |*  |因当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
