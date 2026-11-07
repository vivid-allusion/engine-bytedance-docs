---
title: "DescribeEdgeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeRanking"
---

<span id="api-说明"></span>
## API 说明

基于 CDN 收到的用户请求，该 API 按分组对一系列的指标数据进行汇总，并对这些汇总数据按从大到小排序。分组条件包括域名和计费区域。

要调用该 API，您需要指定一个指标，一个分组条件，一个统计时间段和一个时间粒度。您还可以指定多个过滤条件（包括计费区域）对用户请求进行过滤。您最多能查询过去 92 天的数据。

数据稳定性：受网络波动影响，边缘节点上统计的指标数据可能会发生变化。大多数情况下，指标数据会在 12 小时内逐步稳定下来。

数据时效性：指标数据可能会有 5 分钟左右的延时。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您是刚开始使用数据统计的 API，请务必先阅读以下文档，这将有助于您理解该 API 文档。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn">统计时间段说明</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/lHMepA">指标的定义以及统计方式</a></div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeEdgeRanking&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeEdgeRanking`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Item |String |是 |表示一个分组条件，用于对 `Metric` 数据进行汇总。该参数有以下取值：<br><br><br>* `domain`：表示 `Domain` 所指定的域名。<br><br>* `billingRegion`：表示 `BillingRegion` 所指定的计费区域。 |`domain` |
|Metric |String |是 |表示一个指标。该参数有以下取值：<br><br><br>* `in_traffic`：表示用户向 CDN 传输的数据量，单位是 bytes。<br><br>* `in_bandwidth`：表示基于用户向 CDN 传输的数据量而计算的带宽峰值，单位是 bps。<br><br>* `out_traffic`：表示 CDN 向用户传输的数据量，单位是 bytes。<br><br>* `out_bandwidth`：表示基于 CDN 向用户传输的数据量而计算的带宽峰值，单位是 bps。<br><br>* `requests`：表示 CDN 收到的所有用户请求的数量。<br><br>* `dynamic_requests`：对于 CDN 收到的用户请求，该指标表示满足以下所有条件的用户请求数量。<br><br>   * 请求方法既不是 GET，也不是 HEAD。<br><br>   * CDN 的响应状态码不是 405。<br><br>* `static_requests`：对于 CDN 收到的用户请求，该指标表示满足以下所有条件的用户请求数量。<br><br>   * 请求方法是 GET 或者 HEAD。<br><br>   * CDN 的响应状态码不是 405。<br><br><br>关于每个指标的详情以及统计方式，参见 [指标的定义以及统计方式](https://docs.byteplus.com/en/docs/byteplus-cdn/lHMepA)。 |`traffic` |
|BillingRegion |String |否 |表示一个或多个计费区域，用于对用户请求进行过滤。该 API 对来自这些计费区域的用户请求统计 `Metric` 数据。多个计费区域之间使用逗号（,）分隔。该参数有以下取值：<br><br><br>* `CHN`：表示中国内地。<br><br>* `EU`：表示欧洲区。<br><br>* `NA`：表示北美区。<br><br>* `SA`：表示南美区。<br><br>* `MEA`：表示中东区和非洲区。<br><br>* `AP1`：表示亚太一区。<br><br>* `AP2`：表示亚太二区。<br><br>* `AP3`：表示亚太三区。<br><br><br>如果不指定 `BillingRegion`，表示不使用该参数对请求进行过滤。 |`CHN,EU` |
|StartTime |Long |是 |表示统计时间段的开始时间，格式是 Unix 时间戳，精度是秒。`StartTime` 必须早于或者等于 `EndTime`。同时，`StartTime` 和 `EndTime` 所表示的统计时间段不能超过 31 天。 |`1710259200` |
|EndTime |Long |是 |表示统计时间段的结束时间，格式是 Unix 时间戳，精度是秒。 |`1710836303` |
|Interval |String |否 |表示一个时间粒度。该 API 基于 `Interval` 将 `StartTime` 和 `EndTime` 所表示的统计时间段拆分成一系列的时间区间，然后对每个时间区间统计 `Metric` 的数据。<br><br>关于 `Interval` 参数是如何用来拆分统计时间段，参考 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn)。<br><br>该参数有以下取值：<br><br><br>* `1min`：表示时间粒度是 1 分钟。<br><br>* `5min`：表示时间粒度是 5 分钟。<br><br><br>您可以指定的时间粒度受 `StartTime` 和 `EndTime` 所表示的时间范围的影响。<br><br><br>* 如果时间范围 <= 1 天，您可以指定的时间粒度有 `1min`、`5min`。<br><br>* 如果 1 天 < 时间范围 <= 31 天，您可以指定的时间粒度有 `5min`。<br><br><br>该参数的默认值是 `5min`。如果默认值不匹配时间范围，API 请求会失败。 |`5min` |
|Project |String |否 |表示一个项目。如果不指定 `Project`，表示所有项目。<br><br>对于 `Project` 和 `Domain`：<br><br><br>* 当您指定 `Project`，不指定 `Domain` 时，CDN 按 `Item` 统计指定项目的 `Metric` 数据。参见 [项目数据是如何统计的](https://docs.byteplus.com/en/docs/18/20607#%E9%A1%B9%E7%9B%AE%E6%95%B0%E6%8D%AE%E6%98%AF%E5%A6%82%E4%BD%95%E7%BB%9F%E8%AE%A1%E7%9A%84)。<br><br>* 其他情况下，CDN 按 `Item` 统计指定域名的 `Metric` 数据。<br><br><br>参见 [Item、Project、Domain 的配置组合](https://docs.byteplus.com/en/docs/18/20607#item%E3%80%81project%E3%80%81domain-%E7%9A%84%E9%85%8D%E7%BD%AE%E7%BB%84%E5%90%88)。 |`my_project` |
|Domain |String |否 |表示一个或多个域名，用于对用户请求进行过滤。您最多可以指定 50 个域名。多个域名之间使用逗号（,）分隔。如果不指定 `Domain`，表示所有域名。关于 `Domain` 参数的额外描述，参见 `Project` 参数。<br><br>说明<br><br>当子用户调用该 API 时，请留意以下说明：<br><br><br>* 子用户只能指定其有权限访问的域名。子用户可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) 获取其有权限访问的域名。<br><br>* 如果不指定该参数，表示所有该子用户有权限访问的那些域名。 |`www.example.com,www.test.com,img.example.com` |
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


<span id="item、project、domain-的配置组合"></span>
### Item、Project、Domain 的配置组合


|**分组条件** |**过滤条件** ||**说明** |
|---|---|---|---|
|**Item** |**Project** |**Domain** ||
|domain |指定 |指定 |对于指定的域名，统计每个**域名**的指标数据。 |
||指定 |不指定 |对于指定项目下的所有域名，统计每个**域名**的指标数据。 |
||不指定 |指定 |对于指定的域名，统计每个**域名**的指标数据。 |
||不指定 |不指定 |对于所有域名，统计每个**域名**的指标数据。 |
|project |指定 |指定 |*非法* |
||指定 |不指定 |对于指定的项目，统计每个**项目**的指标数据。 |
||不指定 |指定 |*非法* |
||不指定 |不指定 |对于所有项目，统计每个**项目**的指标数据。 |
|billingRegion |指定 |指定 |对于指定的域名，统计每个**域名**的指标数据。 |
||指定 |不指定 |对于指定的项目，统计每个**项目**的指标数据。 |
||不指定 |指定 |对于指定的域名，统计每个**域名**的指标数据。 |
||不指定 |不指定 |对于所有域名，统计每个**域名**的指标数据。 |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Item |String |表示请求参数 `Item` 所指定的分组条件。 |`domain` |
|TopDataDetails |Object[] |表示该 API 返回的结果数据。 | |
|Metric |String |表示请求参数 `Metric` 所指定的指标。 |`requests` |
|ValueDetails |Object[] |表示一组数据对象，包含由 `Item` 汇总的 `Metric` 数据的详情。这些数据对象按照 `Value` 从大到小排序。 | |
|ItemKey |String |表示属于 `Item` 的一个值。<br><br><br>* 当 `Item` 是 `domain` 时，`ItemKey` 是请求参数 `Domain` 所指定列表中的一个域名。<br><br>* 当 `Item` 是 `BillingRegion` 时，`ItemKey` 是请求参数 `BillingRegion` 所指定列表中的一个计费区域。 |`www.example.com` |
|Ratio |Double |表示该 `ItemKey` 的 `Value` 在所有 `ItemKey` 的 `Value` 总和中的占比。<br><br>需要留意的是，当 `Metric` 是 `bandwidth` 时，该参数无效，其值始终是 `0`。 |`0.978` |
|Timestamp |Long |表示 `Value` 的时间点，单位是 Unix 时间戳，精度是秒。该参数仅当 `Metric` 是 `bandwidth` 时才有效，表示带宽峰值的时间。如果 `Metric` 不是 `bandwidth`，该参数无效，其值始终是 `0`。 |`1710419700` |
|Value |Double |表示该 `ItemKey` 的汇总 `Metric` 数据。 |`456` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "out_traffic",
    "Item": "domain",
    "BillingRegion": "CHN,EU",
    "Project": "my_project",
    "Domain": "www.example.com,www.test.com,img.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202404230653511721F4B223CB40DB0A16",
        "Action": "DescribeEdgeRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "TopDataDetails": [
            {
                "Metric": "out_traffic",
                "ValueDetails": [
                    {
                        "ItemKey": "www.example.com",
                        "Ratio": 0.8358,
                        "Timestamp": 0,
                        "Value": 63217888212.6
                    },
                    {
                        "ItemKey": "www.test.com",
                        "Ratio": 0.1642,
                        "Timestamp": 0,
                        "Value": 12417784242.6
                    },
                    {
                        "ItemKey": "img.example.com",
                        "Ratio": 0,
                        "Timestamp": 0,
                        "Value": 1584509.3
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
