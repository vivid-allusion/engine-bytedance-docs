---
title: "CertificateDeleteOrganization - Deleting the information template"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateDeleteOrganization"
---

Call this API to delete an information template.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CertificateDeleteOrganization`

Action to execute. Set the value to CertificateDeleteOrganization.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**OrganizationId ** string必选 `Example: org-879f6502723b4e0f8762cf3528f4****`

ID of the Information template to be deleted.

> You can call the [CertificateGetOrganizationList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetOrganizationList) API to query all information template IDs.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
POST /?Action=CertificateDeleteOrganization&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20241108T031715Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20241108/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
    "OrganizationId": "org-879f6502723b4e0f8762cf3528f4****"
}
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241108172924396E5E7C0FD523056E3A",
        "Action": "CertificateDeleteOrganization",
        "Version": "2024-10-01",
        "Service": "certificate_service",
        "Region": "ap-southeast-1"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|400 |NotFound.Organization |The specified organization is not found |The specified information template does not exist. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
