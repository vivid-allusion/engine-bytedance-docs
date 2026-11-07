---
title: "DescribeLiveTranscodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetranscodedata-zh-CN"
---

调用 `DescribeLiveTranscodeData` API，查询指定直播域名在指定时间范围内的转码时长用量。

<span id="Requirements"></span>
## 要求


* 计费情况：有关转码价格，请参阅 [Transcoding](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-transcoding)。

* 限制：支持查询指定域名（包括已删除域名）产生的转码总时长。

* 频率限制：每个账号每秒最多30次查询

* 数据延迟：20分钟


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveTranscodeData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含 [common parameters](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTranscodeData` |该API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com","push2.example.com"]` |域名列表。默认情况下为空，表示将查询你在 BytePlus MediaLive 下所有域名的转码用量数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或在 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取待查询的域名。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，需同时传入 <code>应用</code> 和 <code>流</code> 参数。</div><br> |
|流 |String |否 |`example_stream` |直播流URL中的StreamName字段。可包含大写和小写字母（A\-Z，a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度数据时，必须同时传入 <code>应用</code> 和 <code>流</code> 参数。</div><br> |
|TranscodeType |Array of String |否 |`["Normal_H264","ByteHD_H265"]` |视频编码格式：若为空，则不指定具体编码格式。支持的取值如下：<br><br><br>* `Normal_H264`：H.264。<br><br>* `Normal_H265`：H.265。<br><br>* `Normal_H266`：H.266。<br><br>* `ByteHD_H264`：极智超清模式下的H.264。<br><br>* `ByteHD_H265`：极智超清模式下的H.265。<br><br>* `ByteHD_H266`：极智超清模式下的H.266。<br><br>* `Audio`：纯音频流。 |
|分辨率 |Array of String |否 |`["720P","1080P"]` |转码分辨率档位为可选项，默认不指定分辨率。例如，选择 `720P` 表示转码配置将针对面积（长边乘短边）大于 `480P` 分辨率（640x480）且不超过 `720P` 分辨率（1280x720）的视频。支持的取值及含义如下：<br><br><br>* `480P`：640 × 480；<br><br>* `720P`：1280 × 720；<br><br>* `1080P`：1920 × 1080；<br><br>* `2K`：2560 × 1440；<br><br>* `4K`：4096 × 2160；<br><br>* `8K`：大于4096 x 2160；<br><br>* `0P`：纯音频转码，表示无视频内容。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，需采用RFC 3339格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">单次查询的最大时间跨度为93天，历史查询的最大时间范围为366天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |否 |`86400` |数据聚合时间颗粒度：数据聚合的单位，当前接口默认且仅支持以86400秒（1天）为间隔进行数据聚合。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专属返回调用结果参数，请参见下表。更多详情请参阅 [Request response](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com","push2.example.com"]` |域名列表。 |
|应用 |String |`live` |查询流颗粒度数据时的流的AppName字段。 |
|流 |String |`example_stream` |查询流颗粒度数据时的流的StreamName字段。 |
|TranscodeType |Array of String |`["Normal_H264","ByteHD_H265"]` |查询的视频编码格式，支持以下取值：<br><br><br>* `Normal_H264`: H.264。<br><br>* `Normal_H265`: H.265。<br><br>* `Normal_H266`: H.266。<br><br>* `ByteHD_H264`: 高清低码转码下的H.264。<br><br>* `ByteHD_H265`: 高清低码转码下的H.265。<br><br>* `ByteHD_H266`: 高清低码转码下的H.266。<br><br>* `Audio`: 纯音频流。 |
|分辨率 |Array of String |`["720P","1080P"]` |查询的转码分辨率档位，支持以下取值及对应像素维度：<br><br><br>* `480P`: 640 × 480；<br><br>* `720P`: 1280 × 720；<br><br>* `1080P`: 1920 × 1088；<br><br>* `2K`: 2560 × 1440；<br><br>* `4K`: 4096 × 2160；<br><br>* `8K`: 大于4096 × 2160；<br><br>* `0P`: 音频转码，表示无视频内容。 |
|StartTime |String |`2021-04-13T00:00:00Z` |查询范围的开始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |String |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |`300` |数据颗粒度，单位为秒。 |
|时长 |Float |`12.860403541550001` |指定时间范围内的转码总时长，单位为分钟。 |
|TranscodeDataList |Array of [TranscodeDataList](https://docs.byteplus.com/en/docs/24/107049#transcodedatalist) |`-` |所有颗粒度数据：所有可用时间颗粒度的数据。 |


<span id="transcodedatalist"></span>
### TranscodeDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TranscodeType |String |`Normal_H264` |查询的视频编码格式，支持以下取值：<br><br><br>* `Normal_H264`: H.264。<br><br>* `Normal_H265`: H.265。<br><br>* `Normal_H266`: H.266。<br><br>* `ByteHD_H264`: 高清低码转码下的H.264。<br><br>* `ByteHD_H265`: 高清低码转码下的H.265。<br><br>* `ByteHD_H266`: 高清低码转码下的H.266。<br><br>* `Audio`: 纯音频流。 |
|分辨率 |String |`720P` |查询的转码分辨率档位，支持以下取值：<br><br><br>* `480P`: 640 × 480；<br><br>* `720P`: 1280 × 720；<br><br>* `1080P`: 1920 × 1088；<br><br>* `2K`: 2560 × 1440；<br><br>* `4K`: 4096 × 2160；<br><br>* `8K`: 大于4096 × 2160；<br><br>* `0P`: 音频转码，表示无视频内容。 |
|TimeStamp |String |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的开始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|时长 |Float |`1.4475713543666666` |当前数据聚合时间颗粒度内的转码总时长，单位为分钟。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTranscodeData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "push2.example.com"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 86400
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveTranscodeData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 86400,
        "Duration": 12.860403541550001,
        "TranscodeDataList": [
            {
                "Duration": 1.4475713543666666,
                "Resolution": "720P",
                "TimeStamp": "2022-03-07T00:00:00Z",
                "TranscodeType": "Normal_H264"
            },
            {
                "Duration": 11.412832187183334,
                "Resolution": "720P",
                "TimeStamp": "2022-03-08T00:00:00Z",
                "TranscodeType": "Normal_H264"
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [Common error codes of BytePlus OpenAPI](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107049#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持部门](https://console.byteplus.com/workorder/create)。 |
