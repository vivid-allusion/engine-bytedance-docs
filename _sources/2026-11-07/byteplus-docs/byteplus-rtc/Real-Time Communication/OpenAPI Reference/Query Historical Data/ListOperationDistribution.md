---
title: "ListOperationDistribution"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-163727"
---

You can call the `ListOperationDistribution` interface to query the geographical distribution (first\-level administrative divisions/countries) of your application's offline audio & video call operation quality index data for a specific period.

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ListOperationDistribution&Version=2023\-11\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListOperationDistribution` |Interface name. The value of this interface: `ListOperationDistribution` |
|Version |String |Yes |`2023-11-01` |OpenAPI version. The value of this interface: `2023-11-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2021-07-24T00:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2021-07-26T00:00:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|Indicator |String |Yes |`user_count` |The indicator name. You can query only `user_num`.<br><br>`user_num`means the total number of users during the selected time period. The duplicate user ID will be removed. |
|Dimension |String |Yes |`province` |The query dimensions.<br><br><br>* `province`<br><br>   First\-level administrative divisions within a country such as China's 23 provinces, 5 autonomous regions (Inner Mongolia, Guangxi, Tibet, Ningxia, Xinjiang), 4 municipalities (Beijing, Tianjin, Shanghai, Chongqing), 2 Special Administrative Regions(Hong Kong and Macao), and Taiwan.<br><br>* country |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`user_num` |The indicator name. |
|Dimension |String |`-` |The query dimension. |
|Data |Array of [GetListOperationDistributionData](https://docs.byteplus.com/en/docs/12/14234#getlistoperationdistributiondata) |`-` |The indicators. |


<span id="getlistoperationdistributiondata"></span>
### GetListOperationDistributionData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Value |Double |`666.00` |The number of users during the selected time period. Display only two digits after the decimal point. |
|Proportion |Double |`66.66` |The percentage of users from a province/country in the total number of users. Display only two digits after the decimal point. |
|DistributionName |String |`上海` |The query dimensions |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ListOperationDistribution&Version=2023-11-01
{
    "AppId": "You****pId",
    "StartTime": "2021-07-24T00:00:00+08:00",
    "EndTime": "2021-07-26T00:00:00+08:00",
    "Indicator": "user_count",
    "Dimension": "province"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "Your_****estId",
        "Action": "ListOperationDistribution",
        "Version": "2023-11-01",
        "Service": "rtc",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Name": "user_num",
        "Dimension": "province",
        "Data": [
            {
                "DistributionName": "Shanghai",
                "Value": 666,
                "Proportion": 66.66
            },
            {
                "DistributionName": "Beijing",
                "Value": 123,
                "Proportion": 12.31
            }
        ]
    }
}
```


&nbsp;
