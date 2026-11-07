---
title: "DescribeCdnAccessLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnAccessLog"
---

获取指定域名的访问日志。该 API 返回的是这些访问日志的下载 URL。BytePLus CDN 按小时在整点对访日日志进行打包。

数据保留期限：在调用该 API 时，建议您指定时间段的时间跨度不超过 30 天，不然可能由于日志数量庞大导致 API 调用超时。

日志延时：CDN 默认按小时粒度，在整点对过去一小时内采集到的日志进行打包，生成日志包。日志包大约在生成后的 3 小时可以被下载。由于网络延时等原因，CDN 采集到的日志可能会有最长 24 小时的延迟。对于采集到的延迟日志，CDN 会将其追加到相应的日志包中。因此，日志包在生成后的 24 小时内可能会有日志的追加。

<span id="使用限制"></span>
## 使用限制

节流限制：您每秒最多可以提交 20 个 API 请求。

<span id="请求说明"></span>
## 请求说明


* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021\-03\-01


<span id="请求参数"></span>
## 请求参数

<span id="query"></span>
### Query


|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCdnAccessLog`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |


<span id="body"></span>
### Body


|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个域名。该 API 获取的是该域名的访问日志。 |`www.example.com` |
|ServiceRegion |String |否 |表示一个服务区域，用于对访问日志进行过滤。该参数有以下取值：<br><br><br>* `chinese_mainland`：表示 **中国内地**。<br><br>* `global`：表示 **全球**。<br><br>* `outside_chinese_mainland`：表示 **全球（不包含中国内地）** 。<br><br><br>该参数的默认值是 `global`。 |`global` |
|StartTime |Long |是 |表示日志统计时间段的开始时间，时间格式是 Unix 时间戳。需要留意的是，`StartTime` 并非日志统计时间段的实际开始时间。<br><br>实际开始时间为 `StartTime` 在小时粒度的向后取整。<br><br>例子：<br><br><br>* 您指定的 `StartTime` 所表示的时间是 15:07。则实际开始时间是 16:00。<br><br>* 您指定的 `StartTime` 所表示的时间是 15:00。则实际开始时间是 15:00。 |`1641844915` |
|EndTime |Long |是 |表示日志统计时间段的结束时间，时间格式是 Unix 时间戳。需要留意的是，`EndTime` 并非日志统计时间段的实际结束时间。<br><br>实际结束时间为 `EndTime` 在小时粒度的向后取整。 |`1641953589` |
|PageNum |Long |否 |表示一个页码。该 API 返回的是该页码所指定的分页上的那些日志包。<br><br>该 API 返回的日志包是根据 `PageSize` 而分页的。假设该 API 返回的日志包数量是 100，您指定的 `PageSize` 是 `10`，那么返回的日志包是分布在 10 个页上。如果您指定的 `PageNum` 是 `2`，表示获取第 2 页上的那些日志包。<br><br>如果您指定的分页上没有日志包，则返回结果中 `DomainLogDetails` 参数的值为 `null`。<br><br>`PageNum` 的默认值是 `1`。 |`1` |
|PageSize |Long |否 |表示每个分页包含的日志包数量。<br><br>该参数的取值范围是 1\-100，默认值是 `10`。 |`10` |


<span id="返回参数"></span>
## 返回参数


|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Domain |String |表示请求参数中的 `Domain`。 |`www.a.com` |
|PageSize |Long |表示请求参数中的 `PageSize`。 |`100` |
|PageNum |Long |表示请求参数中的 `PageNum`。 |`1` |
|TotalCount |Long |表示符合过滤条件的日志包数量。 |`100` |
|DomainLogDetails |Object[] |表示该 API 返回的日志包列表。 | |
|LogName |String |表示列表中一个日志包的名称。名称的命名规范是 <*Domain*\>_<*Start_Time*\>_<*End_Time*\>.gz。<br><br>说明<br><br>在日志包名称中，`Start_Time` 和 `End_Time` 的时区是 UTC+08:00。 |`www.example.com_20210707100000_20210707110000.gz` |
|StartTime |Long |表示该日志包所对应的日志统计时间段的实际开始时间，格式是 Unix 时间戳。<br><br>`StartTime` 与 `EndTime` 之间的时间间隔是 1 小时。 |`1642392000` |
|EndTime |Long |表示该日志包所对应的日志统计时间段的实际结束时间，格式是 Unix 时间戳。 |`1642395600` |
|LogPath |String |表示日志包的下载 URL。下载 URL 的有效期为 24 小时。 |`URL1` |
|LogSize |Long |表示日志包的大小，单位为 `bytes`。<br><br>说明<br><br>由于日志包在生成后的 24 小时内可能会有延迟日志的追加，每次调用该 API 获取的日志包大小可能会有变化。请以最新获取的日志包大小为准。 |`9107` |


<span id="示例"></span>
## 示例

<span id="请求示例"></span>
### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021-03-01
{
    "PageSize": 10,
    "PageNum": 1,
    "Domain": "www.example.com",
    "StartTime": 1717236489,
    "EndTime": 1717409289,
    "ServiceRegion": "global"
}
```


