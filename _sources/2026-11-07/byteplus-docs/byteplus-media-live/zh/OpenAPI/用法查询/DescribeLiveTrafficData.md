---
title: "DescribeLiveTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata-zh-CN"
---

调用 `DescribeLiveTrafficData` API，在指定时间范围内查询指定直播域名的流量使用情况。此外，还包括推流域名的上行流量数据和拉流域名的下行流量数据。

<span id="Requirements"></span>
## 要求


* 计费情况：有关价格信息，请参阅 [直播服务费用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees)。

* 限制：

   * 支持查询流量使用数据（包括已删除的域名）；

   * 流量使用数据用于计费对账，其采集方式与流量数据监控不同。请使用 [DescribeLiveMetricTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivemetrictrafficdata) 查询直播流量监控数据。

* 频率限制：每个账号每秒最多查询30次。

* 数据延迟：15分钟。

* 数据指标：流量数据以1000为基数计算，例如，1 GB = 1000 MB。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveTrafficData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveTrafficData` |API操作。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["example.com"]` |域名列表。默认情况下为空，表示将查询你在BytePlus MediaLive下所有域名的流量使用数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或在BytePlus MediaLive控制台的 [域名管理](https://console.byteplus.com/live/main/domain/list) 页面获取待查询的域名。 |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流协议。默认包含所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于HTTP的推拉流协议，传输视频格式为FLV。<br><br>* `HTTP-HLS`：基于HTTP的推拉流协议，传输视频格式为TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议。<br><br>* `CMAF`：基于HTTP的高效自适应视频流协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如查询 <code>QUIC</code> 协议时，不能同时查询其他协议。</div><br> |
|ISPList |Array of String |否 |`["telecom"]` |提供网络类型接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。<br><br><br>如需获取各运营商标识，可调用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107035#region) |否 |`-` |CDN节点IP所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 与 <code>UserRegionList</code> 不能在同一请求中同时使用。</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107035#region) |否 |`-` |客户端 IP 所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 和 <code>UserRegionList</code> 不能在同一个请求中同时使用。</div><br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|Aggregation |Integer |否 |`300` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `300`（默认）：5 分钟。以 5 分钟为颗粒度聚合时，单次查询的最大时间跨度为 31 天，历史查询的最大时间范围为 366 天。<br><br>* `3600`：1 小时。以 1 小时为颗粒度聚合时，单次查询的最大时间跨度为 93 天，历史查询的最大时间范围为 366 天。<br><br>* `86400`：1 天。以 1 天为颗粒度聚合时，单次查询的最大时间跨度为 93 天，历史查询的最大时间范围为 366 天。 |
|DetailField |Array of String |否 |`["Domain"]` |数据分割的维度默认不进行分割。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当使用 <code>DetailField</code> 参数指定数据分割维度，并且 <code>DomainList</code>、<code>ProtocolList</code> 或 <code>ISPList</code> 参数中至少有一个传入多个值时，返回调用结果才会按维度进行数据分割。</div><br> |


<span id="region"></span>
### Region


|**Parameter** |**Data Type** |**Required** |**Sample Value** |**接口行为** |
|---|---|---|---|---|
|Area |String |否 |`CN` |区域信息中的主要区域标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。 |
|Country |String |否 |`CN` |区域信息中的国家标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。按国家筛选时，需要同时传入 `Area` 和 `Country`。 |
|Province |String |否 |`beijing` |区域信息中的省份标识符目前仅支持中国大陆、香港、澳门和台湾，其他国家或地区暂不支持。可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取标识符信息。按省份筛选时，需要同时传入 `Area`、`Country` 和 `Province` |


<span id="Response parameters"></span>
## 返回调用结果

有关API专属返回调用结果，请参见下表。更多详情请参阅 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**Parameter** |**Data Type** |**Sample Value** |**接口行为** |
|---|---|---|---|
|DomainList |Array of String |`["example.com"]` |域名列表。 |
|ProtocolList |Array of String |`["HTTP-FLV", "RTMP"]` |推拉流协议，协议说明如下：<br><br><br>* `HTTP-FLV`：基于 HTTP 的推拉流协议，视频格式为 FLV。<br><br>* `HTTP-HLS`：基于 HTTP 的推拉流协议，视频格式为 TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：快速 UDP 网络连接协议，一种基于 UDP 的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种高效、适应性强的基于 HTTP 的视频流协议。 |
|ISPList |Array of String |`["telecom"]` |表示互联网服务提供商（ISP）标识符的数组。有效选项包括：<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网络（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107035#region)数组 |`-` |CDN节点IP所属区域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107035#region)数组 |`-` |客户端IP所属区域列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|DetailField |字符串数组 |`["Domain"]` |用于数据分割的维度及其说明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。 |
|TotalUpTraffic |浮点数 |`20` |查询时间范围内的上行流量总量，单位为GB。 |
|TotalDownTraffic |浮点数 |`20` |查询时间范围内的下行流量总量，单位为GB。 |
|TrafficDataList |[TrafficData](https://docs.byteplus.com/en/docs/24/107035#trafficdata)数组 |`-` |每个颗粒度的全部数据。 |
|TrafficDetailDataList |[TrafficDetailData](https://docs.byteplus.com/en/docs/24/107035#trafficdetaildata)数组 |`-` |按维度分割的数据。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当使用<code>DetailField</code>参数指定数据分割维度，并且<code>DomainList</code>、<code>ProtocolList</code>或<code>ISPList</code>参数中至少有一个传入多个值时，返回调用结果中才会出现按维度分割的数据。</div><br> |


<span id="region"></span>
### Region


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识符。 |
|Country |字符串 |`CN` |区域信息中的国家标识符。 |
|Province |字符串 |`beijing` |区域信息中的省份标识符。 |


<span id="trafficdata"></span>
### TrafficData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|UpTraffic |浮点数 |`20` |当前数据聚合颗粒度内产生的上行流量总量，单位为GB。 |
|DownTraffic |浮点数 |`20` |当前数据聚合颗粒度内产生的下行流量总量，单位为GB。 |


<span id="trafficdetaildata"></span>
### TrafficDetailData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`example.com` |按域名维度分割数据时的域名信息。 |
|Protocol |字符串 |`HTTP-FLV` |按推拉流协议维度分割数据时的协议信息。 |
|ISP |字符串 |`telecom` |按运营商维度分割数据时的运营商信息。 |
|TotalUpTraffic |浮点数 |`0` |按当前维度分割后产生的上行流量总量，单位为GB。 |
|TotalDownTraffic |浮点数 |`0` |按当前维度分割后产生的下行流量总量，单位为GB。 |
|TrafficDataList |[TrafficData](https://docs.byteplus.com/en/docs/24/107035#trafficdata)数组 |`-` |按当前维度分割后，所有时间颗粒度下的数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveTrafficData&Version=2023-01-01
{
    "DomainList": [
        "example.com"
    ],
    "ProtocolList": [
        "HTTP-FLV",
        "RTMP"
    ],
    "ISPList": [
        "telecom"
    ],
    "RegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Protocol"
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "cn-north-1"
    },
    "Result": {
        "DomainList": [
            "example.com"
        ],
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "ISPList": [
            "telecom"
        ],
        "RegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "TotalUpTraffic": 20,
        "TotalDownTraffic": 20,
        "TrafficDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            },
            {
                "TimeStamp": "2022-04-13T00:05:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "TrafficDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "TotalUpTraffic": 20,
                "TotalDownTraffic": 20,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20
                    }
                ]
            },
            {
                "Protocol": "RTMP",
                "TotalUpTraffic": 0,
                "TotalDownTraffic": 0,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 0,
                        "DownTraffic": 0
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpTraffic": 0,
                        "DownTraffic": 0
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107035#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |因当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书），请求被拒绝。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
