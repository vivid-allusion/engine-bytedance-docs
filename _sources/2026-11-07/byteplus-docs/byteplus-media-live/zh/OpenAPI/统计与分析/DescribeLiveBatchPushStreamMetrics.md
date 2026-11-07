---
title: "DescribeLiveBatchPushStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchpushstreammetrics-2023-zh-CN"
---

调用 `DescribeLiveBatchPushStreamMetrics` API，查询推流域名下一个或多个流的推流统计数据，包括帧率、码率、显示时间戳（PTS）等。您可以使用这些统计数据来监控推流会话的健康状况。您可以查询已删除域名的数据。

<span id="Requirements"></span>
## 要求


* 限制：支持查询已删除域名产生的历史流数据。

* 频率限制：每个账号每秒最多查询30次。

* 数据延迟：30秒。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveBatchPushStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**参数说明** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBatchPushStreamMetrics` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**参数说明** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |推流域名。您可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的推流域名。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询指定直播流的监控数据时，需同时指定应用和流。</div><br> |
|流 |String |否 |`example_stream` |直播流URL中的StreamName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询指定直播流的监控数据时，需同时指定应用和流。</div><br> |
|StartTime |String |是 |`2021-08-16T00:00:00Z` |查询范围的起始时间，需采用RFC 3339格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">单次查询的最大时间跨度为24小时，历史查询时间范围为366天；</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59Z` |查询范围的结束时间，需采用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |否 |`5` |返回数据的时间颗粒度，单位为秒。有效值包括：<br><br><br>* `5`<br><br>* `30`<br><br>* `60`（默认值） |
|AggType |String |否 |`max` |聚合算法，数据聚合时间颗粒度内动态指标的值及含义如下。<br><br><br>* `max`：（默认值）计算聚合时间颗粒度内的最大值；<br><br>* `avg`：计算聚合时间颗粒度内的平均值。 |


<span id="Response parameters"></span>
## 返回参数

有关API专属返回参数，请参见下表。更多详情请参见[请求与响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**参数说明** |
|---|---|---|---|
|Domain |String |`push.example.com` |推流域名。 |
|应用 |String |`live` |直播流URL中的AppName字段。 |
|流 |String |`example_stream` |直播流URL中的StreamName字段。 |
|StartTime |String |`2021-08-16T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |String |`2021-08-16T00:01:59Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |`5` |返回数据的时间颗粒度，单位为秒。有效值包括：<br><br><br>* `5`<br><br>* `30`<br><br>* `60`（默认值） |
|StreamMetricList |[StreamMetricList](https://docs.byteplus.com/en/docs/24/106996#streammetriclist) 数组 |`-` |按指定时间颗粒度聚合的监控数据。 |
|AggType |String |`max` |聚合算法，数据聚合时间颗粒度内动态指标的值及含义如下。<br><br><br>* `max`：（默认值）计算聚合时间颗粒度内的最大值；<br><br>* `avg`：计算聚合时间颗粒度内的平均值。 |


<span id="streammetriclist"></span>
### StreamMetricList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |String |`push.example.com` |推流的域名。 |
|App |String |`live` |直播流 URL 中的应用字段。 |
|Stream |String |`example_stream` |直播流 URL 中的流字段。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/106996#metriclist) 数组 |`-` |按指定时间颗粒度聚合的监控数据。 |
|SessionID |String |`1961227fe2ab4da7a3f28` |单次推流的唯一 ID。 |


<span id="metriclist"></span>
### MetricList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00+08:00` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用 RFC3339 UTC 时间格式，精确到秒。 |
|Bitrate |Float |`20` |聚合算法在数据聚合时间颗粒度内获得的视频码率，单位为 kbps。 |
|Framerate |Float |`20` |聚合算法在数据聚合时间颗粒度内获得的视频帧率，单位为 fps。 |
|AudioFramerate |Float |`20` |聚合算法在数据聚合时间颗粒度内获得的音频帧率（每秒传输的音频数据包数量）。 |
|AudioBitrate |Float |`20` |聚合算法在数据聚合时间颗粒度内获得的音频码率，单位为 kbps。 |
|AudioPts |Double |`9558439` |当前数据聚合时间颗粒度内最后一个音频帧的显示时间戳（PTS），单位为毫秒。 |
|VideoPts |Double |`9558438` |当前数据聚合时间颗粒度内最后一个视频帧的显示时间戳（PTS），单位为毫秒。 |
|PtsDelta |Float |`1` |聚合算法在当前数据聚合时间颗粒度内获得的所有音频帧和视频帧的显示时间戳差值，即所有音频 PTS 与视频 PTS 的最大差值，单位为毫秒。 |
|AudioFrameGap |Float |`20` |聚合算法在当前数据聚合时间颗粒度内获得的相邻音频帧的显示时间戳差值，单位为毫秒。 |
|VideoFrameGap |Float |`20` |聚合算法在当前数据聚合时间颗粒度内获得的相邻视频帧的显示时间戳差值，单位为毫秒。 |
|StreamBeginTime |Long |`1723726121000` |推流开始时间，采用 Unix 时间戳，单位为毫秒。 |
|FirstFrameTime |Integer |`10` |推流连接建立到收到首帧的耗时，单位为毫秒。 |
|ClientIp |String |`127.0.0.1` |推流客户端的 IP 地址。 |
|ServerIp |String |`127.0.0.1` |推流服务器的 IP 地址。 |
|Resolution |String |`1280x720` |推流画面分辨率。 |
|VCodec |String |`H264` |视频编码。 |
|ACodec |String |`AAC` |音频编解码。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchPushStreamMetrics&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 5,
    "AggType": "max"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveBatchPushStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "push.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 5,
        "StreamMetricList": [
            {
                "Domain": "push.example.com",
                "App": "live",
                "Stream": "example_stream",
                "MetricList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Bitrate": 20,
                        "Framerate": 20,
                        "AudioFramerate": 20,
                        "AudioBitrate": 20,
                        "AudioPts": 9558439,
                        "VideoPts": 9558438,
                        "PtsDelta": 1,
                        "AudioFrameGap": 20,
                        "VideoFrameGap": 20,
                        "FirstFrameTime": 10,
                        "ClientIp": "127.0.0.1",
                        "ServerIp": "127.0.0.1",
                        "Resolution": "1280x720",
                        "StreamBeginTime": 1723726121000,
                        "VCodec": "H264",
                        "ACodec": "AAC"
                    }
                ],
                "SessionID": "1961227fe2ab4da7a3f28"
            }
        ],
        "AggType": "max"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106996#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |由于当前账号下不存在所请求的资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
