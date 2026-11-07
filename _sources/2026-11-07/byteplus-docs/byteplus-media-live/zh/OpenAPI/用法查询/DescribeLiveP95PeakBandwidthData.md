---
title: "DescribeLiveP95PeakBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivep95peakbandwidthdata-zh-CN"
---

调用 `DescribeLiveP95PeakBandwidthData` API，查询指定直播域名在指定时间范围内的95百分位带宽峰值使用情况，包括推流域名的上行95百分位带宽峰值和拉流域名的下行95百分位带宽峰值。

<span id="Requirements"></span>
## 要求


* 限制：支持查询指定域名（包括已删除域名）产生的95百分位带宽峰值使用数据。

* 频率限制：每个账号每秒最多查询30次

* 数据延迟：15分钟

* 数据指标：带宽数据以1000为基数进行计算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveP95PeakBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除了API专属参数外，还必须携带[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveP95PeakBandwidthData` |API操作。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。默认情况下为空，表示将查询你在BytePlus MediaLive下所有域名的带宽使用数据。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API或前往BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的域名。 |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，需使用RFC 3339格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">单次查询的最大时间跨度为31天，历史查询的最大时间范围为366天。</div><br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，需使用RFC 3339格式，精确到秒。 |
|Aggregation |Integer |否 |`300` |数据聚合的时间颗粒度为秒，当前接口默认且仅支持以`300`秒为间隔进行数据分段。 |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "HTTP-HLS"]` |推拉流协议。默认表示所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于HTTP协议的推拉流协议，采用FLV格式进行视频传输。<br><br>* `HTTP-HLS`：基于HTTP协议的推拉流协议，采用TS格式进行视频传输。<br><br>* `RTMP`：实时消息传输协议，用于实时消息传输。<br><br>* `RTM`：实时媒体协议，用于超低延时直播。<br><br>* `SRT`：安全可靠传输协议，用于安全可靠的流传输。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议。<br><br>* `CMAF`：通用媒体应用格式，一种多功能流媒体协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若查询<code>QUIC</code>协议时，不能同时查询其他协议。</div><br> |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/106964#region) |否 |`-` |CDN节点IP所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">RegionList和UserRegionList不能在同一个请求中同时使用。</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/106964#region) |否 |`-` |客户端 IP 所属区域列表，默认表示全部区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 和 <code>UserRegionList</code> 不能在同一个请求中同时使用。</div><br> |


<span id="region"></span>
### Region


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |String |否 |`CN` |区域信息中的主要区域标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。 |
|Country |String |否 |`CN` |区域信息中的国家标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。按国家过滤时，需要同时传入 'Area' 和 'Country'。 |
|Province |String |否 |`beijing` |区域信息中的省份标识符目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取标识符信息。按省份过滤时，需要同时传入 `Area`、`Country` 和 `Province`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关API专属返回调用结果参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |String 数组 |`["push.example.com"]` |域名列表。 |
|StartTime |String |`2022-04-18T20:00:00Z` |查询范围的起始时间（UTC 时间，RFC 3339 格式，精确到秒）。 |
|EndTime |String |`2022-04-18T22:00:00Z` |查询范围的结束时间（UTC 时间，RFC 3339 格式，精确到秒）。 |
|Aggregation |Integer |`300` |数据颗粒度，单位为秒。 |
|ProtocolList |String 数组 |`["HTTP-FLV", "HTTP-HLS"]` |推拉流协议。默认表示全部协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于 HTTP 协议的推拉流协议，采用 FLV 格式进行视频传输。<br><br>* `HTTP-HLS`：基于 HTTP 协议的推拉流协议，采用 TS 格式进行视频传输。<br><br>* `RTMP`：RTMP，用于实时消息传输。<br><br>* `RTM`：实时媒体协议，用于超低延时直播。<br><br>* `SRT`：安全可靠传输协议，用于安全可靠的流传输。<br><br>* `QUIC`：Quick UDP Internet Connections，一种基于 UDP 的新型低延迟互联网传输协议。<br><br>* `CMAF`：通用媒体应用格式，一种多用途流协议。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/106964#region) 数组 |`-` |CDN 节点 IP 所属区域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/106964#region) 数组 |`-` |客户端 IP 所属区域列表。 |
|P95PeakBandwidth |Float |`100` |指定时间范围内 95 分位上行和下行带宽峰值之和。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若请求时指定了多个 <code>RegionList</code>，则返回这些区域的 95 分位上行和下行带宽峰值之和。</div><br> |
|P95PeakTimestamp |String |`2022-04-18T22:00:00Z` |95 分位带宽峰值的时间戳，UTC 时间，RFC 3339 格式，精确到秒。 |


<span id="region"></span>
### Region


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |String |`CN` |区域信息中的区域标识符。 |
|Country |String |`CN` |区域信息中的国家标识符。 |
|Province |String |`beijing` |区域信息中的省份标识符。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveP95PeakBandwidthData&Version=2023-01-01
{
    "StartTime": "2022-04-18T20:00:00Z",
    "EndTime": "2022-04-18T22:00:00Z",
    "Aggregation": 300
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveP95PeakBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "StartTime": "2022-04-18T20:00:00Z",
        "EndTime": "2022-04-18T22:00:00Z",
        "Aggregation": 300,
        "P95PeakBandwidth": 100,
        "P95PeakTimestamp": "2022-04-18T22:00:00Z"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/106964#request-parameters)进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生了内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
