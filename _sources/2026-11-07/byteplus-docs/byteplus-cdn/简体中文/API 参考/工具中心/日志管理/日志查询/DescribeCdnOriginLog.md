---
title: "DescribeCdnOriginLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/describecdnoriginlog-zh-cn"
---

获取指定域名的回源日志。该 API 返回的是这些回源日志的下载 URL。BytePlus CDN 按小时在整点对回源日志进行打包。

要使用该 API，请 [提交工单](https://console.byteplus.com/workorder/create)。

您可以下载过去 62 天内的回源日志。在调用该 API 时，建议您指定时间段的时间跨度不超过 30 天，不然可能由于日志数量庞大导致 API 调用超时。

## 使用说明

## 日志字段说明

**日志示例**

`2026-10-19 15:23:45    xxx.x.xxx.xx    xx.xxx.xx.xxx    video.example.com    /video/tos/cn/tos-cn-ve-15c001/sample.mp4    Expires=1792404225&OSSAccessKeyId=LTAIxxxx&Signature=abc123%3D&a=2329&br=1200&bt=1200    200    10485760    86    10485760    Mon, 19 Oct 2026 07:20:11 GMT    0b5f3a9c7d8e4f1a9c2b6d3e5f789012    origin-storage.example.com`

**字段说明**

|字段编号 |字段名称 |字段含义 |示例值 |
|---|---|---|---|
|1 |ds_req_ts_standard |CDN 节点向源站发起回源请求的时间，格式为 `yyyy-MM-dd HH:mm:ss`，时区为 UTC+8。 |`2026-10-19 15:23:45` |
|2 |client_ip |发起请求的客户端 IP 地址。 |`xxx.x.xxx.xx` |
|3 |bind_addr_ip |CDN 节点回源时使用的内网 IP 地址。该地址不是源站看到的对端 IP。 |`xx.xxx.xx.xxx` |
|4 |server_name |客户端请求的加速域名。加速域名为泛域名时，记录客户端实际请求的子域名。 |`video.example.com` |
|5 |ds_http_uri |回源请求 URL 的路径，不含查询字符串。 |`/video/sample.mp4` |
|6 |ds_http_query |回源请求 URL 的查询字符串，按原样记录，不含 `?`。 |`Expires=1792404225&OSSAccessKeyId=LTAIxxxx&Signature=abc123%3D&a=2329&br=1200&bt=1200` |
|7 |status_code |源站返回的 HTTP 状态码。 |`200` |
|8 |recv_bytes |CDN 节点在本次回源中从源站接收的响应体字节数，不含响应头。 |`10485760` |
|9 |total_cost_ms |从 CDN 节点向源站发送请求到接收完源站响应最后一个字节的时长，单位为毫秒。 |`860` |
|10 |content_length |源站响应头 `Content-Length` 的值，单位为字节。 |`10485760` |
|11 |last_modified |源站响应头 `Last-Modified` 的值，按原样记录。 |`Mon, 19 Oct 2026 07:20:11 GMT` |
|12 |trace_id |本次回源请求的追踪 ID，用于排查问题时定位请求。 |`0b5f3a9c7d8e4f1a9c2b6d3e5f789012` |
|13 |src_name |本次回源实际请求的源站（主源站或备源站），取值为源站配置中的域名或 IP 地址。 |`origin-storage.example.com` |

## 使用限制

**节流限制**：您每秒最多可以发送 20 个 API 请求。

**日志延时**：CDN 默认按小时粒度，在整点对过去一小时内采集到的日志进行打包，生成日志包。日志包大约在生成后的 3 小时可以被下载。由于网络延时等原因，CDN 采集到的日志可能会有最长 24 小时的延迟。对于采集到的延迟日志，CDN 会将其追加到相应的日志包中。因此，日志包在生成后的 24 小时内可能会有日志的追加。

## 请求说明

* Request Method：POST

* Request URL：https://cdn.byteplusapi.com/?Action=DescribeCdnOriginLog&Version=2021\-03\-01

## 请求参数

### Query

|参数 |类型 |是否必选 |描述 |
|---|---|---|---|
|Action |String |是 |接口名称。当前 API 的名称为 `DescribeCdnOriginLog`。 |
|Version |String |是 |接口版本。当前 API 的版本为 `2021-03-01`。 |

### Body

|参数 |类型 |是否必选 |描述 |示例值 |
|---|---|---|---|---|
|Domain |String |是 |表示一个域名。该 API 获取的是该域名的回源请求日志。 |`www.example.com` |
|StartTime |Long |是 |表示日志统计时间段的开始时间，时间格式是 Unix 时间戳。`StartTime` 离当前日期不能超过 62 天。<br><br>需要留意的是，`StartTime` 并非日志统计时间段的实际开始时间。实际开始时间为 `StartTime` 在小时粒度的向后取整。<br><br>例子：<br><br><br>* 您指定的 `StartTime` 所表示的时间是 15:07。则实际开始时间是 16:00。<br><br>* 您指定的 `StartTime` 所表示的时间是 15:00。则实际开始时间是 15:00。 |`1785227326` |
|EndTime |Long |是 |表示日志统计时间段的结束时间，时间格式是 Unix 时间戳。需要留意的是，`EndTime` 并非日志统计时间段的实际结束时间。<br><br>实际结束时间为 `EndTime` 在小时粒度的向后取整。 |`1790152126` |
|PageNum |Long |否 |表示一个页码。该 API 返回的是该页码所指定的分页上的那些日志包。<br><br>该 API 返回的日志包是根据 `PageSize` 而分页的。假设该 API 返回的日志包数量是 100，您指定的 `PageSize` 是 `10`，那么返回的日志包是分布在 10 个页上。如果您指定的 `PageNum` 是 `2`，表示获取第 2 页上的那些日志包。<br><br>如果您指定的分页上没有日志包，则返回结果中 `DomainLogDetails` 参数的值为 `null`。<br><br>`PageNum` 的默认值是 `1`。 |`1` |
|PageSize |Long |否 |表示每个分页包含的日志包数量。<br><br>该参数的取值范围是 1\-100，默认值是 `10`。 |`10` |
|ServiceRegion |String |否 |表示发起回源请求的 CDN 节点所在的服务区域，用于对回源日志进行过滤。该参数有以下取值：<br><br><br>* `chinese_mainland`：表示 **中国内地**。<br><br>* `outside_chinese_mainland`：表示 **全球（不包含中国内地）** 。<br><br><br>该参数的默认值是 `chinese_mainland`。 |`chinese_mainland` |

## 返回参数

|参数 |类型 |描述 |示例值 |
|---|---|---|---|
|Domain |String |表示请求参数中的 `Domain`。 |`www.example.com` |
|DomainLogDetails |Object[] |表示该 API 返回的日志包列表。 | |
|EndTime |Long |表示该日志包所对应的日志统计时间段的实际结束时间，格式是 Unix 时间戳。 |`1642395600` |
|LogName |String |表示列表中一个日志包的名称。名称的命名规范是 `<Domain>*origin*<StartTime>_<EndTime>.gz`。 |`www.example.com_origin_20210707100000_20210707110000.gz` |
|LogPath |String |表示日志包的下载 URL。下载 URL 的有效期为 24 小时。 |`URL1` |
|LogSize |Long |表示日志包的大小，单位为 `bytes`。<br><br>说明<br><br>由于日志包在生成后的 24 小时内可能会有延迟日志的追加，每次调用该 API 获取的日志包大小可能会有变化。请以最新获取的日志包大小为准。 |`9107` |
|StartTime |Long |表示该日志包所对应的日志统计时间段的实际开始时间，格式是 Unix 时间戳。<br><br>`StartTime` 与 `EndTime` 之间的时间间隔是 1 小时。 |`1642392000` |
|PageNum |Long |表示请求参数中的 `PageNum`。 |`1` |
|PageSize |Long |表示请求参数中的 `PageSize`。 |`10` |
|TotalCount |Long |表示符合过滤条件的日志包数量。 |`1` |

## 示例

### 请求示例

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnOriginLog&Version=2021-03-01
{
    "Domain": "www.example.com",
    "StartTime": 1793145600,
    "EndTime": 1793318400
}
```

### 返回示例

```json
{
    "ResponseMetadata": {
        "RequestId": "2026103006472918B1F87E1A574154FA14",
        "Action": "DescribeCdnOriginLog",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Domain": "www.example.com",
        "DomainLogDetails": [
            {
                "EndTime": 1793257200,
                "LogName": "www.example.com_origin_20261029140000_20261029150000.gz",
                "LogPath": "https://bdcdn-data-log.bytetos.com/cdn-openapi/bslog/file-download/v3?fileName=www.example.com_origin_20261029140000_20261029150000.gz&accountId=3000xxxxxx&domain=www.example.com&token=79fedxxxxx",
                "LogSize": 1016,
                "StartTime": 1793253600
            }
        ],
        "PageNum": 1,
        "PageSize": 10,
        "TotalCount": 1
    }
}
```
