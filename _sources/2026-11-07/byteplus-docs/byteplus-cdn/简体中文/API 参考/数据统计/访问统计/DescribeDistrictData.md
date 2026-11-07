---
title: "DescribeDistrictData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictData"
---

<span id="api-说明"></span>
## API 说明

基于 CDN 收到的用户请求，该 API 对一个指标统计各时间点的指标细分数据。

要调用该 API，您需要指定一个指标，一个统计时间段和一个时间粒度。您还可以指定多个过滤条件对用户请求进行过滤。您最多能查询过去 92 天的数据。

数据稳定性：受网络波动影响，边缘节点上统计的指标数据可能会发生变化。大多数情况下，指标数据会在 12 小时内逐步稳定下来。因此，该 API 返回的指标数据并非账单中显示的用量，仅供参考。实际用量请以账单为准。

数据时效性：指标数据可能会有 5 分钟左右的延时。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您刚接触 CDN 的统计 API，请务必先阅读以下文档，这将有助于您理解该 API 文档。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn">统计时间段说明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/lHMepA">指标的定义以及统计方式</a></div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeDistrictData&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeDistrictData`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Metric |String |是 |表示一个指标。该参数有以下取值：<br><br><br>* `in_traffic`：表示用户向 CDN 传输的数据量，单位是 bytes。<br><br>* `in_bandwidth`：表示基于用户向 CDN 传输的数据量而计算的带宽，单位是 bps。<br><br>* `out_traffic`：表示 CDN 向用户传输的数据量，单位是 bytes。<br><br>* `out_bandwidth`：表示基于 CDN 向用户传输的数据量而计算的带宽，单位是 bps。<br><br>* `requests`：表示 CDN 收到的所有用户请求的数量。<br><br>* `dynamic_requests`：对于 CDN 收到的用户请求，该指标表示满足以下所有条件的用户请求数量。<br><br>   * 请求方法既不是 GET，也不是 HEAD。<br><br>   * CDN 的响应状态码不是 405。<br><br>* `static_requests`：对于 CDN 收到的用户请求，该指标表示满足以下所有条件的用户请求数量。<br><br>   * 请求方法是 GET 或者 HEAD。<br><br>   * CDN 的响应状态码不是 405。<br><br>* `qps`：表示 CDN 收到的用户请求的 QPS。<br><br>* `response_time`：表示 CDN 响应用户请求所耗费的平均时间，单位是毫秒（ms）。<br><br>* `avg_speed`：表示 CDN 在响应用户请求时的平均数据传输速度，单位是 Bps。该指标的数据是对响应状态码是 2xx 的用户请求统计的。<br><br>* `status_all`：在 CDN 对用户请求的响应中，该参数表示以下类别的状态码数量：<br><br>   * 所有状态码的数量。<br><br>   * 2xx 状态码的数量。<br><br>   * 3xx 状态码的数量。<br><br>   * 4xx 状态码的数量。<br><br>   * 5xx 状态码的数量。<br><br>   * 每个状态码的数量。<br><br>* `status_2xx`：表示 2xx 状态码的数量以及该类别下每个状态码的数量。<br><br>* `status_3xx`：表示 3xx 状态码的数量以及该类别下每个状态码的数量。<br><br>* `status_4xx`：表示 4xx 状态码的数量以及该类别下每个状态码的数量。<br><br>* `status_5xx`：表示 5xx 状态码的数量以及该类别下每个状态码的数量。<br><br><br>关于每个指标的详情以及统计方式，参见 [指标的定义以及统计方式](https://docs.byteplus.com/en/docs/byteplus-cdn/lHMepA)。<br><br>说明<br><br>如果您指定 `Metric` 为 `response_time` 或者 `avg_speed`，请务必指定 `Protocol`。参见 `Protocol` 参数的描述。 |`traffic` |
|StartTime |Long |是 |表示统计时间段的开始时间，格式是 Unix 时间戳，精度是秒。`StartTime` 必须早于或者等于 `EndTime`。同时，`StartTime` 与 `EndTime` 所表示的统计时间段不能超过 31 天。 |`1710259200` |
|EndTime |Long |是 |表示统计时间段的结束时间，格式是 Unix 时间戳，精度是秒。 |`1710836303` |
|Interval |String |否 |表示一个时间粒度。该 API 基于 `Interval` 将 `StartTime` 和 `EndTime` 所表示的统计时间段拆分成一系列的时间区间，然后对每个时间区间统计 `Metric` 数据。<br><br>关于 `Interval` 参数是如何用来拆分统计时间段，参考 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn)。<br><br>该参数有以下取值：<br><br><br>* `1min`：表示时间粒度是 1 分钟。<br><br>* `5min`：表示时间粒度是 5 分钟。<br><br>* `hour`：表示时间粒度是 1 小时。<br><br>* `day`：表示时间粒度是 1 天。<br><br><br>您可以指定的时间粒度受 `StartTime` 和 `EndTime` 所表示的时间范围的影响。<br><br><br>* 如果时间范围 <= 1 天，您可以指定的时间粒度包含 `1min`、`5min`、`hour`。<br><br>* 如果 1 天 < 时间范围 <= 3 天，您可以指定的时间粒度包含 `5min`、`hour`、`day`。<br><br>* 如果 3 天 < 时间范围 <= 31 天，您可以指定的时间粒度包含 `hour`、`day`。<br><br><br>该参数的默认值是 `5min`。如果默认值不匹配时间范围，API 请求会失败。 |`hour` |
|Project |String |否 |表示一个项目。<br><br><br>* 如果您指定了 `Domain`，该 API 对所有您指定的域名统计 `Metric` 数据。<br><br>* 如果您指定了 `Project` ，但未指定 `Domain`，该 API 对您指定的项目统计 `Metric` 数据。参见 [项目数据是如何统计的](https://docs.byteplus.com/en/docs/18/20608#%E9%A1%B9%E7%9B%AE%E6%95%B0%E6%8D%AE%E6%98%AF%E5%A6%82%E4%BD%95%E7%BB%9F%E8%AE%A1%E7%9A%84)。<br><br>* 如果您既未指定 `Project` ，也未指定 `Domain`，该 API 对所有域名统计 `Metric` 数据。 |`my_project` |
|Domain |String |否 |表示一个或多个域名，用于对用户请求进行过滤。该 API 对您指定的每个域名统计 `Metric` 数据。您最多可以指定 50 个域名。多个域名之间使用逗号（,）分隔。如果不指定 `Domain`，表示不使用该参数对请求进行过滤。<br><br>如果您指定了 `Project`，您指定的域名必须是属于该 `Project` 的。<br><br>说明<br><br>当子用户调用该 API 时，请留意以下说明：<br><br><br>* 子用户只能指定其有权限访问的域名。子用户可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn) 获取其有权限访问的域名。<br><br>* 如果不指定该参数，表示所有该子用户有权限访问的那些域名。 |`www.example.com,www.test.com,img.example.com` |
|Location |String |否 |表示国家和地区的代码，用于对用户请求进行过滤。您可以指定一个或者多个代码，CDN 对来自这些国家和地区的用户请求统计 `Metric` 数据。多个国家和地区代码之间使用逗号（,）分隔。您最多可以指定 30 个国家和地区。<br><br><br>* 如果您指定了 `Location`，就不能指定 `Province`，反之亦然。<br><br>* 如果您不指定 `Location`，表示不使用该参数对请求进行过滤。<br><br><br>您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取代码与国家和地区的对应表。 |`CHN,AZE` |
|Province |String |否 |表示中国省级行政区的代码，用于对用户请求进行过滤。您可以指定一个或者多个代码，CDN 对来自这些省级行政区的用户请求统计 `Metric` 数据。多个代码之间使用逗号（,）分隔。您最多可以指定 10 个代码。<br><br>如果您不指定 `Province`，表示不使用该参数对请求进行过滤。<br><br>您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取代码与中国省级行政区的对应表。 |`AH,BJ,CQ,FJ` |
|Isp |String |否 |表示请求所使用的中国网络运营商的代码，用于对用户请求进行过滤。例如，`CT` 表示中国电信。您可以指定一个或者多个代码，CDN 对使用这些网络运营商的用户请求统计 `Metric` 数据。多个代码之间使用逗号（,）分隔。您最多可以指定 5 个代码。<br><br><br>* 当 `Location` 是 `CHN` 或者您指定了 `Province` 时，您才能指定 `Isp`。<br><br>* 当您不指定 `Isp` 时，表示不使用该参数对请求进行过滤。<br><br><br>您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取代码与网络运营商的对应表。 |`CT,CM,CU,GWBN` |
|Protocol |String |否 |表示请求使用的一个应用层协议，用于对用户请求进行过滤。该参数的可用值如下：<br><br><br>* `http`：表示 HTTP 协议。<br><br>* `https`：表示 HTTPS 协议。<br><br>* `quic`：表示 QUIC 协议。<br><br>* `websocket`：表示 WebSocket 协议。<br><br>* `non-websocket`：表示 HTTP 协议， HTTPS 协议和 QUIC 协议。<br><br><br>如果不指定 `Protocol`，表示不使用该参数对请求进行过滤。<br><br>说明<br><br>如果 `Metric` 是 `response_time` 或者 `avg_speed`，请指定 `Protocol` 以过滤掉 WebSocket 协议。因为对于 WebSocket 请求，这两个指标的数据不准确。 |`https` |
|IpVersion |String |否 |表示请求使用的一个网络层协议，用于对用户请求进行过滤。该参数的可用值如下：<br><br><br>* `IPv4`：表示 IPv4 协议。<br><br>* `IPv6`：表示 IPv6 协议。<br><br><br>如果不指定 `IpVersion`，表示不使用该参数对请求进行过滤。 |`IPv4` |
|TimeZone |String |否 |表示 `Metric` 数据的时区。该参数有以下取值：<br><br><br>* `Etc/GMT`：表示的时区是 UTC+00:00。<br><br>* `Etc/GMT-1`、`Etc/GMT-2`、...、`Etc/GMT-12`：表示的时区分别是 UTC+01:00、UTC+02:00、...、UTC+12:00。<br><br>* `Etc/GMT+1`、`Etc/GMT+2`、...、`Etc/GMT+12`：表示的时区分别是 UTC\-01:00、UTC\-02:00、...、UTC\-12:00。<br><br><br>该参数的默认值是 `Etc/GMT-8`。 |`Etc/GMT-8` |


<span id="项目数据是如何统计的"></span>
### 项目数据是如何统计的

在对一个项目统计指标数据时，CDN 统计的是项目内域名的数据。


* 如果统计时间段内有一个域名转出该项目，该项目的指标数据不会包含转出后该域名的数据。

* 如果统计时间段内有一个域名转入该项目，该项目的指标数据会包含转入后该域名的数据。


**示例**

考虑以下场景：


* 您指定的统计时间段是某天的 8:00\-10:00。

* 域名X 在 9:00 从另一个项目转移到项目A。域名Y 一直在项目A 中。


在这个场景中，如果您对项目A 统计指标数据，则指标数据涵盖：


* 域名X 在 9:00 至 10:00 之间的指标数据。

* 域名Y 在 8:00 至 10:00 之间的指标数据。


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|MetricDataList |Object[] |表示该 API 返回的结果数据。 | |
|Metric |String |表示请求参数 `Metric` 所指定的指标。 |`traffic` |
|Values |Object[] |表示基于 `Interval` 统计出的一组 `Metric` 数据对象。 | |
|TimeStamp |Long |表示 `Value` 所对应的时间区间的开始时间，格式是 Unix 时间戳，精度是秒。参见 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn). |`1710273600` |
|Value |Double |表示一个 `Metric` 细分数据。 |`4567` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDistrictData&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "day",
    "IpVersion": "IPv4",
    "Isp": "CT,CM,CU,GWBN",
    "Metric": "out_traffic",
    "Project": "my_project",
    "Protocol": "https",
    "Province": "AH,BJ,CQ,FJ"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031916110305F6D27733C2CA667E04",
        "Action": "DescribeDistrictData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "Metric": "out_traffic",
                "Values": [
                    {
                        "TimeStamp": 1710201600,
                        "Value": 31667254.3
                    },
                    {
                        "TimeStamp": 1710288000,
                        "Value": 35425907
                    },
                    {
                        "TimeStamp": 1710374400,
                        "Value": 33508322.1
                    },
                    {
                        "TimeStamp": 1710460800,
                        "Value": 29844611.5
                    },
                    {
                        "TimeStamp": 1710547200,
                        "Value": 19993227.1
                    },
                    {
                        "TimeStamp": 1710633600,
                        "Value": 19567554.6
                    },
                    {
                        "TimeStamp": 1710720000,
                        "Value": 32469929.8
                    },
                    {
                        "TimeStamp": 1710806400,
                        "Value": 30702487.2
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
