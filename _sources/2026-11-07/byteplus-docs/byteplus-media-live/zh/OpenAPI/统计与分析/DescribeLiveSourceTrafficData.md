---
title: "DescribeLiveSourceTrafficData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivesourcetrafficdata-zh-CN"
---

调用`DescribeLiveSourceTrafficData` API，查询指定拉流域名或源流在指定时间范围内产生的回源流量和带宽的监控数据。

<span id="Requirements"></span>
## 要求


* 限制：支持查询指定拉流域名（包括已删除域名）或指定源流产生的流量用量数据。

* 频率限制：每个账号每秒最多30次查询。

* 数据延迟：

   * 当聚合颗粒度为60秒时，数据延迟为5分钟；

   * 其他时间颗粒度下，数据延迟为15分钟。

* 数据指标：

   * 流量数据以1000进制计算，例如，1 GB = 1000 MB。

   * 带宽数据以1000进制计算，例如，1 Mbps = 1000 Kbps。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveSourceTrafficData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用除需传入API专有参数外，还需传入[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveSourceTrafficData` |API操作名。 |
|Version |String |是 |`2023-01-01` |本API操作的版本号。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |Array of String |否 |`["pull.example.com", "pull2.example.com"]` |拉流域名列表。默认情况下为空，表示查询所有域名的回源流量和带宽数据。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API或前往BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip"><code>DomainList</code>和<code>Domain</code>二选一传入，不可同时传入。</div><br> |
|Domain |String |否 |`pull.example.com` |查询流颗粒度数据时需传入拉流域名，并需同时传入`应用`和`流`。可调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail)接口或前往BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度的回源流监控数据时，需同时指定<code>Domain</code>、<code>应用</code>和<code>流</code>以确定源流。</div><br> |
|应用 |String |否 |`live` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、短横线（\-）和点（.），长度为1~30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度的回源流监控数据时，需同时指定<code>Domain</code>、<code>应用</code>和<code>流</code>以确定源流。</div><br> |
|流 |String |否 |`example_stream` |直播流URL中的StreamName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、短横线（\-）和点（.），长度为1~100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询流颗粒度的回源流监控数据时，需同时指定<code>Domain</code>、<code>应用</code>和<code>流</code>以确定源流。</div><br> |
|ISPList |字符串数组 |否 |`["telecom", "unicom"]` |提供网络接入服务的运营商标识。默认包含所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：中国广电；<br><br>* `huashu`：华数传媒。<br><br><br>如需获取各运营商的标识，可调用[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107029#userregionlist)数组 |否 |`-` |客户端 IP 所属区域列表，默认表示全部区域。 |
|Aggregation |整数 |否 |`300` |数据聚合的颗粒度，单位为秒，支持以下选项：<br><br><br>* `60`：1 分钟。<br><br>* `300`：（默认）5 分钟。<br><br>* `3600`：1 小时。 |
|DetailField |字符串数组 |否 |`["Domain"]` |默认不提供数据分割的维度。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当通过<code>DetailField</code>参数指定数据分割维度，且<code>DomainList</code>或<code>ISPList</code>参数至少有一个传入多个值时，返回调用结果中才会按维度分割数据。</div><br> |
|StartTime |字符串 |是 |`2021-04-13T00:00:00Z` |查询时间范围的起始时间，格式为 RFC 3339，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">历史查询时间范围为 366 天，单次查询的最大时间跨度取决于 DetailField 和 Aggregation。关系说明如下。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">未进行维度分割或仅按一个维度分割数据时：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每 60 秒聚合一次时，单次查询的最大时间跨度为 24 小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每 300 秒聚合一次时，单次查询的最大时间跨度为 31 天。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每 3600 秒聚合一次时，单次查询的最大时间跨度为 31 天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">按两个及以上维度分割数据时：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每 60 秒聚合一次时，单次查询的最大时间跨度为 3 小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每 300 秒聚合一次时，单次查询的最大时间跨度为 24 小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每 3600 秒聚合一次时，单次查询的最大时间跨度为 7 天。</div><br> |
|EndTime |字符串 |是 |`2021-04-14T00:00:00Z` |查询时间范围的结束时间，格式为 RFC 3339，精确到秒。 |


<span id="userregionlist"></span>
### UserRegionList


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |区域信息中的大区标识可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。 |
|Country |字符串 |否 |`CN` |区域信息中的国家标识可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。按国家筛选时，需同时传入`Area`和`Country`。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取标识信息。按省份筛选时，需要同时传入`Area`、`Country`和`Province` |


<span id="Response parameters"></span>
## 返回参数

关于API专有的唯一返回参数，请参见下表。更多详情请参见[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com", "push2.example.com"]` |域名列表。 |
|Domain |字符串 |`push.example.com` |在按流颗粒度查询流量数据时指定的域名。 |
|应用 |字符串 |`live` |在按流颗粒度查询流量数据时指定的应用名称。 |
|流 |字符串 |`example_stream` |在按流颗粒度查询流量数据时指定的流名称。 |
|ISPList |字符串数组 |`["telecom", "unicom"]` |提供网络接入服务的运营商标识。默认包含所有运营商。支持的运营商如下。<br><br><br>* `unicom`: 中国联通；<br><br>* `railcom`: 中国铁通；<br><br>* `telecom`: 中国电信；<br><br>* `mobile`: 中国移动；<br><br>* `cernet`: 中国广电；<br><br>* `tianwei`: 中国天威；<br><br>* `alibaba`: 阿里巴巴集团；<br><br>* `tencent`: 腾讯控股；<br><br>* `drpeng`: Dr.鹏电信传媒集团；<br><br>* `btvn`: 广播电视网络（BTVN）；<br><br>* `huashu`: 华数传媒。 |
|UserRegionList |[UserRegionList](https://docs.byteplus.com/en/docs/24/107029#userregionlist)数组 |`-` |客户端IP所属地区列表。 |
|DetailField |字符串数组 |`["Domain"]` |数据分割维度及其说明如下：<br><br><br>* `Domain`: 域名；<br><br>* `ISP`: 网络服务提供商。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用RFC 3339格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|TotalTraffic |浮点数 |`20` |指定查询时间范围内的总回源流量，单位为GB。 |
|PeakBandwidth |浮点数 |`20` |指定时间范围内的回源峰值带宽，单位为Mbps。 |
|TrafficDataList |[TrafficDataList](https://docs.byteplus.com/en/docs/24/107029#trafficdatalist)数组 |`-` |包含所有时间颗粒度的流量和带宽数据列表。 |
|TrafficDetailDataList |[TrafficDetailDataList](https://docs.byteplus.com/en/docs/24/107029#trafficdetaildatalist)数组 |`-` |按维度分割的流量和带宽数据列表。 |


<span id="userregionlist"></span>
### UserRegionList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Area |字符串 |`CN` |区域信息中的区域标识。 |
|Country |字符串 |`CN` |区域信息中的国家标识。 |
|Province |字符串 |`beijing` |区域信息中的省份标识。 |


<span id="trafficdatalist"></span>
### TrafficDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按时间颗粒度聚合数据时，每个时间颗粒度的起始时间，采用RFC3339 UTC时间格式，精确到秒。 |
|流量 |浮点数 |`20` |当前数据聚合颗粒度内产生的回源流量，单位为GB。 |
|带宽 |浮点数 |`20` |当前数据聚合颗粒度内的回源峰值带宽，单位为Mbps。 |


<span id="trafficdetaildatalist"></span>
### TrafficDetailDataList


|**参数** |**数据类型** |**示例值** |**接口行为** |
|---|---|---|---|
|Domain |字符串 |`push.example.com` |按域名维度分割数据时的域名信息。 |
|ISP |字符串 |`telecom` |按运营商维度分割数据时的运营商信息。 |
|TotalTraffic |浮点数 |`20` |当前维度分割后的总回源流量，单位为GB。 |
|PeakBandwidth |浮点数 |`20` |当前维度分割后的回源峰值带宽，单位为Mbps。 |
|TrafficDataList |[TrafficDataList](https://docs.byteplus.com/en/docs/24/107029#trafficdatalist)数组 |`-` |当前维度分割后所有时间颗粒度下的流量数据列表。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveSourceTrafficData&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "live",
    "Stream": "example_stream",
    "ISPList": [
        "telecom",
        "unicom"
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
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribeLiveSourceTrafficData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "push.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ISPList": [
            "telecom",
            "unicom"
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
        "TotalTraffic": 20,
        "TrafficDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Traffic": 20,
                "Bandwidth": 20
            }
        ],
        "TrafficDetailDataList": [
            {
                "Domain": "push.example.com",
                "ISP": "telecom",
                "TotalTraffic": 20,
                "TrafficDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Traffic": 20,
                        "Bandwidth": 10
                    }
                ],
                "PeakBandwidth": 20
            }
        ],
        "PeakBandwidth": 20
    }
}
```


<span id="Error codes"></span>
## 错误码

以下为本次操作相关的错误码。其他错误码请参见[BytePlus OpenAPI通用错误码](https://docs.byteplus.com/en/byteplus-platform/reference/common-error-codes)。


|**状态码** |**错误码** |**错误信息** |**接口行为** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/107029#request-parameters)说明进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有所请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
