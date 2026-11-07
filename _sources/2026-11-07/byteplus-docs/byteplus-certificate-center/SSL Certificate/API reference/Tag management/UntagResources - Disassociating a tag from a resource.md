---
title: "UntagResources - Disassociating a tag from a resource"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/UntagResources"
---

Call this API to disassociate tags with your Certificate Center resources.

## Instructions

Certificate Center resources include certificate instances and information templates. Call this API to disassociate tags with certificate instances and information templates.

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: UntagResources`

Action to execute. Set the value to UntagResources.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**ResourceType ** string必选 `Example: organization_info`

Type of the certificate center resource to be operated on. This parameter can take the following values:

* `child_cert_instance`: Certificate instance

* `organization_info`: Information template

**ResourceIds ** string[]必选 `Example: org-f18bd9529257456ca26dc9f3c494****`

List of resource IDs from which tags are to be disassociated.

* For certificate instances, the resource ID represents the certificate instance ID.

> You can call the [CertificateGetInstanceList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificategetInstancelist) API to get all certificate instance IDs.

* For information templates, the resource ID represents the information template ID.

> You can call the [CertificateGetOrganizationList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetOrganizationList) API to get all information template IDs.

**TagKeys ** string[]必选 `Example: env`

List of tag keys to be disassociated.

## Response parameters

This API has no unique response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request examples

```json
POST /?Action=UntagResources&Version=2024-10-01 HTTP/1.1
Host: certificate-service.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260113T093227Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260113/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ResourceType": "organization_info",
  "ResourceIds": [
    "org-f18bd9529257456ca26dc9f3c494****"
  ],
  "TagKeys": [
    "env"
  ]
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20260113173233071143184144551018",
    "Action": "UntagResources",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "cn-beijing"
  },
  "Result": {}
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|400 |InvalidParameter |The specified parameter %s is invalid. |The specified parameter value is invalid. |
|400 |NotFound.Resource |The specified resource is not found. |The specified resource does not exist. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error. |
