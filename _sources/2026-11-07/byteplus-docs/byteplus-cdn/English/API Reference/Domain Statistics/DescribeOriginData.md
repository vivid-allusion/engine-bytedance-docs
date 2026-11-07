---
title: "DescribeOriginData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginData_En"
---

<span id="api-description"></span>
## API Description

Based on origin requests sent to the origin server by CDN, this API calculates the metric breakdown data at each time point for the specified metric.

To call the API, you need to specify a metric, a statistical period and a time granularity. You can also specify multiple filter conditions to filter origin requests. You can query data for up to the past 92 days.

Data Stability: Metric data calculated on regional cache nodes may change due to network fluctuations. Generally, the metric data will progressively stabilize within 12 hours. Therefore, the metric data returned by this API is not the usage shown in the bill and is for reference only. Please refer to the bill for actual usage.

Data timeliness: Metric data may have a delay of about 5 minutes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are new to the CDN statistics API, please ensure to read the following documents first to aid your understanding of this API:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en">Statistical Time Period</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metric Reference</a></div>



<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeOriginData&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeOriginData`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Metric |String |Yes |Indicates a metric. The parameter has the following values:<br><br><br>* `in_traffic`: refers to the amount of data transferred by the origin to the CDN, measured in bytes.<br><br>* `in_bandwidth`: refers to the bandwidth calculated based on the amount of data transferred by the origin to the CDN, measured in bps.<br><br>* `out_traffic`: refers to the amount of data transferred by the CDN to the origin, measured in bytes.<br><br>* `out_bandwidth`: refers to the bandwidth calculated based on the amount of data transferred by the CDN to the origin, measured in bps.<br><br>* `requests`: refers to the number of origin requests.<br><br>* `qps`: refers to the Queries Per Second (QPS) of origin requests.<br><br>* `response_time`: refers to the average time taken by the CDN to receive responses from the origin, measured in milliseconds (ms).<br><br>* `status_all`: For the responses that the CDN receives from the origin, this parameter refers to the number of status codes in the following categories:<br><br>   * The number of all status codes.<br><br>   * The number of 2xx status codes.<br><br>   * The number of 3xx status codes.<br><br>   * The number of 4xx status codes.<br><br>   * The number of 5xx status codes.<br><br>   * The number of each individual status code.<br><br>* `status_2xx`: refers to the number of 2xx status codes and each individual status code in this category.<br><br>* `status_3xx`: refers to the number of 3xx status codes and each individual status code in this category.<br><br>* `status_4xx`: refers to the number of 4xx status codes and each individual status code in this category.<br><br>* `status_5xx`: refers to the number of 5xx status codes and each individual status code in this category.<br><br><br>For specific details and calculation methods of each metric, see [Metric Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4). |`traffic` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days. |`1710259200` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710836303` |
|Interval |String |No |Indicates a time granularity. This API segments the statistical period represented by `StartTime` and `EndTime` into a series of time intervals based on `Interval`, and then calculate the `Metric` data for each time interval.<br><br>For how `Interval` is used to segment the statistical period, refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en).<br><br>The parameter has the following values:<br><br><br>* `1min`: indicates a granularity of 1 minute.<br><br>* `5min`: indicates a granularity of 5 minutes.<br><br>* `hour`: indicates a granularity of 1 hour.<br><br>* `day`: indicates a granularity of 1 day.<br><br><br>The granularity you can specify is influenced by the time span represented by `StartTime` and `EndTime`:<br><br><br>* For time span <= 1 day, the granularities you can specify are `1min`, `5min`, `hour`.<br><br>* For 1 day < time span <= 3 days, the granularities you can specify are `5min`, `hour`, `day`.<br><br>* For 3 days < time span <= 31 days, the granularities you can specify are `hour` and `day`.<br><br><br>The default value for this parameter is `5min`. If this does not match the time span, the API request will fail. |`hour` |
|Project |String |No |Indicates a project.<br><br><br>* If you specify `Domain`, this API will collect `Metric` data for all the domains you specified.<br><br>* If you specify `Project` but do not specify `Domain`, this API will collect `Metric` data for the project you specified. See [How project data is collected](https://docs.byteplus.com/en/docs/18/20756#how-project-data-is-collected).<br><br>* If you do not specify `Project` or `Domain`, this API will collect `Metric` data for all domains. |`my_project` |
|Domain |String |No |Indicates one or more domains used to filter user requests. This API will collect `Metric` data for each domain you specified. You can specify up to 50 domains. Separate multiple domains with commas (,). If `Domain` is not specified, it means this parameter is not used to filter requests.<br><br>If you specify `Project`, the domains you specified must belong to that `Project`.<br><br>tip<br><br>When an IAM user calls this API, please note the following:<br><br><br>* IAM users can only specify the domain names they have permission to access. IAM users can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to get the domain names they have permission to access.<br><br>* If this parameter is not specified, it means all the domain names that the IAM user has permission to access. |`www.example.com,www.test.com,img.example.com` |
|TimeZone |String |No |Indicates the time zone of the `Metric` data. The parameter has the following values:<br><br><br>* `Etc/GMT`: refers to the timezone UTC+00:00.<br><br>* `Etc/GMT-1`, `Etc/GMT-2`, ..., `Etc/GMT-12`: refers to the timezones UTC+01:00, UTC+02:00, ..., UTC+12:00 respectively.<br><br>* `Etc/GMT+1`, `Etc/GMT+2`, ..., `Etc/GMT+12`: refers to the timezones UTC\-01:00, UTC\-02:00, ..., UTC\-12:00 respectively.<br><br><br>The default value for this parameter is `Etc/GMT-8`. |`Etc/GMT-8` |


<span id="how-project-data-is-collected"></span>
### How project data is collected

When collecting metric data for a project, CDN collects data for the domains within the project.


* If a domain is transferred out of the project during the statistical time period, the metric data for the project will not include the data for the domain after it is transferred out.

* If a domain is transferred into the project during the statistical time period, the metric data for the project will include the data for the domain after it is transferred in.


**Example**

Consider the following scenario:


* The statistical time period you specified is from 8:00 to 10:00 on a certain day.

* Domain X is transferred to Project A from another project at 9:00. Domain Y has always been in Project A.


In this scenario, if you collect metric data for Project A, the metric data will cover:


* The metric data for Domain X from 9:00 to 10:00.

* The metric data for Domain Y from 8:00 to 10:00.


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|MetricDataList |Object[] |Indicates the result data returned by this API. | |
|Metric |String |Indicates the metric specified by the request parameter `Metric`. |`traffic` |
|Values |Object[] |Indicates a set of `Metric` data objects calculated based on `Interval`. | |
|TimeStamp |Long |Indicates the start time of the time interval corresponding to `Value`, in Unix timestamp format with a precision of seconds. See [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en). |`1710273600` |
|Value |Double |Indicates a `Metric` breakdown data. |`4568` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeOriginData&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "day",
    "Metric": "out_traffic",
    "Project": "my_project"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202404230658256DB1CC6291C10133A8C6",
        "Action": "DescribeOriginData",
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
                        "Value": 3889061
                    },
                    {
                        "TimeStamp": 1710288000,
                        "Value": 3968016
                    },
                    {
                        "TimeStamp": 1710374400,
                        "Value": 3202556
                    },
                    {
                        "TimeStamp": 1710460800,
                        "Value": 3347793
                    },
                    {
                        "TimeStamp": 1710547200,
                        "Value": 1572368
                    },
                    {
                        "TimeStamp": 1710633600,
                        "Value": 1771534
                    },
                    {
                        "TimeStamp": 1710720000,
                        "Value": 2932340
                    },
                    {
                        "TimeStamp": 1710806400,
                        "Value": 4164708
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