<span id="返回示例"></span>
### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "202406031008365F2C63BC765D774E4A8C",
        "Action": "DescribeCdnAccessLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "singapore"
    },
    "Result": {
        "Domain": "perfops2.byte-test.com",
        "DomainLogDetails": [
            {
                "EndTime": 1717401600,
                "LogName": "www.example.com_20240603150000_20240603160000_outsideChineseMainland.gz",
                "LogPath": "URL1",
                "LogSize": 4009503,
                "StartTime": 1717398000
            },
            {
                "EndTime": 1717398000,
                "LogName": "www.example.com_20240603140000_20240603150000.gz",
                "LogPath": "URL2",
                "LogSize": 849,
                "StartTime": 1717394400
            },
            {
                "EndTime": 1717398000,
                "LogName": "www.example.com_20240603140000_20240603150000_outsideChineseMainland.gz",
                "LogPath": "URL3",
                "LogSize": 3616460,
                "StartTime": 1717394400
            },
            {
                "EndTime": 1717394400,
                "LogName": "www.example.com_20240603130000_20240603140000.gz",
                "LogPath": "URL4",
                "LogSize": 1163,
                "StartTime": 1717390800
            },
            {
                "EndTime": 1717394400,
                "LogName": "www.example.com_20240603130000_20240603140000_outsideChineseMainland.gz",
                "LogPath": "URL5",
                "LogSize": 2958868,
                "StartTime": 1717390800
            },
            {
                "EndTime": 1717390800,
                "LogName": "www.example.com_20240603120000_20240603130000.gz",
                "LogPath": "URL6",
                "LogSize": 269,
                "StartTime": 1717387200
            },
            {
                "EndTime": 1717390800,
                "LogName": "www.example.com_20240603120000_20240603130000_outsideChineseMainland.gz",
                "LogPath": "URL7",
                "LogSize": 2630368,
                "StartTime": 1717387200
            },
            {
                "EndTime": 1717387200,
                "LogName": "www.example.com_20240603110000_20240603120000_outsideChineseMainland.gz",
                "LogPath": "URL8",
                "LogSize": 2584924,
                "StartTime": 1717383600
            },
            {
                "EndTime": 1717383600,
                "LogName": "www.example.com_20240603100000_20240603110000_outsideChineseMainland.gz",
                "LogPath": "URL9",
                "LogSize": 3587479,
                "StartTime": 1717380000
            },
            {
                "EndTime": 1717380000,
                "LogName": "www.example.com_20240603090000_20240603100000.gz",
                "LogPath": "URL10",
                "LogSize": 592,
                "StartTime": 1717376400
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "TotalCount": 50
    }
}
```


&nbsp;
