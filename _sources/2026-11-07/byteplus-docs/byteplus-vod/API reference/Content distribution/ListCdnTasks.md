---
title: "ListCdnTasks"
product: "BytePlus Video on Demand"
product_code: "byteplus-vod"
source: "https://docs.byteplus.com/en/docs/byteplus-vod/reference-listcdntasks"
---

This interface is used to obtain the list of refresh preheat tasks in the specified space.

<span id="http-request"></span>
## HTTP request

Endpoint: https://vod.byteplusapi.com?Action=ListCdnTasks&Version=2023\-01\-01

<span id="request-parameters"></span>
## Request parameters

All APIs must be called with the [common parameters](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#request-structure) in addition to API\-specific parameters.


|Parameter |Data Type |Required |Sample Value |Description |
|---|---|---|---|---|
|Action |String |Yes |`ListCdnTasks` |The API action. For the current API, the value is `ListCdnTasks`. |
|Version |String |Yes |`2023-01-01` |The API version. For the current API, the value is `2023-01-01`. |
|SpaceName |String |Yes |`test` |The VOD space name. You can obtain the space name through the following methods:<br><br><br>* View the names of all spaces under the current account on the [Space](https://console.byteplus.com/vodpaas/overview/?) of the BytePlus VOD console.<br><br>* Call the [ListSpace](https://docs.byteplus.com/en/docs/byteplus-vod/reference-listspace) interface to obtain the names of all spaces under the current account. |
|TaskId |String |No |`6242b6d******4e9451a3cff` |The task ID. Only supports query for a single ID. |
|DomainName |String |No |`example.vod.com` |The domain name. It only supports a single query. |
|TaskType |String |No |`refresh_file` |The task type. The values are as follows:<br><br><br>* `refresh_file`: The URL refresh.<br><br>* `refresh_dir`: The directory refresh.<br><br>* `preload`: The URL preloading. |
|Status |String |No |`complete` |The task status. Separate multiple statuses with a comma `,`. Possible values are as follows:<br><br><br>* `complete`: Execution successful.<br><br>* `running`: Executing.<br><br>* `failed`: Execution failed. |
|StartTimestamp |Integer |No |`1703433600` |The start time. The number of seconds elapsed since UTC 1970\-01\-01 to the current time. If not specified, it defaults to 00:00:00 on the current day.<br><br><div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="tip">Only data from the past 7 days can be queried.</div><br> |
|EndTimestamp |Integer |No |`1703519999` |The end time. The number of seconds elapsed since UTC 1970\-01\-01 to the current time. If not provided, the default is 23:59:59 of the current day. |
|PageNum |Integer |No |`1` |The page number. Default is 1. The range is greater than or equal to 1. |
|PageSize |Integer |No |`10` |The page size. The number of entries displayed per page. Default is 10. The value range is no greater than 50. |


#{.custom\-md\-table\-5}#

<span id="response-parameters"></span>
## Response parameters

For unique API\-specific response parameters, see the table below. For more details, refer to the [Response](https://docs.byteplus.com/en/docs/byteplus-vod/reference-introduction#response) section.


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|TotalCount |Integer |`1` |The total number of records. |
|PageNum |Integer |`1` |The page number. |
|PageSize |Integer |`1` |The page size. |
|ContentInfos |Array of [ContentInfo](https://docs.byteplus.com/en/docs/25/8051#contentinfo) |`-` |The task record list. |


#{.custom\-md\-table\-4}#

<span id="contentinfo"></span>
### ContentInfo


|Parameter |Data Type |Sample Value |Description |
|---|---|---|---|
|ItemId |String |`ItemId` |The record ID. It can be empty. |
|Url |String |`Url` |The task URL. |
|Status |String |`complete` |The task status. The possible values are as follows:<br><br><br>* `complete`: Execution successful.<br><br>* `running`: In execution.<br><br>* `failed`: Execution failed. |
|TaskType |String |`refresh_file` |The task type. Possible values are as follows:<br><br><br>* `refresh_file`: URL refresh.<br><br>* `refresh_dir`: Directory refresh.<br><br>* `preload`: URL preloading. |
|CreateTimestamp |Integer |`1` |The task creation time. The unit is Unix seconds timestamp. |
|TaskId |String |`TaskId` |The task ID. |
|Message |String | |The task information. |


#{.custom\-md\-table\-4}#

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
https://vod.byteplusapi.com?Action=ListCdnTasks&Version=2023-01-01&SpaceName=test&TaskId=6242b6d******4e9451a3cff&DomainName=example.vod.com&TaskType=refresh_file&Status=complete&StartTimestamp=1703433600&EndTimestamp=1703519999&PageNum=1&PageSize=10
```


<span id="sample-response"></span>
### Sample response

```json
{ 
    "ResponseMetadata": 
    { 
        "RequestId": "202412240414526BE29DC31444A6C6ED51", 
        "Action": "ListCDNTasks", 
        "Version": "2023-01-01", 
        "Service": "vod", 
        "Region": "ap-singapore-1" 
    }, 
        "Result": 
         { "TotalCount": 1, 
        "PageNum": 1, 
        "PageSize": 10, 
        "ContentInfos": [ 
            { "ItemId": "e2517b7c643b376ad356d780e183f1f6", 
            "Url": "http://vod.example-test.com/a.mp4", 
            "Status": "complete", 
            "TaskType": "refresh_file", 
            "CreateTimestamp": 1735013647, 
            "TaskId": "refresh_url_fccf35a0d6d34f6294d7b62476cc4188565336ac9ab1c2bd" 
            }
            ] 
        } 
}
```


<span id="error-codes"></span>
## Error codes

The following are the error codes related to the current operation. For other error codes, see the [shared errors of BytePlus VOD](https://docs.byteplus.com/en/docs/byteplus-vod/reference-common-error-codes).


|Status Code |Error Code |Error Message |Description |
|---|---|---|---|
|400 |InvalidParameter.InvalidSpaceName |\- |The invalid SpaceName. |


#{.custom\-md\-table\-4}#

&nbsp;
