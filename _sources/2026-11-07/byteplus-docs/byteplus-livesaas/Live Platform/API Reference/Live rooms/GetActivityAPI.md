---
title: "GetActivityAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/docs-getactivityapi"
---

Call the GetActivityAPI operation to get the basic information of a live room, such as its status and viewing page address.

<span id="requirement"></span>
## Requirement

Quota: 120 queries per minute per account

<span id="http-request"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01`

* Method: GET


<span id="request-parameters"></span>
## Request parameters

Not all shared request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters).

<span id="query"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetActivityAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |
|ActivityId |Long |Yes |`17218346****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |


<span id="response-parameters"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|Id |Long |`17218346****` |The activity ID of the live room. |
|Name |String |`Live Room A` |The name of the live room. |
|LiveTime |Long |`1642070520` |The start time of the live stream in Unix timestamp format. Unit: seconds.<br><br>This may not be the actual start time of the live stream. |
|IsBeginLiveEnable |Integer |`0` |Indicates whether a scheduled start time is enabled.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. You can only start a live stream after the specified start time. |
|IsAutoEndEnable |Integer |`1` |Indicates whether the stream is configured to end automatically at the specified time.<br><br>Valid values:<br><br><br>* `0`: Disabled.<br><br>* `1`: Enabled. |
|EndTime |Long |`1642170520` |The end time of the live stream in Unix timestamp format. Unit: seconds. |
|CoverImage |String |`//example.image` |The URL of the cover image in landscape mode.<br><br>The URL includes a protocol header if configured via an API call, but not if configured via the console. |
|VerticalCoverImage |String |`//example.image` |The URL of the cover image in portrait mode.<br><br>If not specified, this defaults to the value of `CoverImage`.<br><br>The URL includes a protocol header if configured via an API call, but not if configured via the console. |
|Status |Integer |`2` |The live room status.<br><br>Valid values:<br><br><br>* `1`: Live.<br><br>* `2`: Preview.<br><br>* `3`: Playback.<br><br>* `4`: Over. |
|ViewUrl |String |`https://live.byteplus.com/7420/*******` |The URL of the live room's viewing page. |
|IsPageViewEnable |Integer |`-` |Deprecated. |
|IsLockPreview |Integer |`1` |Indicates whether the preview is locked.<br><br>Valid values:<br><br><br>* `0`: The preview is not locked.<br><br>* `1`: The preview is locked. The viewing page is locked in the **Preview** status and cannot play the live stream or its playback. |
|OwnerSubAccount |String |`admin@bytedance.com` |The account that created the live room. If this value is `admin@example.com`, the live room was created by your main BytePlus account. |
|LiveMode |Integer |`1` |The live stream latency type.<br><br>Valid values:<br><br><br>* `1`: Ultra\-low latency with a latency of 1 to 2 seconds.<br><br>* `2`: Normal latency with a latency of 5 to 10 seconds. |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```JSON
GET https://livesaas.byteplusapi.com/?Action=GetActivityAPI&Version=2020-06-01&ActivityId=17218346****
```


<span id="sample-response"></span>
### Sample response

```JSON
{
    "ResponseMetadata":{
        "RequestId":"202201201826170101501312091D1C09D2",
        "Action":"GetActivityAPI",
        "Version":"2020-06-01",
        "Service":"livesaas",
        "Region":"ap-singapore-1",
        "SystemTime":1632070520
    },
    "Result":{
        "Id":17218346****,      
        "Name":"Live Room A",
        "LiveTime":1642070520,
        "IsBeginLiveEnable": 0,
        "EndTime": 1642170520,
        "IsAutoEndEnable": 1,
        "CoverImage":"//example.image",
        "VerticalCoverImage":"//example.image",
        "Status":2,
        "ViewUrl":"https://live.byteplus.com/7420/*******", 
        "IsPageViewEnable"：1,
        "IsLockPreview":1,  
        "OwnerSubAccount":"admin@bytedance.com",
        "LiveMode":1        
    }
}
```


<span id="error-codes"></span>
## Error codes

For a list of shared error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
