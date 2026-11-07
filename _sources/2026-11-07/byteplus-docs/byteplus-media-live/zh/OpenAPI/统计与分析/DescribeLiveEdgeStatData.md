---
title: "DescribeLiveEdgeStatData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describeliveedgestatdata-2023-zh-CN"
---

调用`DescribeLiveEdgeStatData`接口，可查询指定协议、运营商、区域及时间范围下的上行和下行流量、上行和下行带宽峰值，以及在线流产生的请求数等数据。

<span id="Usage scenario"></span>
## 使用场景


* 限制：

   * 带宽数据用于数据监控，其采集方式与带宽使用数据不同。请使用[DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata)接口查询直播带宽使用数据。

   * 流量数据用于数据监控，其采集方式与流量使用数据不同。请使用[DescribeLiveTrafficData](https://docs.byteplus.com/en/docs/byteplus-media-live/describelivetrafficdata) API查询直播流量使用数据。

* 频率限制：每个账号每秒最多查询30次。

* 数据延迟：

   * 当聚合颗粒度为60秒时，数据延迟为5分钟；

   * 其他时间颗粒度下，数据延迟为15分钟。

* 数据指标：

   * 带宽数据以1000为基数进行计算，例如，1 Mbps = 1000 Kbps。

   * 流量数据以1000为基数进行计算，例如，1 GB = 1000 MB。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveEdgeStatData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除需传递API专属参数外，还需传递[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveEdgeStatData` |API操作名称。 |
|Version |String |是 |`2023-01-01` |本API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |String数组 |否 |`["push.example.com","pull.example.com"]` |域名列表。默认情况下为空，表示将查询你在BytePlus MediaLive下的所有域名。你可以调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail)API或在BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的域名。 |
|AppList |String数组 |否 |`["live","vodlive"]` |直播流URL中的AppName字段列表。默认情况下为空，表示将查询所有AppName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至30个字符。 |
|StreamList |String数组 |否 |`["stream001","stream002"]` |直播流URL中的StreamName字段列表。默认情况下为空，表示将查询所有StreamName。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至100个字符。 |
|ProtocolList |String数组 |否 |`["HTTP-FLV", "RTMP"]` |推拉流协议。默认包含所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于HTTP的推拉流协议，传输视频格式为FLV。<br><br>* `HTTP-HLS`：基于HTTP的推拉流协议，传输视频格式为TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：快速UDP互联网连接协议，一种基于UDP的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种用于高效、适应性视频流通过 HTTP 传输的协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">如果查询 <code>QUIC</code> 协议，则无法同时查询其他协议。</div><br> |
|ISPList |字符串数组 |否 |`["unicom", "telecom"]` |提供网络接入服务的运营商标识符。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。<br><br>   如需获取各运营商的标识符，可调用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107014#region) 数组 |否 |`-` |CDN 节点 IP 所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 与 <code>UserRegionList</code> 不能在同一请求中同时使用。</div><br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107014#region) 数组 |否 |`-` |客户端 IP 所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code> 与 <code>UserRegionList</code> 不能在同一请求中同时使用。</div><br> |
|DetailField |字符串数组 |否 |`["Domain"]` |数据分割的维度默认不进行分割。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。<br><br>* `Area`：CDN 节点 IP 所属区域。<br><br>* `Country`：客户端 IP 所属国家。<br><br>* `UserArea`：客户端 IP 所属区域。<br><br>* `UserCountry`：客户端 IP 所属国家。 |
|Aggregation |整数 |否 | |数据聚合的颗粒度，以秒为单位，支持如下选项：<br><br><br>* `60`：1 分钟。<br><br>* `300`：（默认）5 分钟。<br><br>* `3600`：1 小时。 |
|StartTime |字符串 |是 |`2024-12-12T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">历史查询时间范围为 366 天，单次查询的最大时间跨度取决于 DetailField 和 Aggregation。关系说明如下。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">当不进行维度分割或仅按一个维度分割数据时：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">当数据每 60 秒聚合一次时，单次查询的最大时间跨度为 24 小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">当数据每 300 秒聚合一次时，单次查询的最大时间跨度为 31 天。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">当数据每 3600 秒聚合一次时，单次查询的最大时间跨度为 31 天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">当按两个及以上维度分割数据时：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">当数据每 60 秒聚合一次时，单次查询的最大时间跨度为 3 小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">当数据每 300 秒聚合一次时，单次查询的最大时间跨度为 24 小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">当数据每 3600 秒聚合一次时，单次查询的最大时间跨度为 7 天。</div><br> |
|EndTime |字符串 |是 |`2024-12-12T00:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |


<span id="region"></span>
### Region


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |区域信息中的主要区域标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。 |
|Country |字符串 |否 |`CN` |区域信息中的国家标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。按国家筛选时，需要同时传入`Area`和`Country`。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取标识信息。按省份筛选时，需要同时传入`Area`、`Country`和`Province`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于API专属返回调用结果参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com","pull.example.com"]` |域名列表。 |
|AppList |字符串数组 |`["live","livevod"]` |应用名称列表。 |
|StreamList |字符串数组 |`["stream001","stream002"]` |流名称列表。 |
|ProtocolList |字符串数组 |`["HTTP-FLV", "RTMP"]` |推拉流协议。可用协议说明如下：<br><br><br>* `HTTP-FLV`：基于 HTTP 的推拉流协议，视频格式为 FLV。<br><br>* `HTTP-HLS`：基于 HTTP 的推拉流协议，视频格式为 TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：基于 UDP 的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种基于 HTTP 的高效自适应视频流协议。 |
|ISPList |字符串数组 |`["unicom","telecom"]` |用于表示互联网服务提供商（ISP）标识的数组。有效选项包括：<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网络（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|RegionList |[ResponseRegion](https://docs.byteplus.com/en/docs/24/107014#responseregion) 数组 |`-` |CDN 节点 IP 所属区域列表。 |
|UserRegionList |[ResponseRegion](https://docs.byteplus.com/en/docs/24/107014#responseregion) 数组 |`-` |客户端 IP 所属区域列表。 |
|DetailField |字符串数组 |`[Domain]` |数据分割维度及其说明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。<br><br>* `Area`：CDN 节点 IP 所属区域。<br><br>* `Country`：客户端 IP 所属国家。<br><br>* `UserArea`：客户端 IP 所属区域。<br><br>* `UserCountry`：客户端 IP 所属国家。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|StartTime |字符串 |`2024-12-12T00:00:00Z` |查询范围的起始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |字符串 |`2024-12-12T01:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|PeakUpBandwidth |浮点型 |`10` |查询时间范围内的上行带宽峰值，单位为 Mbps。 |
|PeakDownBandwidth |浮点型 |`10` |查询时间范围内的下行带宽峰值，单位为 Mbps。 |
|TotalUpTraffic |浮点型 |`20` |查询时间范围内的上行流量总量，单位为 GB。 |
|TotalDownTraffic |浮点型 |`20` |查询时间范围内的下行流量总量，单位为 GB。 |
|TotalRequest |浮点型 |`5` |请求次数。 |
|EdgeStatDataList |[EdgeStatDataList](https://docs.byteplus.com/en/docs/24/107014#edgestatdatalist) 数组 |`-` |所有时间颗粒度的数据。 |
|EdgeStatDetailDataList |[EdgeStatDetailDataList](https://docs.byteplus.com/en/docs/24/107014#edgestatdetaildatalist) 数组 |`-` |按维度分割的数据。 |


<span id="responseregion"></span>
### ResponseRegion


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识。 |
|Country |字符串 |`CN` |区域信息中的国家标识。 |
|Province |字符串 |`beijing` |区域信息中的省份标识。 |


<span id="edgestatdatalist"></span>
### EdgeStatDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |数据按颗粒度聚合时，每个时间颗粒度的起始时间，采用 RFC3339 UTC 时间格式，精确到秒。 |
|UpTraffic |Float |`20` |当前数据聚合颗粒度内产生的上行流量总量，单位为 GB。 |
|DownTraffic |Float |`20` |当前数据聚合颗粒度内产生的下行流量总量，单位为 GB。 |
|UpBandwidth |Float |`10` |当前数据聚合颗粒度内的上行带宽峰值，单位为 Mbps。 |
|DownBandwidth |Float |`10` |当前数据聚合颗粒度内的下行带宽峰值，单位为 Mbps。 |
|Request |Float |`5` |当前数据聚合颗粒度内的请求数量。 |


<span id="edgestatdetaildatalist"></span>
### EdgeStatDetailDataList


|**Parameter** |**Data Type** |**Sample Value** |**接口行为** |
|---|---|---|---|
|Domain |String |`push.example.com` |按域名维度分割数据时的域名信息。 |
|Protocol |String |`HTTP-FLV` |按推拉流协议维度分割数据时的协议信息。 |
|ISP |String |`telecom` |按运营商维度分割数据时的运营商信息。 |
|Area |String |`CN` |按 CDN 节点 IP 所在区域维度分割数据时的区域信息。 |
|Country |String |`CN` |按 CDN 节点 IP 所在国家维度分割数据时的国家信息。 |
|UserArea |String |`CN` |按客户端 IP 所在区域维度分割数据时的区域信息。 |
|UserCountry |String |`CN` |按客户端 IP 所在国家维度分割数据时的国家信息。 |
|PeakUpBandwidth |Float |`10` |当前维度分割后上行带宽峰值，单位为 Mbps。 |
|PeakDownBandwidth |Float |`10` |当前维度分割后下行带宽峰值，单位为 Mbps。 |
|TotalUpTraffic |Float |`20` |当前维度分割后上行流量总量，单位为 GB。 |
|TotalDownTraffic |Float |`20` |当前维度分割后下行流量总量，单位为 GB。 |
|TotalRequest |Float |`5` |当前维度分割后的请求数量。 |
|EdgeStatDataList |Array of [EdgeStatDataList](https://docs.byteplus.com/en/docs/24/107014#edgestatdatalist) |`-` |当前维度分割后所有时间颗粒度的数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveEdgeStatData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "pull.example.com"
    ],
    "ProtocolList": [
        "HTTP-FLV",
        "RTMP"
    ],
    "ISPList": [
        "unicom",
        "telecom"
    ],
    "RegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2024-12-12T00:00:00Z",
    "EndTime": "2024-12-12T00:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Domain"
    ],
    "AppList": [
        "live",
        "vodlive"
    ],
    "StreamList": [
        "stream001",
        "stream002"
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveEdgeStatData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "pull.example.com"
        ],
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "RegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "StartTime": "2024-12-12T00:00:00Z",
        "EndTime": "2024-12-12T01:00:00Z",
        "Aggregation": 300,
        "TotalUpTraffic": 20,
        "TotalDownTraffic": 20,
        "AppList": [
            "live",
            "livevod"
        ],
        "StreamList": [
            "stream001",
            "stream002"
        ],
        "PeakUpBandwidth": 10,
        "PeakDownBandwidth": 10,
        "TotalRequest": 5,
        "EdgeStatDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpTraffic": 20,
                "DownTraffic": 20,
                "UpBandwidth": 10,
                "DownBandwidth": 10,
                "Request": 5
            }
        ],
        "EdgeStatDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "push.example.com",
                "ISP": "telecom",
                "TotalUpTraffic": 20,
                "TotalDownTraffic": 20,
                "PeakUpBandwidth": 10,
                "PeakDownBandwidth": 10,
                "TotalRequest": 5,
                "EdgeStatDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpTraffic": 20,
                        "DownTraffic": 20,
                        "UpBandwidth": 10,
                        "DownBandwidth": 10,
                        "Request": 5
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
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107014#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验未通过。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如仍返回错误码，请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
