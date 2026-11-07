---
title: "GetDependencyInstallTaskStatus"
product: "Function Service"
product_code: "faas"
source: "https://docs.byteplus.com/en/docs/faas/GetDependencyInstallTaskStatus"
---

Viewing the status of dependency installation tasks.

<span id=".6K-35rGC6K-05piO"></span>
## Request description


* Request method: POST

* Request URL: http://open.volcengineapi.com/?Action=GetDependencyInstallTaskStatus&Version=2024\-06\-06


<span id=".6LCD6K-V"></span>
## Debugging

[去调试](https://api.byteplus.com/api-explorer/debug?action=GetDependencyInstallTaskStatus&serviceCode=vefaas&version=2024-06-06&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters


|**Parameter** |**Type** |**Required** |**Sample value** |**Description** |
|---|---|---|---|---|
|Action |String |Yes |GetDependencyInstallTaskStatus |Interface name. The name of the current API is `GetDependencyInstallTaskStatus`. |
|Version |String |Yes |2024\-06\-06 |Interface version. The current version of the API is `2024-06-06 `. |
|FunctionId |String |Yes |wrwsk\*\*\*\* |Function ID. |


<span id=".6K-35rGC56S65L6L"></span>
## Sample requests

```JSON
POST http://open.volcengineapi.com/?Action=GetDependencyInstallTaskStatus&Version=2024-06-06 HTTP/1.1
Content-Type: application/json
{
    "FunctionId": "wrwsk****"
}
```


<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters


|**Parameter** |**Type** |**Sample value** |**Description** |
|---|---|---|---|
|FunctionId |String |wrwsk\*\*\*\* |Function ID. |
|Status |String |InProgress |The status of a task. Possible values are as follows:<br><br><br>* `Enqueued`: The task is in the processing queue.<br><br>* `Dequeued`: The task is removed from the processing queue.<br><br>* `InProgress`: The task is currently being processed.<br><br>* `Canceling/Canceled`: In the process of canceling the task, or the task is already canceled.<br><br>* `Timeout`: Timeout occurred during the task.<br><br>* `Failed`: Failure occurred during the task.<br><br>* `Succeeded`: The task succeeded. |
|CreateTime |String |2020\-05\-20T13:00:55Z |The time when the task is created. |
|FinishTime |String |2020\-05\-20T13:00:55Z |The end time of the task. The task is considered ended if any of the following status is returned.<br><br><br>* `Canceled`: The task is canceled.<br><br>* `Timeout`: Timeout occurred during the task.<br><br>* `Failed`: Failure occurred during the task.<br><br>* `Succeeded`: The task succeeded. |


<span id=".6L-U5Zue56S65L6L"></span>
## Sample responses

```JSON
HTTP/1.1 200 OK
Content-Type: application/json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "GetDependencyInstallTaskStatus",
        "Version": "2024-06-06",
        "Service": "vefaas",
        "Region": "cn-beijing"
    },
    "Result": {
        "FunctionId": "wrwsk****",
        "Status": "InProgress",
        "CreateTime": "2020-05-20T13:00:55Z",
        "FinishTime": "2020-05-20T13:00:55Z"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

There is no error code dedicated to this interface currently. If you encounter an exception when calling the interface, you can refer to [Public error codes](https://docs.byteplus.com/en/docs/faas/Public_error_code) for troubleshooting.
