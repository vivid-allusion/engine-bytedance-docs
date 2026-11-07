---
title: "DeleteDataMigrateTask - Delete Migration Task"
product: "Data Migration Service"
product_code: "dms"
source: "https://docs.byteplus.com/en/docs/dms/DeleteDataMigrateTask_-_Delete_Migration_Task"
---

Call the DeleteDataMigrateTask API to delete a migration task.

<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following lists only the request parameters specific to this API and some common parameters For more information, see [Common Parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">string </span><span data-api-tag="require|3QUrKq">必选</span> `Example: DeleteDataMigrateTask`

Action to perform. Value: DeleteDataMigrateTask.



**Version ** <span data-label="purple">string </span><span data-api-tag="require|YdQGAI">必选</span> `Example: 2018-01-01`

API version. Value: 2018\-01\-01.



**ID ** <span data-label="purple">long </span><span data-api-tag="require|3nAvyK">必选</span> `Example: 298676`

ID of the task to be deleted.



**TaskName ** <span data-label="purple">string </span>`Optional` `Example: test`

Name of the task to be deleted.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters For more information, see [Response Structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6K-35rGC56S65L6L"></span>
## Sample request

```text
POST /?Action=DeleteDataMigrateTask&Version=2018-01-01 HTTP/1.1
Host: dms.cn-beijing.byteplusapi.com.cn
Content-Type: application/json; charset=UTF-8
X-Date: 20250811T040716Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250811/cn-beijing/dms/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ID": 298676
}
```


<span id=".6L-U5Zue56S65L6L"></span>
## Sample response

```json
{
  "ResponseMetadata": {
    "RequestId": "20250812155534182018034052D5****",
    "Action": "DeleteDataMigrateTask",
    "Version": "2018-01-01",
    "Service": "dms",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

The following table lists the error codes related to the service logic of this API. For public error codes, see the [Public Error Codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.


|Status Code |Error Code |Error message |Description |
|---|---|---|---|
|404 |TaskNotFound |TaskNotFound |Task does not exist. |
