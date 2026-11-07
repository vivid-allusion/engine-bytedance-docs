---
title: "CertificateGetDcvParam - Getting the verification requirements of domain"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetDcvParam_-_Getting_the_verification_requirements_of_domain"
---

Call this API to obtain the specific requirements for completing domain ownership validation. These requirements guide you through the necessary configurations to prove that you can manage the domain for which the certificate is issued.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CertificateGetDcvParam`

Action to execute. Set the value to CertificateGetDcvParam.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**InstanceId ** string必选 `Example: cert-46d8415d27374dfc8ea6caab0141****`

Specify the certificate instance ID.

> You can call the [CertificateGetInstanceList](https://www.volcengine.com/docs/6638/1413343) API to get all certificate instance IDs.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**ValidationType ** string`Example: dns_txt`

The method for domain ownership validation. This parameter can take the following values:

* `dns_cname`: DNS verification (based on CNAME records).

* `dns_txt`: DNS verification (based on TXT records).

* `https`: File verification (based on HTTPS requests).

* `http`: File verification (based on HTTP requests).

**DomainsToBeValidated ** object[]`Example: \-`

Specific verification requirements.

**ValidationDomain ** string`Example: _dnsauth.example.com`

Depending on the verification method, the meaning of this parameter differs accordingly:

* For DNS verification, this parameter represents the domain. You need to configure DNS records for that domain.

* For file verification, this parameter represents the file path. You need to create the verification file as indicated by that path.

**Value ** string`Example: 2024iabf9qriabfiadnaiowh`

Depending on the verification method, the meaning of this parameter differs accordingly:

* For DNS verification, this parameter also denotes the value of the DNS record.

* For file verification, this parameter also denotes the content of the verification file.

## Request example

```json
POST /?Action=CertificateGetDcvParam&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20251114T090424Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251114/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "cert-46d8415d27374dfc8ea6caab0141****"
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20251114170428186047190023284C48",
    "Action": "CertificateGetDcvParam",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ValidationType": "dns_txt",
    "DomainsToBeValidated": [
      {
        "ValidationDomain": "_dnsauth.example.com",
        "Value": "2024iabf9qriabfiadnaiowh"
      }
    ]
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MalformedRequest |The request is malformed |Request parameters format is invalid. |
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|400 |NotFound.CertificateInstance |The specified certificate was not found. |The specified certificate does not exist |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
