---
title: "DescribeLiveBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/DescribeLiveBandwidthData-zh-CN"
---

调用 `DescribeLiveBandwidthData` API，在指定时间范围内查询指定直播域名的带宽使用情况，包括推流域名的上行带宽峰值和拉流域名的下行带宽峰值。

## 要求

* 计费情况：关于带宽计费，请参见 [直播服务费用](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-live-streaming-service-fees)。

* 限制：

   * 支持查询已删除域名产生的带宽使用数据。

   * 带宽使用数据用于计费和对账，与带宽数据监控的采集方式不同。请使用 [DescribeLiveMetricBandwidthData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeLivemetricbandwidthdata) 查询直播带宽监控数据。

* 频率限制：每个账号每秒最多查询30次

* 数据延迟：15分钟

* 数据指标：带宽数据以1000为基数计算，例如，1 Mbps = 1000 Kbps。

* 统计规则：带宽使用数据每5分钟统计一次。根据查询时间和颗粒度设置，返回时间范围内的最大值以及颗粒度内的最大值。

## HTTP请求

* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveBandwidthData&Version=2023\-01\-01

## 请求参数

### 通用参数

所有API调用时，除API专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### 查询

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBandwidthData` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |

### 请求体参数

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |String数组 |否 |`["push.example.com"]` |域名列表。默认情况下为空，表示会查询你在BytePlus MediaLive下所有域名的带宽使用数据。你可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API或在BytePlus MediaLive控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取需要查询的域名。 |
|ProtocolList |String数组 |否 |`["HTTP-FLV", "RTMP"]` |推拉流协议。默认包含所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于HTTP的推拉流协议，传输视频格式为FLV。<br><br>* `HTTP-HLS`：基于HTTP的推拉流协议，传输视频格式为TS。<br><br>* `RTMP`：实时消息传输协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种基于HTTP的高效自适应视频流协议。<br><br><br>> **说明**<br><br><br>> 若查询 `QUIC` 协议时，不能同时查询其他协议。<br> |
|ISPList |String数组 |否 |`["telecom", "unicom"]` |提供网络接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；Peng Telecom & Media Group;<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。<br><br><br>如需获取各运营商标识，可调用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/124025#region)数组 |否 |`-` |CDN节点IP所属区域列表，默认表示全部区域。<br><br>> **说明**<br><br><br>> `RegionList` 与 `UserRegionList` 不能在同一个请求中同时使用。<br> |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/124025#region) 数组 |否 |`-` |客户端IP所属区域列表，默认表示全部区域。<br><br>> **说明**<br><br><br>> `RegionList` 与 `UserRegionList` 不能在同一个请求中同时使用。<br> |
|StartTime |字符串 |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |否 |`300` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `300`（默认）：5分钟。以5分钟为颗粒度聚合时，单次查询的最大时间跨度为31天，历史查询的最大时间范围为366天。<br><br>* `3600`：1小时。以1小时为颗粒度聚合时，单次查询的最大时间跨度为93天，历史查询的最大时间范围为366天。<br><br>* `86400`：1天。以1天为颗粒度聚合时，单次查询的最大时间跨度为93天，历史查询的最大时间范围为366天。 |
|DetailField |字符串数组 |否 |`["Domain"]` |数据分割的维度默认不进行分割。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。<br><br><br>> **说明**<br><br><br>> 仅当使用 `DetailField` 参数指定数据分割维度，且 `DomainList`、`ProtocolList` 或 `ISPList` 参数中至少有一个传入多个值时，返回调用结果才会按维度进行数据分割。<br> |

### Region

|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |区域信息中的主要区域标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。 |
|Country |字符串 |否 |`CN` |区域信息中的国家标识符可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。按国家过滤时，需要同时传入 'Area' 和 'Country'。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识符，目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取标识符信息。按省份过滤时，需要同时传入 `Area`、`Country` 和 `Province` |

## 返回调用结果参数

有关唯一的API专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com"]` |域名列表。 |
|ProtocolList |字符串数组 |`["HTTP-FLV", "RTMP"]` |推拉流协议，协议说明如下：<br><br><br>* `HTTP-FLV`：基于HTTP的推拉流协议，视频格式为FLV。<br><br>* `HTTP-HLS`：基于HTTP的推拉流协议，视频格式为TS。<br><br>* `RTMP`：实时消息协议。<br><br>* `RTM`：实时媒体，超低延时直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种高效自适应HTTP视频流协议。 |
|ISPList |字符串数组 |`["telecom"]` |互联网服务提供商（ISP）标识符数组。有效选项包括：<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网络（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士；鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/124025#region)数组 |`-` |CDN节点IP所属区域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/124025#region)数组 |`-` |客户端IP所属区域列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的开始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|DetailField |字符串数组 |`["Domain"]` |数据分割维度及其说明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。 |
|PeakUpBandwidth |浮点数 |`20` |获取指定时间范围内的上行带宽峰值，单位为Mbps。 |
|PeakDownBandwidth |浮点数 |`20` |获取指定时间范围内的下行带宽峰值，单位为Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/124025#bandwidthdata)数组 |`-` |每个时间颗粒度的全部数据。 |
|BandwidthDetailDataList |[BandwidthDetailData](https://docs.byteplus.com/en/docs/24/124025#bandwidthdetaildata)数组 |`-` |按维度分割的数据。<br><br>> **说明**<br><br><br>> 仅当使用`DetailField`参数指定按维度分割的数据，并且`DomainList`、`ProtocolList`或`ISPList`参数至少有一个提供了多个值时，返回调用结果中才会出现按维度分割的数据。<br> |

### Region

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识符。 |
|Country |字符串 |`CN` |区域信息中的国家标识符。 |
|Province |字符串 |`beijing` |区域信息中的省份标识符。 |

### BandwidthData

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|UpBandwidth |浮点数 |`20` |当前数据聚合时间颗粒度内的上行带宽峰值，单位为Mbps。 |
|DownBandwidth |浮点数 |`20` |当前数据聚合时间颗粒度内的下行带宽峰值，单位为Mbps。 |

### BandwidthDetailData

|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`push.example.com` |按域名维度分割数据时的域名信息。 |
|Protocol |字符串 |`RTMP` |按推拉流协议维度分割数据时的协议信息。 |
|ISP |字符串 |`telecom` |按运营商维度分割数据时的运营商信息。 |
|PeakUpBandwidth |浮点数 |`20` |按维度分割数据后，当前维度的上行带宽峰值，单位为Mbps。 |
|PeakDownBandwidth |浮点数 |`20` |按维度分割数据后，当前维度的下行带宽峰值，单位为Mbps。 |
|BandwidthDataList |[BandwidthData](https://docs.byteplus.com/en/docs/24/124025#bandwidthdata)数组 |`-` |按维度分割数据后，当前维度下所有时间颗粒度的数据。 |

## 示例

### 示例请求

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBandwidthData&Version=2023-01-01
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

### 示例返回调用结果

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveBandwidthData",
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
        "PeakUpBandwidth": 20,
        "PeakDownBandwidth": 20,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "UpBandwidth": 20,
                "DownBandwidth": 20
            },
            {
                "TimeStamp": "2022-04-13T00:05:00Z",
                "UpBandwidth": 20,
                "DownBandwidth": 20
            }
        ],
        "BandwidthDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "PeakUpBandwidth": 20,
                "PeakDownBandwidth": 20,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 20,
                        "DownBandwidth": 20
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpBandwidth": 20,
                        "DownBandwidth": 20
                    }
                ]
            },
            {
                "Protocol": "RTMP",
                "PeakUpBandwidth": 0,
                "PeakDownBandwidth": 0,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "UpBandwidth": 0,
                        "DownBandwidth": 0
                    },
                    {
                        "TimeStamp": "2022-04-13T00:05:00Z",
                        "UpBandwidth": 0,
                        "DownBandwidth": 0
                    }
                ]
            }
        ]
    }
}
```

## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/124025#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
