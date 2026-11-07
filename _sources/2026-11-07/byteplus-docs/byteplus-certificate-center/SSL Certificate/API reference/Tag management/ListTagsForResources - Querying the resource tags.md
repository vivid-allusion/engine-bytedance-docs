---
title: "ListTagsForResources - Querying the resource tags"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/ListTagsForResources"
---

Call this API to query the tags bound to your certificate center resources.

## Instructions

Certificate Center resources include certificate instances and information templates. You can call this API to query the tags bound to a certificate instance or an information template.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: ListTagsForResources`

The action to perform. Value: ListTagsForResources.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**ResourceType ** string必选 `Example: organization_info`

The type of certificate center resource to be queried. This parameter can take the following values:

* `child_cert_instance`: Certificate instance

* `organization_info`: Information template

**ResourceIds ** string[]`optional` `Example: org-f18bd9529257456ca26dc9f3c494****`

List of resource IDs to query. `ResourceIds` and `TagFilters` cannot both be empty at the same time.

* For certificate instances, the resource ID represents the certificate instance ID.

> You can call the [CertificateGetInstanceList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificategetInstancelist) API to get all certificate instance IDs.

* For information templates, the resource ID represents the information template ID.

> You can call the CertificateGetOrganizationList API to get all information template IDs.

**TagFilters ** object[]`optional` `Example:`

Tag filter, used to retrieve resources that are bound to the specified tag(s). `ResourceIds` and `TagFilters` cannot both be empty at the same time.

**Key ** string必选 `Example: env`

The tag key.

**Values ** string[]必选 `Example: test`

The tag value.

**PageNumber ** integer`optional` `Example: 1`

Set the page number to be returned. Default: 1.

**PageSize ** integer`optional` `Example: 10`

Set the number of tag information items per page. Default value: 10. Maximum value: 100.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**ResourceTags ** object[]`Example:`

The list of tag information bound to the resource.

**ResourceType ** string`Example: organization_info`

Resource type. This parameter can take the following values:

* `child_cert_instance`: Certificate instance

* `organization_info`: Information template

**ResourceId ** string`Example: org-f18bd9529257456ca26dc9f3c494****`

Resource ID.

**TagKey ** string`Example: env`

The tag key.

**TagValue ** string`Example: test`

The tag value.

**PageNumber ** integer`Example: 1`

Current page number.

**PageSize ** integer`Example: 20`

Total number of pages.

**TotalCount ** integer`Example: 50`

Total number of tag information entries that meet the criteria.

## Request example

```json
POST /?Action=ListTagsForResources&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260804T083033Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260804/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "ResourceType": "organization_info",
  "ResourceIds": [
    "org-f18bd9529257456ca26dc9f3c494****"
  ],
  "TagFilters": [
    {
      "Key": "env",
      "Values": [
        "test"
      ]
    }
  ],
  "PageNumber": 1,
  "PageSize": 10
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "2026011317310609715718709816D73F",
    "Action": "ListTagsForResources",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "ResourceTags": [
      {
        "ResourceType": "organization_info",
        "ResourceId": "org-f18bd9529257456ca26dc9f3c494****",
        "TagKey": "env",
        "TagValue": "test"
      }
    ],
    "PageNumber": 1,
    "PageSize": 20,
    "TotalCount": 50
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |InvalidParameter |The specified parameter %s is invalid. |The specified parameter value is invalid. |
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error. |
