---
title: "DeleteManagedTask - Deleting a managed task"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/deletemanagedtask"
---

Call this API to delete a specified certificate managed task.

<span id="instructions"></span>
## Instructions


* Only tasks with the status Cancelled can be deleted. For a Running task, you must first call the [TerminateManagedTask](https://docs.byteplus.com/en/docs/byteplus-certificate-center/terminatemanagedtask) API to cancel it before calling this API to delete it.

* Deletion is irreversible. Please ensure the task is no longer needed before deleting it.


<span id="request-description"></span>
## Request description

Maximum 20 requests per second per tenant.

<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="query"></span>
### Query


|Parameters |Types |Required |Example value |Description |
|---|---|---|---|---|


<span id="body"></span>
### Body


|Parameters |Types |Required |Example value |Description |
|---|---|---|---|---|


<span id="response-parameters"></span>
## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="request-examples"></span>
## Request examples

```json
POST /?Action=DeleteManagedTask&Version=2021-06-01 HTTP/1.1 
Host: open.byteplusapi.com 
Content-Type: application/json; charset=UTF-8 
X-Date: 20260423T095153Z 
X-Content-Sha256: 287e874e******d653b44d21e 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f 

{ 
  "delete_reason": "Business decommissioned, no longer needs automatic renewal", 
  "task_id": "task-9769162398fb4ea6b69fc5f5de12****" 
}
```


<span id="response-examples"></span>
## Response examples

```json
{ 
  "ResponseMetadata": { 
    "RequestId": "2026042317515725022421023418DFFB", 
    "Action": "DeleteManagedTask", 
    "Version": "2021-06-01", 
    "Service": "certificate_service", 
    "Region": "cn-beijing" 
  }, 
  "Result": {} 
}
```


<span id="error-codes"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MalformedRequest |The request is malformed |Specified parameter format is invalid. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
