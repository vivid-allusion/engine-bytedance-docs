---
title: "DescribeBillingDetail"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeBillingDetail_cn"
---

<span id="使用说明"></span>
## 使用说明

基于 BytePlus CDN 收到的用户请求和向源站发送的请求，该 API 对一个计费指标统计一系列细分数据。

要调用该 API，您需要指定一个计费指标，一个统计时间段和一个时间粒度。您还可以指定多个过滤条件对用户请求进行过滤。

数据稳定性：受网络波动影响，边缘节点上统计的指标数据可能会发生变化。大多数情况下，指标数据会在 12 小时内逐步稳定下来。因此，该 API 返回的计费指标数据并非账单中显示的用量，仅供参考。实际用量请以账单为准。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">如果您刚开始使用 CDN 的统计 API，请务必先阅读以下文档，这将有助于您理解该 API 文档。</div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/docs_cn-pricing-cn">计费说明</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn">统计时间段说明</a></div>


   * <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/lHMepA">指标的定义以及统计方式</a></div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeBillingDetail&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeBillingDetail`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|StartTime |Long |是 |表示统计时间段的开始时间，格式是 Unix 时间戳，精度是秒。<br><br><br>* `StartTime` 与 `EndTime` 所表示的统计时间段不能超过 31 天。<br><br>* `StartTime` 距离调用该 API 的时间不能超过 1 年。 |`1717222134` |
|EndTime |Long |是 |表示统计时间段的结束时间，格式是 Unix 时间戳，精度是秒。 |`1717567734` |
|Interval |String |否 |表示一个时间粒度。该 API 基于 `Interval` 将 `StartTime` 和 `EndTime` 所表示的统计时间段拆分成一系列的时间区间，然后对每个时间区间统计 `Metric` 数据。<br><br>关于 `Interval`参数是如何用来拆分统计时间段，参考 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn)。<br><br>该参数有以下取值：<br><br><br>* `5min`：表示时间粒度是 5 分钟。<br><br>* `hour`：表示时间粒度是 1 小时。<br><br>* `day`：表示时间粒度是 1 天。<br><br><br>该参数的默认值是 `5min`。<br><br>说明<br><br>账单数据是基于 5 分钟粒度而统计的。因此，如果您在调用该 API 时指定 `Interval` 是 `5min`，您获取的是账单数据的细分。基于 `hour` 和 `day` 的细分数据是供您参考的。 |`hour` |
|Project |String |否 |表示一个项目。<br><br><br>* 如果您指定了 `Domain`，该 API 对所有您指定的域名统计 `Metric` 数据。<br><br>* 如果您指定了 `Project` ，但未指定 `Domain`，该 API 对您指定的项目统计 `Metric` 数据。参见 [项目数据是如何统计的](https://docs.byteplus.com/en/docs/18/31225#%E9%A1%B9%E7%9B%AE%E6%95%B0%E6%8D%AE%E6%98%AF%E5%A6%82%E4%BD%95%E7%BB%9F%E8%AE%A1%E7%9A%84)。<br><br>* 如果您既未指定 `Project` ，也未指定 `Domain`，该 API 对所有域名统计 `Metric` 数据。 |`default` |
|Domain |String |否 |表示一个或多个域名，用于对用户请求进行过滤。该 API 对您指定的每个域名统计 `Metric` 数据。您最多可以指定 50 个域名。多个域名之间使用逗号（,）分隔。如果不指定 `Domain`，表示不使用该参数对请求进行过滤。<br><br>如果您指定了 `Project`，您指定的域名必须是属于该 `Project` 的。<br><br>说明<br><br>当子用户调用该 API 时，请留意以下说明：<br><br><br>* 子用户只能指定其有权限访问的域名。子用户可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn) 获取其有权限访问的域名。<br><br>* 如果不指定该参数，表示所有该子用户有权限访问的那些域名。 |`www.example.com,img.example.com` |
|Metric |String |是 |表示一个指标。该参数有以下取值：<br><br><br>* `out_traffic`：表示 CDN 向用户传输的数据量，单位是 bytes。<br><br>* `bandwidth`：表示基于 CDN 向用户传输的数据量而计算的带宽，单位是 bps。<br><br>* `out_origin_traffic`：表示 CDN 向源站传输的数据量，单位是 bytes。<br><br>* `requests`：表示计费的请求数，包含 HTTP 请求数和 HTTPS 请求数。如果您启用了 QUIC，QUIC 请求数包含在 HTTPS 请求数中。<br><br><br>关于指标的统计方式，参见 [指标的定义以及统计方式](https://docs.byteplus.com/en/docs/byteplus-cdn/lHMepA)。 |`out_traffic` |
|BillingRegion |String |否 |表示一个计费区域，用于对用户请求进行过滤。该 API 对来自这些计费区域的用户请求统计 `Metric` 数据。该参数有以下取值：<br><br><br>* `CHN`：表示中国内地。<br><br>* `EU`：表示欧洲区。<br><br>* `NA`：表示北美区。<br><br>* `SA`：表示南美区。<br><br>* `MEA`：表示中东区和非洲区。<br><br>* `AP1`：表示亚太一区。<br><br>* `AP2`：表示亚太二区。<br><br>* `AP3`：表示亚太三区。<br><br>* `Oversea`：表示除中国内地以外的所有计费区域。<br><br><br>如果不指定 `BillingRegion`，表示不使用该参数对请求进行过滤。 |`AP1` |
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
|TimestampPoint |Object[] |表示基于 `Interval` 统计出的一组 `Metric` 数据对象。 | |
|TimeStamp |Long |表示 `Value` 所对应的时间区间的开始时间，格式是 Unix 时间戳，精度是秒。参见 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn). |`1717257600` |
|Value |Double |表示一个 `Metric` 细分数据。 |`1158128.4` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeBillingDetail&Version=2021-03-01
{
    "StartTime": 1724295929,
    "EndTime": 1724303129,
    "Interval": "hour",
    "Metric": "out_traffic",
    "BillingRegion": "AP1",
    "Domain": "www.example.com,img.example.com"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2024082912185802D3C01A023DB6542739",
        "Action": "DescribeBillingDetail",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TimestampPoint": [
            {
                "TimeStamp": 1724295600,
                "Value": 1158128.4
            },
            {
                "TimeStamp": 1724299200,
                "Value": 1174175.2000000002
            },
            {
                "TimeStamp": 1724302800,
                "Value": 1194607.7
            }
        ]
    }
}
```
