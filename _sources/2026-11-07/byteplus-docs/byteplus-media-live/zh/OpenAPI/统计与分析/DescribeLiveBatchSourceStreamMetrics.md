---
title: "DescribeLiveBatchSourceStreamMetrics"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivebatchsourcestreammetrics-zh-CN"
---

获取在指定拉流域名下，所有或指定源拉流流在指定时间范围内的监控数据，例如音视频的帧率和码率。您可以使用监控数据评估源拉流流的健康状况。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">您可以获取由已删除域名生成的历史源拉流流数据。</div>


<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多30次请求

* 数据延迟：15分钟


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveBatchSourceStreamMetrics&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBatchSourceStreamMetrics` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Domain |String |是 |`pull.example.com` |拉流域名。您可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或在**Domains**页面的[BytePlus MediaLive控制台](https://console.byteplus.com/live/main/domain/list)获取源拉流流用于拉流的域名。 |
|应用 |String |否 |`live` |应用名称。参数值必须与直播流地址中的`AppName`字段值一致。参数值长度必须为1\-30个字符，并包含以下字符：<br><br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 数字（0\-9）<br><br>* 连字符（\-）<br><br>* 下划线（_）<br><br>* 点（.）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">获取指定源拉流流的监控数据时，此参数为必填，且必须同时传递<code>Stream</code>参数。</div><br> |
|Stream |String |否 |`example_stream` |流名称。参数值必须与直播流地址中的`StreamName`字段值一致。参数值长度必须为1\-100个字符，并包含以下字符：<br><br><br>* 小写字母（a\-z）<br><br>* 大写字母（A\-Z）<br><br>* 数字（0\-9）<br><br>* 连字符（\-）<br><br>* 下划线（_）<br><br>* 点（.）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">获取指定源拉流流的监控数据时，此参数为必填，且必须同时传递<code>应用</code>参数。</div><br> |
|StartTime |String |是 |`2021-08-16T00:00:00+08:00` |查询范围的起始时间（RFC 3339格式的UTC时间，精确到秒）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">最大历史查询范围为366天。单次查询的最大时间跨度为1天。</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59+08:00` |查询范围的结束时间（RFC 3339格式的UTC时间，精确到秒）。 |
|Aggregation |Integer |否 |`30` |数据聚合的时间颗粒度，单位为秒。默认值：`60`。有效值：<br><br><br>* `30`：30秒。<br><br>* `60`：1分钟。 |
|AggType |String |否 |`max` |数据聚合时间颗粒度内动态指标的聚合算法。默认值：`max`。有效值：<br><br><br>* `max`：在聚合时间颗粒度内计算最大值。<br><br>* `avg`：在聚合时间颗粒度内计算平均值。 |


<span id="Response parameters"></span>
## 返回参数

有关唯一的API专属返回参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|域名 |字符串 |`pull.example.com` |拉流域名。 |
|应用 |字符串 |`live` |应用名称。 |
|流 |字符串 |`example_stream` |流名称。 |
|StartTime |字符串 |`2021-04-13T00:00:00+08:00` |查询范围的起始时间（RFC 3339 格式的 UTC 时间，精确到秒）。 |
|EndTime |字符串 |`2021-04-14T00:00:00+08:00` |查询范围的结束时间（RFC 3339 格式的 UTC 时间，精确到秒）。 |
|Aggregation |整数 |`30` |数据聚合的时间颗粒度，单位为秒。有效值：<br><br><br>* `30`：30 秒。<br><br>* `60`：1 分钟。 |
|流指标列表 |[流指标列表](https://docs.byteplus.com/en/docs/24/107050#streammetriclist)数组 |`-` |源拉流信息。 |
|AggType |字符串 |`max` |在数据聚合时间颗粒度内的动态指标聚合算法。有效值：<br><br><br>* `max`：在聚合时间颗粒度内计算最大值。<br><br>* `avg`：在聚合时间颗粒度内计算平均值。 |


<span id="streammetriclist"></span>
### StreamMetricList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|域名 |字符串 |`pull.example.com` |拉流域名。 |
|应用 |字符串 |`live` |应用名称。 |
|流 |字符串 |`example_stream` |流名称。 |
|指标列表 |[指标列表](https://docs.byteplus.com/en/docs/24/107050#metriclist)数组 |`-` |按指定时间颗粒度聚合的监控数据。 |


<span id="metriclist"></span>
### MetricList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|时间戳 |字符串 |`2022-04-13T00:00:00+08:00` |按时间颗粒度聚合数据时，每个颗粒度的起始时间（RFC 3339 格式的 UTC 时间，精确到秒）。 |
|码率 |浮点数 |`20` |当前数据聚合时间颗粒度内，通过聚合算法获得的视频码率，单位为 kbps。 |
|帧率 |浮点数 |`20` |当前数据聚合时间颗粒度内，通过聚合算法获得的视频帧率，单位为 fps。 |
|音频帧率 |浮点数 |`20` |当前数据聚合时间颗粒度内，通过聚合算法获得的音频帧率，单位为 fps。 |
|音频码率 |浮点数 |`20` |当前数据聚合时间颗粒度内，通过聚合算法获得的音频码率，单位为 kbps。 |
|音频PTS |双精度浮点数 |`1651831909` |当前数据聚合时间颗粒度内最后一个音频帧的显示时间戳（PTS），单位为毫秒。 |
|视频PTS |双精度浮点数 |`1651831910` |当前数据聚合时间颗粒度内最后一个视频帧的 PTS，单位为毫秒。 |
|PTS 差值 |浮点数 |`1` |当前数据聚合时间颗粒度内，通过聚合算法获得的音频帧与视频帧 PTS 差值的最大值或平均值，即所有`音频PTS`与`视频PTS`的差值的最大值或平均值，单位为毫秒。 |
|音频帧间隔 |浮点数 |`20` |当前数据聚合时间颗粒度内，通过聚合算法获得的相邻音频帧 PTS 差值的最大值的平均值，单位为毫秒。 |
|视频帧间隔 |浮点数 |`20` |当前数据聚合时间颗粒度内，通过聚合算法获得的相邻视频帧 PTS 差值的最大值或平均值，单位为毫秒。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchSourceStreamMetrics&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "StartTime": "2021-08-16T00:00:00+08:00",
    "EndTime": "2021-08-16T00:01:59+08:00",
    "Aggregation": 30,
    "AggType": "max"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveBatchSourceStreamMetrics",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "StartTime": "2021-04-13T00:00:00+08:00",
        "EndTime": "2021-04-14T00:00:00+08:00",
        "Aggregation": 30,
        "StreamMetricList": [
            {
                "Domain": "pull.example.com",
                "App": "live",
                "Stream": "example_stream",
                "MetricList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00+08:00",
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
        ],
        "AggType": "max"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下是与当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参阅[请求参数](https://docs.byteplus.com/en/docs/24/107050#request-parameters)接口行为以进行校验。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用、配置模版和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
