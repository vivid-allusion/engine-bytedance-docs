---
title: "DescribeOriginStatusCodeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginStatusCodeRanking"
---

<span id="api-说明"></span>
## API 说明

基于 CDN 从源站收到的响应状态码，该 API 按域名对一系列的指标数据进行汇总，并对这些汇总数据按从大到小排序。

要调用该 API，您需要指定一个状态码指标，一个统计时间段和一个时间粒度。您还可以指定多个过滤条件对回源请求进行过滤。您最多能查询过去 92 天的数据。

数据稳定性：受网络波动影响，回源节点上统计的指标数据可能会发生变化。大多数情况下，指标数据会在 12 小时内逐步稳定下来。

数据时效性：指标数据可能会有 5 分钟左右的延时。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您是刚开始使用数据统计的 API，请务必先阅读以下文档，这将有助于您理解该 API 文档。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn">统计时间段说明</a></div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeOriginStatusCodeRanking&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeOriginStatusCodeRanking`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Item |String |是 |表示一个分组条件。当前，该参数值只能是 `domain`，表示按 `Domain` 对 `Metric` 数据进行汇总。 |`domain` |
|Metric |String |是 |对于内容分发网络收到的源站响应，该参数表示以下某个类别的状态码数量：<br><br><br>* `status_2xx`：表示 2xx 状态码数量。<br><br>* `status_3xx`：表示 3xx 状态码数量。<br><br>* `status_4xx`：表示 4xx 状态码数量。<br><br>* `status_5xx`：表示 5xx 状态码数量。 |`status_4xx` |
|StartTime |Long |是 |表示统计时间段的开始时间，格式是 Unix 时间戳，精度是秒。`StartTime` 必须早于或者等于 `EndTime`。同时，`StartTime` 和 `EndTime` 所表示的统计时间段不能超过 31 天。 |`1710259200` |
|EndTime |Long |是 |表示统计时间段的结束时间，格式是 Unix 时间戳，精度是秒。 |`1710836303` |
|Interval |String |否 |表示一个时间粒度。该 API 基于 `Interval` 将 `StartTime` 和 `EndTime` 所表示的统计时间段拆分成一系列的时间区间，然后对每个时间区间统计 `Metric` 的数据。<br><br>关于 `Interval` 参数是如何用来拆分统计时间段，参考 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn)。<br><br>该参数有以下取值：<br><br><br>* `1min`：表示时间粒度是 1 分钟。<br><br>* `5min`：表示时间粒度是 5 分钟。<br><br><br>您可以指定的时间粒度受 `StartTime` 和 `EndTime` 所表示的时间范围的影响。<br><br><br>* 如果时间范围 <= 1 天，您可以指定的时间粒度有 `1min`、`5min`。<br><br>* 如果 1 天 < 时间范围 <= 31 天，您可以指定的时间粒度只能是 `5min`。<br><br><br>该参数的默认值是 `5min`。如果默认值不匹配时间范围，API 请求会失败。 |`1min` |
|Project |String |否 |表示一个项目。<br><br><br>* 如果您指定了 `Domain`，该 API 对所有您指定的域名统计 `Metric` 数据。<br><br>* 如果您指定了 `Project` ，但未指定 `Domain`，该 API 对您指定的项目统计 `Metric` 数据。参见 [项目数据是如何统计的](https://docs.byteplus.com/en/docs/18/20615#%E9%A1%B9%E7%9B%AE%E6%95%B0%E6%8D%AE%E6%98%AF%E5%A6%82%E4%BD%95%E7%BB%9F%E8%AE%A1%E7%9A%84)。<br><br>* 如果您既未指定 `Project` ，也未指定 `Domain`，该 API 对所有域名统计 `Metric` 数据。 |`my_project` |
|Domain |String |否 |表示一个或多个域名，用于对用户请求进行过滤。该 API 对您指定的每个域名统计 `Metric` 数据。您最多可以指定 50 个域名。多个域名之间使用逗号（,）分隔。如果不指定 `Domain`，表示不使用该参数对请求进行过滤。<br><br>如果您指定了 `Project`，您指定的域名必须是属于该 `Project` 的。<br><br>说明<br><br>当子用户调用该 API 时，请留意以下说明：<br><br><br>* 子用户只能指定其有权限访问的域名。子用户可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) 获取其有权限访问的域名。<br><br>* 如果不指定该参数，表示所有该子用户有权限访问的那些域名。 |`www.example.com,www.test.com,img.example.com` |
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
|Item |String |表示请求参数 `Item` 所指定的分组条件。 |`domain` |
|Metric |String |表示请求参数 `Metric` 所指定的指标。 |`status_4xx` |
|TopDataDetails |Object[] |表示一组数据对象，包含由 `Item` 汇总的 `Metric` 数据的详情。每个数据对象包含每个类别下状态码的数量和占比。这些数据对象按指定的 `Metric` 从大到小排序。 | |
|ItemKey |String |表示 `Domain` 列表中的一个域名。 |`www.example.com` |
|Status2xx |Double |表示对于该 `ItemKey`，2xx 状态码的数量。 |`45678` |
|Status2xxRatio |Double |表示对于该 `ItemKey`，2xx 状态码的数量占比。 |`0.47` |
|Status3xx |Double |表示对于该 `ItemKey`，3xx 状态码的数量。 |`0` |
|Status3xxRatio |Double |表示对于该 `ItemKey`，3xx 状态码的数量占比。 |`0` |
|Status4xx |Double |表示对于该 `ItemKey`，4xx 状态码的数量。 |`3` |
|Status4xxRatio |Double |表示对于该 `ItemKey`，4xx 状态码的数量占比。 |`0.0001` |
|Status5xx |Double |表示对于该 `ItemKey`，5xx 状态码的数量。 |`0` |
|Status5xxRatio |Double |表示对于该 `ItemKey`，5xx 状态码的数量占比。 |`0` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeOriginStatusCodeRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Metric": "status_2xx",
    "Item": "domain",
    "Project": "my_project",
    "Domain": "www.example.com,www.test.com,img.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403200014241036C312826267DE2108",
        "Action": "DescribeOriginStatusCodeRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "Metric": "status_2xx",
        "TopDataDetails": [
            {
                "ItemKey": "www.example.com",
                "Status2xx": 2933327,
                "Status2xxRatio": 0.814,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 0,
                "Status4xxRatio": 0,
                "Status5xx": 0,
                "Status5xxRatio": 0
            },
            {
                "ItemKey": "www.test.com",
                "Status2xx": 635508,
                "Status2xxRatio": 0.1764,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 80665,
                "Status4xxRatio": 0.3138,
                "Status5xx": 185105,
                "Status5xxRatio": 1
            },
            {
                "ItemKey": "img.example.com",
                "Status2xx": 8153,
                "Status2xxRatio": 0.0023,
                "Status3xx": 0,
                "Status3xxRatio": 0,
                "Status4xx": 0,
                "Status4xxRatio": 0,
                "Status5xx": 0,
                "Status5xxRatio": 0
            }
        ]
    }
}
```


&nbsp;
