---
title: "DescribeLivePlayStatusCodeData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveplaystatuscodedata-zh-CN"
---

调用`DescribeLivePlayStatusCodeData` API，查询指定时间范围内域名的请求状态码占比，包括推流请求、拉流请求和源站请求。

<span id="Requirements"></span>
## 要求


* 限制：支持查询特定域名（包括已删除域名）产生的推拉流请求或回源请求的状态码分布。

* 频率限制：每个账号每秒最多30次查询

* 数据延迟：15分钟


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLivePlayStatusCodeData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用除需传入API专有参数外，还需传入[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLivePlayStatusCodeData` |API操作名称。 |
|Version |String |是 |`2023-01-01` |本API操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["push.example.com", "pull.example.com"]` |域名列表。默认情况下为空，表示查询所有域名的请求状态码占比数据。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API或前往BytePlus MediaLive控制台的[域名](https://console.byteplus.com/live/main/domain/list)页面获取用于查询请求状态码占比数据的域名。 |
|ISPList |Array of String |否 |`["telecom"]` |提供网络接入服务的运营商标识。默认表示全部运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：中国广电；<br><br>* `huashu`：华数传媒。<br><br><br>如需获取各运营商标识，可调用[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107041#region) |否 |`-` |CDN节点IP所属区域列表，默认表示全部区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code>和<code>UserRegionList</code>不可在同一次请求中同时使用。</div><br> |
|UserRegionList |Array of [Region](https://docs.byteplus.com/en/docs/24/107041#region) |否 |`-` |客户端IP所属区域列表，默认表示全部区域。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>RegionList</code>和<code>UserRegionList</code>不可在同一次请求中同时使用。</div><br> |
|StartTime |String |是 |`2024-04-28T14:00:00Z` |查询范围的起始时间，RFC 3339格式，精确到秒。 |
|EndTime |String |是 |`2024-04-28T14:00:00Z` |查询范围的结束时间，RFC 3339格式，精确到秒。 |
|Aggregation |Integer |否 |`300` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `60`：1分钟。按1分钟聚合时，单次查询最大跨度为24小时，历史查询时间范围为366天；<br><br>* `300`：（默认）5分钟。按5分钟聚合时，单次查询最大跨度为31天，历史查询时间范围为366天；<br><br>* `3600`：1小时。按每1小时聚合时，单次查询的最大时间跨度为93天，历史查询的时间范围为366天。 |
|DetailField |字符串数组 |否 |`["Domain"]` |数据拆分的维度默认不进行分割。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>DetailField</code>参数指定了拆分维度，并且以下参数至少有一个传入多个值时，数据按维度拆分才会出现在返回调用结果中：<code>DomainList</code>或<code>ISPList</code>。</div><br> |
|Type |字符串 |否 |`Access` |请求类型，取值及含义如下：<br><br><br>* `Access`：（默认）推流和拉流请求。<br><br>* `Source`：回源请求。 |


<span id="region"></span>
### Region


|**Parameter** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取区域信息中的主要区域标识。 |
|Country |字符串 |否 |`CN` |可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取区域信息中的国家标识。按国家过滤时，需要同时传入`Area`和`Country`。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取标识信息。按省份过滤时，需要同时传入`Area`、`Country`和`Province`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关API专有返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**Parameter** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com", "pull.example.com"]` |域名列表。 |
|ISPList |字符串数组 |`["telecom"]` |提供网络接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国广电；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|RegionList |[Region](https://docs.byteplus.com/en/docs/24/107041#region)数组 |`-` |CDN节点IP所属区域列表。 |
|UserRegionList |[Region](https://docs.byteplus.com/en/docs/24/107041#region)数组 |`-` |客户端IP所属区域列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|Type |字符串 |`Access` |请求类型，取值及含义如下：<br><br><br>* `Access`：推流和拉流请求。<br><br>* `Source`：回源请求。 |
|DetailField |字符串数组 |`["Domain"]` |数据拆分维度及其说明如下：<br><br><br>* `Domain`：域名。<br><br>* `ISP`：互联网服务提供商。 |
|StatusSummaryDataList |[StatusSummaryData](https://docs.byteplus.com/en/docs/24/107041#statussummarydata)数组 |`-` |当前查询条件下状态码占比。 |
|StatusDataList |[StatusData](https://docs.byteplus.com/en/docs/24/107041#statusdata)数组 |`-` |所有时间颗粒度的数据。 |
|StatusDetailDataList |[StatusDetailData](https://docs.byteplus.com/en/docs/24/107041#statusdetaildata)数组 |`-` |按维度拆分的数据。 |


<span id="region"></span>
### Region


|**Parameter** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识。 |
|Country |字符串 |`CN` |区域信息中的国家标识。 |
|Province |字符串 |`beijing` |区域信息中的省份标识。 |


<span id="statussummarydata"></span>
### StatusSummaryData


|**Parameter** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|StatusCode |整数 |`400` |请求状态码。 |
|Value |整数 |`67` |当前状态码出现的次数。 |
|百分比 |浮点数 |`67` |当前状态码在所有状态码总数中的出现比例。 |


<span id="statusdata"></span>
### StatusData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|时间戳 |字符串 |`2021-08-16T00:00:00Z` |按颗粒度聚合数据时，每个颗粒度的起始时间，格式为 RFC3339 UTC 时间，精确到秒。 |
|StatusSummaryDataList |[StatusSummaryData](https://docs.byteplus.com/en/docs/24/107041#statussummarydata) 数组 |`-` |当前数据聚合颗粒度内的状态码详细数据。 |


<span id="statusdetaildata"></span>
### StatusDetailData


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|域名 |字符串 |`pull.example.com` |拉流域名。 |
|ISP |字符串 |`unicom` |互联网服务提供商。 |
|StatusDataList |[StatusData](https://docs.byteplus.com/en/docs/24/107041#statusdata) 数组 |`-` |每个时间戳的颗粒度数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLivePlayStatusCodeData&Version=2023-01-01
{
    "DomainList": [
        "push.example.com",
        "pull.example.com"
    ],
    "UserRegionList": [
        {
            "Area": "CN",
            "Country": "CN",
            "Province": "beijing"
        }
    ],
    "StartTime": "2024-04-28T14:00:00Z",
    "EndTime": "2024-04-28T14:00:00Z",
    "Aggregation": 300,
    "DetailField": [
        "Domain"
    ],
    "Type": "Access"
}
```


<span id="Sample response"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLivePlayStatusCodeData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "push.example.com",
            "pull.example.com"
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
            "Domain"
        ],
        "StatusSummaryDataList": [
            {
                "StatusCode": 400,
                "Value": 67,
                "Percent": 67
            }
        ],
        "StatusDataList": [
            {
                "TimeStamp": "2021-08-16T00:00:00Z",
                "StatusSummaryDataList": [
                    {
                        "StatusCode": 400,
                        "Value": 67,
                        "Percent": 67
                    }
                ]
            }
        ],
        "StatusDetailDataList": [
            {
                "Domain": "pull.example.com",
                "ISP": "unicom",
                "StatusDataList": [
                    {
                        "TimeStamp": "2021-08-16T00:00:00Z",
                        "StatusSummaryDataList": [
                            {
                                "StatusCode": 400,
                                "Value": 67,
                                "Percent": 67
                            }
                        ]
                    }
                ]
            }
        ],
        "Type": "Access"
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为当前操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107041#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有所需资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
