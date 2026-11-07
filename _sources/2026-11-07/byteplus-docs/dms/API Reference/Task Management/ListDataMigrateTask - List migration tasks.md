---
title: "ListDataMigrateTask - List migration tasks"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/ListDataMigrateTask_-_List_migration_tasks"
---

Call the ListDataMigrateTask API to list migration tasks.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Below are the unique request parameters for this API and some common parameters. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|n7cZsm">必选</span> `Example value: ListDataMigrateTask`

Operation to be performed: ListDataMigrateTask.



**Version** <span data-label="purple">string</span> <span data-api-tag="require|tE6Y2N">必选</span>`Example value: 2018-01-01`

API version, value: 2018\-01\-01.



**Offset ** <span data-label="purple">integer </span><span data-api-tag="require|QE7iuQ">必选</span>`Example value: 0`

The starting position for each listing. The starting position for the most recently created task is 0.



**Limit ** <span data-label="purple">integer </span>`Optional` `Example value: 10`

The number of migration tasks returned by the request.



**TaskStatus ** <span data-label="purple">string </span>`Optional` `Example value: Success`

Specify the task statuses to list. The possible values are as follows:


* `Preparing`: Task is being prepared.

* `Transferring`: Task is in progress.

* `Suspended`: Task has been suspended.

* `Success`: Task completed successfully.

* `Stopping`: Task is stopping.

* `Stopped`: The task has been stopped.

* `Failure`: The task has failed.

* `ResultGenerating`: Generating task result.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Below are the unique response parameters for this API. For more information, refer to [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**Count ** <span data-label="purple">integer </span>`Example value: 10`

Number of tasks returned in this request.



**Total ** <span data-label="purple">integer </span>`Example value: 10`

Total number of tasks that meet the specified status



**TaskList ** <span data-label="purple">object[] </span>`Example: -`

Migration task list.


**CreateTime ** <span data-label="purple">string </span>`Example value: 2024-05-14 19:20:39`

Time when the task is created.



**TaskID ** <span data-label="purple">long </span>`Example: 298686`

Migration task ID.



**TaskName ** <span data-label="purple">string </span>`Example value: dms`

Name of the migration task.



**TaskStatus ** <span data-label="purple">string </span>`Example: Success`

Task status. Descriptions of possible values are as follows:


* `Preparing`: The task is being prepared.

* `Transferring`: The task is in progress.

* `Suspended`: The task has been paused.

* `Success`: The task completed successfully.

* `Stopping`: The task is stopping.

* `Stopped`: The task has been stopped.

* `Failure`: The task failed.

* `ResultGenerating`: Generate the task result.



**TaskProgress ** <span data-label="purple">object </span>`Example value: -`

Migration progress of the task.


**FailedBytes ** <span data-label="purple">long </span>`Example value: 0`

Number of bytes failed to migrate.



**FailedObjects ** <span data-label="purple">long </span>`Example: 0`

Number of failed migration objects.



**RemainingBytes ** <span data-label="purple">long </span>`Example value: 0`

Number of bytes not migrated.



**RemainingObjects ** <span data-label="purple">long </span>`Example: 0`

Number of objects not yet migrated.



**NotExistBytes ** <span data-label="purple">long </span>`Example value: 0`

Bytes that do not exist—bytes deleted from the source during migration.



**NotExistObjectCount** <span data-label="purple">long</span> `Example value: 0`

Number of missing objects, which indicates the number of objects deleted from the source during migration.



**SkipBytes ** <span data-label="purple">long </span>`Example value: 0`

Skipped bytes. DMS skips objects in archive, cold archive, and deep cold archive storage; when the overwrite policy is set to "no overwrite", DMS also skips files with the same name. Skipped bytes refer to the total number of bytes for all objects skipped during migration.



**SkipObjectCount ** <span data-label="purple">long </span>`Example: 0`

Number of skipped objects. DMS skips objects that are archived, cold archived, or deep cold archived; when the overwrite policy is set to not overwrite, DMS also skips files with the same name. The number of skipped objects is the total count of all objects skipped during the migration process.



**TotalBytes ** <span data-label="purple">long </span>`Example value: 5357251`

Total number of bytes.



**TotalObjects ** <span data-label="purple">long </span>`Example value: 10003`

Total number of objects.



**TransferredBytes ** <span data-label="purple">long </span>`Example: 5357251`

Number of bytes migrated successfully.



**TransferredObjects ** <span data-label="purple">long </span>`Example value: 10003`

Number of successfully migrated objects.



**TransferBytesSpeed** <span data-label="purple">long</span> `Example value: 100`

Average migration bandwidth.



**TransferCountSpeed ** <span data-label="purple">long </span>`Example value: 100`

Migration average QPS.





&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=ListDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20240511T081028Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240511/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "Offset": 0,
  "TaskStatus": "Success"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240511161041155141166252D1****",
    "Action": "ListDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {
        "Count": 1,
        "TaskList": [
            {
                "CreateTime": "2024-05-14 19:20:39",
                "TaskID": 84,
                "TaskName": "test",
                "TaskProgress": {
                    "FailedBytes": 0,
                    "FailedObjects": 0,
                    "NotExistBytes": 0,
                    "NotExistObjectCount": 0,
                    "RemainingBytes": 0,
                    "RemainingObjects": 0,
                    "SkipBytes": 5357251,
                    "SkipObjectCount": 10003,
                    "TotalBytes": 5357251,
                    "TotalObjects": 10003,
                    "TransferBytesSpeed": 0,
                    "TransferCountSpeed": 0,
                    "TransferredBytes": 0,
                    "TransferredObjects": 0
                },
                "TaskStatus": "Success"
            }
        ],
        "Total": 40
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists error codes related to this API and its business logic. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error Code |Error message |Description |
|---|---|---|---|
|400 |InvalidParameter |Invalid Parameter. |Invalid parameter. |
