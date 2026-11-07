---
title: "CertificateGetOrganizationList - Getting the information template list"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetOrganizationList"
---

Call this API to get the list of created information templates.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CertificateGetOrganizationList`

Action to execute. Set the value to CertificateGetOrganizationList.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**OrganizationIds ** string[]`optional` `Example: org-879f6502723b4e0f8762cf3528f4****`

Specify the ID of the information template.

**OrganizationType ** string`optional` `Example: Enterprise`

Specify the type of the information template. This parameter can take the following values:

* `Individual`: Personal type template

* `Enterprise`: Enterprise type template

**Tag ** string`optional` `Example: doc-test`

Specify the name of the information template. Support fuzzy match.

**ProjectName ** string`optional` `Example: default`

Specify name of the BytePlus project to which the information template belongs.

**PageNumber ** integer`optional` `Example: 1`

Set the page number of the returned results. Valid range: \>= 1. Default: 1.

**TagFilters ** object[]`optional` `Example: -`

Specify list of resource tags bound to the information template.

**Key ** string必选 `Example: env`

The tag key.

**Values ** string[]必选 `Example: test`

The tag value list.

**PageSize ** integer`optional` `Example: 10`

Set maximum number of information templates per page. Default: 10. Default: 100.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PageNumber ** integer`Example: 1`

Current page number.

**PageSize ** integer`Example: 10`

Maximum number of information templates per page.

**TotalCount ** integer`Example: 1`

Number of information templates that meet the query conditions.

**Organizations ** object[]`Example: `

List of information template objects.

**Tags ** object[]`Example: -`

List of resource tags bound to the information template.

**Key ** string`Example: env`

The tag key.

**Value ** string`Example: test`

The tag value.

**OrganizationId ** string`Example: org-879f6502723b4e0f8762cf3528f4****`

Information template ID.

**CreatedTime ** string`Example: 2025-01-06 19:11:43`

Creation time of the information template.

**Account ** string`Example: 210000XXXX`

BytePlus account ID.

**Tag ** string`Example: doc-test-updated`

Information template name.

**Type ** string`Example: Enterprise`

Type of the information template. This parameter can take the following values:

* `Individual`: Personal type template

* `Enterprise`: Enterprise type template

**Name ** string`Example: Test Enterprise`

Enterprise name.

**Department ** string`Example: System department`

Enterprise department.

**PostalCode ** string`Example: 079903`

Postal code of the enterprise location.

**Address ** string`Example: 10 Anson Road, #20-01`

Enterprise address.

**City ** string`Example: Singapore`

City where the enterprise is located.

**Province ** string`Example: Singapore`

Province or state where the enterprise is located.

**Country ** string`Example: SG`

Two\-letter country code of the enterprise.

**Email ** string`Example: doc-test@example.com`

Enterprise email.

**BusinessLicenseNo ** string`Example: 11100000000000000R`

Enterprise Unified Social Credit Code.

**Contact ** object`Example: N/A`

Certificate contact information.

**FirstName ** string`Example: San`

Contact's first name.

**LastName ** string`Example: Zhang`

Contact's last name.

**Email ** string`Example: zhangsan@example.com`

Contact e\-mail.

**Phone ** string`Example: +6581234567`

Contact phone number.

**IdCardNo ** string`Example: 310000202010202020`

Contact ID card number.

**ProjectName ** string`Example: default`

Name of the BytePlus project to which the information template belongs.

## Request examples

```json
POST /?Action=CertificateGetOrganizationList&Version=2024-10-01 HTTP/1.1
Host: ap-southeast-1
Content-Type: application/json; charset=UTF-8
X-Date: 20260511T025304Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260511/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "OrganizationIds": [
    "org-879f6502723b4e0f8762cf3528f4****"
  ],
  "OrganizationType": "Enterprise",
  "Tag": "doc-test",
  "ProjectName": "default",
  "PageNumber": 1,
  "TagFilters": [
    {
      "Key": "env",
      "Values": [
        "test"
      ]
    }
  ],
  "PageSize": 10
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202605111053131752552020816251C8",
    "Action": "CertificateGetOrganizationList",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 1,
    "Organizations": [
      {
        "Tags": [
          {
            "Key": "env",
            "Value": "test"
          }
        ],
        "OrganizationId": "org-879f6502723b4e0f8762cf3528f4****",
        "CreatedTime": "2025-01-06 19:11:43",
        "Account": "210000XXXX",
        "Tag": "doc-test-updated",
        "Type": "Enterprise",
        "Name": "Test Enterprise",
        "Department": "System department",
        "PostalCode": "079903",
        "Address": "10 Anson Road, #20-01",
        "City": "Singapore",
        "Province": "Singapore",
        "Country": "SG",
        "Email": "doc-test@example.com",
        "BusinessLicenseNo": "11100000000000000R",
        "Contact": {
          "FirstName": "San",
          "LastName": "Zhang",
          "Email": "zhangsan@example.com",
          "Phone": "+6581234567",
          "IdCardNo": "310000202010202020"
        },
        "ProjectName": "default"
      }
    ]
  }
}
```

## Error codes

The table below lists the business\-related error codes of the operation. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).

|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |MalformedRequest |The request is malformed |Request parameters format is invalid. |
|400 |InvalidParameter |The specified parameter %s is invalid. |The specified parameter value is invalid. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error. |
