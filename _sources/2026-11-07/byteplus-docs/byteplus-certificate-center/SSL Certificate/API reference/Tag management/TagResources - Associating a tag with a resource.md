---
title: "TagResources - Associating a tag with a resource"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/TagResources"
---

Call this API to associate tags with your Certificate Center resources.

## Instructions

Certificate Center resources include certificate instances and information templates. Call this API to associate tags with certificate instances and information templates.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: TagResources`

Action to execute. Set the value to TagResources.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**ResourceType ** string必选 `Example: organization_info`

Type of the certificate center resource to be operated on. This parameter can take the following values:

* `child_cert_instance`: Certificate instance

* `organization_info`: Information template

**ResourceIds** string[] 必选 `Example: org-f18bd9529257456ca26dc9f3c494****`

List of resource IDs to which tags are to be bound.

* For certificate instances, the resource ID represents the certificate instance ID.

> You can call the [CertificateGetInstanceList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificategetInstancelist) API to get all certificate instance IDs.

* For information templates, the resource ID represents the information template ID.

> You can call the CertificateGetOrganizationList API to get all information template IDs.

**Tags ** object[]必选 `Example:`

List of tag key‑value pairs to be bound.

**Key ** string必选 `Example: env`

The tag key.

**Value ** string必选 `Example: test`

The tag value.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
POST /?Action=TagResources&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260113T093144Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260113/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ResourceType": "organization_info",
  "ResourceIds": [
    "org-f18bd9529257456ca26dc9f3c494****"
  ],
  "Tags": [
    {
      "Key": "env",
      "Value": "test"
    }
  ]
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20260113173150242160021186EE1CB3",
    "Action": "TagResources",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "ap-southeast-1"
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
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
