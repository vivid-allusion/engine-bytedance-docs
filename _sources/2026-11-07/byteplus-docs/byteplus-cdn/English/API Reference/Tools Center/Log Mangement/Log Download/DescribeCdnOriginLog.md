---
title: "DescribeCdnOriginLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/describecdnoriginlog-en-us"
---

Retrieves the download URLs of origin logs for a domain. BytePlus CDN packages origin logs into hourly log files at the top of each hour.

This API is available on request. To request access, [submit a ticket](https://console.byteplus.com/workorder/create).

You can download origin logs from the past 62 days. To avoid timeouts caused by large log volumes, we recommend that the time range in each request not exceed 30 days.

## Instructions

## Log fields

**Sample log entry**

`2026-10-19 15:23:45    xxx.x.xxx.xx    xx.xxx.xx.xxx    video.example.com    /video/tos/cn/tos-cn-ve-15c001/sample.mp4    Expires=1792404225&OSSAccessKeyId=LTAIxxxx&Signature=abc123%3D&a=2329&br=1200&bt=1200    200    10485760    86    10485760    Mon, 19 Oct 2026 07:20:11 GMT    0b5f3a9c7d8e4f1a9c2b6d3e5f789012    origin-storage.example.com`

**Fields**

Each log entry is a single line of tab\-separated fields, in the order listed below.

|No. |Field |Description |Example |
|---|---|---|---|
|1 |ds_req_ts_standard |Time at which the CDN server sent the origin request, in `yyyy-MM-dd HH:mm:ss` format (UTC+8). |`2026-10-19 15:23:45` |
|2 |client_ip |IP address of the client that sent the request. |`xxx.x.xxx.xx` |
|3 |bind_addr_ip |Internal IP address that the CDN server used for the origin request. This is not the source IP address that the origin sees. |`xx.xxx.xx.xxx` |
|4 |server_name |Domain that the client requested. For a wildcard domain, this field records the actual subdomain that the client requested. |`video.example.com` |
|5 |ds_http_uri |Path of the origin request URL, excluding the query string. |`/video/sample.mp4` |
|6 |ds_http_query |Query string of the origin request URL, recorded as is, without the leading `?`. |`Expires=1792404225&OSSAccessKeyId=LTAIxxxx&Signature=abc123%3D&a=2329&br=1200&bt=1200` |
|7 |status_code |HTTP status code returned by the origin. |`200` |
|8 |recv_bytes |Size of the response body, in bytes, that the CDN server received from the origin for this request. Response headers are not included. |`10485760` |
|9 |total_cost_ms |Time, in milliseconds, from when the CDN server sent the request to the origin to when the CDN server received the last byte of the origin response. |`860` |
|10 |content_length |Value of the `Content-Length` header in the origin response, in bytes. |`10485760` |
|11 |last_modified |Value of the `Last-Modified` header in the origin response, recorded as is. |`Mon, 19 Oct 2026 07:20:11 GMT` |
|12 |trace_id |Trace ID of the origin request. You can use it to locate the request when troubleshooting. |`0b5f3a9c7d8e4f1a9c2b6d3e5f789012` |
|13 |src_name |Origin that the CDN server actually requested (the primary origin or a backup origin), shown as the domain name or IP address configured for that origin. |`origin-storage.example.com` |

## Usage Limits

**Rate limit**: You can send up to 20 API requests per second.

**Log delivery delay**: By default, BytePlus CDN packages logs hourly. At the top of each hour, CDN writes the log entries collected during the previous hour to a log file and compresses the file. A log file is typically available for download about 3 hours after it is generated. Because of network latency and other factors, CDN may receive some log entries up to 24 hours late. CDN appends these late entries to the corresponding log file, so a log file may continue to grow for up to 24 hours after it is generated.

## Usage

* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCdnOriginLog&Version=2021\-03\-01

## Request Parameters

### Query Parameters

|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCdnOriginLog`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |

### Request Body

|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |The domain whose origin logs you want to retrieve. |`www.example.com` |
|StartTime |Long |Yes |The start of the time range, as a Unix timestamp. `StartTime` cannot be more than 62 days before the current date.<br><br>Note that `StartTime` is not necessarily the actual start of the time range. The actual start time is `StartTime` rounded up to the nearest hour.<br><br>Examples:<br><br><br>* If `StartTime` is 15:07, the actual start time is 16:00.<br><br>* If `StartTime` is 15:00, the actual start time is 15:00. |`1785227326` |
|EndTime |Long |Yes |The end of the time range, as a Unix timestamp. Note that `EndTime` is not necessarily the actual end of the time range.<br><br>The actual end time is `EndTime` rounded up to the nearest hour. |`1790152126` |
|PageNum |Long |No |The page number of the results to return.<br><br>The API paginates the returned log files based on `PageSize`. For example, if the API returns 100 log files and `PageSize` is `10`, the results span 10 pages. To get the log files on page 2, set `PageNum` to `2`.<br><br>If the specified page contains no log files, the value of `DomainLogDetails` in the response is `null`.<br><br>Default: `1`. |`1` |
|PageSize |Long |No |The number of log files per page.<br><br>Valid values: 1 to 100. Default: `10`. |`10` |
|ServiceRegion |String |No |The service region of the CDN servers that sent the origin requests. Use this parameter to filter origin logs. Valid values:<br><br><br>* `chinese_mainland`: **Chinese Mainland**.<br><br>* `outside_chinese_mainland`: **Global (excluding Chinese Mainland)** .<br><br><br>Default: `chinese_mainland`. |`chinese_mainland` |

## Response Parameters

|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Domain |String |The `Domain` specified in the request. |`www.example.com` |
|DomainLogDetails |Object[] |The list of log files returned by the API. | |
|EndTime |Long |The actual end time of the period that the log file covers, as a Unix timestamp. |`1642395600` |
|LogName |String |The name of the log file, in the format `<Domain>*origin*<StartTime>_<EndTime>.gz`. |`www.example.com_origin_20210707100000_20210707110000.gz` |
|LogPath |String |The download URL of the log file. The URL is valid for 24 hours. |`URL1` |
|LogSize |Long |The size of the log file, in bytes.<br><br>tip<br><br>CDN may append late log entries to a log file for up to 24 hours after the file is generated, so the size can differ between API calls. The size returned by the most recent call is the current one. |`9107` |
|StartTime |Long |The actual start time of the period that the log file covers, as a Unix timestamp.<br><br>Each log file covers one hour, so `EndTime` is always one hour after `StartTime`. |`1642392000` |
|PageNum |Long |The `PageNum` specified in the request. |`1` |
|PageSize |Long |The `PageSize` specified in the request. |`10` |
|TotalCount |Long |The total number of log files that match the filter criteria. |`1` |

## Samples

### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnOriginLog&Version=2021-03-01
{
    "Domain": "www.example.com",
    "StartTime": 1793145600,
    "EndTime": 1793318400
}
```

### Sample response

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
