---
title: "GetAccountDataByTimeIntervalAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getaccountdatabyTimeintervalapi"
---

Call this API to retrieve aggregated data for all live rooms under your BytePlus account within a specified time interval. The returned data includes key metrics such as the total number of live rooms, cumulative views, unique viewers, and total watch duration.

<span id="aa541d6f"></span>
## Requirement


* Quota: 20 queries per minute per account

* Data latency: 1\-3 hours


<span id="a564cbb1"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetAccountDataByTimeIntervalAPI&Version=2020-06-01`

* Method: GET


<span id="8865ec2a"></span>
## Request parameters

Not all shared request parameters are included in the following table. For a complete list, see [Shared request parameters](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-parameters#f1706967).

<span id="8578a4ac"></span>
### **Query**


|**Name** |**Data Type** |**Required** |**Sample Value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |`GetAccountDataByTimeIntervalAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|BeginTime |Long |Yes |`1692339016` |The start time of the time range in Unix timestamp format. Unit: seconds.<br><br>Data for this time range is returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The time range cannot exceed 365 days (31,536,000 seconds).</div><br> |
|EndTime |Long |Yes |`1700115016` |The end time of the time range in Unix timestamp format. Unit: seconds.<br><br>Data for this time range is returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The time range cannot exceed 365 days (31,536,000 seconds).</div><br> |


<span id="124cd05e"></span>
## **Response parameters**


|**Name** |**Data Type** |**Sample Value** |**Description** |
|---|---|---|---|
|EventTimes |Integer |`55` |The total number of live rooms created in the selected time range under your BytePlus account. |
|ViewTime |Integer |`390` |The cumulative number of views for all live rooms in the selected time range under your BytePlus account.<br><br>If a viewer refreshes the viewing page once, the number of views increases by 1. |
|ViewPeople |Integer |`200` |The cumulative number of unique viewers for all live rooms in the selected time range under your BytePlus account. Viewers who use the same device are counted as a single viewer. |
|ViewDuration |Integer |`6000` |The cumulative watch duration for all live rooms in the selected time range under your BytePlus account. Unit: minutes. |
|ViewEventTimesPerPeople |Double |`2` |The average number of live rooms viewed per viewer in the selected time range. This value is calculated by dividing the sum of unique viewers for all live rooms by the cumulative number of unique viewers.<br><br>The numerator (sum of unique viewers for all live rooms) counts a viewer for each room they join. The denominator (cumulative number of unique viewers) counts a viewer only once, regardless of how many rooms they join.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Devices with identical device IDs are considered the same device.</div><br> |
|ViewDurationPerPeople |Double |`30` |The average watch duration per viewer in the selected time range. This value is calculated by dividing the cumulative watch duration by the cumulative number of unique viewers. Unit: minutes. |
|ViewTimesPerPeople |Double |`1.95` |The average number of views per viewer in the selected time range under your BytePlus account, which is calculated as the cumulative views divided by the cumulative unique viewers. |


<span id="02d94806"></span>
## Samples

<span id="43bb91f0"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetAccountDataByTimeIntervalAPI&Version=2020-06-01&BeginTime=1692339016&EndTime=1700115016
```


<span id="74b36b31"></span>
### **Sample response**

```JSON
{
    "ResponseMetadata": {
        "Action": "GetAccountDataByTimeIntervalAPI",
        "Region": "ap-singapore-1",
        "RequestId": "202201201826170101501312091D1C09D2",
        "Service": "livesaas",
        "SystemTime": 1700125016,
        "Version": "2020-06-01"
    },
    "Result": {
        "EventTimes": 55,
        "ViewTime ": 390,
        "ViewPeople": 200,
        "ViewDuration": 6000,
        "ViewEventTimesPerPeople": 2,
        "ViewDurationPerPeople": 30,
        "ViewTimesPerPeople": 1.95
  }
}
```


<span id="6fa7036e"></span>
## Error codes

For a list of shared error codes, see [Shared error and status codes](https://docs.byteplus.com/en/byteplus-livesaas/docs/shared-error-and-status-codes).
