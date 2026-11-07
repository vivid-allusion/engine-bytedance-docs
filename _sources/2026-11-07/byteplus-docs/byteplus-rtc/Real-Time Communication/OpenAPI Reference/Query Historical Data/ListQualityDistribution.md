---
title: "ListQualityDistribution"
product: "BytePlus RTC"
product_code: "byteplus-rtc"
source: "https://docs.byteplus.com/en/docs/byteplus-rtc/docs-163728"
---

You can call this interface to query the offline quality index data of an application's audio & video calls in different dimensions over a period of time.

<span id="usage-scenario"></span>
## Usage scenario

Call `ListQualityDistribution` to track the performance of your App across a range of dimensions, including first\-level administrative divisions, countries, operation systems, and network types.

<span id="requirements"></span>
## Requirements


|Category |Frequency capping |
|---|---|
|Maximum number of queries |* **10** times per minute<br><br>* **60** times per day |
|The furthest queryable time |Last **30** days |
|Maximum time span of single query |**7** days |
|Data Delay |**8** hours |


<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://open.byteplusapi.com?Action=ListQualityDistribution&Version=2020\-12\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Listed below are the parameters specific to this request. For the complete list of public request parameters, see [Request Parameters](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-69828#request-parameters) .

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListQualityDistribution` |Interface name. The value of this interface: `ListQualityDistribution` |
|Version |String |Yes |`2020-12-01` |OpenAPI version. The value of this interface: `2020-12-01` |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|AppId |String |Yes |`You****pId` |The only identifier for your audio & video app |
|StartTime |String |Yes |`2021-07-24T00:00:00+08:00` |Start timestamp for querying in the format of RFC3339 in second |
|EndTime |String |Yes |`2021-07-25T00:00:00+08:00` |End timestamp for querying in the format of RFC3339 in second |
|Indicator |String |Yes |`join_room_success_rate` |The performance indicators. **Choose only one indicator per query.**   For more information about the performance indicators, see [Performance Indicators](https://docs.byteplus.com/en/docs/byteplus-rtc/docs-1167931#performanceindicators). |
|Dimension |String |Yes |`Province` |The query dimensions. **Choose only one dimension per query.** <br><br>&nbsp;<br><br>You can choose from the following dimensions:<br><br><br>* `Country`<br><br>* `OS`: The Operation System.<br><br>   Include: `android`, `ios`, `macos`, `windows`, and `linux`.\- `Access`: The network type, including `2g`, `3g`, `4g`, `5g`, and `wifi`. |
|ProductType |String |No |`native` |Product type. You can choose from the followings:\- `native`: For mobile device and PC, including Android, iOS, Linux, Mac, and Windows.<br><br><br>* `web`: For browsers<br><br>   The default value is `native`. |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Indicators |Array of [Indicator](https://docs.byteplus.com/en/docs/12/14235#indicator) |`-` |The indicator name. |


<span id="indicator"></span>
### Indicator


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`5s_join_room_success_rate` |The indicator name. |
|Data |Array of [DistributionData](https://docs.byteplus.com/en/docs/12/14235#distributiondata) |`-` | |


<span id="distributiondata"></span>
### DistributionData


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TimeStamp |String |`2022-12-12T14:00:30+08:00` |The start time of your query. Use the RFC 3339 format. |
|Dimension |String |`windows` |The query dimension. |
|Value |Double |`99.06` |The indicator data. Display only two digits after the decimal point. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://open.byteplusapi.com?Action=ListQualityDistribution&Version=2020-12-01
{
    "AppId": "You****pId",
    "StartTime": "2022-12-09T00:00:00+08:00",
    "EndTime": "2022-12-10T00:00:00+08:00",
    "Indicator": "stall_rate",
    "ProductType": "native",
    "Dimension": "Country"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata":{
        "RequestId":"Your_RequestId",
        "Action":"ListQualityDistribution",
        "Version":"2020-12-01",
        "Service":"rtc",
        "Region":"ap-singapore-1"
    },
    "Result":{
       "Indicators": [
                "Name": "80ms_audio_stall_rate",
                "Data": [
                    {
                        "TimeStamp": "2022-12-09T00:00:00+08:00",
                        "Value": 0.54,
                        "Dimension": "China"
                    },
                    {
                        "TimeStamp": "2022-12-09T00:00:00+08:00",
                        "Value": 0.43,
                        "Dimension": "Denmark"
                    },
                    {
                        "TimeStamp": "2022-12-10T00:00:00+08:00",
                        "Value": 0.52,
                        "Dimension": "China"
                    },
                    {
                        "TimeStamp": "2022-12-10T00:00:00+08:00",
                        "Value": 0.38,
                        "Dimension": "Denmark"
                    },
                    
                ]
            },
            {
                "Name": "500ms_video_stall_rate",
                "Data": [
                    {
                        "TimeStamp": "2022-12-09T00:00:00+08:00",
                        "Value": 0.45,
                        "Dimension": "China"
                    },
                    {
                        "TimeStamp": "2022-12-09T00:00:00+08:00",
                        "Value": 0.47,
                        "Dimension": "Denmark"
                    },
                    {
                        "TimeStamp": "2022-12-10T00:00:00+08:00",
                        "Value": 0.62,
                        "Dimension": "China"
                    },
                    {
                        "TimeStamp": "2022-12-10T00:00:00+08:00",
                        "Value": 0.37,
                        "Dimension": "Denmark"
                    },
                ]
            }
        ]
    }
}
```


&nbsp;
