---
title: "DescribeOriginStatusCodeRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginStatusCodeRanking_En"
---

<span id="api-description"></span>
## API Description

Based on the origin responses received by the CDN, the API aggregates a series of metric data by domain name and sorts the aggregated data from large to small.

To call the API, you need to specify a metric, a statistical time period, and a time granularity. You can also specify multiple filter conditions to filter origin requests. You can query data for up to the past 92 days.

Data Stability: Metric data calculated on regional cache nodes may change due to network fluctuations. Generally, the metric data will progressively stabilize within 12 hours.

Data timeliness: Metric data may have a delay of about 5 minutes.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are new to the CDN statistics API, please ensure to read the following documents first to aid your understanding of this API:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en">Statistical Time Period</a></div>


* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4">Metric Reference</a></div>



<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You may submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeOriginStatusCodeRanking&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeOriginStatusCodeRanking`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Item |String |Yes |Indicates a grouping condition for aggregating `Metric` data. Currently, the value for this parameter must be `domain`, meaning that the `Metric` data is aggregated by the domain names that are specified in `Domain`. |`domain` |
|Metric |String |Yes |For origin responses received by the CDN, this parameter indicates the number of status codes in one of the following categories:<br><br><br>* `status_2xx`: refers to the number of 2xx status codes.<br><br>* `status_3xx`: refers to the number of 3xx status codes.<br><br>* `status_4xx`: refers to the number of 4xx status codes.<br><br>* `status_5xx`: refers to the number of 5xx status codes. |`status_4xx` |
|Interval |String |No |Indicates a time granularity. This API segments the statistical period represented by `StartTime` and `EndTime` into a series of time intervals based on `Interval`, and then calculate the `Metric` data for each time interval.<br><br>For how `Interval` is used to segment the statistical period, refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en).<br><br>The parameter has the following values:<br><br><br>* `1min`: indicates a granularity of 1 minute.<br><br>* `5min`: indicates a granularity of 5 minutes.<br><br><br>The time granularity you can specify is influenced by the time range represented by `StartTime` and `EndTime`.<br><br><br>* If time range <= 1 day, you can specify `1min` or `5min`.<br><br>* If 1 < time range <= 31 days, you can only specify `5min`.<br><br><br>The default value of this parameter is `5min`. If the default value doesn't match the time range, the API request will fail. |`1min` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days. |`1710259200` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710836303` |
|Project |String |No |Indicates a project.<br><br><br>* If you specify `Domain`, this API will collect `Metric` data for all the domains you specified.<br><br>* If you specify `Project` but do not specify `Domain`, this API will collect `Metric` data for the project you specified. See [How project data is collected](https://docs.byteplus.com/en/docs/18/20765#how-project-data-is-collected).<br><br>* If you do not specify `Project` or `Domain`, this API will collect `Metric` data for all domains. |`my_project` |
|Domain |String |No |Indicates one or more domains used to filter user requests. This API will collect `Metric` data for each domain you specified. You can specify up to 50 domains. Separate multiple domains with commas (,). If `Domain` is not specified, it means this parameter is not used to filter requests.<br><br>If you specify `Project`, the domains you specified must belong to that `Project`.<br><br>tip<br><br>When an IAM user calls this API, please note the following:<br><br><br>* IAM users can only specify the domain names they have permission to access. IAM users can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to get the domain names they have permission to access.<br><br>* If this parameter is not specified, it means all the domain names that the IAM user has permission to access. |`www.example.com,www.test.com,img.example.com` |
|TimeZone |String |No |Indicates the time zone of the `Metric` data. The parameter has the following values:<br><br><br>* `Etc/GMT`: refers to the timezone UTC+00:00.<br><br>* `Etc/GMT-1`, `Etc/GMT-2`, ..., `Etc/GMT-12`: refers to the timezones UTC+01:00, UTC+02:00, ..., UTC+12:00 respectively.<br><br>* `Etc/GMT+1`, `Etc/GMT+2`, ..., `Etc/GMT+12`: refers to the timezones UTC\-01:00, UTC\-02:00, ..., UTC\-12:00 respectively.<br><br><br>The default value of this parameter is `Etc/GMT-8`. |`Etc/GMT-8` |


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
|Item |String |Indicates the grouping condition specified by the request parameter `Item`. |`domain` |
|Metric |String |Indicates the metric specified by the request parameter `Metric`. |`status_4xx` |
|TopDataDetails |Object[] |Indicates a set of data objects containing the details of `Metric` data aggregated by `Item`. Each data object contains the number and ratio of status codes in each category. These data objects are sorted from largest to smallest by the specified `Metric`. | |
|ItemKey |String |Indicates a domain name in the `Domain` list. |`www.example.com` |
|Status2xx |Double |Indicates the ratio of 2xx status codes for this `ItemKey`. |`45678` |
|Status2xxRatio |Double |Indicates the ratio of 2xx status codes for this `ItemKey`. |`0.47` |
|Status3xx |Double |Indicates the number of 3xx status codes for this `ItemKey`. |`0` |
|Status3xxRatio |Double |Indicates the ratio of 3xx status codes for this `ItemKey`. |`0` |
|Status4xx |Double |Indicates the number of 4xx status codes for this `ItemKey`. |`3` |
|Status4xxRatio |Double |Indicates the ratio of 4xx status codes for this `ItemKey`. |`0.0001` |
|Status5xx |Double |Indicates the number of 5xx status codes for this `ItemKey`. |`0` |
|Status5xxRatio |Double |Indicates the ratio of 5xx status codes for this `ItemKey`. |`0` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

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


<span id="sample-response"></span>
### Sample response

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
