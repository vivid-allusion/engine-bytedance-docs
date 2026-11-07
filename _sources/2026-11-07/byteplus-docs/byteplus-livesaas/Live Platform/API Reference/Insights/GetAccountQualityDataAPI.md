---
title: "GetAccountQualityDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccountqualitydataapi"
---

Call this API to gets the data on the live streaming quality of all the live rooms under your BytePlus account in a specific time range.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note that you can currently only get data from applications integrated with the iOS/Android Viewer SDK.</div>


<span id="a5fecde7"></span>
## Requirements


* Quota: 120 queries per minute per account

* Prerequisite: A BytePlus account or an IAM user with the super administrator role. For more information, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="57b1847f"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetAccountQualityDataAPI&Version=2023-08-01`

* Method: GET


<span id="0659ac9b"></span>
## Request parameters

Not all shared request parameters are included in the following table. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="21812e6d"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetAccountQualityDataAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|BeginTime |Long |Yes |`1702263015` |The start time of the query time range in Unix timestamp format. Unit: seconds. |
|EndTime |Long |Yes |`1702264015` |The end time of the query time range in Unix timestamp format. Unit: seconds. |


<span id="154a269b"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|AccountData |Object of [AccountData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getaccountqualitydataapi#638706eb) |`-` |The data on the live streaming quality of all the live rooms under your BytePlus account in the specified time range. |


<span id="638706eb"></span>
### AccountData


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PullSuccessRate |Double |`100` |The pull success rate. This is the percentage of successful stream plays on viewer devices. This metric measures the probability of viewers successfully pulling the stream.<br><br>Calculation: Pull success rate = (Total successful plays for all live rooms / Total play attempts for all live rooms) \* 100% |
|StallTimePer100Sec |Double |`0` |The stall time per 100 seconds. This metric indicates the duration of video stalls for every 100 seconds of playback time in a live stream. Unit: seconds.<br><br>This metric measures the severity of video stalls during playback.<br><br>Calculation: Stall time per 100 seconds = (Total stall duration for all live rooms / Total playback duration for all live rooms) \* 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the time interval between the rendered video frame and the previous rendered video frame exceeds 200 ms, the interval is added to the duration of video freezing. Continuous monitoring and optimization of this metric can enhance the smoothness of video playing and improve user experience.</div><br> |
|FirstFrameTime |Double |`0` |The average time to first frame per viewer under your BytePlus account, indicating the time from the launch of the live video player to the display of the first video frame on the screen during a live stream. Unit: milliseconds.<br><br>This metric measures how long viewers wait for a live video to start playing.<br><br>Calculation method:<br><br><br>* Time to first frame for a viewer = Timestamp of first frame displayed \- Timestamp player launch<br><br>* Average time to first frame = Total time to first frame for all viewers in all live rooms under your BytePlus account / Total number of viewers for all live rooms under your BytePlus account |


<span id="276bff99"></span>
## Samples

<span id="0c1dde7c"></span>
### Sample request

```JSON
Get https://livesaas.byteplusapi.com/?Action=GetAccountQualityDataAPI&Version=2023-08-01&BeginTime=1702263015&EndTime=1702264015
```


<span id="7238a117"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetAccountQualityDataAPI", 
        "Version": "2023-08-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1703347287 
    }, 
   "Result": {
        "AccountData": {
            "PullSuccessRate": 100,
            "StallTimePer100Sec": 0,
            "FirstFrameTime": 0
        }
    }
}
```


<span id="63ff57ff"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).


|Name |Message |Solution |
|---|---|---|
|100000 |Internal error. |Contact technical support. |
|100005 |The specified parameter BeginTime is invalid. |Change the `BeginTime` value. |
|100005 |The EndTime cannot be equal to or earlier than the BeginTime. |Change the `EndTime` value. |
|100005 |The time interval between BeginTime and EndTime cannot be less than 1 minute. |Check and change the `BeginTime` and `EndTime` values. |
|100005 |The time interval between BeginTime and EndTime cannot be more than 365 days. |Check and change the `BeginTime` and `EndTime` values. |
|100005 |The time interval between BeginTime and EndTime cannot be set to over 365 days ago. |Check and change the `BeginTime` and `EndTime` values. |
