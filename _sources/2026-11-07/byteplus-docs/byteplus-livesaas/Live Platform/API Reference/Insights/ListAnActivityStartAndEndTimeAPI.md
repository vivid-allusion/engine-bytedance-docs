---
title: "ListAnActivityStartAndEndTimeAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi"
---

Call this API to get the start and end time of each live stream that has occurred in a specific live room.

<span id="f270d7d5"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="b9c6469a"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListAnActivityStartAndEndTimeAPI&Version=2020-06-01`

* Method: GET


<span id="924137a8"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="70cc26ca"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListAnActivityStartAndEndTimeAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="0b7c1c03"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|StartAndEndTime |Array of [StartAndEndTime](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listanactivitystartandendtimeapi#f3921d52) |`-` |The start and end times for each live stream. |


<span id="f3921d52"></span>
### StartAndEndTime


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|OrderNumber |Integer |`1` |The sequence number of the live stream start time and end time, indicating the order in which they occurred. |
|StartTime |Long |`1625811440` |The Unix timestamp, in seconds, for when the live stream starts. |
|EndTime |Long |`1625811571` |The Unix timestamp, in seconds, for when the live stream ends.<br><br>The value `0` indicates the live stream has not ended. |


<span id="b2bcadd6"></span>
## Samples

<span id="c8a1ed92"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListAnActivityStartAndEndTimeAPI&Version=2020-06-01&ActivityId=17218346****
```


<span id="61b76c18"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202201201826170101501312091D1C09D2",
    "Action": "ListAnActivityStartAndEndTimeAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1656067132
  },
  "Result": {
    "StartAndEndTime": [
      {
        "OrderNumber": 1,
        "StartTime": 1625811440,
        "EndTime": 1625811571
      },
      {
        "OrderNumber": 2,
        "StartTime": 1625811609,
        "EndTime": 1626405481
      },
      {
        "OrderNumber": 3,
        "StartTime": 1626405692,
        "EndTime": 0
      }
    ]
  }
}
```


<span id="5a39ebb7"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
