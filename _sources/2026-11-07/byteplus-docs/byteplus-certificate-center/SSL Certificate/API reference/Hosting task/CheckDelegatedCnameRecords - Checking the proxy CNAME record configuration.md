---
title: "CheckDelegatedCnameRecords - Checking the proxy CNAME record configuration"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/checkdelegatedcnamerecords"
---

Call this API to check whether the proxy CNAME record for the specified certificate has been correctly configured and has taken effect in the DNS resolution of the domains covered by the certificate.

<span id="instructions"></span>
## Instructions

First, call the [CreateDelegatedCnameRecords](https://docs.byteplus.com/en/docs/byteplus-certificate-center/createdelegatedcnamerecords?lang=en) API to obtain the required CNAME records. After configuring them with your DNS provider, call this API to verify that the configuration is correct.

<span id="request-description"></span>
## Request description

Maximum 20 requests per second per tenant.

<span id="request-parameters"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).


|Parameters |Types |Required |Example value |Description |
|---|---|---|---|---|
|Action |String |Yes |CheckDelegatedCnameRecords |Action to execute. Set the value to CheckDelegatedCnameRecords. |
|Version |String |Yes |2021\-06\-01 |The API version. Value: 2021\-06\-01. |
|instance_id |String |Yes |cert\-9e3dee3cd50a42f9852f0928507b\*\*\*\* |Certificate instance ID, the ID of the certificate whose CNAME configuration needs to be verified. |


<span id="response-parameters"></span>
## Response parameters

The following table lists only the response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameters |Types |Example value |Description |
|---|---|---|---|
|check_result |Boolean |true |CNAME verification result,`true` indicates that the CNAME records for all domains are correctly configured and have taken effect; `false` indicates that there are domains that failed verification. |
|failed_domains |Array of String |[] |List of domains that failed verification, when `check_result` is `true`, this field is an empty array. |


<span id="request-examples"></span>
## Request examples

```json
GET /?Action=CheckDelegatedCnameRecords&Version=2021-06-01&instance_id=cert-9e3dee3cd50a42f9852f0928507b**** HTTP/1.1 
Host: open.byteplusapi.com 
X-Date: 20260423T091158Z 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f 
{ 
    "instance_id": "cert-9e3dee3cd50a42f9852f0928507b****" 
}

```


<span id="response-examples"></span>
## Response examples

```json
{ 
  "ResponseMetadata": { 
    "RequestId": "20260423171128251072194197093E8B", 
    "Action": "CheckDelegatedCnameRecords", 
    "Version": "2021-06-01", 
    "Service": "certificate_service", 
    "Region": "cn-beijing" 
  }, 
  "Result": { 
    "check_result": true, 
    "failed_domains": [ 
      "[]" 
    ] 
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
