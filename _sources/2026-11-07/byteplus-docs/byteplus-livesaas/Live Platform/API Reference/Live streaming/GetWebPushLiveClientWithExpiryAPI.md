---
title: "GetWebPushLiveClientWithExpiryAPI"
product: "BytePlus Live"
product_code: "byteplus-livesaas"
source: "https://docs.byteplus.com/en/docs/byteplus-livesaas/getwebpushliveclientwithexpiryapi"
---

Call this API to get the URL for the live streaming page of a live room. This allows a host to start a live stream from a web browser without logging in. The returned URL expires after a specified time period.

<span id="88078564"></span>
## Requirement


* Quota: 120 queries per minute per account

* Prerequisite: A BytePlus account or an IAM user with the Live control \> View only or Edit permission. For more information, see [Managing users, organizations, and roles](https://docs.byteplus.com/docs/byteplus-livesaas/docs-managing-iam-users-and-roles).


<span id="d8d3af2c"></span>
## HTTP request


* URL: `https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientWithExpiryAPI&Version=2020-06-01`

* Method: POST


<span id="82b326f4"></span>
## Request parameters

Not all common request parameters are included in the following tables. For a complete list, see [Common request parameters](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-parameters#f1706967).

<span id="3998820f"></span>
### Query


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`GetWebPushLiveClientWithExpiryAPI` |API operation. |
|Version |String |Yes |`2020-06-01` |The version of this API operation. Current version: `2020-06-01`. |


<span id="763ef914"></span>
### Body


|Name |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|ActivityId |Long |Yes |`17218312****` |The activity ID of the live room. You can get the ID by calling [ListActivityAPI](https://docs.byteplus.com/docs/byteplus-livesaas/docs-listactivityapi). |
|ExpiredTime |Long |No |`10` |The expiration time for the URL. The URL becomes invalid after this period.<br><br>Unit: seconds.<br><br>Default value: `10`.<br><br>Value range: [1,300] |


<span id="3bbf0ac3"></span>
## Response parameters


|Name |Data Type |Sample Value |Description |
|---|---|---|---|
|ActivityId |Long |`17218312****` |The activity ID of the live room. |
|Url |String |`https://byteplus-console.byteintl.net/livesaas/webpush/micromode/{activityId}?webpush_token=MXlRdjhuaUF0OGZUQmlMWFNTdFo3ZEZpMXQ3U0kwLzZrR2JpR1BnOUZ3Z253cWJyM0Zub3ZYVzIwdEYvSnh5QlFHSmpkVDJJT3lpcC9yK25vUFlrcXhmYkVSWFBTekNNbUhXNG5KcENvK092aTRhaG8xbHd6VkJZdHRLRWN5cjRvMz****RiSmE0SnE2WHM4MVkrWU9BPT0=` |The URL for the live streaming page. The host can use this URL to start a stream from a web browser without logging in. The URL expires after the specified duration. |


<span id="29a8e2eb"></span>
## Samples

<span id="4bcaf942"></span>
### Sample request

```JSON
POST https://livesaas.byteplusapi.com/?Action=GetWebPushLiveClientWithExpiryAPI&Version=2020-06-01
{
    "ActivityId": 17218312****,
    "ExpiredTime": 10  
}
```


<span id="57c6761e"></span>
### Sample response

```JSON
{ 
    "ResponseMetadata": { 
        "RequestId": "202201201826170101501312091D1C09D2", 
        "Action": "GetWebPushLiveClientWithExpiryAPI", 
        "Version": "2020-06-01", 
        "Service": "livesaas", 
        "Region": "ap-singapore-1", 
        "SystemTime": 1656067132 
    }, 
    "Result": {
        "ActivityId": 17218312****,
        "Url": "https://byteplus-console.byteintl.net/livesaas/webpush/micromode/{activityId}?webpush_token=MXlRdjhuaUF0OGZUQmlMWFNTdFo3ZEZpMXQ3U0kwLzZrR2JpR1BnOUZ3Z253cWJyM0Zub3ZYVzIwdEYvSnh5QlFHSmpkVDJJT3lpcC9yK25vUFlrcXhmYkVSWFBTekNNbUhXNG5KcENvK092aTRhaG8xbHd6VkJZdHRLRWN5cjRvMz****RiSmE0SnE2WHM4MVkrWU9BPT0="
    }
}
```


<span id="6e60f4b7"></span>
## Error codes

For a list of common error codes, see [Common error and status codes](https://docs.byteplus.com/docs/byteplus-livesaas/docs-shared-error-and-status-codes).
