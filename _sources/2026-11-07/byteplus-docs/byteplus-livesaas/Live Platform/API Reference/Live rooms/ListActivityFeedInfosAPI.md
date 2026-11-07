---
title: "ListActivityFeedInfosAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/listactivityfeedinfosapi"
---

Gets the basic information of all the existing live rooms under your account, including the cover image, virtual popularity, host account, and creation time.

<span id="requirements"></span>
## Requirements

Rate limit: 120 requests per minute per account

<span id="http-request"></span>
## HTTP request


* Method: POST

* Endpoint: https://livesaas.byteplusapi.com/?Action=ListActivityFeedInfosAPI&Version=2023\-08\-01


<span id="request-parameters"></span>
## Request parameters

<span id="common-parameters"></span>
### Common parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="query"></span>
### Query


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListActivityFeedInfosAPI` |API operation. |
|Version |String |Yes |`2023-08-01` |The version of this API operation. Current version: `2023-08-01`. |


<span id="body-parameters"></span>
### Body parameters


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNumber |Integer |No |`1` |The number of the page to return. Default value: `1`. The value must be equal to or greater than 1. |
|PageSize |Integer |No |`10` |The number of results to return on each page. Default value: `10`. Value range: [1,100]. |
|SortBy |String |No |`Status` |The rules for sorting live rooms. Default value: `Status`. If the value you pass is not one of the following, the default value will be used.<br><br>Valid values:<br><br><br>* `Status`: Sort by live room status first, then sort by start time of the live room in descending order within each status.<br><br>* `LiveTime`: Sort by the start time of the live room.<br><br>* `CreateTime`: Sort by the creation time of the live room. |
|SortOrder |String |No |`Desc` |The order of sorting live rooms. Default value: `Asc`. If the value you pass is not one of the following, the default value will be used.<br><br>Valid values:<br><br><br>* `Desc`: Descending order.<br><br>* `Asc`: Ascending order.<br><br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">When the value of <code>SortBy</code> is set to <code>Status</code>, the ascending order of live room status is: Live, Preview, Playback, Over. Regardless of the value of <code>SortOrder</code>, live rooms are sorted by start time in descending order within each status.</div><br> |
|SiteTagNews |Array of [SiteTagNews](https://docs.byteplus.com/en/docs/11/31948#sitetagnews) |No |`-` |Live rooms with any of these category tag values are to be returned.<br><br>You can get the list of category tags by calling [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2). |


<span id="sitetagnews"></span>
### SiteTagNews


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |Array of String |Yes |`["1","2"]` |The category tag values.<br><br>Live rooms with any of these category tag values are to be returned. |
|Name |String |No |`Tag A` |The name of the category tag.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Pass either <code>Name</code> or <code>Index</code>. If both are passed, only the <code>Name</code> takes effect. If neither is passed, the default value of <code>Index</code> is used.</div><br> |
|Index |Integer |No |`0` |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Default value: `0`. Value range: [0,19].<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Pass either <code>Name</code> or <code>Index</code>. If both are passed, only the <code>Name</code> takes effect. If neither is passed, the default value of <code>Index</code> is used.</div><br> |


<span id="response-parameters"></span>
## Response parameters


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNumber |Integer |`1` |The page number of the returned page. |
|PageSize |Integer |`10` |The number of results returned on each page. |
|TotalCount |Integer |`1` |The total number of returned live rooms. |
|List |Array of [List](https://docs.byteplus.com/en/docs/11/31948#list) |`-` |List of returned live rooms. |


<span id="list"></span>
### List


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`181062****058998` |The activity ID of the returned live room. |
|ActivityName |String |`Live room A` |The name of the returned live room. |
|Status |Integer |`2` |The status of the returned live room. Valid values:<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |
|CoverImageUrl |String |`//example.image` |The URL of the returned live room's cover image in landscape mode.<br><br>If the cover image is set via an API call, the URL includes a protocol header. If set via the console, it does not include a protocol header. |
|VerticalCoverImageUrl |String |`//example.image` |The URL of the returned live room's cover image in portrait mode.<br><br>If the cover image is set via an API call, the URL includes a protocol header. If set via the console, it does not include a protocol header. |
|Token |String |`qI****` |The user token in public mode for the Web Viewer SDK.<br><br>When integrating the Web Viewer SDK, set the value of `token` to the current parameter value and the value of `mode` to `1`. |
|VirtualPeopleCount |Integer |`100` |The virtual popularity of the returned live room. |
|HostName |String |`Host A` |The name of the host account. |
|HostAvatarImageUrl |String |`//example.image` |The URL of the host account avatar.<br><br>If the host account avatar is set via an API call, the URL includes a protocol header. If set via the console, it does not include a protocol header. |
|CreateTime |Integer |`1726818793` |The creation time of the returned live room in Unix timestamp format. Unit: seconds. |
|SiteTags |Array of [SiteTags](https://docs.byteplus.com/en/docs/11/31948#sitetags) |`-` |List of category tags in the returned live room. |


<span id="sitetags"></span>
### SiteTags


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag A` |The name of the category tag. |
|Value |String |`1` |The category tag value. |
|Index |Integer |`0` |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Value range: [0,19]. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://livesaas.byteplusapi.com/?Action=ListActivityFeedInfosAPI&Version=2023-08-01
{
    "PageNumber": 1,
    "PageSize": 10,
    "SortBy": "Status",
    "SortOrder": "Desc",
    "SiteTagNews": [
        {
            "Value": [
                "1",
                "2"
            ],
            "Name": "Tag A",
            "Index": 0
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Service": "livesaas",
        "Region": "ap-singapore-1",
        "Action": "ListActivityFeedInfosAPI",
        "Version": "2023-08-01",
        "SystemTime": 1826818793
    },
    "Result": {
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "List": [
            {
                "ActivityId": 181062****058998,
                "ActivityName": "Live room A",
                "Status": 2,
                "CoverImageUrl": "//example.image",
                "VerticalCoverImageUrl": "//example.image",
                "Token": "qI****",
                "VirtualPeopleCount": 100,
                "HostName": "Host A",
                "HostAvatarImageUrl": "//example.image",
                "CreateTime": 1726818793,
                "SiteTags": [
                    {
                        "Name": "Tag A",
                        "Value": "1",
                        "Index": 0
                    }
                ]
            }
        ]
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).

&nbsp;
