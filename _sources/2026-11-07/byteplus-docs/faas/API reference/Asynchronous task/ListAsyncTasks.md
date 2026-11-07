---
title: "ListAsyncTasks"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/ListAsyncTasks"
---

Obtain a list of asynchronous tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://vefaas.ap\-southeast\-1.byteplusapi.com/?Action=ListAsyncTasks&Version=2024\-06\-06


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Require or Not** |**sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |ListAsyncTasks |Interface name. The name of the API is `ListAsyncTasks`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06`. |
|FunctionId |String |Yes |wrw\*\*\*\*\*\* |Function ID.<br><br>You can call the [ListFunctions](https://docs.byteplus.com/en/docs/faas/ListFunctions) interface to obtain function ID (`Items.Id`). |
|Filter |Object of [ListAsyncTasksFilter](https://docs.byteplus.com/en/docs/192/65923#listasynctasksfilter) |No |\- |Filter conditions for querying asynchronous tasks. |
|OrderBy |Object of [OrderBy](https://docs.byteplus.com/en/docs/192/65923#orderby) |No |\- |Parameter configuration for sorting the asynchronous tasks that have been queried. |
|PageNumber |Integer |No |1 |The starting page number for paginated queries. The default value is 1. |
|PageSize |Integer |No |20 |Number of records displayed per page in paginated queries. Available values:<br><br><br>* Minimum value: 1<br><br>* Maximum value: 100<br><br>* Default value: 20 |


<span id="listasynctasksfilter"></span>
### ListAsyncTasksFilter


|**Parameter** |**Type** |**Require or Not** |**Sample value** |**Description** |
|---|---|---|---|---|
|Status |Array of String |No |["Pending", "Running", "Succeeded", "Failed", "Terminated", "Unknown"] |Task status. Available values:<br><br><br>* **Pending**: The task is waiting to be executed.<br><br>* **Running**: The task is in progress.<br><br>* **Succeeded**: The task has been executed successfully.<br><br>* **Failed**: Task execution failed.<br><br>* **Terminated**: The task has been terminated.<br><br>* **Unknown**: An unknown error occurred.<br><br><br><div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div><br><br><br><div data-tips="true" data-tips-type="default">Multiple statuses are allowed in a request with half\-width commas as separators (,).<code>,</code> </div><br> |
|RequestId |String |No |634f6fbf\-e7fa\-4d87\-85e3\-\*\*\*\*\*\* |ID of the task to be queried. This parameter is used to query the status of a single task.<br><br>Task IDs can be found by going to [Function Service console](https://console.byteplus.com/vefaas), selecting "Function" in the left navigation bar and clicking the function name to open the details page, and then going to **Asynchronous task** tab. |
|SubmitTimeBegin |Long |No |1751853600 |Filter by the time range in which tasks were submitted. Set the start time of the time range:<br><br><br>* Format: Unix timestamp.<br><br>* Unit: second. |
|SubmitTimeEnd |Long |No |1752458400 |Filter by the time range in which tasks were submitted. Set the end time of the time range:<br><br><br>* Format: Unix timestamp:<br><br>* Unit: second. |


<span id="orderby"></span>
### OrderBy


|**Parameter** |**Type** |**Require or Not** |**Sample value** |**Description** |
|---|---|---|---|---|
|Key |String |Yes |SubmitTime |The sorting keys for the task list. Available values:<br><br><br>* **SubmitTime**: Sort by task submission time.<br><br><br><div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div><br><br><br><div data-tips="true" data-tips-type="warning">The parameter <strong>Key</strong> is required in <strong>OrderBy</strong>, <strong> </strong> </div><br> |
|Ascend |Boolean |No |true |Specify the order direction of the returned task list. Available values:<br><br><br>* **false**: (default) descending order<br><br>* **true**: ascending order |


<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```json
POST http://vefaas.ap-southeast-1.byteplusapi.com/?Action=ListAsyncTasks&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrw******",
    "Filter": {
        "Statuses": [
            "Pending",
            "Running",
            "Succeeded",
            "Failed",
            "Terminated",
            "Unknown"
        ],
        "RequestId": "634f6fbf-e7fa-4d87-85e3-******",
        "SubmitTimeEnd": 1752458400,
        "SubmitTimeBegin": 1751853600
    },
    "OrderBy": {
        "Key": "SubmitTime",
        "Ascend": true
    },
    "PageNumber": 1,
    "PageSize": 20
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Items |Array of [AsyncTask](https://docs.byteplus.com/en/docs/192/65923#asynctask) |\- |Task list. |
|Total |Integer |1,000 |Number of tasks. |


<span id="asynctask"></span>
### AsyncTask


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|Status |String |Succeeded |Task status. |
|RequestId |String |634f6fbf\-e7fa\-4d87\-85e3\-\*\*\*\*\*\* |Task ID. |
|SubmitTime |String |2025\-07\-10 11:42:08.575 +0000 UTC |Task submission time. |
|EndTime |String |2025\-07\-10 11:44:08.579 +0000 UTC |Task end time. |
|ExecutionRecords |Array of [ExecutionRecord](https://docs.byteplus.com/en/docs/192/65923#executionrecord) |\- |Task execution records. |


<span id="executionrecord"></span>
### ExecutionRecord


|**Parameter** |**Type** |**sample value** |**Description** |
|---|---|---|---|
|Status |String |Succeeded |Execution status of a single task. |
|Command |String |./run.sh |Commands executed in the task. |
|StartTime |String |2025\-07\-10 11:42:08.575 +0000 UTC |Start time of a single task. |
|EndTime |String |2025\-07\-10 11:44:08.579 +0000 UTC |End time of a single task. |
|ErrorMessage |String |error executing command ./dummy_run.sh: exit status 127, please check the logs for more details |The error message of the task. |
|InstanceName |String |wrwskdhbd\-vd9qztck6t\-\*\*\*\*\*\* |The instance name of the task. |
|RevisionNumber |Integer |1 |The instance version of the task. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "ListAsyncTasks",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "Items": [
            {
                "Status": "Succeeded",
                "EndTime": "2025-07-10 11:44:08.579 +0000 UTC",
                "RequestId": "634f6fbf-e7fa-4d87-85e3-8b085944a71b",
                "SubmitTime": "2025-07-10 11:42:08.575 +0000 UTC",
                "ExecutionRecords": [
                    {
                        "Status": "Succeeded",
                        "Command": "./run.sh",
                        "StartTime": "2025-07-10 11:42:08.575 +0000 UTC",
                        "EndTime": "2025-07-10 11:44:08.579 +0000 UTC",
                        "InstanceName": "wrwskdhbd-vd9qztck6t-******",
                        "RevisionNumber": 1
                    }
                ]
            }
        ],
        "Total": 1000
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error code

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [public error code](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
