---
title: "DescribeLiveStreamCountData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata-zh-CN"
---

获取指定推流、回源拉流或转码流在特定时间范围内的峰值流数量。

<span id="Requirements"></span>
## 要求


* 请求频率限制：每个账号每秒最多30次请求

* 数据延迟：5分钟


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveStreamCountData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStreamCountData` |API操作名称。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|StartTime |String |是 |`2021-08-16T00:00:00+08:00` |查询范围的起始时间（UTC时间，RFC 3339格式，精确到秒）。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">最大历史查询范围为366天。单次查询的最大时间跨度取决于数据聚合的颗粒度。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">若数据每60秒聚合一次，即<code>Aggregation</code>的值设置为<code>60</code>，则单次查询最大时间跨度为24小时。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若数据每300秒聚合一次，即<code>Aggregation</code>的值设置为<code>300</code>，则单次查询最大时间跨度为31天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">若数据每3600秒聚合一次，即<code>Aggregation</code>的值设置为<code>3600</code>，则单次查询最大时间跨度为31天。</div><br> |
|EndTime |String |是 |`2021-08-16T00:01:59+08:00` |查询范围的结束时间（UTC时间，RFC 3339格式，精确到秒）。 |
|DomainList |String数组 |否 |`["push.exmaple.com","push2.example.com"]` |用于直播的域名列表。默认情况下，此列表为空，表示返回所有域名的峰值流数量。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023)或在**Domains**页面的[BytePlus MediaLive控制台](https://console.byteplus.com/live/main/domain/list)获取用于直播的域名。 |
|StreamType |String数组 |否 |`["push"]` |流类型。默认情况下，将返回所有流类型的峰值流数量。有效值：<br><br><br>* `push`：推流。<br><br>* `relay-source`：回源拉流。<br><br>* `transcode`：转码流。 |
|ISPList |String数组 |否 |`["telecom"]` |互联网服务提供商（ISP）标识。默认情况下，将返回所有ISP的峰值流数量。有效值：<br><br><br>* `unicom`：中国联通。<br><br>* `telecom`：中国电信。<br><br>* `mobile`：中国移动。<br><br>* `cernet`：中国教育和科研网（CERNET）。<br><br>* `drpeng`：Dr.鹏电信传媒集团<br><br>* `btvn`：广播电视网络（BTVN）<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">仅当<code>StreamType</code>的值为<code>push</code>时，此参数生效。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">你也可以调用<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata">DescribeLiveISPData</a>获取ISP标识。</div><br> |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107016#userregionlist)数组 |否 |`-` |客户端IP所属区域列表。默认情况下，将返回所有区域的峰值流数量。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>StreamType</code>的值为<code>push</code>时，此参数生效。</div><br> |
|Aggregation |Integer |否 |`60` |用于数据聚合的时间颗粒度，单位为秒。默认值：`300`。有效取值：<br><br><br>* `60`：1分钟。<br><br>* `300`：5分钟。<br><br>* `3600`：1小时。 |
|DetailField |字符串数组 |否 |`["Domain"]` |用于数据分割的维度。默认情况下，数据不会按维度进行分割。<br><br>当前该参数仅支持取值`Domain`，表示按域名分割数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>DomainList</code>参数设置多个值时，该参数才生效。</div><br> |


<span id="userregionlist"></span>
### UserRegionList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`AP1` |区域标识符。可调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取区域标识符。 |
|Country |字符串 |否 |`CN` |国家标识符。可调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取国家标识符。如需按国家筛选，需同时传入`Area`和`Country`参数。 |
|Province |字符串 |否 |`HK` |省份标识符。可调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取省份标识符。如需按省份筛选，必须同时传入`Area`、`Country`和`Province`参数。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专属返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com","push2.example.com"]` |域名列表。 |
|StartTime |字符串 |`2021-08-16T00:00:00+08:00` |查询范围的起始时间（UTC时间，RFC 3339格式，精确到秒）。 |
|EndTime |字符串 |`2021-08-16T00:01:59+08:00` |查询范围的结束时间（UTC时间，RFC 3339格式，精确到秒）。 |
|Aggregation |整数 |`60` |用于数据聚合的时间颗粒度，单位为秒。有效取值：<br><br><br>* `60`：1分钟。<br><br>* `300`：5分钟。<br><br>* `3600`：1小时。 |
|DetailField |字符串数组 |`["Domain"]` |用于数据分割的维度。当前该参数仅支持取值`Domain`，表示按域名分割数据。 |
|StreamType |字符串数组 |`["push"]` |流类型。有效取值：<br><br><br>* `push`：推流。<br><br>* `relay-source`：源站拉流。<br><br>* `transcode`：转码流。 |
|PeakCount |整数 |`100` |当前查询条件下的流峰值，即在指定时间范围内推流、源站拉流或转码流的最大并发数。 |
|TotalStreamDataList |[TotalStreamDataList](https://docs.byteplus.com/en/docs/24/107016#totalstreamdatalist)数组 |`-` |所有时间颗粒度的数据。 |
|StreamDetailDataList |[StreamDetailDataList](https://docs.byteplus.com/en/docs/24/107016#streamdetaildatalist)数组 |`-` |按域名分割的数据。 |
|ISPList |字符串数组 |`["telecom"]` |互联网服务提供商（ISP）标识符。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107016#userregionlist)数组 |`-` |客户端IP所属区域列表。 |


<span id="totalstreamdatalist"></span>
### TotalStreamDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2021-08-16T00:00:00+08:00` |按时间颗粒度聚合数据时，每个颗粒度的起始时间（UTC时间，RFC 3339格式，精确到秒）。 |
|PeakCount |整数 |`100` |当前时间颗粒度下聚合数据的最大流数量。 |


<span id="streamdetaildatalist"></span>
### StreamDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`push.example.com` |按域名分割数据时的域名信息。 |
|TotalStreamDataList |[TotalStreamDataList](https://docs.byteplus.com/en/docs/24/107016#totalstreamdatalist)数组 |`-` |按域名分割后，当前域名下所有时间颗粒度的数据。 |


<span id="userregionlist"></span>
### UserRegionList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`AP1` |区域标识符。 |
|Country |字符串 |`CN` |国家标识符。 |
|Province |字符串 |`HK` |省份标识符。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStreamCountData&Version=2023-01-01
{
    "DomainList": [
        "example1.com",
        "example2.com"
    ],
    "StartTime": "2021-08-16T00:00:00Z",
    "EndTime": "2021-08-16T00:01:59Z",
    "Aggregation": 60,
    "DetailField": [
        "Domain"
    ],
    "StreamType": [
        "pull",
        "relay-source"
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveSourceStreamCountData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "example1.com",
            "example2.com"
        ],
        "StartTime": "2021-08-16T00:00:00Z",
        "EndTime": "2021-08-16T00:01:59Z",
        "Aggregation": 60,
        "DetailField": [
            "Domain"
        ],
        "StreamType": [
            "pull",
            "relay-source"
        ],
        "PeakCount": 100,
        "TotalStreamDataList": [
            {
                "TimeStamp": "2021-08-16T00:00:00Z",
                "PeakCount": 100
            }
        ],
        "StreamDetailDataList": [
            {
                "Domain": "example1.com",
                "TotalStreamDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "PeakCount": 100
                    }
                ]
            },
            {
                "Domain": "example2.com",
                "TotalStreamDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "PeakCount": 100
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**Status Code** |**Error Code** |**Error Message** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107016#request-parameters)接口行为进行校验。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域命名空间、域名、应用、配置模版和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
