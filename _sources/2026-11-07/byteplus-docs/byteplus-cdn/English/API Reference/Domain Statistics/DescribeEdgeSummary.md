---
title: "DescribeEdgeSummary"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeEdgeSummary_En"
---

<span id="api-description"></span>
## API Description

The API aggregates data for a metric based on user requests received by the CDN.

To call the API, you need to specify a metric, a statistical period and a time granularity. You can also specify multiple filter conditions (including billing region) to filter user requests. You can query data for up to the past 92 days.

Data Stability: Metric data calculated on edge cache nodes may change due to network fluctuations. Generally, the metric data will progressively stabilize within 12 hours. Therefore, the metric data returned by this API is not the usage shown in the bill and is for reference only. Please refer to the bill for actual usage.

Data timeliness: Metric data may have a delay of about 5 minutes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are new to the CDN statistics API, please ensure to read the following documents first to aid your understanding of this API:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en">Statistical Time Period</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metric Reference</a></div>



<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit a maximum of 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeEdgeSummary&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeEdgeSummary`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Metric |String |Yes |Indicates a metric. The parameter has the following values:<br><br><br>* `in_traffic`: refers to the amount of data transferred by users to the CDN, measured in bytes.<br><br>* `in_bandwidth`: refers to the peak bandwidth calculated based on the amount of data transferred by users to the CDN, measured in bps.<br><br>* `out_traffic`: refers to the amount of data transferred by the CDN to users, measured in bytes.<br><br>* `out_bandwidth`: refers to the peak bandwidth calculated based on the amount of data transferred by the CDN to users, measured in bps.<br><br>* `requests`: refers to the number of user requests received by the CDN.<br><br>* `dynamic_requests`: For user requests received by the CDN, this metric refers to the number of user requests that meet all of the following criteria:<br><br>   * The request method is neither GET nor HEAD.<br><br>   * The CDN response status code is not 405.<br><br>* `static_requests`: For user requests received by the CDN, this metric refers to the number of user requests that meet all of the following criteria:<br><br>   * The request method is GET or HEAD.<br><br>   * The CDN response status code is not 405.<br><br>* `qps`: refers to the peak QPS of user requests received by the CDN.<br><br>* `response_time`: refers to the average time taken by the CDN to respond to user requests, measured in milliseconds (ms).<br><br>* `avg_speed`: refers to the average data transfer speed when CDN responds to user requests, measured in Bps. This metric's data is calculated based on user requests with response status codes of 2xx.<br><br>* `status_all`: For CDN responses to user requests, this metric refers to the quantity of the following categories of status codes:<br><br>   * The total number of all status codes.<br><br>   * The number of all 2xx status codes.<br><br>   * The number of all 3xx status codes.<br><br>   * The number of all 4xx status codes.<br><br>   * The number of all 5xx status codes.<br><br>   * The number of each individual status code.<br><br>* `status_2xx`: refers to the quantity of 2xx status codes and each individual status code starting with the digit 2.<br><br>* `status_3xx`: refers to the quantity of 3xx statuses and each individual status code starting with the digit 3.<br><br>* `status_4xx`: refers to the quantity of 4xx status codes and each individual status code starting with the digit 4.<br><br>* `status_5xx`: refers to the quantity of 5xx status codes and each individual status code starting with the digit 5.<br><br><br>For specific details and calculation methods of each metric, see [Metric Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4). |`traffic` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days. |`1710259200` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710836303` |
|Interval |String |No |Indicates a time granularity. This API segments the statistical period represented by `StartTime` and `EndTime` into a series of time intervals based on `Interval`, and then calculate the `Metric` data for each time interval.<br><br>For how `Interval` is used to segment the statistical period, refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en).<br><br>The parameter has the following values:<br><br><br>* `1min`: indicates a granularity of 1 minute.<br><br>* `5min`: indicates a granularity of 5 minutes.<br><br><br>The granularity you can specify is influenced by the time range between `StartTime` and `EndTime`.<br><br><br>* If the time range is <= 1 day, you can specify `1min` or `5min`.<br><br>* If 1 day < time range <= 31 days, you can only specify `5min`.<br><br><br>The default value for this parameter is `5min`. If the default does not match the time range, the API request will fail. |`5min` |
|Project |String |No |Indicates a project.<br><br><br>* If you specify `Domain`, this API will collect `Metric` data for all the domains you specified.<br><br>* If you specify `Project` but do not specify `Domain`, this API will collect `Metric` data for the project you specified. See [How project data is collected](https://docs.byteplus.com/en/docs/18/20764#how-project-data-is-collected).<br><br>* If you do not specify `Project` or `Domain`, this API will collect `Metric` data for all domains. |`my_project` |
|Domain |String |No |Indicates one or more domains used to filter user requests. This API will collect `Metric` data for each domain you specified. You can specify up to 50 domains. Separate multiple domains with commas (,). If `Domain` is not specified, it means this parameter is not used to filter requests.<br><br>If you specify `Project`, the domains you specified must belong to that `Project`.<br><br>tip<br><br>When an IAM user calls this API, please note the following:<br><br><br>* IAM users can only specify the domain names they have permission to access. IAM users can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to get the domain names they have permission to access.<br><br>* If this parameter is not specified, it means all the domain names that the IAM user has permission to access. |`www.example.com,www.test.com,img.example.com` |
|BillingRegion |String |No |Indicates one or multiple billing regions, used for filtering user requests. This API calculates `Metric` data for requests originating from these billing regions. Billing regions are separated by a comma (,). The parameter has the following values:<br><br><br>* `CHN`: represents Mainland China.<br><br>* `EU`: represents the Europe region.<br><br>* `NA`: represents the North America region.<br><br>* `SA`: represents the South America region.<br><br>* `MEA`: represents the Middle East and Africa region.<br><br>* `AP1`: represents Asia Pacific region one.<br><br>* `AP2`: represents Asia Pacific region two.<br><br>* `AP3`: represents Asia Pacific region three.<br><br><br>If `BillingRegion` is not specified, it indicates that this parameter is not used to filter requests. |`CHN,EU` |
|TimeZone |String |No |Indicates the timezone for `StartTime` and `EndTime`. The parameter can take the following values:<br><br><br>* `Etc/GMT`: The timezone is UTC+00:00.<br><br>* `Etc/GMT-1`, `Etc/GMT-2`, ..., `Etc/GMT-12`: The timezones are respectively UTC+01:00, UTC+02:00, ..., UTC+12:00.<br><br>* `Etc/GMT+1`, `Etc/GMT+2`, ..., `Etc/GMT+12`: The timezones are respectively UTC\-01:00, UTC\-02:00, ..., UTC\-12:00.<br><br><br>The default value of this parameter is `Etc/GMT-8`. |`Etc/GMT-8` |


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
|Value |Double |Indicates the aggregated `Metric` data. |`3475788` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeEdgeSummary&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "bandwidth",
    "Project": "my_project",
    "BillingRegion": "CHN,EU"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240423065708E622246DA96029C147AF",
        "Action": "DescribeEdgeSummary",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "Metric": "out_traffic",
                "Value": 75637256964.5
            }
        ]
    }
}
```


&nbsp;
