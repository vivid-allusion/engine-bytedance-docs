---
title: "DescribeCdnAccessLog"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecdnaccesslog"
---

Get access logs for a specified domain name. The API returns the download URLs for these access logs. BytePlus CDN packages access logs by hour.

Data retention period: When calling the API, it is recommended that you specify a time span of no more than 30 days, otherwise the API call may time out due to the large number of logs.

Log delay: By default, CDN packages logs collected in the past hour at an hourly granularity, generating log packages at the top of each hour. Log packages are available for download approximately 3 hours after generation. Due to factors such as network latency, logs collected by CDN may have a delay of up to 24 hours. For these delayed logs, CDN appends them to their corresponding log packages. Therefore, log packages may have logs appended within 24 hours after their generation.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCdnAccessLog&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCdnAccessLog`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Indicates a domain name. This API obtains the access logs of the domain name. |`www.example.com` |
|ServiceRegion |String |No |Indicates a service region, used to filter access logs. This parameter has the following values:<br><br><br>* `chinese_mainland`: Indicates **Chinese Mainland**.<br><br>* `global`: Indicates **Global**.<br><br>* `outside_chinese_mainland`：Indicates **Global (Excluding Chinese Mainland)** .<br><br><br>The default value of this parameter is `global`. |`global` |
|StartTime |Long |Yes |Indicates the start time of the log statistics period in Unix timestamp format. Note that `StartTime` is not the actual start time of the log statistics period.<br><br>The actual start time is rounded up to the next hour from `StartTime`.<br><br>Examples:<br><br><br>* If your specified `StartTime` represents 15:07, the actual start time will be 16:00.<br><br>* If your specified `StartTime` represents 15:00, the actual start time will be 15:00. |`1641844915` |
|EndTime |Long |Yes |Indicates the end time of the log statistics period in Unix timestamp format. Note that `EndTime` is not the actual end time of the log statistics period.<br><br>The actual end time is rounded up to the next hour from `EndTime`. |`1641953589` |
|PageNum |Long |No |Indicates a page number. The API returns the log packages on the page specified by the page number.<br><br>The log packages returned by the API are paged according to `PageSize`. Assume that the number of log packages returned by the API is 100, and the `PageSize` you specify is `10`, then the returned log packages are distributed on 10 pages. If the `PageNum` you specify is `2`, it means to get the log packages on page 2.<br><br>If there is no log package on the page you specify, the value of the `DomainLogDetails` parameter in the returned result is `null`.<br><br>The default value of `PageNum` is `1`. |`1` |
|PageSize |Long |No |Indicates the number of log packages contained in each page.<br><br>The value range of this parameter is 1\-100, and the default value is `10`. |`1` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Domain |String |Indicates `Domain` in the request parameter. |`www.a.com` |
|PageSize |Long |Indicates `PageSize` in the request parameter. |`100` |
|PageNum |Long |Indicates `PageNum` in the request parameter. |`1` |
|TotalCount |Long |Indicates the number of log packages that meet the filtering conditions. |`100` |
|DomainLogDetails |Object[] |Indicates the list of log packages returned by the API. | |
|LogName |String |Indicates the name of a log package in the list. The naming convention is <*Domain*\>_<*Start_Time*\>_<*End_Time*\>.gz.<br><br>tip<br><br>In the log package names, the time zone of `Start_Time` and `End_Time` is UTC+08:00. |`www.example.com_20210707100000_20210707110000.gz` |
|StartTime |Long |Indicates the actual start time of the log statistics period corresponding to this log package in Unix timestamp format.<br><br>The time interval between `StartTime` and `EndTime` is 1 hour. |`1642392000` |
|EndTime |Long |Indicates the actual end time of the log statistics period corresponding to this log package in Unix timestamp format. |`1642395600` |
|LogPath |String |Indicates the download URL of the log package. The download URL is valid for 24 hours. |`URL1` |
|LogSize |Long |Indicates the size of the log package, in `bytes`.<br><br>tip<br><br>Delayed logs might be appended to the log package within 24 hours after the package is created . Therefore, the size of the log package obtained from each API call might vary. Please refer to the size of the most recently obtained log package. |`9107` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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
