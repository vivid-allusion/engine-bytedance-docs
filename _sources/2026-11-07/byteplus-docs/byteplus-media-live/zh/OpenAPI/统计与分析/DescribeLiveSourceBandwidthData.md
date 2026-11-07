---
title: "DescribeLiveSourceBandwidthData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcebandwidthdata-zh-CN"
---

调用 `DescribeLiveSourceBandwidthData` API，以查询指定拉流域名或源流在指定时间范围内产生的源带宽监控数据。

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">自2025年2月18日起，我们将不再维护此旧版API。其文档将于2025年5月18日下线。建议迁移至新版UpdateUser接口。详情请参见<a href="https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata">DescribeLiveSourceTrafficData</a>文档。</div>


<span id="Requirements"></span>
## 要求


* 限制：支持查询指定拉流域名（包括已删除域名）或指定源流产生的带宽使用数据。

* 频率限制：每个账号每秒最多查询30次

* 数据延迟：

   * 当聚合颗粒度为60秒时，数据延迟为5分钟；

   * 其他时间颗粒度的数据延迟为15分钟。

* 数据指标：带宽数据以1000为基数进行计算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSourceBandwidthData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专属参数外，还需包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSourceBandwidthData` |API操作。 |
|Version |String |是 |`2023-01-01` |此API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["pull.example.com", "pull2.example.com"]` |拉流域名列表。默认情况下为空，表示将查询所有域名的源带宽使用数据。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API或访问BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取需查询的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">应仅提供<code>DomainList</code>或<code>Domain</code>，不可同时提供。</div><br> |
|Domain |String |否 |`pull.example.com` |查询流颗粒度数据时需填写拉流域名，并需同时提供`应用`和`流`。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail)接口或前往BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取需查询的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度的源带宽监控数据时，需同时指定<code>Domain</code>、<code>应用</code>和<code>流</code>以确定源流。</div><br> |
|应用 |String |否 |`live` |源流的AppName字段支持字母数字（A\-Z，a\-z，0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度的源流带宽监控数据时，需同时指定<code>Domain</code>、<code>应用</code>和<code>流</code>以确定源流。</div><br> |
|流 |String |否 |`example_stream` |源流的StreamName字段支持字母数字（A\-Z，a\-z，0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在以流颗粒度查询源流的带宽监控数据时，需要同时指定<code>Domain</code>、<code>App</code>和<code>Stream</code>以确定源流。</div><br> |
|ISPList |字符串数组 |否 |`["telecom"]` |提供网络接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士。鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒；<br><br><br>如需获取各运营商的标识，可调用[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107005#userregionlist)数组 |否 |`-` |客户端IP所属区域列表，默认表示所有区域。 |
|StartTime |字符串 |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |否 |`300` |数据聚合颗粒度，单位为秒，支持以下选项：<br><br><br>* `60`：1分钟。按1分钟聚合时，单次查询的最大时间跨度为24小时，历史查询时间范围为366天；<br><br>* `300`：（默认）5分钟。按5分钟聚合时，单次查询的最大时间跨度为31天，历史查询时间范围为366天；<br><br>* `3600`：1小时。按1小时聚合时，单次查询的最大时间跨度为93天，历史查询时间范围为366天。 |
|DetailField |字符串数组 |否 |`["Domain"]` |默认情况下，数据不会按维度进行分段。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当使用<code>DetailField</code>参数指定数据分段维度，且<code>DomainList</code>或<code>ISPList</code>参数至少有一个传入多个值时，返回调用结果中才会按维度进行数据分段。</div><br> |


<span id="userregionlist"></span>
### UserRegionList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |区域信息中的主要区域标识可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。 |
|Country |字符串 |否 |`CN` |区域信息中的国家标识可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。按国家过滤时，需要同时传入`Area`和`Country`。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取标识信息。按省份过滤时，需要同时传入`Area`、`Country`和`Province` |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专属返回调用结果参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["pull.example.com", "pull2.example.com"]` |域名列表。 |
|Domain |字符串 |`pull.example.com` |以流颗粒度查询流量数据时指定的域名。 |
|App |字符串 |`live` |以流颗粒度查询流量数据时指定的应用名称。 |
|Stream |字符串 |`example_stream` |在以流颗粒度查询流量数据时指定的流名称。 |
|ISPList |字符串数组 |`["telecom"]` |用于指示互联网服务提供商（ISP）标识符的数组。有效选项包括：<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107005#userregionlist)数组 |`-` |客户端IP所属区域列表。 |
|DetailField |字符串数组 |`["Domain"]` |用于数据分割的维度及其说明如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|PeakBandwidth |浮点数 |`20` |指定时间范围内的源站峰值带宽，单位为Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107005#bandwidthdatalist)数组 |`-` |包含所有时间颗粒度带宽数据的列表。 |
|BandwidthDetailDataList |[BandwidthDetailDataList](https://docs.byteplus.com/en/docs/24/107005#bandwidthdetaildatalist)数组 |`-` |按维度分割后带宽数据的列表。 |


<span id="userregionlist"></span>
### UserRegionList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识符。 |
|Country |字符串 |`CN` |区域信息中的国家标识符。 |
|Province |字符串 |`beijing` |区域信息中的省份标识符。 |


<span id="bandwidthdatalist"></span>
### BandwidthDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|Bandwidth |浮点数 |`20` |当前数据聚合时间颗粒度内的源站峰值带宽，单位为Mbps。 |


<span id="bandwidthdetaildatalist"></span>
### BandwidthDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`pull.example.com` |按域名维度分割数据时的域名信息。 |
|ISP |字符串 |`telecom` |按ISP维度分割数据时的ISP信息。 |
|PeakBandwidth |浮点数 |`20` |按维度分割后当前维度的源站峰值带宽，单位为Mbps。 |
|BandwidthDataList |[BandwidthDataList](https://docs.byteplus.com/en/docs/24/107005#bandwidthdatalist)数组 |`-` |按维度分割后当前维度下所有时间颗粒度的带宽数据列表。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceBandwidthData&Version=2023-01-01
{
    "DomainList": [
        "pull.example.com",
        "pull2.example.com"
    ],
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ISPList": [
        "telecom"
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
        "Action": "DescribeLiveSourceBandwidthData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainList": [
            "pull.example.com",
            "pull2.example.com"
        ],
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ISPList": [
            "telecom"
        ],
        "UserRegionList": [
            {
                "Area": "CN",
                "Country": "CN",
                "Province": "beijing"
            }
        ],
        "DetailField": [
            "Domain"
        ],
        "StartTime": "2021-04-13T00:00:00Z",
        "EndTime": "2021-04-14T00:00:00Z",
        "Aggregation": 300,
        "PeakBandwidth": 20,
        "BandwidthDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Bandwidth": 20
            }
        ],
        "BandwidthDetailDataList": [
            {
                "Domain": "pull.example.com",
                "ISP": "telecom",
                "PeakBandwidth": 20,
                "BandwidthDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Bandwidth": 20
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


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107005#request-parameters)接口行为进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下无请求资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
