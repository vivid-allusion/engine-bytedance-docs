---
title: "DescribeLiveStreamSessionData"
product: "BytePlus MediaLive"
product_code: "byteplus-media-live"
source: "https://docs.byteplus.com/en/docs/byteplus-media-live/describelivestreamsessiondata-zh-CN"
---

调用 `DescribeLiveStreamSessionData` API，在指定时间范围内查询指定域下所有在线流或指定在线流的请求次数和最大在线观众数。

<span id="Requirements"></span>
## 要求


* 限制：支持查询指定直播域（包括已删除域）的请求次数和最大并发观众数。

* 速率限制：每个账号每秒最多30次查询

* 数据延迟：

   * 当聚合颗粒度为60秒时，数据延迟为5分钟；

   * 其他时间颗粒度的数据延迟为15分钟。


<span id="HTTP request"></span>
## HTTP请求


* 方法：POST

* Endpoint：https://open.byteplusapi.com/?Action=DescribeLiveStreamSessionData&Version=2023\-01\-01


<span id="Request parameters"></span>
## 请求参数

<span id="Common parameters"></span>
### 通用参数

所有API调用时，除API专用参数外，还必须包含[通用参数](https://docs.byteplus.com/en/byteplus-platform/reference/common-parameters)。

<span id="Query"></span>
### 查询


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|Action |String |是 |`DescribeLiveStreamSessionData` |API操作。 |
|Version |String |是 |`2023-01-01` |该API操作的版本。当前版本：2023\-01\-01。 |


<span id="Body parameters"></span>
### Body参数


|**参数** |**数据类型** |**是否必填** |**示例值** |**接口行为** |
|---|---|---|---|---|
|DomainList |String数组 |否 |`["pull.example.com"]` |拉流域名列表。默认情况下为空，表示会查询所有域的请求次数和在线观众数据。可通过调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail) API或访问BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">应提供<code>DomainList</code>或<code>Domain</code>，不可同时提供。</div><br> |
|Domain |String |否 |`pull.example.com` |在按流颗粒度查询数据时，必须提供拉流域名，并同时提供`应用`和`流`参数。可通过调用[ListDomainDetail](https://docs.byteplus.com/en/docs/byteplus-media-live/docs-listdomaindetail)接口或访问BytePlus MediaLive控制台的[Domains](https://console.byteplus.com/live/main/domain/list)页面获取待查询的拉流域名。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在按流颗粒度查询请求次数和在线用户数据时，必须同时指定<code>Domain</code>、<code>应用</code>和<code>流</code>参数以确定直播流。</div><br> |
|应用 |String |否 |`example_app` |直播流URL中的AppName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至30个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在按流颗粒度查询源流量监控数据时，必须指定<code>Domain</code>、<code>应用</code>和<code>流</code>以标识具体源流。</div><br> |
|流 |String |否 |`example_stream` |直播流URL中的StreamName字段。可包含大写字母（A\-Z）、小写字母（a\-z）、数字（0\-9）、下划线（_）、连字符（\-）和点（.），长度为1至100个字符。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">在按流颗粒度查询源流量监控数据时，必须指定<code>Domain</code>、<code>应用</code>和<code>流</code>以标识源流。</div><br> |
|ProtocolList |String数组 |否 |`["HTTP-FLV", "RTMP"]` |推拉流协议。默认表示所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于HTTP协议的推拉流协议，采用FLV格式进行视频传输。<br><br>* `HTTP-HLS`：基于HTTP协议的推拉流协议，采用TS格式进行视频传输。<br><br>* `RTMP`：用于实时消息传输的RTMP协议。<br><br>* `RTM`：用于超低延时直播的实时媒体协议。<br><br>* `SRT`：用于安全可靠流传输的安全可靠传输协议。<br><br>* `QUIC`：基于UDP的新型低延迟互联网传输协议（Quick UDP Internet Connections）。<br><br>* `CMAF`：通用媒体应用格式协议，具备多功能流传输能力。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">查询QUIC协议时，不能同时查询其他协议。</div><br> |
|ISPList |字符串数组 |否 |`["telecom"]` |提供网络接入服务的运营商标识。默认表示所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研网（CERNET）；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：中国广电；<br><br>* `huashu`：华数传媒。<br><br><br>如需获取各运营商标识，可调用[DescribeLiveISPData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveispdata)。 |
|RegionList |[RegionList](https://docs.byteplus.com/en/docs/24/106995#regionlist)数组 |否 |`-` |CDN节点IP所属区域列表，默认表示所有区域。 |
|Aggregation |整数 |否 | |数据聚合的颗粒度，单位为秒，支持如下选项：<br><br><br>* `60`：1分钟。<br><br>* `300`：（默认）5分钟。<br><br>* `3600`：1小时。 |
|DetailField |字符串数组 |否 |`["Domain"]` |数据默认不按维度拆分。支持的维度如下：<br><br><br>* `Domain`：域名；<br><br>* `ISP`：互联网服务提供商；<br><br>* `Protocol`：推拉流协议。<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">仅当<code>DetailField</code>参数指定了拆分维度，且以下参数之一提供了多个值时：<code>DomainList</code>、<code>ProtocolList</code>或<code>ISPList</code>，返回调用结果才会按维度拆分数据。</div><br> |
|StartTime |字符串 |是 |`2021-04-13T00:00:00Z` |查询范围的起始时间，采用RFC 3339格式，精确到秒。<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">历史查询时间范围为366天，单次查询的最大时间跨度取决于DetailField和Aggregation。关系描述如下。</div><br><br><br><br>* <div data-tips="true" data-tips-type="tip">未进行维度拆分或仅按一个维度拆分数据时：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每60秒聚合一次，单次查询最大时间跨度为24小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每300秒聚合一次，单次查询最大时间跨度为31天。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每3600秒聚合一次，单次查询最大时间跨度为31天。</div><br><br><br>* <div data-tips="true" data-tips-type="tip">按两个及以上维度拆分数据时：</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每60秒聚合一次，单次查询最大时间跨度为3小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每300秒聚合一次，单次查询最大时间跨度为24小时。</div><br><br><br>   * <div data-tips="true" data-tips-type="tip">数据每3600秒聚合一次，单次查询最大时间跨度为7天。</div><br> |
|EndTime |字符串 |是 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |


<span id="regionlist"></span>
### RegionList


|**参数** |**数据类型** |**是否必填** |**示例值** |**描述** |
|---|---|---|---|---|
|Area |字符串 |否 |`CN` |区域信息中的主要区域标识符可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。 |
|Country |字符串 |否 |`CN` |区域信息中的国家标识符可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取。按国家过滤时，需同时传入 'Area' 和 'Country'。 |
|Province |字符串 |否 |`beijing` |区域信息中的省份标识符目前不支持中国大陆、香港、澳门、台湾以外的国家或地区。可通过调用[DescribeLiveRegionData](https://docs.byteplus.com/en/docs/byteplus-media-live/describeliveregiondata)获取标识符信息。按省份过滤时，需同时传入`Area`、`Country`和`Province`。 |


<span id="Response parameters"></span>
## 返回调用结果参数

有关唯一的API专用返回调用结果参数，请参见下表。更多详情请参考[请求返回调用结果](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response)部分。


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|DomainList |字符串数组 |`["push.example.com"]` |域名列表。 |
|Domain |字符串 |`pull.example.com` |拉流域名。 |
|App |字符串 |`live` |直播流 URL 中的 AppName 字段。 |
|Stream |字符串 |`example_stream` |直播流 URL 中的 StreamName 字段。 |
|ProtocolList |字符串数组 |`["HTTP-FLV", "RTMP"]` |推拉流协议。默认表示所有协议类型。支持的协议如下。<br><br><br>* `HTTP-FLV`：基于 HTTP 协议的推拉流协议，采用 FLV 格式进行视频传输。<br><br>* `HTTP-HLS`：基于 HTTP 协议的推拉流协议，采用 TS 格式进行视频传输。<br><br>* `RTMP`：用于实时消息传输的 RTMP 协议。<br><br>* `RTM`：用于超低延时直播的实时媒体协议。<br><br>* `SRT`：用于安全可靠传输的 SRT 协议。<br><br>* `QUIC`：基于 UDP 的新型低延迟互联网传输协议。<br><br>* `CMAF`：通用媒体应用格式协议。 |
|ISPList |字符串数组 |`["telecom", "unicom"]` |提供网络接入服务的运营商标识符。默认包含所有运营商。支持的运营商如下。<br><br><br>* `unicom`：中国联通；<br><br>* `railcom`：中国铁通；<br><br>* `telecom`：中国电信；<br><br>* `mobile`：中国移动；<br><br>* `cernet`：中国教育和科研计算机网；<br><br>* `tianwei`：中国天威；<br><br>* `alibaba`：阿里巴巴集团；<br><br>* `tencent`：腾讯控股；<br><br>* `drpeng`：鹏博士电信传媒集团；<br><br>* `btvn`：广播电视网络（BTVN）；<br><br>* `huashu`：华数传媒。 |
|RegionList |[RegionList](https://docs.byteplus.com/en/docs/24/106995#regionlist)数组 |`-` |CDN 节点 IP 所属区域列表。 |
|StartTime |字符串 |`2021-04-13T00:00:00Z` |查询范围的开始时间，采用 RFC 3339 格式，精确到秒。 |
|EndTime |字符串 |`2021-04-14T00:00:00Z` |查询范围的结束时间，采用 RFC 3339 格式，精确到秒。 |
|Aggregation |整数 |`300` |数据颗粒度，单位为秒。 |
|DetailField |字符串数组 |`["Domain"]` |数据分割维度：<br><br><br>* `Domain`：域名。<br><br>* `ISP`：互联网服务提供商。<br><br>* `Protocol`：推拉流协议。 |
|TotalRequest |整数 |`20` |指定查询时间范围内的请求总数。 |
|PeakOnlineUser |整数 |`20` |指定查询时间范围内的并发在线用户峰值。 |
|TotalHitRate |双精度 |`13.45` |指定时间范围内所有域名和协议的整体边缘请求命中率。用于评估边缘请求缓存机制对源站负载的减轻效果。 |
|SessionDataList |[SessionDataList](https://docs.byteplus.com/en/docs/24/106995#sessiondatalist)数组 |`-` |所有时间颗粒度的数据。 |
|SessionDetailDataList |[SessionDetailDataList](https://docs.byteplus.com/en/docs/24/106995#sessiondetaildatalist)数组 |`-` |按具体维度分割的数据。 |


<span id="regionlist"></span>
### RegionList


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|区域 |字符串 |`CN` |区域信息中的区域标识符。 |
|国家 |字符串 |`CN` |区域信息中的国家标识符。 |
|省份 |字符串 |`beijing` |区域信息中的省份标识符。 |


<span id="sessiondatalist"></span>
### SessionDataList


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|TimeStamp |字符串 |`2022-04-13T00:00:00Z` |按颗粒度聚合数据时，每个时间颗粒度的起始时间，采用 RFC3339 UTC 时间格式，精确到秒。 |
|Request |整数 |`10` |当前数据聚合颗粒度内的请求次数。 |
|OnlineUser |整数 |`20` |当前数据聚合颗粒度内的在线用户峰值。 |
|HitRate |双精度 |`13.45` |指定颗粒度下的边缘请求命中率（例如每 60 秒或每 5 分钟）。 |


<span id="sessiondetaildatalist"></span>
### SessionDetailDataList


|**参数** |**数据类型** |**示例值** |**描述** |
|---|---|---|---|
|Domain |字符串 |`pull.example.com` |按域名维度拆分数据时的域名信息。 |
|Protocol |字符串 |`HTTP-FLV` |按流协议维度拆分数据时的协议信息。 |
|ISP |字符串 |`telecom` |按 ISP 维度拆分数据时的 ISP 信息。 |
|TotalRequest |整数 |`20` |数据拆分后当前维度的请求次数。 |
|PeakOnlineUser |整数 |`20` |数据拆分后当前维度的在线用户峰值。 |
|TotalHitRate |浮点型 |`13.45` |数据按特定维度（如`Domain`）拆分后，在指定查询时间范围内每个维度的整体边缘请求命中率。该指标用于评估不同数据分段的缓存效率。 |
|SessionDataList |[SessionDataList](https://docs.byteplus.com/en/docs/24/106995#sessiondatalist) 数组 |`-` |数据拆分后当前维度的所有时间颗粒度数据。 |


<span id="Samples"></span>
## 示例

<span id="Sample request"></span>
### 请求示例

```json
POST https://open.byteplusapi.com/?Action=DescribeLiveStreamSessionData&Version=2023-01-01
{
    "Domain": "pull.example.com",
    "App": "example_app",
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
    "StartTime": "2021-04-13T00:00:00Z",
    "EndTime": "2021-04-14T00:00:00Z",
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
        "Action": "DescribeLiveStreamSessionData",
        "Version": "2023-01-01",
        "Service": "live",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "pull.example.com",
        "App": "live",
        "Stream": "example_stream",
        "ProtocolList": [
            "HTTP-FLV",
            "RTMP"
        ],
        "ISPList": [
            "telecom",
            "unicom"
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
        "TotalRequest": 20,
        "PeakOnlineUser": 20,
        "TotalHitRate": 13.41,
        "SessionDataList": [
            {
                "TimeStamp": "2022-04-13T00:00:00Z",
                "Request": 10,
                "OnlineUser": 20,
                "HitRate": 13.41
            }
        ],
        "SessionDetailDataList": [
            {
                "Protocol": "HTTP-FLV",
                "Domain": "pull.example.com",
                "ISP": "telecom",
                "TotalRequest": 20,
                "PeakOnlineUser": 20,
                "SessionDataList": [
                    {
                        "TimeStamp": "2022-04-13T00:00:00Z",
                        "Request": 20,
                        "OnlineUser": 20,
                        "HitRate": 13.41
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


|**状态码** |**错误码** |**错误信息** |**描述** |
|---|---|---|---|
|400 |InvalidParam |*  |输入参数无效或不符合要求。请参考[请求参数](https://docs.byteplus.com/en/docs/24/106995#request-parameters)描述进行检查。 |
|403 |RequestForbidden |*  |请求被拒绝，因为当前账号下没有请求的资源（资源包括域名空间、域名、应用名称、配置和证书）。 |
|500 |InternalError |发生内部错误，请联系管理员。 |发生内部错误。请[联系支持](https://console.byteplus.com/workorder/create)。 |
