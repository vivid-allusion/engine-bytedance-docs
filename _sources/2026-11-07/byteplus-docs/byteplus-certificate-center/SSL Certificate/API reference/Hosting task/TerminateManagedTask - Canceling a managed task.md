---
title: "TerminateManagedTask - Canceling a managed task"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/terminatemanagedtask"
---

Call this API to cancel a certificate managed task that is in the Enabled (running) state.

<span id="precautions"></span>
## Precautions

After the managed task is cancelled, BytePlus Certificate Center will no longer automatically renew or replace your certificate.

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

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="request-examples"></span>
## Request examples

```json
POST /?Action=TerminateManagedTask&Version=2021-06-01 HTTP/1.1 
Host: open.byteplusapi.com 
Content-Type: application/json; charset=UTF-8 
X-Date: 20260423T093747Z 
X-Content-Sha256: 287e874e******d653b44d21e 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f 

{ 
  "task_id": "ahgp" 
}
```


<span id="response-examples"></span>
## Response examples

```json
{ 
  "ResponseMetadata": { 
    "RequestId": "2026042317375115308122406929FD93", 
    "Action": "TerminateManagedTask", 
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
