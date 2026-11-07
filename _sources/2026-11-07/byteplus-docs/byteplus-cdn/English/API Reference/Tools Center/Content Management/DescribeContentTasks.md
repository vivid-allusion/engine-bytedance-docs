---
title: "DescribeContentTasks"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describecontenttasks"
---

Obtain purge and prefetch tasks submitted in the past 7 days, broken down to each URL in these tasks. The return results show the details of each task, including the execution result of the task. You can use multiple filtering options to filter the task list.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeContentTasks`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|UrlList |String[] |No |Indicates a list of URLs used to filter the query results to obtain task details for each URL in the list. Each URL must start with `http://` or `https://`.<br><br>This parameter is a string array.<br><br>If you specify `Url` at the same time, `Url` will not take effect. |`["https://www.example.com/1.jpg","https://www.example.com/2.jpg"]` |
|DomainName |String |No |Indicates a domain name used to filter the query results to obtain tasks where the URL contains this domain name. |`www.example.com` |
|TaskID |String |No |Indicates a task ID used to obtain all tasks with this ID. |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |
|TaskType |String |Yes |Indicates a task type used to filter the query results to obtain tasks of this type. The available values for this parameter are:<br><br><br>* `refresh_file`: Indicates a URL Purge task.<br><br>* `refresh_dir`: Indicates a Directory Purge task.<br><br>* `preload`: Indicates a URL Prefetch task.<br><br>* `refresh_regex`: Indicates a RegEx Purge task. |`preload` |
|Status |String |No |Indicates a task status used to filter the query results to obtain tasks in this status. The available values for this parameter are:<br><br><br>* `complete`: Indicates completed tasks.<br><br>* `running`: Indicates tasks in progress.<br><br>* `failed`: Indicates failed tasks.<br><br><br>If this parameter is not specified, the task list will not be filtered by this parameter. |`complete` |
|StartTime |Long |No |Indicates a start time, in Unix timestamp format, to obtain tasks submitted later than or equal to this time. Please note that you cannot query tasks submitted more than 7 days ago.<br><br>You must specify both `StartTime` and `EndTime`, or neither. If neither is specified, tasks submitted in the past 7 days are obtained. |`1641844915` |
|EndTime |Long |No |Indicates an end time, in Unix timestamp format, to obtain tasks submitted earlier than or equal to this time. |`1641845373` |
|PageNum |Long |No |Indicates a page number used to obtain tasks on that page. The default value of this parameter is `1`.<br><br>CDN paginates tasks that meet the filtering conditions. You can calculate the number of pages based on the values of the `Total` and `PageSize` parameters in the response body. |`1` |
|PageSize |Long |No |Indicates the number of tasks contained per page. The value range for this parameter is 1\-1000, and the default value is `50`. |`10` |
|Url |String |No |It is **not recommended** to use this parameter; please use `UrlList` instead.<br><br>The function of this parameter is the same as `UrlList`. When specifying multiple URLs in `Urls`, the URLs must be separated by `\n`.<br><br>If you specify both `UrlList` and `Urls`, only `UrlList` takes effect. |`https://www.example.com/1.jpg\nhttps://www.example.com/2.jpg` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|Total |Long |Indicates the total number of tasks that meet the filtering conditions. |`2` |
|PageNum |Long |Indicates the `PageNum` in the request body. |`1` |
|PageSize |Long |Indicates the `PageSize` in the request body. |`100` |
|Data |Object[] |Indicates the list of URL tasks on `PageNum`. If the page number indicated by `PageNum` does not exist or there are no tasks on that page, the value of this parameter is `null`. | |
|Url |String |Indicates the URL operated on by a task in the list. |`https://www.example.com/1.jpg` |
|Status |String |Indicates the status of the task. This parameter has the following values:<br><br><br>* `complete`: Indicates the task is completed.<br><br>* `running`: Indicates the task is executing.<br><br>* `failed`: Indicates the task execution failed. |`complete` |
|TaskType |String |Indicates the type of the task. This parameter has the following values:<br><br><br>* `refresh_file`: Indicates a URL Purge task.<br><br>* `refresh_dir`: Indicates a Directory Purge task.<br><br>* `preload`: Indicates a URL Prefetch task.<br><br>* `refresh_regex`: Indicates a RegEx Purge task. |`preload` |
|RefreshPrefix |Boolean |Indicates whether the "Purge by Prefix" configuration is present in the task. This parameter is valid only when `TaskType` is `refresh_dir`. This parameter has the following values:<br><br><br>* `true`: Indicates that this configuration is present in the task.<br><br>* `false`: Indicates that this configuration is not present in the task.<br><br><br>If `TaskType` is not `refresh_dir`, the value of this parameter is always `false`. |`true` |
|CreateTime |Long |Indicates the submission time of the task, in Unix timestamp format. |`1601371409` |
|TaskID |String |Indicates the ID of the task. |`prefetch_url_89c25a1aa3044b39921387190fc9b0e438f3d071f278f031` |
|Process |String |Indicates the progress of the task, expressed as a percentage. |`70%` |
|Delete |Boolean |Indicates whether the task specifies deleting files in the cache. This parameter is valid only when `TaskType` is `refresh_dir`. This parameter has the following values:<br><br><br>* `true`: Indicates deleting files in the cache.<br><br>* `false`: Indicates not deleting files in the cache, only marking them as expired.<br><br><br>When `TaskType` is not `refresh_dir`, the value of `Delete` is always `false`. |`false` |
|Remark |String |* If `Status` is `failed` and CDN can identify the issue, this parameter records the reason for the task failure.<br><br>* In other cases, the value of this parameter is empty (""). |`origin_error` |
|StatusCode |Long |* If `Remark` is not empty (""), this parameter value indicates the origin server's response status code. The status code is 4xx or 5xx.<br><br>* If `Remark` is empty (""), this parameter will not appear. | |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeContentTasks&Version=2021-03-01
{
    "StartTime": 1625587200,
    "EndTime": 1625673600,
    "TaskType": "preload",
    "PageSize": 10,
    "PageNum": 1
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202406301133492C6A5B1ABB315058A120",
        "Action": "DescribeContentTasks",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "Data": [
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "origin_error",
                "Status": "failed",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/2.txt"
            },
            {
                "CreateTime": 1719738505,
                "Process": "100%",
                "Remark": "",
                "Status": "complete",
                "TaskID": "prefetch_url_3ed013a15c0f47258ed8feff3700f7396222fb893dade871",
                "TaskType": "preload",
                "Url": "https://www.example.com/1.txt"
            }
        ],
        "PageNum": 1,
        "PageSize": 50,
        "Total": 2
    }
}
```


&nbsp;
