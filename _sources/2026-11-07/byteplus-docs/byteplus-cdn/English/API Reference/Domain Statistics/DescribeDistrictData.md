---
title: "DescribeDistrictData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeDistrictData_En"
---

<span id="api-description"></span>
## API Description

Based on user requests received by the CDN, this API calculates the metric breakdown data at each time point for the specified metric.

To call the API, you need to specify a metric, a statistical period and a time granularity. You can also specify multiple filter conditions to filter user requests. You can query data for up to the past 92 days.

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

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeDistrictData&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeDistrictData`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Metric |String |Yes |Indicates a metric. Available values for this parameter are as follows:<br><br><br>* `in_traffic`: Indicates the amount of data transferred by users to the CDN, measured in bytes.<br><br>* `in_bandwidth`: Indicates the peak bandwidth calculated based on the amount of data transferred by users to the CDN, measured in bps.<br><br>* `out_traffic`: Indicates the amount of data transferred by the CDN to users, measured in bytes.<br><br>* `out_bandwidth`: Indicates the peak bandwidth calculated based on the amount of data transferred by the CDN to users, measured in bps.<br><br>* `requests`: Indicates the total number of user requests received by the CDN.<br><br>* `dynamic_requests`: Indicates the number of user requests received by the CDN that meet all of the following criteria:<br><br>   * The request method is neither GET nor HEAD.<br><br>   * The response status code from the CDN is not 405.<br><br>* `static_requests`: Indicates the number of user requests received by the CDN that meet all of the following criteria:<br><br>   * The request method is GET or HEAD.<br><br>   * The response status code from the CDN is not 405.<br><br>* `qps`: Indicates the Queries Per Second (QPS) of user requests received by the CDN.<br><br>* `response_time`: Indicates the average time CDN takes to respond to user requests, measured in milliseconds (ms).<br><br>* `avg_speed`: Indicates the average data transfer speed when CDN responds to user requests, measured in Bps. This metric's data is calculated based on user requests with response status codes of 2xx.<br><br>* `status_all`: Indicates the quantity of all response codes in CDN's responses to user requests, including the counts of each category of codes starting with the digits 2, 3, 4, and 5, as well as the count of each individual code number.<br><br>* `status_2xx`: Indicates the quantity of status codes starting with the digit 2, including each individual 2xx code number.<br><br>* `status_3xx`: Indicates the quantity of status codes starting with the digit 3, including each individual 3xx code number.<br><br>* `status_4xx`: Indicates the quantity of status codes starting with the digit 4, including each individual 4xx code number.<br><br>* `status_5xx`: Indicates the quantity of status codes starting with the digit 5, including each individual 5xx code number.<br><br><br>For details and statistical methods for each metric, see see [Metric Reference](https://docs.byteplus.com/en/docs/byteplus-cdn/QzMnM4). |`traffic` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days. |`1710259200` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710836303` |
|Interval |String |No |Indicates a time granularity. This API segments the statistical period represented by `StartTime` and `EndTime` into a series of time intervals based on `Interval`, and then calculate the `Metric` data for each time interval.<br><br>For how `Interval` is used to segment the statistical period, refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en).<br><br>The parameter has the following values:<br><br><br>* `1min`: indicates a granularity of 1 minute.<br><br>* `5min`: indicates a granularity of 5 minutes.<br><br>* `hour`: indicates a granularity of 1 hour.<br><br>* `day`: indicates a granularity of 1 day.<br><br><br>The granularity you can specify is influenced by the time span represented by `StartTime` and `EndTime`:<br><br><br>* For time span <= 1 day, the granularities you can specify are `1min`, `5min`, `hour`.<br><br>* For 1 day < time span <= 3 days, the granularities you can specify are `5min`, `hour`, `day`.<br><br>* For 3 days < time span <= 31 days, the granularities you can specify are `hour` and `day`.<br><br><br>The default value for this parameter is `5min`. If this does not match the time span, the API request will fail. |`hour` |
|Project |String |No |Indicates a project.<br><br><br>* If you specify `Domain`, this API will collect `Metric` data for all the domains you specified.<br><br>* If you specify `Project` but do not specify `Domain`, this API will collect `Metric` data for the project you specified. See [How project data is collected](https://docs.byteplus.com/en/docs/18/20755#how-project-data-is-collected).<br><br>* If you do not specify `Project` or `Domain`, this API will collect `Metric` data for all domains. |`my_project` |
|Domain |String |No |Indicates one or more domains used to filter user requests. This API will collect `Metric` data for each domain you specified. You can specify up to 50 domains. Separate multiple domains with commas (,). If `Domain` is not specified, it means this parameter is not used to filter requests.<br><br>If you specify `Project`, the domains you specified must belong to that `Project`.<br><br>tip<br><br>When an IAM user calls this API, please note the following:<br><br><br>* IAM users can only specify the domain names they have permission to access. IAM users can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to get the domain names they have permission to access.<br><br>* If this parameter is not specified, it means all the domain names that the IAM user has permission to access. |`www.example.com,www.test.com,img.example.com` |
|Location |String |No |Indicates the codes for countries and regions, used for filtering user requests. You can specify one or more codes, with the CDN calculating `Metric` data for requests from these areas. Codes are separated by commas, and a maximum of 30 countries and regions can be specified.<br><br><br>* If `Location` is specified, you cannot specify `Province`, and vice versa.<br><br>* If `Location` is not specified, it means that this parameter is not used to filter user requests.<br><br><br>You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to obtain the correspondence table of codes with countries and regions. |`CHN,AZE` |
|Province |String |No |Indicates the codes for provincial administrative regions in China, used for filtering user requests. You may specify one or several codes, with the CDN calculating `Metric` data for requests from these regions. Codes are delimited by commas, and you can specify up to 10 codes.<br><br>If `Province` is not specified, it means that this parameter is not used to filter user requests.<br><br>You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to obtain the correspondence table of codes with provincial administrative regions. |`AH,BJ,CQ,FJ` |
|Isp |String |No |Indicates the code of the Chinese network operators used for filtering user requests, such as `CT` for China Telecom. You can specify one or several codes, with the CDN calculating `Metric` data for user requests from these operators. Codes are separated by commas, and a maximum of 5 codes can be specified.<br><br><br>* You can only specify `Isp` when `Location` is `CHN` or when `Province` is specified.<br><br>* If `Isp` is not specified, it means that this parameter is not used to filter user requests.<br><br><br>You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to obtain the correspondence table of codes with network operators. |`CT,CM,CU,GWBN` |
|Protocol |String |No |Indicates an application layer protocol used for filtering user requests. The parameter has the following values:<br><br><br>* `http`: refers to the HTTP protocol.<br><br>* `https`: refers to the HTTPS protocol.<br><br>* `quic`: refers to the QUIC protocol.<br><br>* `websocket`: refers to the WebSocket protocol.<br><br>* `non-websocket`: refers to the HTTP protocol, HTTPS protocol and QUIC protocol.<br><br><br>If `Protocol` is not specified, it means that this parameter is not used to filter user requests.<br><br>tip<br><br>If `Metric` is `response_time` or `avg_speed`, please specify `Protocol` to filter out the WebSocket protocol. This is because the data for these two metrics is inaccurate for WebSocket requests. |`https` |
|IpVersion |String |No |Indicates a network layer protocol used for filtering user requests. The parameter has the following values:<br><br><br>* `IPv4`: refers to the IPv4 protocol.<br><br>* `IPv6`: refers to the IPv6 protocol.<br><br><br>If `IpVersion` is not specified, it means that this parameter is not used to filter user requests. |`IPv4` |
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
|Value |Double |Indicates a `Metric` breakdown data. The time zone of `Value` is `TimeZone`. |`4567` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeDistrictData&Version=2021-03-01
{
    "Domain": "www.example.com,www.test.com,img.example.com",
    "StartTime": 1710259200,
    "EndTime": 1710835599,
    "Interval": "day",
    "IpVersion": "IPv4",
    "Isp": "CT,CM,CU,GWBN",
    "Metric": "out_traffic",
    "Project": "my_project",
    "Protocol": "https",
    "Province": "AH,BJ,CQ,FJ"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2024031916110305F6D27733C2CA667E04",
        "Action": "DescribeDistrictData",
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
                        "Value": 31667254.3
                    },
                    {
                        "TimeStamp": 1710288000,
                        "Value": 35425907
                    },
                    {
                        "TimeStamp": 1710374400,
                        "Value": 33508322.1
                    },
                    {
                        "TimeStamp": 1710460800,
                        "Value": 29844611.5
                    },
                    {
                        "TimeStamp": 1710547200,
                        "Value": 19993227.1
                    },
                    {
                        "TimeStamp": 1710633600,
                        "Value": 19567554.6
                    },
                    {
                        "TimeStamp": 1710720000,
                        "Value": 32469929.8
                    },
                    {
                        "TimeStamp": 1710806400,
                        "Value": 30702487.2
                    }
                ]
            }
        ]
    }
}
```


&nbsp;
