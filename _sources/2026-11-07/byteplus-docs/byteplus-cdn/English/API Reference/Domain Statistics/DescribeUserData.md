---
title: "DescribeUserData"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeUserData_En"
---

<span id="api-description"></span>
## API Description

Based on user requests received by CDN, this API calculates the number of unique client IP addresses at each time point.

To call the API, you need to specify a domain name, a statistical time period, and a time granularity. You can also specify multiple filter conditions to filter user requests. You can query data for up to the past 92 days.

Data Stability: Metric data calculated on edge cache nodes may change due to network fluctuations. Generally, the metric data will progressively stabilize within 12 hours.

Data timeliness: The number of unique visitors is based on hourly granularity metric data. Therefore, the data statistics may have a delay of about 2 hours. For example, for the number of unique visitors during the time period from 09:00 to 10:00, you can get the accurate results around 11:00.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">If you are new to the CDN statistics API, please ensure to read the following documents first to aid your understanding of this API:</div>



* <div data-tips="true" data-tips-type="tip"><a href="https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en">Statistical Time Period</a></div>



<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeUserData`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Indicates a domain name, used to filter user requests.<br><br>tip<br><br>When an IAM user invokes this API, please be aware of the following:<br><br><br>* IAM users can only specify domain names they have access permissions for. They can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to retrieve domain names they are authorized to access. |`www.example.com` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days. |`1710259200` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710836303` |
|Interval |String |Yes |Indicates a time granularity. This API segments the statistical period represented by `StartTime` and `EndTime` into a series of time intervals based on `Interval`, and then calculate the `Metric` data for each time interval.<br><br>For how `Interval` is used to segment the statistical period, refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en).<br><br>The parameter has the following values:<br><br><br>* `hour`: indicates a granularity of 1 hour.<br><br>* `day`: indicates a granularity of 1 day. |`hour` |
|IpVersion |String |No |Indicates a network layer protocol used for filtering user requests. The parameter has the following values:<br><br><br>* `IPv4`: refers to the IPv4 protocol.<br><br>* `IPv6`: refers to the IPv6 protocol.<br><br><br>If `IpVersion` is not specified, it means that this parameter is not used to filter user requests. |`IPv4` |
|Location |String |No |Indicates the codes for countries and regions, used for filtering user requests. You can specify one or more codes, with the CDN calculating `Metric` data for requests from these areas. Codes are separated by commas, and a maximum of 30 countries and regions can be specified.<br><br><br>* If `Location` is specified, you cannot specify `Province`, and vice versa.<br><br>* If `Location` is not specified, it means that this parameter is not used to filter user requests.<br><br><br>You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to obtain the correspondence table of codes with countries and regions. |`AZE` |
|Province |String |No |Indicates the codes for provincial administrative regions in China, used for filtering user requests. You may specify one or several codes, with the CDN calculating `Metric` data for requests from these regions. Codes are delimited by commas, and you can specify up to 10 codes.<br><br>If `Province` is not specified, it means that this parameter is not used to filter user requests.<br><br>You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to obtain the correspondence table of codes with provincial administrative regions. |`AH` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|MetricDataList |Object[] |Indicates a set of data objects containing the number of unique client IP addresses at each time point. | |
|TimeStamp |Long |Indicates a time point, formatted as a Unix timestamp with second precision. Refer to [Statistical Time Period](https://docs.byteplus.com/en/docs/byteplus-cdn/aboutStat-API_en). |`1710950400` |
|Value |Double |Indicates the number of unique client IP addresses for this `TimeStamp` time point. The time zone of `Value` is UTC+08:00。 |`42` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeUserData&Version=2021-03-01
{
    "Domain": "www.example.com",
    "StartTime": 1710950400,
    "EndTime": 1710998170,
    "Interval": "hour",
    "IpVersion": "IPv4",
    "Province": "AH"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202403220141458C564C77FA147001D2E1",
        "Action": "DescribeUserData",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "MetricDataList": [
            {
                "TimeStamp": 1710950400,
                "Value": 421
            },
            {
                "TimeStamp": 1710954000,
                "Value": 428
            },
            {
                "TimeStamp": 1710957600,
                "Value": 439
            },
            {
                "TimeStamp": 1710961200,
                "Value": 436
            },
            {
                "TimeStamp": 1710964800,
                "Value": 435
            },
            {
                "TimeStamp": 1710968400,
                "Value": 446
            },
            {
                "TimeStamp": 1710972000,
                "Value": 433
            },
            {
                "TimeStamp": 1710975600,
                "Value": 430
            },
            {
                "TimeStamp": 1710979200,
                "Value": 428
            },
            {
                "TimeStamp": 1710982800,
                "Value": 412
            },
            {
                "TimeStamp": 1710986400,
                "Value": 423
            },
            {
                "TimeStamp": 1710990000,
                "Value": 417
            },
            {
                "TimeStamp": 1710993600,
                "Value": 394
            },
            {
                "TimeStamp": 1710997200,
                "Value": 407
            }
        ]
    }
}
```


&nbsp;
