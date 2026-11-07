---
title: "ListActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-listactivityapi"
---

Gets the basic information of all the existing live rooms under your account.

This API operation can return up to 10,000 of the most recent live rooms. You can configure conditions such as the room status (`Status`) and live stream time (`LiveTime`) to refine the search.

<span id="requirement"></span>
## Requirement

Rate limit: 120 requests per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=ListActivityAPI&Version=2020-06-01`

* Method: POST


<span id="request-parameters"></span>
## Request parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListActivityAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of the API operation. The value for this operation is `2020-06-01`. |


<span id="body"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|PageNo |Integer |No |`1` |The number of the page to return. Default value: `1`.<br><br>This API operation supports returning at most 10,000 results, which means `PageNo` × `PageItemCount` must be less than or equal to 10,000. |
|PageItemCount |Integer |No |`10` |The number of results to return on each page. Default value: `10`.<br><br>This API operation supports returning at most 10,000 results, which means `PageNo` × `PageItemCount` must be less than or equal to 10,000. |
|Name |String |No |`Live Room A` |Returns live rooms whose names contain this value.<br><br>For example, if the parameter value is `Live Room A`, live rooms that contain the keyword Live Room A in their names are returned, such as Live Room ABC, Live Room a, and live room ab. |
|Status |Integer |No |`0` |Returns live rooms with the specified status.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: All.<br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over.<br><br><br>Over is a status when a live stream has ended but no playback is released to the viewing page. |
|LiveTime |Long |No |`1680193976` |The live stream time in Unix timestamp format. Unit: seconds.<br><br>Returns live rooms whose live stream time is at or after this value.<br><br>This time may not be the time the live stream actually starts. |
|IsLockPreview |Integer |No |`0` |Specifies whether to return live rooms whose previews are locked. Default value: `0`.<br><br>Valid values:<br><br><br>* `-1`: Returns all live rooms.<br><br>* `0`: Returns live rooms whose previews are not locked.<br><br>* `1`: Returns live rooms whose previews are locked. |
|SiteTagNews |Array of [SiteTagNews](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |No |`-` |Returns live rooms with any of these category tag values.<br><br>You can get the list of category tags by calling [ListSiteTagAPIV2](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listsitetagapiv2). |
|HostAccountId |Integer |No |`112038` |The ID of the host account.<br><br>Returns live rooms associated with this host account.<br><br>You can get the ID by calling [GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi). |
|HostAccountName |String |No |`Host A` |The name of the host account. Fuzzy search is supported.<br><br>Returns live rooms associated with this host account.<br><br>You can get the name by calling [GetBusinessAccountInfoAPI](https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getbusinessaccountinfoapi). |
|LiveMode |Integer |No |`0` |Returns live rooms with the specified live stream latency type.<br><br>Default value: `0`.<br><br>Valid values:<br><br><br>* `0`: Both ultra\-low latency and normal latency.<br><br>* `1`: Ultra\-low latency with a latency of 1 to 2 seconds.<br><br>* `2`: Normal latency with a latency of 5 to 10 seconds. |
|SortBy |String |No |`Status` |The rules for sorting live rooms. Default value: `Status`. Valid values:<br><br><br>* `Status`: Sort by live room status first, then sort by start time of the live room in descending order within each status.<br><br>* `LiveTime`: Sort by the start time of the live room.<br><br>* `CreateTime`: Sort by the creation time of the live room. |
|SortOrder |String |No |`Desc` |The order of sorting live rooms. Default value: `Asc`. Valid values:<br><br><br>* `Desc`: Descending order.<br><br>* `Asc`: Ascending order.<br><br><br>When `SortBy` is set to `Status`, results are grouped by status in ascending order (Live, Preview, Playback, Over). Within each group, live rooms are always sorted by start time in descending order, regardless of the `SortOrder` value. |
|FollowerUserName |String |No |`admin@bytedance.com` |The account used to create the live room. By default, live rooms created by all accounts are to be returned. To get live rooms created by the BytePlus account, set the parameter value to `admin@bytedance.com`. To get live rooms created by a specific IAM user, set the parameter value to the account of the IAM user. You can get the account of an IAM user on the **Account center** \> **Authorization** \> **Users** page of the [BytePlus Live console](https://console.byteplus.com/livesaas/accountManagement/userManage). |


<span id="sitetagnews"></span>
#### SiteTagNews


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Value |Array of String |Yes |`["1","2"]` |The category tag values.<br><br>Live rooms with any of these category tag values are to be returned. |
|Name |String |No |`Tag A` |The name of the category tag.<br><br>Specify either `Name` or `Index`. If you provide both, `Name` takes precedence. If you provide neither, the default value of `Index` is used. |
|Index |Integer |No |`0` |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/).<br><br>Default value: `0`. Value range: [0,19].<br><br>Specify either `Name` or `Index`. If you provide both, `Name` takes precedence. If you provide neither, the default value of `Index` is used. |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|PageNo |Integer |`1` |The page number of the returned page. |
|PageItemCount |Integer |`10` |The number of results returned on each page. |
|TotalItemCount |Integer |`1` |The total number of returned live rooms. |
|Activities |Array of [Activities](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |`-` |List of returned live rooms. |


<span id="activities"></span>
### Activities


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |Long |`17218346****` |The activity ID of the returned live room. |
|Name |String |`Live Room A` |The name of the returned live room. |
|Status |Integer |`1` |The status of the returned live room.<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |
|CoverImage |String |`https://p1-live.****.image` |The URL of the returned live room's cover image in landscape mode, which includes the protocol header. |
|CreateTime |Integer |`1680093000` |The time when the returned live room was created in Unix timestamp format. Unit: seconds. |
|ViewUrl |String |`https://live.byteplus.com/7420/******` |The viewing page address of the returned live room. |
|LiveTime |Integer |`1680193976` |The live stream time in Unix timestamp format. Unit: seconds.<br><br>This time may not be the time the live stream actually starts. |
|StreamStartTime |Integer |`1681094000` |The time when the live stream of the returned live room was last pushed in Unix timestamp format. Unit: seconds.<br><br>A value of `0` indicates that the live stream has never been pushed.<br><br>This is the time the live stream actually starts. |
|OnlineStatus |Integer |`-` |Deprecated. |
|IsLockPreview |Integer |`0` |Indicates whether the preview of the returned live room is locked.<br><br><br>* `0`: The preview is not locked.<br><br>* `1`: The preview is locked. |
|SiteTags |Array of [SiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |`-` |List of category tags in the returned live room. |
|TextSiteTags |Array of [TextSiteTags](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi) |`-` |List of text tags in the returned live room. |
|HostAccountId |Integer |`112038` |The ID of the host account that is associated with the returned live room. |
|HostAccountName |String |`Host A` |The name of the host account that is associated with the returned live room. |
|LiveMode |Integer |`0` |The live stream latency type of the returned live room.<br><br><br>* `0`: If a live room was created before BytePlus Live supports the ultra\-low latency feature and does not have the live stream latency type updated, then the parameter value is `0`. In other words, the latency type is normal latency. For more information about the ultra\-low latency feature, see [Ultra-low latency live streaming](https://docs.byteplus.com/docs/byteplus-livesaas/ultra-low-latency-live-streaming).<br><br>* `1`: Ultra\-low latency with a latency of 1 to 2 seconds.<br><br>* `2`: Normal latency with a latency of 5 to 10 seconds. |
|VerticalCoverImage |String |`https://p2-live.xxxx.image` |The URL of the returned live room's cover image in portrait mode, which includes the protocol header. |
|SubAccountName |String |`admin@bytedance.com` |The account used to create the live room. The parameter value `admin@bytedance.com` indicates that the live room is created by the BytePlus account. |


<span id="sitetags"></span>
#### SiteTags


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag A` |The name of the category tag. |
|Value |String |`1` |The category tag value. |
|Index |Integer |`0` |The index of the category tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|DbIndex |Integer |`-` |Deprecated. |
|Show |Integer |`-` |Deprecated. |
|Id |Integer |`-` |Deprecated. |


<span id="textsitetags"></span>
#### TextSiteTags


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Name |String |`Tag B` |The name of the text tag. |
|Value |String |`3` |The text tag value. |
|Index |Integer |`0` |The index of the text tag, which identifies the display order on the [BytePlus Live console](https://console.byteplus.com/livesaas/liveManagement/). |
|DbIndex |Integer |`-` |Deprecated. |
|Show |Integer |`-` |Deprecated. |
|Id |Integer |`-` |Deprecated. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=ListActivityAPI&Version=2020-06-01 
{ 
    "PageNo": 1, 
    "PageItemCount": 10, 
    "SiteTagNews": [ 
            { 
                  "Index": 0, 
                  "Value": ["1","2"] 
            } 
    ]    
} 
```


<span id="sample-response"></span>
### Sample response

```JSON
{
  "ResponseMetadata": {
    "RequestId": "202201201826170101501312091D1C09D2",
    "Action": "ListActivityAPI",
    "Version": "2020-06-01",
    "Service": "livesaas",
    "Region": "ap-singapore-1",
    "SystemTime": 1690293975
  },
  "Result": {
    "PageNo": 1,
    "PageItemCount": 10,
    "TotalItemCount": 1,
    "Activities": [
      {
        "Id": 17218346****,
        "Name": "Live Room A",
        "Status": 1,
        "CoverImage": "https://p1-live.****.image",
        "CreateTime": 1680093000,
        "ViewUrl": "https://live.byteplus.com/7420/******",
        "LiveTime": 1680193976,
        "StreamStartTime": 1681094000,
        "IsLockPreview": 0,
        "SiteTags": [
          {
            "Index": 0,
            "Name": "Tag A",
            "Value": 1,
            "DbIndex": 1,
            "Show": 0,
            "Id": 0
          }
        ],
        "TextSiteTags": [
          {
            "Index": 0,
            "Name": "Tag B",
            "Value": "3",
            "DbIndex": 1,
            "Show": 0,
            "Id": 0
          }
        ],
        "HostAccountId": 112038,
        "HostAccountName": "Host A",
        "LiveMode": 0,  
        "VerticalCoverImage": "https://p2-live.****.image",      
        "OnlineStatus": 0,
        "SubAccountName": "admin@bytedance.com"
      }
    ]
  }
}
```


<span id="error-codes"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
