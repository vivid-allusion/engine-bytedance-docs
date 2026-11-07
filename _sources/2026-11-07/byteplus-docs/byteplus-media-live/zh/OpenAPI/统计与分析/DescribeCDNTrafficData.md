---
title: "DescribeCDNTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/docs-describecdntrafficdata-zh-CN"
---

调用 `DescribeCDNTrafficData` API，在指定时间范围内查询访问直播录制和截图时所使用的 CDN 流量。

<span id="Requirements"></span>
## 要求


* 频率限制：每个账号每秒最多查询 1 次。

* 数据延迟：4 分钟。


<span id="HTTP request"></span>
## HTTP 请求


* 方法：POST

* 接口地址：https://open.byteplusapi.com/?Action=DescribeCDNTrafficData&Version=2020\-08\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有 API 调用时，除需传递 API 专属参数外，还需包含 [通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeCDNTrafficData` |API 操作名称。 |
|Version |String |是 |`2020-08-01` |该 API 操作的版本。当前版本：2020\-08\-01。 |


<span id="Body parameters"></span>
### 请求体参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|StartTime |String |是 |`2022-04-08T00:00:00Z` |查询范围的起始时间，RFC 3339 格式，精确到秒。 |
|EndTime |String |是 |`2022-04-08T00:00:00Z` |查询范围的结束时间，RFC 3339 格式，精确到秒。 |
|DomainList |String 数组 |否 |`["push.example.com"]` |待查询的域名列表。如未指定，将查询账号下所有域名。可调用 [ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail-2023) API 或访问 BytePlus MediaLive 控制台的 [Domains](https://console.byteplus.com/live/main/domain/list) 页面获取域名。 |
|Interval |Integer |是 |`300` |数据颗粒度。单位：秒。仅可设置为 300。 |
|RegionList |[RegionList](https://docs.byteplus.com/en/docs/24/107000#regionlist) 数组 |是 |`-` |区域列表。 |


<span id="regionlist"></span>
### RegionList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |String |是 |`Global` |支持的值：<br><br><br>* `AsiaPacific-1`<br><br>* `AsiaPacific-2`<br><br>* `AsiaPacific-3`<br><br>* `NorthAmerica`<br><br>* `SouthAmerica`<br><br>* `Europe`<br><br>* `MiddleEast`<br><br>* `Global`：非中国大陆 |
|Country |String |否 |`-` |预留字段，暂不支持。 |
|Province |String |否 |`-` |预留字段，暂不支持。 |


<span id="Response parameters"></span>
## 返回调用结果参数

关于唯一的 API 专属返回调用结果参数，请参见下表。更多详情请参见 [请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response) 部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |String 数组 |`["push.example.com"]` |待查询的域名列表。 |
|Interval |Integer |`300` |数据颗粒度。 |
|StartTime |String |`2022-04-08T00:00:00Z` |查询范围的起始时间，RFC 3339 格式，精确到秒。 |
|EndTime |String |`2022-04-08T00:00:00Z` |查询范围的结束时间，RFC 3339 格式，精确到秒。 |
|TrafficTotalData |[CDNTrafficData](https://docs.byteplus.com/en/docs/24/107000#cdntrafficdata) 数组 |`-` |按时间颗粒度聚合的数据。 |
|TrafficDetailDataList |[TrafficDetailDataList](https://docs.byteplus.com/en/docs/24/107000#trafficdetaildatalist) 数组 |`-` |按时间颗粒度和域名聚合的数据。 |


<span id="cdntrafficdata"></span>
### CDNTrafficData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |String |`2022-04-08T00:00:00Z` |每个颗粒度区间的起始时间（UTC 时间，RFC 3339 格式）。 |
|Traffic |Float |`22` |CDN 流量数据，单位为 GB。 |


<span id="trafficdetaildatalist"></span>
### TrafficDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |String |`push.example.com` |域名。 |
|TrafficDataList |[CDNTrafficData](https://docs.byteplus.com/en/docs/24/107000#cdntrafficdata) 数组 |`-` |按时间颗粒度聚合的数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeCDNTrafficData&Version=2020-08-01
{
    "StartTime": "2022-04-08T00:00:00Z",
    "EndTime": "2022-04-08T00:00:00Z",
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "Interval": 300
}
```


<span id="Sample response"></span>
### 返回调用结果示例

```json
{
  "ResponseMetadata":{
    "RequestId":"202207130928130102511970410745B8DC",
    "Action":"DescribeCDNTrafficData",
    "Version":"2020-08-01",
    "Service":"live",
    "Region":"ap-singapore-1"
  },
  "Result":{
    "StartTime": "2022-04-08T00:00:00Z",
    "EndTime": "2022-04-08T00:00:00Z",
    "DomainList": [
        "push.example.com",
        "push.example2.com"
    ],
    "Interval": 300,
    "TrafficTotalData": [
        {
            "Timestamp": "2022-04-08T00:00:00Z",
            "Traffic": 276.00
        },
        {
            "Timestamp": "2022-04-08T01:00:00Z",
            "Traffic": 276.00
        }
    ],
    "TrafficDetailDataList": [
        {
            "Domain": "push.example.com",
            "TrafficDataList": [
                {
                    "TimeStamp": "2022-04-08T00:00:00Z",
                    "Traffic": 138.00
                },
                {
                    "TimeStamp": "2022-04-08T01:00:00Z",
                    "Traffic": 138.00
                }
            ]
        },
        {
            "Domain": "push.example2.com",
            "TrafficDataList": [
                {
                    "TimeStamp": "2022-04-08T00:00:00Z",
                    "Traffic": 138.00
                },
               {
                    "TimeStamp": "2022-04-08T01:00:00Z",
                    "Traffic": 138.00
                }
            ]
        }
    ]
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见 [BytePlus OpenAPI 通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|200 |CommonErr |*  |未分类错误。建议重试。如仍返回该错误码，请 [联系支持](https://console.byteplus.com/workorder/create)。 |
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考 [请求参数](https://docs.byteplus.com/en/docs/24/107000#request-parameters)说明进行检查。 |
|400 |InvalidParam.BindError |请求参数错误，请检查输入数据 |参数校验失败。请检查数据类型是否正确。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.AccountIDNotAllow |该 AccountID 无权访问对应资源，请检查请求参数 |请求被拒绝，因为当前账号下不存在所请求的资源（资源包括域名空间、域名、应用、配置和证书）。 |
|403 |RequestForbidden.BillingStatus |该 AccountID 的计费情况不可用，请开通服务或充值。 |视频直播服务未开启或账号欠费，导致账单不可用。请检查服务开通状态和账号欠费状态。 |
|404 |ResourceNotFound |*  |未找到资源（包括域名空间、域名、应用、配置和证书）。建议重试。如果仍返回该错误码，请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|500 |InternalError.DB |发生与数据库相关的内部错误，请联系管理员。 |发生与数据库相关的内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|502 |InternalServiceError.BadResponse |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
|504 |InternalServiceTimeout |内部服务超时。请联系管理员。 |内部服务超时。请[联系支持](https://console.byteplus.com/workorder/create)。 |
