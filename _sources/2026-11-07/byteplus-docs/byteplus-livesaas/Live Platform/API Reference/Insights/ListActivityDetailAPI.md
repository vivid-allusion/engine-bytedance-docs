---
title: "ListActivityDetailAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivitydetailapi"
---

Call this API to get key metrics such as total live duration, average watch time, unique viewers (UV), and peak concurrent users (PCU) for specific live rooms within a given time range.

<span id="0d7f64af"></span>
## Requirements


* Quota: 100 queries per minute per account

* Data latency: 5 minutes


<span id="f713d23f"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListActivityDetailAPI&Version=2020-06-01`

* Method: GET


<span id="3442b2a9"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="0a89855a"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListActivityDetailAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="0aee7785"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNumber |Integer |No |`1` |The page number to return.<br><br>Default value: `1`.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This API operation supports returning at most 10,000 results, which means <code>PageNumber</code> × <code>PageSize</code> must be less than or equal to 10,000.</div><br> |
|PageSize |Integer |No |`10` |The number of results to return on each page.<br><br>Default value: `10`.<br><br>Value range: [1,100]<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">This API operation supports returning at most 10,000 results, which means <code>PageNumber</code> × <code>PageSize</code> must be less than or equal to 10,000.</div><br> |
|SortMode |String |No |`desc` |The sort order.<br><br>Default value: `desc`.<br><br>Valid values:<br><br><br>* `asc`: In ascending order.<br><br>* `desc`: In descending order. |
|SortField |String |No |`LiveTime` |Specifies the dimension by which to sort the data.<br><br>Default value: `LiveTime`.<br><br>Valid values:<br><br><br>* `LiveTime`: The live stream time of the live room, which may not be the time the live stream actually starts.<br><br>* `LiveDuration`: The total live duration of the live room.<br><br>* `PCU`: The number of peak concurrent visitors of the live room.<br><br>* `UV`: The number of unique viewers or visitors of the live room.<br><br>* `PV`: The number of total views or visits of the live room.<br><br>* `CommentCount`: The number of comments in the live room.<br><br>* `WatchDurationPerPeople`: The average watch or visit duration for the live room. |
|ActivityName |String |No |`Live room A` |Filters for live rooms whose names contain this value. |
|StartLiveTime |Long |Yes |`1692339016` |The start time of the time range in Unix timestamp format. Unit: seconds.<br><br>Data from this time range will be returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The time range cannot exceed 365 days (31,536,000 seconds).</div><br> |
|EndLiveTime |Long |Yes |`1700115016` |The end time of the time range in Unix timestamp format. Unit: seconds.<br><br>Data from this time range will be returned.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">The time range cannot exceed 365 days (31,536,000 seconds).</div><br> |
|PlayStatus |Integer |Yes |`11` |Specifies what data is to be returned. Valid values:<br><br><br>* `1`: Returns data generated while the live room is in the "Live" status.<br><br>* `2`: Returns data generated while the live room is in the "Preview" status, even if no preview is playing on the viewing page.<br><br>* `3`: Returns data generated while the live room is in the "Playback" status, even if no playback is playing on the viewing page.<br><br>* `10`: Data generated when your live room is in the **Live**, **Preview**, **Playback**, or **Over** status is returned, even if no preview or playback is playing on the viewing page.<br><br>* `11`: Data generated when your live room is in the **Live**, **Preview**, or **Playback** status is returned, even if no preview or playback is playing on the viewing page.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If the value is <code>1</code>, <code>2</code>, <code>3</code>, or <code>11</code>, the total views, unique viewers, average watch time, and total watch time are returned. If the value is <code>10</code>, the total visits, unique visitors, average visit duration, and total visit duration are returned.</div><br> |


<span id="c24c437f"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNumber |Integer |`1` |The returned page number. |
|PageSize |Integer |`10` |The number of results returned on each page. |
|TotalCount |Integer |`1` |The total number of matching results found. |
|Activities |Array of [Activities](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivitydetailapi#305f7323) |`-` |The data for the returned live rooms. |


<span id="305f7323"></span>
### Activities


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`17218346****` |The activity ID of the live room. |
|ActivityName |String |`Live room A` |The name of the live room. |
|LiveTime |Long |`1692559016` |The scheduled start time of the live stream in Unix timestamp format. Unit: seconds.<br><br>This may differ from the actual start time. |
|LiveDuration |Long |`899` |The total live duration. Unit: seconds. |
|PV |Long |`412` |The total views or visits.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">If a viewer or visitor refreshes the viewing page once, the number of views or visits increases by 1.</div><br> |
|UV |Long |`286` |The unique viewers or visitors.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Devices with identical device IDs are considered the same device, and viewers or visitors who use the same device are counted as one person.</div><br> |
|PCU |Long |`47` |The peak concurrent visitors.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Devices with identical device IDs are considered the same device, and visitors who use the same device are regarded as one person.</div><br> |
|CommentCount |Long |`403` |The number of comments sent by the host, viewers, and guests in the live room, including deleted comments and comments under review. |
|WatchDurationPerPeople |Long |`476` |The average watch or visit duration. Unit: minutes. |
|ViewDurationTotal |Long |`800` |The total watch or visit duration. Unit: minutes. |


<span id="c97117a2"></span>
## Samples

<span id="38c2a2ea"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=ListActivityDetailAPI&Version=2020-06-01&StartLiveTime=1692339016&EndLiveTime=1700115016
```


<span id="ae83324e"></span>
### Sample response

```JSON
{
    "ResponseMetadata": {
        "Action": "ListActivityDetailAPI",
        "Region": "ap-singapore-1",
        "RequestId": "202201201826170101501312091D1C09D2",
        "Service": "livesaas",
        "SystemTime": 1700125016,
        "Version": "2020-06-01"
    },
    "Result": {
        "Activities": [
          {
            "ActivityId": 17218346****,
            "ActivityName": "Live room A",
            "LiveTime": 1692559016,
            "LiveDuration": 899,
            "PV": 412,
            "UV": 286,
            "PCU": 47,
            "WatchDurationPerPeople": 476,
            "ViewDurationTotal": 800,
            "CommentCount": 403
          }
        ],
        "TotalCount": 1,
        "PageSize": 10,
        "PageNumber": 1
  }
}
```


<span id="fa56be7f"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
