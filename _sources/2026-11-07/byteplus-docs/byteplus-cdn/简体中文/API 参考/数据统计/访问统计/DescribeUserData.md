---
title: "DescribeUserData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeUserData"
---

<span id="api-说明"></span>
## API 说明

基于 CDN 收到的用户请求，该 API 统计各时间点的独立客户端 IP 地址数量。

要调用该 API，您需要指定一个域名、一个统计时间段和一个时间粒度。您还可以指定多个过滤条件对用户请求进行过滤。您最多能查询过去 92 天的数据。

数据稳定性：受网络波动影响，边缘节点上统计的指标数据可能会发生变化。大多数情况下，指标数据会在 12 小时内逐步稳定下来。

数据时效性：独立访客数量是基于按小时粒度统计的指标数据。因此，数据统计可能会有 2 小时左右的延时。例如，对于 09:00 至 10:00 这个时间段的独立访客数量，您可以在 11:00 左右获取到准确的结果。

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">如果您是刚开始使用数据统计的 API，请务必先阅读以下文档，这将有助于您理解该 API 文档。</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn">统计时间段说明</a></div>



<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeUserData`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|StartTime |Long |是 |表示统计时间段的开始时间，格式是 Unix 时间戳，精度是秒。`StartTime` 必须早于或者等于 `EndTime`。同时，`StartTime` 与 `EndTime` 所表示的统计时间段不能超过 31 天。 |`1710259200` |
|EndTime |Long |是 |表示统计时间段的结束时间，格式是 Unix 时间戳，精度是秒。 |`1710836303` |
|Interval |String |是 |表示一个时间粒度。该 API 基于 `Interval` 将 `StartTime` 和 `EndTime` 所表示的统计时间段拆分成一系列的时间区间，然后对每个时间区间统计独立客户端 IP 地址数量。<br><br>关于 `Interva`参数是如何用来拆分统计时间段，参考 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn)。<br><br>该参数有以下取值：<br><br><br>* `hour`：表示时间粒度是 1 小时。<br><br>* `day`：表示时间粒度是 1 天。 |`hour` |
|Domain |String |是 |表示一个域名，用于对用户请求进行过滤。<br><br>说明<br><br>当子账号调用该 API 时，请留意以下说明：<br><br><br>* 子账号可以指定的域名是该子账号有权限访问的那些域名。子账号可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn) 获取其有权限访问的域名。 |`www.example.com` |
|IpVersion |String |否 |表示请求使用的一个网络层协议，用于对用户请求进行过滤。该参数的可用值如下：<br><br><br>* `IPv4`：表示 IPv4 协议。<br><br>* `IPv6`：表示 IPv6 协议。<br><br><br>如果不指定 `IpVersion`，表示不使用该参数对请求进行过滤。 |`IPv4` |
|Location |String |否 |表示一个国家或地区的代码，用于对用户请求进行过滤。CDN 对来自这些国家和地区的用户请求统计客户端 IP 地址的数量。<br><br><br>* 如果您指定了 `Location`，就不能指定 `Province`，反之亦然。<br><br>* 如果您不指定 `Location`，表示不使用该参数对请求进行过滤。<br><br><br>您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取代码与国家和地区的对应表。 |`AZE` |
|Province |String |否 |表示一个中国省级行政区的代码，用于对用户请求进行过滤。CDN 对来自这些省级行政区的用户请求统计客户端 IP 地址的数量。<br><br>如果您不指定 `Province`，表示不使用该参数对请求进行过滤。<br><br>您可以调用 [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp) 获取代码与中国省级行政区的对应表。 |`AH` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|MetricDataList |Object[] |表示一组数据对象，包含每个时间点的独立客户端 IP 地址数量。 | |
|TimeStamp |Long |表示一个时间点，格式时 Unix 时间戳，精度是秒。参见 [统计时间段说明](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_zh-cn)。 |`1710950400` |
|Value |Double |表示该 `TimeStamp` 时间点的独立客户端 IP 地址数量。该数据的时区是 UTC+08:00。 |`42` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021-03-01
{
    "Domain": "www.example.com",
    "StartTime": 1710950400,
    "EndTime": 1710998170,
    "Interval": "hour",
    "IpVersion": "IPv4",
    "Province": "AH"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202403220141458C564C77FA147001D2E1",
        "Action": "DescribeUserData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "TimeStamp": 1710950400,
                "Value": 421
            },
            {
                "TimeStamp": 1710954000,
                "Value": 428
            },
            {
                "TimeStamp": 1710957600,
                "Value": 439
            },
            {
                "TimeStamp": 1710961200,
                "Value": 436
            },
            {
                "TimeStamp": 1710964800,
                "Value": 435
            },
            {
                "TimeStamp": 1710968400,
                "Value": 446
            },
            {
                "TimeStamp": 1710972000,
                "Value": 433
            },
            {
                "TimeStamp": 1710975600,
                "Value": 430
            },
            {
                "TimeStamp": 1710979200,
                "Value": 428
            },
            {
                "TimeStamp": 1710982800,
                "Value": 412
            },
            {
                "TimeStamp": 1710986400,
                "Value": 423
            },
            {
                "TimeStamp": 1710990000,
                "Value": 417
            },
            {
                "TimeStamp": 1710993600,
                "Value": 394
            },
            {
                "TimeStamp": 1710997200,
                "Value": 407
            }
        ]
    }
}
```


&nbsp;
