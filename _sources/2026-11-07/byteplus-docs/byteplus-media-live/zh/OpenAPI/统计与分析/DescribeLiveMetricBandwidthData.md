---
title: "DescribeLiveMetricBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata-zh-CN"
---

调用 `DescribeLiveMetricBandwidthData` API，以查询指定时间范围内直播域名或直播流的带宽监控数据。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自2025年2月18日起，我们将不再维护此旧版API。其文档将于2025年5月18日下线。建议迁移至新版 UpdateUser 接口。详情请参见 <a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamcountdata">DescribeLiveEdgeStatData</a> 文档。</div>


<span id="Requirements"></span>
## 要求


* 限制：

   * 支持查询由特定域名（包括已删除域名）或特定直播流生成的带宽监控数据。

   * 带宽监控数据用于数据监控，其采集方式与带宽使用数据不同。请使用 [DescribeLiveBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/eescribelivebandwidthdata) 查询直播带宽使用数据。

* 频率限制：每个账号每秒最多可查询100次

* 数据延迟：

   * 当聚合颗粒度为60秒时，数据延迟为5分钟；

   * 其他时间颗粒度的数据延迟为15分钟。

* 数据指标：带宽数据以1000为基数进行计算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveMetricBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除需传递API专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveMetricBandwidthData` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com"]` |域名列表。默认情况下为空，表示将查询BytePlus MediaLive下所有域名的带宽使用数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API，或前往BytePlus MediaLive控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取需查询的域名。 |
|应用 |String |否 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在以流颗粒度查询带宽监控数据时，需同时指定 <code>应用</code> 和 <code>流</code> 参数以确定直播流。</div><br> |
|流 |String |否 |`example_stream` |直播流URL中的StreamName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1到100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在以流颗粒度查询带宽监控数据时，需同时指定 <code>应用</code> 和 <code>流</code> 参数以确定直播流。</div><br> |
|ProtocolList |Array of String |否 |`["HTTP-FLV", "RTMP"]` |推拉流协议。默认表示所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于HTTP的推拉流协议，视频格式为FLV。<br><br>* `HTTP-HLS`：基于HTTP的推拉流协议，视频格式为TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议（Quick UDP Internet Connections）。<br><br>* `CMAF`：一种用于高效自适应视频流HTTP传输的协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">若查询<code>QUIC</code>协议时，不能同时查询其他协议。</div><br> |
|ISPList |字符串数组 |否 |`["telecom"]` |提供网络接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。<br><br><br>如需获取各运营商的标识，可调用[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/106992#region)数组 |否 |`-` |CDN节点IP所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code>与<code>UserRegionList</code>不可在同一请求中同时使用。</div><br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/106992#region)数组 |否 |`-` |客户端IP所属区域列表，默认表示所有区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code>与<code>UserRegionList</code>不可在同一请求中同时使用。</div><br> |
|StartTime |字符串 |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |否 |`300` |数据聚合的颗粒度（单位：秒），支持以下选项：<br><br><br>* `60`：1分钟。按1分钟颗粒度聚合时，单次查询最大时间跨度为24小时，历史查询时间范围为366天；<br><br>* `300`：（默认）5分钟。按5分钟颗粒度聚合时，单次查询最大时间跨度为31天，历史查询时间范围为366天；<br><br>* `3600`：1小时。按1小时颗粒度聚合时，单次查询最大时间跨度为93天，历史查询时间范围为366天。 |
|DetailField |字符串数组 |否 |`["Domain"]` |数据分割的维度默认不进行拆分。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">基于指定维度（如Domain、ISP、Protocol）进行数据分割，仅在使用<code>DetailField</code>参数指定分割维度且至少有一个参数（<code>DomainList</code>、<code>ProtocolList</code>或<code>ISPList</code>）传入多个值时才会生效。</div><br> |


<span id="region"></span>
### Region


|**Parameter** |**数据类型** |**必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |区域信息中的主要区域标识可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。 |
|Country |字符串 |否 |`CN` |区域信息中的国家标识可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。按国家筛选时需同时传入Area和Country。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取标识信息。按省份筛选时，需要同时传入`Area`、`Country`和`Province` |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com"]` |域名列表。 |
|应用 |字符串 |`live` |查询流量数据时按流颗粒度指定的AppName字段。 |
|流 |字符串 |`example_stream` |查询流量数据时按流颗粒度指定的StreamName字段。 |
|ProtocolList |字符串数组 |`["HTTP-FLV", "RTMP"]` |推拉流协议，协议说明如下：<br><br><br>* `HTTP-FLV`：基于HTTP的推拉流协议，视频格式为FLV。<br><br>* `HTTP-HLS`：基于HTTP的推拉流协议，视频格式为TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议。<br><br>* `CMAF`：基于HTTP的高效自适应视频流协议。 |
|ISPList |字符串数组 |`["telecom"]` |表示互联网服务提供商（ISP）标识的数组。有效选项包括：<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/106992#region)数组 |`-` |CDN节点IP所属区域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/106992#region)数组 |`-` |客户端IP所属区域列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围起始时间，RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围结束时间，RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|DetailField |字符串数组 |`["Domain"]` |数据拆分维度及说明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。 |
|PeakUpBandwidth |浮点数 |`20` |获取指定时间范围内的上行带宽峰值，单位为Mbps。 |
|PeakDownBandwidth |浮点数 |`20` |获取指定时间范围内的最大下行带宽峰值，单位为Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/106992#bandwidthdata)数组 |`-` |包含所有时间颗粒度带宽数据的数据列表。 |
|BandwidthDetailDataList |[BandwidthDetailData](https://docs.byteplus.com/en/docs/24/106992#bandwidthdetaildata)数组 |`-` |按维度拆分带宽数据的数据列表。 |


<span id="region"></span>
### Region


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识。 |
|Country |字符串 |`CN` |区域信息中的国家标识。 |
|Province |字符串 |`beijing` |区域信息中的省份标识。 |


<span id="bandwidthdata"></span>
### BandwidthData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，格式为RFC3339 UTC时间，精确到秒。 |
|UpBandwidth |浮点数 |`20` |当前数据聚合时间颗粒度内的上行带宽峰值，单位为Mbps。 |
|DownBandwidth |浮点数 |`20` |当前数据聚合时间颗粒度内的下行带宽峰值，单位为Mbps。 |


<span id="bandwidthdetaildata"></span>
### BandwidthDetailData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`push.example.com` |按域名维度拆分数据时的域名信息。 |
|Protocol |字符串 |`HTTP-FLV` |按推拉流协议维度拆分数据时的协议信息。 |
|ISP |字符串 |`telecom` |按ISP维度拆分数据时的ISP信息。 |
|PeakUpBandwidth |浮点数 |`20` |数据按维度拆分后，当前维度的上行带宽峰值，单位为 Mbps。 |
|PeakDownBandwidth |Float |`20` |数据按维度拆分后，当前维度的下行带宽峰值，单位为 Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/106992#bandwidthdata) 数组 |`-` |数据分段后，当前维度下所有时间粒度的数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveMetricBandwidthData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com"
    ],
    "App": "live",
    "Stream": "example_stream",
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
    "UserRegionList": [
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
        "Domain"
    ]
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveMetricBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com"
        ],
        "App": "live",
        "Stream": "example_stream",
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
        "UserRegionList": [
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
            "Domain"
        ],
        "PeakUpBandwidth": 20,
        "PeakDownBandwidth": 20,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 20,
                "DownBandwidth": 20
            }
        ],
        "BandwidthDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "push.example.com",
                "ISP": "telecom",
                "PeakUpBandwidth": 20,
                "PeakDownBandwidth": 20,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00+08:00",
                        "UpBandwidth": null,
                        "DownBandwidth": null
                    }
                ]
            }
        ]
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106992#request-parameters)描述。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
