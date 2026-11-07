---
title: "ResumeDataMigrateTask - Resume migration task"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/ResumeDataMigrateTask_-_Resume_migration_task"
---

Call the ResumeDataMigrateTask API to continue a migration that is paused or has failed.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

Only unique request parameters and some common parameters for this API are listed below. For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|FOcdtA">必选</span> `Example: ResumeDataMigrateTask`

Operation to perform: ResumeDataMigrateTask.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|v3yTgr">必选</span> `Example: 2018-01-01`

API version: 2018\-01\-01.



**TaskID ** <span data-label="purple">long </span><span data-api-tag="require|e7A1IE">必选</span> `Example: 298686`

Task ID.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You can call the ListDataMigrateTask API to query the Task ID.</div>




&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=ResumeDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20240513T120422Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20240513/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "TaskID": 298686
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```text
{
  "ResponseMetadata": {
    "RequestId": "2024051320042813723502419583****",
    "Action": "ResumeDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists error codes related to this API and business logic. For common error codes, see the [Common Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error codes |Error message |Description |
|---|---|---|---|
|400 |TaskCantResume |The task can't resume. |This task cannot continue. |
|404 |TaskNotFound |TaskNotFound |The task does not exist. |
|500 |CommonInner |This feature is currently unavailable. |Internal error. |
