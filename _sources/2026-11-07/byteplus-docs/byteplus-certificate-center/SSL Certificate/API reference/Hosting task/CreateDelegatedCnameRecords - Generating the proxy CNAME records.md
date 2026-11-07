---
title: "CreateDelegatedCnameRecords - Generating the proxy CNAME records"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/createdelegatedcnamerecords"
---

Call this API to generate the DNS CNAME proxy records required for managed renewal of the specified certificate. It returns the domain name prefix (Host) and record value (Value), which you need to configure as a CNAME record at your DNS provider to complete domain ownership verification.

<span id="instructions"></span>
## Instructions


* Before calling this API, ensure that:

   * You have applied for a free certificate [(DigiCert EE or Let's Encrypt) through BytePlus Certificate Center](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-request-free-ssl-certificate).

   * The certificate is in the Issued status.

   * The certificate expiration time is at least 30 days.

* The returned CNAME records must be configured with your domain DNS provider. The system will verify domain ownership through these records.


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

The following table lists only the response parameters specific to this API. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).


|Parameters |Types |Example value |Description |
|---|---|---|---|
|cnameRecords |Array of Object |[{"host": "_dnsauth.auto.example.com", "value": "_dnsauth.abc123.cert.managed.com"}] |List of CNAME proxy records, each element contains a hostname and a record value. |


<span id="request-examples"></span>
## Request examples

```json
POST /?Action=CreateDelegatedCnameRecords&Version=2021-06-01 HTTP/1.1 
Host: open.byteplusapi.com 
Content-Type: application/json; charset=UTF-8 
X-Date: 20260423T090111Z 
X-Content-Sha256: 287e874e******d653b44d21e 
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260423/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f 

{ 
  "instance_id": "cert-9e3dee3cd50a42f9852f0928507b****" 
}
```


<span id="response-examples"></span>
## Response examples

```json
{ 
  "ResponseMetadata": { 
    "RequestId": "20260423170114159164221079254D63", 
    "Action": "CreateDelegatedCnameRecords", 
    "Version": "2021-06-01", 
    "Service": "certificate_service", 
    "Region": "cn-beijing" 
  }, 
  "Result": { 
    "cnameRecords": [ 
      { 
        "host": "_dnsauth.auto.example.com", 
        "value": "_dnsauth.abc123.cert.managed.com" 
      } 
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
