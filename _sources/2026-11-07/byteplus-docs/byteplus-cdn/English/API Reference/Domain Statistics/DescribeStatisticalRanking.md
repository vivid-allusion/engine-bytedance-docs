---
title: "DescribeStatisticalRanking"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeStatisticalRanking_En"
---

Based on the user requests received by the CDN, the API aggregates a series of metric data by popular object types, sorts these aggregated data from large to small, and finally returns these popular objects. Popular object types include the country and region of the requesting client, request URL, Referer domain, objects in the UA string, and the number of client IP addresses.

To call the API, you need to specify a metric, a popular object type, a statistical time period, and a time granularity. You can also specify multiple filter conditions to filter user requests. You can query data for up to the past 92 days.

Data Stability: Metric data calculated on edge cache nodes may change due to network fluctuations. Generally, the metric data will progressively stabilize within 12 hours.

Data timeliness: The popular objects are based on hourly granularity metric data. Therefore, the data statistics may have a delay of about 2 hours. For example, for the popular objects during the time period from 09:00 to 10:00, you can get the accurate results around 11:00.

<span id="usage-limits"></span>
## Usage Limits

Throttling Limit: You can submit a maximum of 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeStatisticalRanking`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Item |String |Yes |Indicates a popular object type as a grouping condition. This API aggregates `Metric` data by `Item` and sorts these aggregated data. This parameter has the following values:<br><br><br>* `region`: refers to the country or region where the client making the request is located.<br><br>* `url`: refers to the request URL.<br><br>* `referer`: refers to the value of the `Referer` header in the request.<br><br>* `ua`: refers to the value of the `User-Agent` header in the request.<br><br>* `clientip`: refers to the IP address of the client.<br><br><br>tip<br><br><br>* When `Item` is `ua`, you need to specify `UaType` as an supplementary grouping condition.<br><br>* When `Item` is `region`, you also need to specify `Area` an supplementary grouping condition. |`region` |
|Metric |String |Yes |Indicates a metric. The available values for this parameter are influenced by `Item`.<br><br><br>* When `Item` is `referer`, `ua`, or `clientip`, the parameter has the following values:<br><br>   * `in_traffic`: indicate the amount of data transferred by users to the CDN, in bytes.<br><br>   * `out_traffic`: refers to the amount of data transferred by the CDN to users, in bytes.<br><br>   * `requests`: indicate the number of user requests received by the CDN.<br><br>   * `dynamic_requests`: indicate the number of user requests received by the CDN that meet all the following conditions:<br><br>      * The request method is neither GET nor HEAD.<br><br>      * The response status code by the CDN is not 405.<br><br>   * `static_requests`: indicate the number of user requests received by the CDN that meet all the following conditions:<br><br>      * The request method is GET or HEAD.<br><br>      * The response status code by the CDN is not 405.<br><br>* When `Item` is `url`, the parameter has the following values:<br><br>   * `in_traffic`<br><br>   * `out_traffic`<br><br>   * `requests`<br><br>   * `dynamic_requests`<br><br>   * `static_requests`<br><br>   * `status_2xx`: In the CDN's responses to user requests, this parameter refers to the number of 2xx status codes.<br><br>   * `status_3xx`: refers to the number of 3xx status codes.<br><br>   * `status_4xx`: refers to the number of 4xx status codes.<br><br>   * `status_5xx`: refers to the number of 5xx status codes.<br><br>* When `Item` is `region`, the parameter has the following values:<br><br>   * `clientip`: refers to the number of unique client IP addresses. This is the default value.<br><br>   * `in_traffic`<br><br>   * `out_traffic`<br><br>   * `requests`<br><br>   * `dynamic_requests`<br><br>   * `status_2xx`<br><br>   * `status_3xx`<br><br>   * `status_4xx`<br><br>   * `status_5xx` |`traffic` |
|StartTime |Long |Yes |Indicates the start time of the statistical period, formatted as a Unix timestamp with second precision. `StartTime` must precede or be equal to `EndTime`. Additionally, the statistical time span represented by `StartTime` and `EndTime` must not exceed 31 days.<br><br>tip<br><br><br>* `StartTime` and `EndTime` specify the statistical time period. However, the start time and end time of the actual statistical time period are both at the hour level.<br><br><br>Example: If `StartTime` indicates 15:07 and `EndTime` indicates 15:21, the actual statistical time period will be [15:00,16:00).<br><br>It should be noted that if `EndTime` happens to be on the hour, the actual statistical time period will be extended by another hour. Assume that the time represented by `StartTime` is 15:07 and the time represented by `EndTime` is 16:00, then the actual statistical time period is [15:00,17:00). |`1710950400` |
|EndTime |Long |Yes |Indicates the end time of the statistical period, formatted as a Unix timestamp with second precision. |`1710998170` |
|Domain |String |Yes |Indicates a domain name, used for filtering user requests. If `Domain` is not specified, it means that this parameter is not used to filter user requests.<br><br>tip<br><br>When an IAM user invokes this API, be aware of the following:<br><br><br>* IAM users can only specify one domain name they have access permissions for. They can call [DescribeTemplateDomains](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplatedomains-7f84f) to retrieve domain names they are authorized to access. |`www.example.com` |
|UaType |String |No |Indicates an object type within the `User-Agent` string. When `Item` is `ua`, the parameter must be specified as an supplementary grouping condition. When `Item` is not `ua`, the parameter is invalid.<br><br>The parameter has the following values:<br><br><br>* `browser`: refers to the browser type within the `User-Agent` string.<br><br>* `system`: refers to the operating system type within the `User-Agent` string.<br><br>* `equipment`: refers to the type of client device within the `User-Agent` string. |`system` |
|Area |String |No |Indicates an area type. This parameter is only valid when `Item` is `region`, and is used as a supplementary grouping condition to obtain the regional distribution of the number of client IP addresses.<br><br>The parameter has the following values:<br><br><br>* `Global`: refers to countries and regions globally.<br><br>* `China`: refers to the provincial administrative regions of China.<br><br><br>tip<br><br><br>* If you do not specify `Metric`, `Area` may not be specified.<br><br>   * If `Area` is not specified, the API will return the number of unique client IP addresses distributed by countries, regions, and provincial administrative regions in China.<br><br>* If you specify `Metric`, `Area` must be specified. |`Global` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Item |String |Indicates the popular object type specified by the request parameter `Item`. |`region` |
|Metric |String |Indicates the metric specified by the request parameter `Metric`. |`traffic` |
|RankingDataList |Object[] |Indicates the set of popular objects returned by this API. | |
|ItemKey |String |Indicates a popular object.<br><br><br>* When `Item` is `url`, the popular object is the path within a request URL.<br><br>* When `Item` is `referer`, the popular object is a Referer domain.<br><br>* When `Item` is `region`, the popular object is the code of a country, a region or a provincial administrative regions in China.<br><br>* When `Item` is `clientip`, the popular object is the client IP address.<br><br>* When `Item` is `ua`,<br><br>   * If `UaType` is `equipment`, the popular object is a device type.<br><br>   * If `UaType` is `system`, the popular object is a type of operating system.<br><br>   * If `UaType` is `browser`, the popular object is a browser type. |`GS` |
|ItemKeyCN |String |* When `Item` is `region`, `ItemKeyCN` is the Chinese name of the region corresponding to `ItemKey`.<br><br>* When `Item` is `url`, `ItemKeyCN` is the path corresponding to `ItemKey`.<br><br>* When `Item` is `clientip`, `ua`, `referer`, `url`, or `referer`, `ItemKeyCN` is the same as `ItemKey`. |`甘肃` |
|Value |Double |Indicates the `Metric` data for `ItemKey`. The time zone of `Value` is UTC+08:00。 |`777` |
|UaType |String |Indicates the object type specified in the request parameter `UaType`. If `UaType` is not included in the request parameters, this parameter will not appear in the returned results. |`system` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeStatisticalRanking&Version=2021-03-01
{
    "Area": "Global",
    "Domain": "www.example.com",
    "StartTime": 1720614677,
    "EndTime": 1721478677,
    "Item": "region",
    "Metric": "clientip"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202407221231341976A83AF08B9822FD8F",
        "Action": "DescribeStatisticalRanking",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Item": "region",
        "Metric": "clientip",
        "RankingDataList": [
            {
                "ItemKey": "USA",
                "ItemKeyCN": "美国",
                "Value": 2857990
            },
            {
                "ItemKey": "IND",
                "ItemKeyCN": "印度",
                "Value": 744081
            },
            {
                "ItemKey": "BRA",
                "ItemKeyCN": "巴西",
                "Value": 695588
            },
            {
                "ItemKey": "FRA",
                "ItemKeyCN": "法国",
                "Value": 454253
            },
            ...
        ]
    }
}
```
