---
title: "StopDataMigrateTask - Pause migration task"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/StopDataMigrateTask_-_Pause_migration_task"
---

Call the StopDataMigrateTask API to pause the migration task.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only the unique request parameters and certain public parameters for this API are listed below. For more information, see [Public parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|pOBWOi">必选</span>`Example: StopDataMigrateTask`

Action to be performed: StopDataMigrateTask.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|TYFHh3">必选</span> `Example value: 2018-01-01`

API version: 2018\-01\-01.



**Task ID ** <span data-label="purple">Long </span><span data-api-tag="require|FOjpVM">必选</span>`Example value: 298686`

Task ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can use the ListDataMigrateTask API to query the task ID.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API has no unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=StopDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20240513T115050Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240513/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "TaskID": 298686
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20240513195105021202241138AE****",
    "Action": "StopDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The table below lists error codes related to this API and its business logic. For public error codes, refer to the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error Code |Error message |Description |
|---|---|---|---|
|400 |TaskCantStop |The task can't stop |Generating migration list. Unable to pause the task. |
|404 |TaskNotFound |TaskNotFound |The task does not exist. |
