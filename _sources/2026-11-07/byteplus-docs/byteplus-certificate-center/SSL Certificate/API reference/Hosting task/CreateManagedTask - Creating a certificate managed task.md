---
title: "CreateManagedTask - Creating a certificate managed task"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/createmanagedtask"
---

Call this API to create a managed task for the specified certificate. Once enabled, the system will automatically renew the certificate before it expires and deploy the new certificate to the specified BytePlus cloud service.

<span id="instructions"></span>
## Instructions


* Before calling this API, you must complete the following prerequisite steps:

   1. Call [CreateDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/createdelegatedcnamerecords?lang=en) to generate CNAME records, obtaining the `host` (domain name) and `value` (record value).

   2. Configure the CNAME records at your DNS provider.

   3. Call [CheckDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/checkdelegatedcnamerecords) API to verify that the configuration has taken effect.

* Only one managed task can be created per certificate.


<span id="request-description"></span>
## Request description

Request frequency: Up to 20 requests per second per tenant.

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

The following table lists only the response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameters |Types |Example value |Description |
|---|---|---|---|
|task_id |String |task\-807aecfba9c7414bb68784cf4126\*\*\*\* |ID of the newly created managed task. |


<span id="request-examples"></span>
## Request examples

```json
POST /?Action=CreateManagedTask&Version=2021-06-01 HTTP/1.1 
Host: open.byteplusapi.com 
Content-Type: application/json; charset=UTF-8 
X-Date: 20260423T095237Z 
X-Content-Sha256: 287e874e******d653b44d21e 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f 

{ 
  "binding_services": [ 
    "CDN" 
  ], 
  "instance_id": "cert-9e3dee3cd50a42f9852f0928507b****", 
  "renew_period": 30, 
  "tag": "prod-cdn-auto-renew" 
}
```


<span id="response-examples"></span>
## Response examples

```json
{ 
  "ResponseMetadata": { 
    "RequestId": "20260423175258141180190203674897", 
    "Action": "CreateManagedTask", 
    "Version": "2021-06-01", 
    "Service": "certificate_service", 
    "Region": "cn-beijing" 
  }, 
  "Result": { 
    "task_id": "task-807aecfba9c7414bb68784cf4126****" 
  } 
}
```


<span id="error-codes"></span>
## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/transitrouter/Public-error-codes).


|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MalformedRequest |The request is malformed |Specified parameter format is invalid. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
