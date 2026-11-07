---
title: "DescribeStatisticalRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeStatisticalRanking"
---

<span id="api-说明"></span>
## API 说明

基于 CDN 收到的用户请求，该 API 按热门对象类型对一系列的指标数据进行汇总，并对这些汇总数据按从大到小排序，最后返回这些热门对象。热门对象类型包括请求客户端所在的国家和地区、请求 URL、Referer 域名、UA 字符串中的对象、独立客户端 IP 地址的数量。

在调用该 API 时，您需要指定一个指标，一个热门对象类型，一个统计时间段和一个时间粒度。您还可以指定多个过滤条件对用户请求进行过滤。您最多能查询过去 92 天的数据。

数据稳定性：受网络波动影响，边缘节点上统计的指标数据可能会发生变化。大多数情况下，指标数据会在 12 小时内逐步稳定下来。

数据时效性：热门对象是基于按小时粒度统计的指标数据。因此，数据统计可能会有 2 小时左右的延时。例如，对于 09:00 至 10:00 这个时间段的热门对象，您可以在 11:00 左右获取到准确的结果。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeStatisticalRanking`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Item |String |是 |表示一个热门对象的类型作为分组和排序条件。 该 API 按 `Item` 对 `Metric` 数据进行汇总并对这些汇总数据进行排序。该参数有以下取值：<br><br><br>* `region`：表示请求客户端所在的国家或地区。<br><br>* `url`：表示请求 URL 中的路径。<br><br>* `referer`：表示请求中的 `Referer` 域名。<br><br>* `ua`：表示请求中的 `User-Agent` 字符串。<br><br>* `clientip`：表示客户端的 IP 地址。<br><br><br>说明<br><br><br>* 当 `Item` 是 `ua` 时，您还需要指定 `UaType` 作为一个补充分组条件。<br><br>* 当 `Item` 是 `region` 时，您还需要指定 `Area` 作为一个补充分组条件。 |`region` |
|Metric |String |是 |表示一个指标。该参数的可用值受 `Item` 的影响。<br><br><br>* 当 `Item` 是 `referer`、`ua` 或 `clientip` 时，该参数有以下取值：<br><br>   * `in_traffic`：表示用户向 CDN 传输的数据量，单位是 bytes。<br><br>   * `out_traffic`：表示 CDN 向用户传输的数据量，单位是 bytes。<br><br>   * `requests`：表示 CDN 收到的用户请求的数量。<br><br>   * `dynamic_requests`：表示 CDN 收到的满足以下所有条件的用户请求数量。<br><br>      * 请求方法既不是 GET，也不是 HEAD。<br><br>      * CDN 的响应状态码不是 405。<br><br>   * `static_requests`：表示 CDN 收到的满足以下所有条件的用户请求数量。<br><br>      * 请求方法是 GET 或者 HEAD。<br><br>      * CDN 的响应状态码不是 405。<br><br>* 当 `Item` 是 `url` 时，该参数有以下取值：<br><br>   * `in_traffic`<br><br>   * `out_traffic`<br><br>   * `requests`<br><br>   * `dynamic_requests`<br><br>   * `static_requests`<br><br>   * `status_2xx`：在 CDN 对用户请求的响应中，该参数表示 2xx 状态码的数量。<br><br>   * `status_3xx`：表示 3xx 状态码的数量。<br><br>   * `status_4xx`：表示 4xx 状态码的数量。<br><br>   * `status_5xx`：表示 5xx 状态码的数量。<br><br>* 当 `Item` 是 `region` 时，该参数有以下取值。<br><br>   * `clientip`：表示独立客户端 IP 地址的数量。该取值是默认值。<br><br>   * `in_traffic`<br><br>   * `out_traffic`<br><br>   * `requests`<br><br>   * `status_2xx`<br><br>   * `status_3xx`<br><br>   * `status_4xx`<br><br>   * `status_5xx` |`traffic` |
|StartTime |Long |是 |表示统计时间段的开始时间，格式是 Unix 时间戳，精度是秒。`StartTime` 必须早于或者等于 `EndTime`。同时，`StartTime` 和 `EndTime` 所表示的统计时间段不能超过 31 天。<br><br>说明<br><br><br>* `StartTime` 和 `EndTime` 指定了统计时间段。但是实际统计时间段的开始时间和结束时间都是小时级别的。<br><br>   例子：`StarTime` 表示的时间是 15:07，`EndTime` 表示的时间是 15:21，那么实际的统计时间段是 [15:00,16:00）。<br><br>   需要留意的是，如果 `EndTime` 正好是整点，则实际的统计时间段还要再往后延长 1 小时。假设 `StartTime` 表示的时间是 15:07，`EndTime` 表示的时间是 16:00，那么实际的统计时间段是 [15:00,17:00)。 |`1710950400` |
|EndTime |Long |是 |表示统计时间段的结束时间，格式是 Unix 时间戳，精度是秒。 |`1710998170` |
|Domain |String |是 |表示一个域名，用于对用户请求进行过滤。<br><br>说明<br><br>当子用户调用该 API 时，请留意以下说明：<br><br><br>* 子用户只能指定一个其有权限访问的域名。子用户可以调用 [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference_cn-describetemplatedomains-7f84f-cn) 获取其有权限访问的域名。 |`www.example.com` |
|UaType |String |否 |表示 User\-Agent 字符串中的一个对象类型。当 `Item` 是 `ua` 时，该参数必须指定，作为一个补充分组条件。当 `Item` 不是 `ua` 时，该参数无效。<br><br>该参数有以下取值：<br><br><br>* `browser`：表示 `User-Agent` 字符串中的浏览器类型。<br><br>* `system`：表示 `User-Agent` 字符串中的操作系统类型。<br><br>* `equipment`：表示 `User-Agent` 字符串中客户端设备的类型。 |`system` |
|Area |String |否 |表示一个地域类型。该参数仅当 `Item` 是 `region` 时有效，作为一个补充分组条件，用于获取客户端 IP 地址数量的地区分布。该参数有以下取值：<br><br><br>* `Global`：表示全球国家和地区。<br><br>* `China`：表示中国省级行政区。<br><br><br>说明<br><br><br>* 如果您不指定 `Metric`，`Area` 可以不被指定。<br><br>   * 如果不指定 `Area`，该 API 将返回按国家、地区、中国省级行政区域分布的独立客户端 IP 地址数量。<br><br>* 如果您指定了 `Metric`，`Area` 必须指定。 |`Global` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Item |String |表示请求参数 `Item` 所指定的热门对象类型。 |`region` |
|Metric |String |表示请求参数 `Metric` 所指定的指标。 |`traffic` |
|RankingDataList |Object[] |表示一组热门对象详情的列表。 | |
|ItemKey |String |表示一个热门对象。<br><br><br>* 当 `Item` 是 `url` 时，该热门对象是一个请求 URL 中的路径。<br><br>* 当 `Item` 是 `referer` 时，该热门对象是一个 `Referer` 域名。<br><br>* 当 `Item` 是 `region` 时，该热门对象是一个国家，地区，或者中国省级行政区的代码。<br><br>* 当 `Item` 是 `clientip` 时，该热门对象是客户端的 IP 地址。<br><br>* 当 `Item` 是 `ua` 时，<br><br>   * 如果 `UaType` 是 `equipment`，该热门对象是某种设备类型。<br><br>   * 如果 `UaType` 是 `system`，该热门对象是某种操作系统。<br><br>   * 如果 `UaType` 是 `browser`，该热门对象是某种浏览器。 |`GS` |
|ItemKeyCN |String |* 当 `Item` 是 `region` 和 `clientip` 时，`ItemKeyCN` 是 `ItemKey` 所对应地区的中文名称。<br><br>* 当 `Item` 是 `url` 时，`ItemKeyCN` 是 `ItemKey` 所对应的路径。<br><br>* 当 `Item` 是 `ua`、`referer`、`url` 或 `referer` 时，`ItemKeyCN` 与 `ItemKey` 相同。 |`甘肃` |
|Value |Double |表示该 `ItemKey` 的汇总 `Metric` 数据。`Value` 的时区是 UTC+08:00。 |`777` |
|UaType |String |表示请求参数中 `UaType` 所指定的对象类型。如果请求参数中不包含 `UaType`，该参数不会在返回结果中出现。 |`system` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021-03-01
{
    "Area": "Global",
    "Domain": "www.example.com",
    "StartTime": 1720614677,
    "EndTime": 1721478677,
    "Item": "region",
    "Metric": "clientip"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202407221231341976A83AF08B9822FD8F",
        "Action": "DescribeStatisticalRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "region",
        "Metric": "clientip",
        "RankingDataList": [
            {
                "ItemKey": "USA",
                "ItemKeyCN": "美国",
                "Value": 2857990
            },
            {
                "ItemKey": "IND",
                "ItemKeyCN": "印度",
                "Value": 744081
            },
            {
                "ItemKey": "BRA",
                "ItemKeyCN": "巴西",
                "Value": 695588
            },
            {
                "ItemKey": "FRA",
                "ItemKeyCN": "法国",
                "Value": 454253
            },
            ...
        ]
    }
}
```
