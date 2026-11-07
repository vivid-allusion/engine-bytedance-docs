---
title: "DescribeLiveASRDurationData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveasrdurationdata-zh-CN"
---

调用 `DescribeLiveASRDurationData` API，在指定时间范围内查询 AI 语音转字幕的时长。

<span id="Requirements"></span>
## 要求

频率限制：每个账号每秒最多 30 次查询

<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveASRDurationData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除了 API 专属参数外，还必须携带 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveASRDurationData` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body 参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。默认情况下为空，表示将查询你 BytePlus MediaLive 下所有域名的 AI 语音转字幕使用时长数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API 或前往 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取待查询的域名。 |
|AppList |Array of String |否 |`["live"]` |应用名称列表，需与直播流 URL 中的 AppName 字段值一致。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为 1 到 30 个字符。 |
|ASRSourceType |String |否 |`ZH` |该参数指的是 AI 语音转字幕过程中语音的语言类型。默认表示查询所有语言。具体取值及含义如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韩文。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>ASRTargetTypeList</code> 和 <code>ASRSourceType</code> 必须同时指定。</div><br> |
|ASRTargetTypeList |Array of String |否 |`["ZH"]` |AI 语音转字幕过程中生成的字幕语言类型列表。默认表示查询所有语言。具体取值及含义如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韩文。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>ASRTargetTypeList</code> 和 <code>ASRSourceType</code> 必须同时指定。</div><br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，格式为 RFC 3339，精确到秒。 |
|EndTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的结束时间，格式为 RFC 3339，精确到秒。 |
|Aggregation |Integer |否 |`300` |聚合时间颗粒度，单位为秒，支持以下颗粒度：<br><br><br>* `300`：（默认）5 分钟。当颗粒度为 5 分钟时，单次查询最大时间跨度为 31 天，历史查询时间范围为 93 天；<br><br>* `3600`：1 小时。当颗粒度为 1 小时时，单次查询最大时间跨度为 93 天，历史查询时间范围为 93 天；<br><br>* `86400`：1 天。当颗粒度为 1 天时，单次查询最大时间跨度为 93 天，历史查询时间范围为 93 天。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |Array of String |`["push.example.com"]` |域名列表。 |
|AppList |字符串数组 |`["live"]` |应用名称列表。 |
|ASRSourceType |字符串 |`ZH` |AI语音转字幕过程中语音的语言类型，取值及含义如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韩文。 |
|ASRTargetTypeList |字符串数组 |`["ZH"]` |AI语音转字幕过程中生成的字幕语言类型列表，取值及含义如下：<br><br><br>* `ZH`：中文；<br><br>* `EN`：英文；<br><br>* `JA`：日文；<br><br>* `KO`：韩文。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|时长 |浮点数 |`1.1` |AI语音转字幕转码的总时长，单位为分钟。 |
|ASRDurationData |[ASRDurationData](https://docs.byteplus.com/en/docs/24/107012#asrdurationdata)数组 |`-` |所有时间颗粒度的数据。 |
|ASRDurationDetailData |[ASRDurationDetailData](https://docs.byteplus.com/en/docs/24/107012#asrdurationdetaildata)数组 |`-` |按AI语音转字幕过程中生成的字幕语言类型拆分的时间颗粒度详细数据。 |


<span id="asrdurationdata"></span>
### ASRDurationData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2021-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339格式的UTC时间戳，精确到秒。 |
|时长 |浮点数 |`1.1` |当前数据聚合时间颗粒度内AI语音转字幕的时长，单位为分钟。 |


<span id="asrdurationdetaildata"></span>
### ASRDurationDetailData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|ASRSourceType |字符串 |`ZH` |AI语音转字幕过程中语音的语言类型。 |
|ASRTargetTypeList |字符串数组 |`["ZH"]` |AI语音转字幕过程中生成的字幕语言类型列表。 |
|ASRDurationData |[ASRDurationData](https://docs.byteplus.com/en/docs/24/107012#asrdurationdata)数组 |`-` |按语音语言类型拆分的所有时间颗粒度数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveASRDurationData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "AppList": [
        "live"
    ],
    "ASRSourceType": "ZH",
    "ASRTargetTypeList": [
        "ZH"
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-13T00:00:00Z",
    "Aggregation": 300
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveASRDurationData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "AppList": [
            "live"
        ],
        "ASRSourceType": "ZH",
        "ASRTargetTypeList": [
            "ZH"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-13T00:00:00Z",
        "Aggregation": 300,
        "Duration": 1.1,
        "ASRDurationData": [
            {
                "TimeStamp": "2021-04-13T00:00:00Z",
                "Duration": 1.1
            }
        ],
        "ASRDurationDetailData": [
            {
                "ASRSourceType": "ZH",
                "ASRTargetTypeList": [
                    "ZH"
                ],
                "ASRDurationData": [
                    {
                        "TimeStamp": "2021-04-13T00:00:00Z",
                        "Duration": 1.1
                    }
                ]
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
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107012#request-parameters)接口行为进行检查。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
