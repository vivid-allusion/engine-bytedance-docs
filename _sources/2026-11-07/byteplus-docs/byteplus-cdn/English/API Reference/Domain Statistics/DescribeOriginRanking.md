---
title: "DescribeOriginRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeOriginRanking_En"
---

<span id="api-description"></span>
## API Description

Based on the origin requests sent by the CDN, the API aggregates a series of metric data by domain names and sorts the aggregated data from large to small.

To call the API, you need to specify a metric, a statistical time period, and a time granularity. You can also specify multiple filter conditions to filter origin requests. You can query data for up to the past 92 days.

Data Stability: Metric data calculated on regional cache nodes may change due to network fluctuations. Generally, the metric data will progressively stabilize within 12 hours.

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

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeOriginRanking&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeOriginRanking`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Item |String |Yes |Indicates a grouping condition for aggregating `Metric` data. Currently, this parameter value can only be `domain`, indicating that the `Metric` data is aggregated by domain names. |`domain` |
|Metric |String |Yes |Indicates a metric. The parameter has the following values:<br><br><br>* `in_traffic`: refers to the amount of data transferred by the origin to the CDN, measured in bytes.<br><br>* `in_bandwidth`: refers to the peak bandwidth calculated based on the amount of data transferred by the origin to the CDN, measured in bps.<br><br>* `out_traffic`: refers to the amount of data transferred by the CDN to the origin, measured in bytes.<br><br>* `out_bandwidth`: refers to the peak bandwidth calculated based on the amount of data transferred by the CDN to the origin, measured in bps.<br><br>* `requests`: refers to the number of origin requests.<br><br><br>For specific details and calculation methods of each metric, see [Metric Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4). |`traffic` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days. |`1710259200` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710836303` |
|Project |String |No |Indicates a project.<br><br><br>* If you specify `Domain`, this API will collect `Metric` data for all the domains you specified.<br><br>* If you specify `Project` but do not specify `Domain`, this API will collect `Metric` data for the project you specified. See [How project data is collected](https://docs.byteplus.com/en/docs/18/20762#how-project-data-is-collected).<br><br>* If you do not specify `Project` or `Domain`, this API will collect `Metric` data for all domains. |`my_project` |
|Domain |String |No |Indicates one or more domains used to filter user requests. This API will collect `Metric` data for each domain you specified. You can specify up to 50 domains. Separate multiple domains with commas (,). If `Domain` is not specified, it means this parameter is not used to filter requests.<br><br>If you specify `Project`, the domains you specified must belong to that `Project`.<br><br>tip<br><br>When an IAM user calls this API, please note the following:<br><br><br>* IAM users can only specify the domain names they have permission to access. IAM users can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to get the domain names they have permission to access.<br><br>* If this parameter is not specified, it means all the domain names that the IAM user has permission to access. |`www.example.com,www.test.com,img.example.com` |
|Interval |String |No |Indicates a time granularity. This API segments the statistical period represented by `StartTime` and `EndTime` into a series of time intervals based on `Interval`, and then calculate the `Metric` data for each time interval.<br><br>For how `Interval` is used to segment the statistical period, refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en).<br><br>The parameter has the following values:<br><br><br>* `1min`: Indicates a granularity of 1 minute.<br><br>* `5min`: Indicates a granularity of 5 minutes.<br><br><br>The time granularity you can specify is influenced by the time range represented by `StartTime` and `EndTime`.<br><br><br>* If time range <= 1 day, you can specify `1min` or `5min`.<br><br>* If 1 < time range <= 31 days, you can only specify `5min`.<br><br><br>The default value of this parameter is `5min`. If the default value doesn't match the time range, the API request will fail. |`5min` |
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
|Item |String |Indicates the data grouping condition specified by the request parameter `Item`. |`domain` |
|TopDataDetails |Object[] |Indicates the result data returned by this API. | |
|Metric |String |Indicates the metric specified by the request parameter `Metric`. | |
|ValueDetails |Object[] |Indicates a set of data objects containing the details of `Metric` data aggregated by `Item`. These data objects are sorted by `Value` from largest to smallest. | |
|ItemKey |String |Indicates a domain name within the `Domain` list. |`www.example.com` |
|Ratio |Double |Indicates the percentage of this `ItemKey`'s `Value` in the total sum of all `ItemKey` values.<br><br>Note that when the `Metric` is `bandwidth`, this parameter is invalid, and its value will always be '0'. |`0.867` |
|Timestamp |Long |Indicates the time when the `Value` data was generated, in Unix timestamp units. This parameter is only valid when `Metric` is `bandwidth`, indicating the time of the bandwidth peak. If `Metric` is not `bandwidth`, then this parameter is invalid and the value will always be '0'. |`1710419700` |
|Value |Double |Indicates the `Metric` data for this `ItemKey`. |`457` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeOriginRanking&Version=2021-03-01
{
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "5min",
    "Metric": "out_traffic",
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
        "RequestId": "2024031923314574F098A8E1F336074314",
        "Action": "DescribeOriginRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "domain",
        "TopDataDetails": [
            {
                "Metric": "out_traffic",
                "ValueDetails": [
                    {
                        "ItemKey": "www.example.com",
                        "Ratio": 0.9614,
                        "Timestamp": 0,
                        "Value": 3003726848
                    },
                    {
                        "ItemKey": "img.example.com",
                        "Ratio": 0.0223,
                        "Timestamp": 0,
                        "Value": 69603224
                    },
                    {
                        "ItemKey": "www.test.com",
                        "Ratio": 0.0073,
                        "Timestamp": 0,
                        "Value": 22942093
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
