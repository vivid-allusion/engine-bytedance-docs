---
title: "GetActivityQualityDataAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityqualitydataapi"
---

Call this API to retrieve live streaming quality data for a specific live room within a given time range. The API returns key performance indicators such as pull stream success rate, stall time per 100 seconds, and average time to first frame.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">Note that data is currently available only for applications integrated with the iOS or Android Viewer SDK.</div>


<span id="e2298f63"></span>
## Requirements


* Quota: 120 queries per minute per account

* Prerequisite: A BytePlus account or an IAM user with the Insights \> View only or Edit permission. For more information, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="7e4ac041"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityQualityDataAPI&Version=2023-08-01`

* Method: GET


<span id="ff444339"></span>
## Request parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).

<span id="ef12448c"></span>
### **Query**


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityQualityDataAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |
|BeginTime |Long |Yes |`1702263015` |The start time of the query time range in Unix timestamp format. Unit: seconds. |
|EndTime |Long |Yes |`1702264015` |The end time of the query time range in Unix timestamp format. Unit: seconds. |
|ActivityId |Long |Yes |`17218346****` |The ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="f6c01293"></span>
## **Response parameters**


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|ActivityData |Object of [ActivityData](https://docs.byteplus.com/docs/byteplus-livesaas/docs-getactivityqualitydataapi#ActivityData) |`-` |The data on the live streaming quality of the live room in the specified time range. |


<span id="2f22f87b"></span>
### ActivityData


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|PullSuccessRate |Double |`100` |The pull stream success rate, indicating the percentage of successful stream plays on viewers' devices during a live stream. You can use this metric to measure the probability that viewers can successfully pull the live stream.<br><br>Calculation method: Pull stream success rate = Total number of successful plays in the live room / Total number of plays in the live room x 100% |
|StallTimePer100Sec |Double |`0` |The average duration of video stalls (freezes) for every 100 seconds of playback. Unit: seconds.<br><br>You can use this metric to measure the severity of video freezing when viewers watch live videos.<br><br>Calculation method: Video freezing duration within 100 seconds = Total duration of video freezing during playing for all viewers in the live room / Total play duration for all viewers in the live room x 100<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the time interval between the rendered video frame and the previous rendered video frame exceeds 200 ms, the interval is added to the duration of video freezing. Continuous monitoring and optimization of this metric can improve playback smoothness and improve user experience.</div><br> |
|FirstFrameTime |Double |`0` |The average time from when a viewer starts the player until the first video frame is displayed. Unit: milliseconds.<br><br>You can use this metric to measure the duration viewers need to wait when starting to watch a live video.<br><br>Calculation methods:<br><br><br>* Time to first frame for a viewer = First frame display timestamp \- Player launch timestamp<br><br>* Average time to first frame = Total time to first frame for all viewers in the live room / Total number of viewers in the live room |


<span id="b6cee885"></span>
## Samples

<span id="46cbe5cf"></span>
### Sample request

```JSON
Get https://livesaas.byteplusapi.com/?Action=GetActivityQualityDataAPI&Version=2023-08-01&BeginTime=1702263015&EndTime=1702264015&ActivityId=17218346****
```


<span id="94c93aa4"></span>
### **Sample response**

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetActivityQualityDataAPI", 
        "Version": "2023-08-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1703347287 
    }, 
    "Result": {
        "ActivityData": {
            "PullSuccessRate": 100,
            "StallTimePer100Sec": 0,
            "FirstFrameTime": 0
        }
    }
}
```


<span id="34b6ffdc"></span>
## Error codes

For a list of shared error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).


|**Name** |**Message** |**Solution** |
|---|---|---|
|100000 |Internal error. |Contact technical support for assistance. |
|100001 |The specified parameter ActivityId is invalid. |Change the `ActivityId` value. |
|100005 |The specified parameter BeginTime is invalid. |Change the `BeginTime` value. |
|100005 |The EndTime cannot be equal to or earlier than the BeginTime. |Change the `EndTime` value. |
|100005 |The time interval between BeginTime and EndTime cannot be less than 1 minute. |Check and change the `BeginTime` and `EndTime` values. |
|100005 |The time interval between BeginTime and EndTime cannot be more than 365 days. |Check and change the `BeginTime` and `EndTime` values. |
|100005 |The time interval between BeginTime and EndTime cannot be set to over 365 days ago. |Check and change the `BeginTime` and `EndTime` values. |
