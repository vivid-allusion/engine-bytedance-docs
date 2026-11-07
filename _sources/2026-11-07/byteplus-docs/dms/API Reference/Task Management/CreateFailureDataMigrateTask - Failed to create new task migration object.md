---
title: "CreateFailureDataMigrateTask - Failed to create new task migration object"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/CreateFailureDataMigrateTask_-_Failed_to_create_new_task_migration_object"
---

Use the CreateFailureDataMigrateTask API to create a new migration task for objects that failed to migrate in the previous task.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters for this API and some common parameters are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|ovzIaA">必选</span>`Example: CreateFailureDataMigrateTask`

Operation to perform: CreateFailureDataMigrateTask.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|fgYliY">必选</span> `Example value: 2018-01-01`

API version. Value: 2018\-01\-01.



**OriginTaskID ** <span data-label="purple">long </span><span data-api-tag="require|JjgUZO">必选</span> `Example value: 298686`

Task ID for migrating failed objects.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the ListDataMigrateTask API to query the task ID.</div>




**TaskName ** <span data-label="purple">string </span><span data-api-tag="require|2E6eZV">必选</span> `Example value: test`

Name of the new task.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only parameters specific to this API are listed below. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**TaskID ** <span data-label="purple">long </span>`Example: 298711`

ID of the new task.



&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=CreateFailureDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20240513T121621Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240513/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "OriginTaskID": 298686,
  "TaskName": "retry"
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "202405132016370652051151833E****",
    "Action": "CreateFailureDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {
    "TaskID": 298711
  }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists error codes related to this interface and its business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error Code |Error message |Description |
|---|---|---|---|
|400 |InvalidTaskName |Task name must contain 3\-32 letters, numbers, and dash (\-), and cannot start or end with dash (\-). |Invalid task name. |
|400 |NoNeedToRetry |No failure object found in original task. |This task has no failed items that need migration. |
|408 |CreateFailureTaskTimeout |Wait creating failure task timeout, been suspended to the background. |Task creation timed out. |
|409 |TaskNameExists |Task name already exists, please select another task name. |Task name is duplicated. |
|500 |InnerDBAccessErr |Access DB failed. |Internal error. |
