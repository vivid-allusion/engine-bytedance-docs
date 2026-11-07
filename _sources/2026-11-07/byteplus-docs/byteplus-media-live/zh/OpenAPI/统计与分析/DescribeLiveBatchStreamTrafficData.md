---
title: "DescribeLiveBatchStreamTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describelivebatchstreamtrafficdata-2023-zh-CN"
---

调用 `DescribeLiveBatchStreamTrafficData` API，查询指定时间范围内的上行和下行流量数据及其明细数据。

## 要求

* 限制：

   * 支持查询指定域名或协议下的流量数据。

   * 支持查询已删除域名下产生的流量数据。

* 频率限制：每个账号每秒 30 次查询。

* 数据延迟：数据延迟为 15 分钟。

* 数据指标：流量数据按 1000 进制计算，例如 1 GB = 1000 MB。

## HTTP 请求

* 方法：POST

* 接入点：https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTrafficData&Version=2023\-01\-01

## 请求参数

### 公共参数

调用所有 API 时，除 API 特定参数外，还必须携带[公共参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

### Query

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveBatchStreamTrafficData` |API 操作。 |
|Version |String |是 |`2023-01-01` |该 API 操作的版本。当前版本：2023\-01\-01。 |

### Body 参数

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|DomainList |String 数组 |否 |`["push.example.com", "push2.example.com"]` |拉流域名列表。默认值为空，表示查询所有域名。您可以调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API，或前往 BytePlus MediaLive 控制台的 [域名](https://console.byteplus.com/live/main/domain/list) 页面，获取要查询的拉流域名。 |
|ProtocolList |String 数组 |否 |`["HTTP-FLV", "RTMP"]` |推拉流协议，协议说明如下：<br><br><br>* `HTTP-FLV`：基于 HTTP 的推拉流协议，以 FLV 格式传输视频。<br><br>* `HTTP-HLS`：基于 HTTP 的推拉流协议，以 TS 格式传输视频。<br><br>* `RTMP`：实时消息传输协议。<br><br>* `RTM`：Real Time Media，超低延迟直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：Quick UDP Internet Connections，基于 UDP 的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种通过 HTTP 实现高效自适应视频流传输的协议。<br><br><br>> **说明**<br><br><br><br>* > 如果查询 QUIC 协议，不能同时查询其他协议。<br><br><br>* > 默认情况下，查询的总流量数据为实际产生的上行和下行流量。<br><br><br>* > 如果传入单个协议进行查询，并对各协议流量求和，结果会大于实际总流量。<br> |
|ISPList |String 数组 |否 |`["telecom"]` |提供网络接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研计算机网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：中国广电网络；<br><br>* `huashu`：华数传媒。<br><br>   如需获取各运营商标识，您可以调用 [DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[RegionList](https://docs.byteplus.com/en/docs/24/107033#regionlist) 数组 |否 |`-` |CDN 节点 IP 所属区域列表，默认表示所有区域。<br><br>> **说明**<br><br><br>> 不支持同时使用 RegionList 和 UserRegionList 参数。<br> |
|UserRegionList |[RegionList](https://docs.byteplus.com/en/docs/24/107033#regionlist) 数组 |否 |`-` |客户端 IP 所属区域列表，默认表示所有区域。<br><br>> **说明**<br><br><br>> 不支持同时使用 RegionList 和 UserRegionList 参数。<br> |
|StartTime |String |是 |`2021-04-13T00:00:00Z` |查询范围的开始时间（UTC 时间，RFC 3339 格式，精确到秒）。<br><br>> **说明**<br><br><br>> 单次查询的最大时间跨度为 24 小时，历史查询时间范围为 366 天。<br> |
|EndTime |String |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间（UTC 时间，RFC 3339 格式，精确到秒）。 |
|PageNum |Integer |否 |`1` |页码。取值必须大于或等于 `1`。默认值：`1`。 |
|PageSize |Integer |否 |`1000` |每页查询结果数量。取值范围：[100,1000]。默认值：`1000`。<br><br>> **说明**<br><br><br>> 如果将此参数设置为 `0`，则使用默认值。<br> |

### RegionList

|参数 |数据类型 |是否必填 |示例值 |描述 |
|---|---|---|---|---|
|Area |String |否 |`CN` |区域信息中的大区标识，可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。 |
|Country |String |否 |`CN` |区域信息中的国家标识，可通过调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取。按国家筛选时，需要同时传入 'Area' 和 'Country'。 |
|Province |String |否 |`beijing` |区域信息中的省份标识，目前不支持中国大陆、香港、澳门和台湾以外的国家或地区。您可以调用 [DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata) 获取标识信息。按省份筛选时，需要同时传入 `Area`、 `Country` 和 `Province` |

## 响应参数

API 特有的响应参数见下表。更多详情请参见[请求响应](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)章节。

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|DomainList |String 数组 |`["push.example.com", "push2.example.com"]` |域名列表。 |
|ProtocolList |String 数组 |`["RTMP"]` |推拉流协议，协议说明如下：<br><br><br>* `HTTP-FLV`：基于 HTTP 的推拉流协议，以 FLV 格式传输视频。<br><br>* `HTTP-HLS`：基于 HTTP 的推拉流协议，以 TS 格式传输视频。<br><br>* `RTMP`：实时消息传输协议。<br><br>* `RTM`：Real Time Media，超低延迟直播协议。<br><br>* `SRT`：安全可靠传输协议。<br><br>* `QUIC`：Quick UDP Internet Connections，基于 UDP 的新型低延迟互联网传输协议。<br><br>* `CMAF`：一种通过 HTTP 实现高效自适应视频流传输的协议。 |
|ISPList |String 数组 |`["telecom"]` |提供网络接入服务的运营商标识。 |
|RegionList |[RegionList](https://docs.byteplus.com/en/docs/24/107033#regionlist-response) 数组 |`-` |CDN 节点 IP 所属区域列表。 |
|UserRegionList |[RegionList](https://docs.byteplus.com/en/docs/24/107033#regionlist-response) 数组 |`-` |客户端 IP 所属区域列表。 |
|StartTime |String |`2022-11-10T00:00:00Z` |查询的开始时间，采用 UTC 时间，按 RFC3339 格式展示，精确到秒。 |
|EndTime |String |`2022-11-11T00:00:00Z` |查询的结束时间，采用 UTC 时间，按 RFC3339 格式展示，精确到秒。 |
|TotalUpTraffic |Float |`40` |查询时间范围内的上行总流量，单位为 GB。 |
|TotalDownTraffic |Float |`40` |查询时间范围内的下行总流量，单位为 GB。 |
|StreamInfoList |[StreamInfoList](https://docs.byteplus.com/en/docs/24/107033#streaminfolist) 数组 |`-` |按流维度划分的数据。 |
|Pagination |[Pagination](https://docs.byteplus.com/en/docs/24/107033#pagination) 对象 |`-` |分页信息。 |

### RegionList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Area |String |`CN` |区域信息中的区域标识。 |
|Country |String |`CN` |区域信息中的国家标识。 |
|Province |String |`beijing` |区域信息中的省份标识。 |

### StreamInfoList

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|Domain |String |`push.example.com` |域名。 |
|App |String |`example_app` |流地址的 AppName 字段。 |
|Stream |String |`example_stream` |流地址的 StreamName 字段。 |
|UpTraffic |Float |`20` |当前流的上行流量，单位为 GB。 |
|DownTraffic |Float |`20` |当前流的下行流量，单位为 GB。 |

### Pagination

|参数 |数据类型 |示例值 |描述 |
|---|---|---|---|
|PageNum |Integer |`1` |当前页码。 |
|PageSize |Integer |`1000` |每页结果数量。 |
|TotalCount |Integer |`2` |结果总数。 |

## 示例

### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveBatchStreamTrafficData&Version=2023-01-01
{
    "StartTime": "2022-11-10T00:00:00Z",
    "EndTime": "2022-11-11T00:00:00Z"
}
```

### 响应示例

```json
{
    "ResponseMetadata": {
        "RequestId": "201806041104200100100232280022D30",
        "Action": "DescribeLiveBatchStreamTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singpore-1"
    },
    "Result": {
        "StartTime": "2022-11-10T00:00:00Z",
        "EndTime": "2022-11-11T00:00:00Z",
        "TotalUpTraffic": 40,
        "TotalDownTraffic": 40,
        "StreamInfoList": [
            {
                "Domain": "push.example.com",
                "Stream": "example_stream",
                "App": "live",
                "UpTraffic": 20,
                "DownTraffic": 20
            },
            {
                "Domain": "push2.example.com",
                "Stream": "example_stream",
                "App": "live",
                "UpTraffic": 20,
                "DownTraffic": 20
            }
        ],
        "Pagination": {
            "PageNum": 1,
            "PageSize": 1000,
            "TotalCount": 2
        }
    }
}
```

## 错误码

以下是与当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 公共错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。

|状态码 |错误码 |错误信息 |描述 |
|---|---|---|---|
|200 |CommonErr |\- |未分类错误。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|400 |InvalidParam |\- |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107033#request-parameters) 说明进行检查。 |
|400 |InvalidParam.BindError |Request parameter error, please check input data |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |\- |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|404 |ResourceNotFound |\- |未找到资源（包括域名空间、域名、应用名称、配置和证书）。建议重试。如果仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|500 |InternalError |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|502 |InternalServiceError.BadResponse |an internal error occurred, please contact the administrator. |发生内部错误。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
|504 |InternalServiceTimeout |Internal Service is timeout. please contact the administrator. |内部服务超时。请 [联系支持](https://console.byteplus.com/workorder/create?step=2&SubProductID=P00000980)。 |
