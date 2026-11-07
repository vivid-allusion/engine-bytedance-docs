---
title: "DescribeLivePushStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivepushstreammetrics-zh-CN"
---

调用 `DescribeLivePushStreamMetrics` API，查询指定时间范围内单个推流的监控数据，如音视频帧率和码率，以评估直播流的健康状况。

<span id="Requirements"></span>
## 要求


* 限制：支持查询由特定域名（包括已删除域名）生成的历史推流数据。

* 频率限制：每个账号每秒最多查询30次

* 数据延迟：30秒


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLivePushStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePushStreamMetrics` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`push.example.com` |推流域名。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面查看用于直播流的推流域名。 |
|应用 |String |是 |`live` |直播流地址中的`AppName`字段。可包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。 |
|流 |String |是 |`example_stream` |直播流地址中的`StreamName`字段。可包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到100个字符。 |
|StartTime |String |是 |`2021-08-16T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">单次查询的最大时间跨度为1天，历史查询的最大时间范围为366天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |否 |`5` |数据聚合的颗粒度（单位：秒），支持以下颗粒度选项：<br><br><br>* `5`：5秒；<br><br>* `30`：（默认）30秒。 |


<span id="Response parameters"></span>
## 返回参数

有关唯一的API专属返回参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |String |`example.com` |推流域名。 |
|应用 |String |`live` |直播流URL中的AppName字段。 |
|流 |String |`example_stream` |直播流URL中的StreamName字段。 |
|StartTime |String |`2021-08-16T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |String |`2021-08-16T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |`5` |数据聚合的颗粒度（单位：秒），支持以下颗粒度选项：<br><br><br>* `5`：5秒；<br><br>* `30`：30秒。 |
|MetricList |[MetricList](https://docs.byteplus.com/en/docs/24/107055#metriclist)数组 |`-` |每个颗粒度下的全部数据。 |


<span id="metriclist"></span>
### MetricList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |String |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|码率 |Float |`20` |当前数据聚合时间颗粒度内的最大视频码率，单位为 kbps。 |
|Framerate |Float |`20` |当前数据聚合时间颗粒度内的最大视频帧率，单位为 fps。 |
|AudioFramerate |Float |`20` |当前数据聚合时间颗粒度内的最大音频帧率，单位为 fps。 |
|AudioBitrate |Float |`20` |当前数据聚合时间颗粒度内的最大音频码率，单位为 kbps。 |
|AudioPts |Double |`9558439` |当前数据聚合时间颗粒度内最后一个音频帧的显示时间戳（PTS），单位为毫秒。 |
|VideoPts |Double |`9558430` |当前数据聚合时间颗粒度内最后一个视频帧的显示时间戳（PTS），单位为毫秒。 |
|PtsDelta |Float |`9` |当前数据聚合时间颗粒度内所有音频帧和视频帧显示时间戳的最大差值，即所有音频 PTS 与视频 PTS 的最大差值，单位为毫秒。 |
|AudioFrameGap |Float |`20` |当前数据聚合时间颗粒度内相邻音频帧显示时间戳的最大差值，单位为毫秒。 |
|VideoFrameGap |Float |`20` |当前数据聚合时间颗粒度内相邻视频帧显示时间戳的最大差值，单位为毫秒。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePushStreamMetrics&Version=2023-01-01
{
    "Domain": "push.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 5
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLivePushStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:00:00Z",
        "Aggregation": 5,
        "MetricList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bitrate": 20,
                "Framerate": 20,
                "AudioFramerate": 20,
                "AudioBitrate": 20,
                "AudioPts": 9558439,
                "VideoPts": 9558430,
                "PtsDelta": 9,
                "AudioFrameGap": 20,
                "VideoFrameGap": 20
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107055#request-parameters)接口行为进行排查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
