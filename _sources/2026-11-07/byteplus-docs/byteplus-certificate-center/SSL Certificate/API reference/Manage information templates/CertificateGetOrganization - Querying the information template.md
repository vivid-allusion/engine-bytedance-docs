---
title: "CertificateGetOrganization - Querying the information template"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetOrganization"
---

Call this API to query the content of the specified information template.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The table below lists only the request parameters unique to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CertificateGetOrganization`

Action to execute. Set the value to CertificateGetOrganization.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**OrganizationId ** string必选 `Example: org-879f6502723b4e0f8762cf3528f4****`

ID of the information template to be queried.

> You can call the [CertificateGetOrganizationList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetOrganizationList) API to get all information template IDs.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**CreatedTime ** string`Example: 2025-01-06 19:11:43`

Creation time of the information template.

**OrganizationId ** string`Example: org-879f6502723b4e0f8762cf3528f4****`

Information template ID.

**Account ** string`Example: 210000XXXX`

VolcanoEngine account ID.

**Tag ** string`Example: doc-test-updated`

Information template name.

**Name ** string`Example: Test Enterprise`

Enterprise name.

**Department ** string`Example: System department`

Enterprise department.

**PostalCode ** string`Example: 100080`

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

**Contact ** object`Example: -`

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

Name of the VolcanoEngine project to which the information template belongs.

**Tags ** object[]`Example: `

List of resource tags bound to the information template.

**Key ** string`Example: env`

The tag key.

**Value ** string`Example: test`

The tag value.

## Request examples

```json
POST /?Action=CertificateGetOrganization&Version=2024-10-01 HTTP/1.1
Host: certificate-service.volcengineapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260511T024853Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260511/cn-beijing/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "OrganizationId": "org-879f6502723b4e0f8762cf3528f4****"
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202605111049320281231110738D1048",
    "Action": "CertificateGetOrganization",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "cn-beijing"
  },
  "Result": {
    "CreatedTime": "2025-01-06 19:11:43",
    "OrganizationId": "org-879f6502723b4e0f8762cf3528f4****",
    "Account": "210000XXXX",
    "Tag": "doc-test-updated",
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
    "ProjectName": "default",
    "Tags": [
      {
        "Key": "env",
        "Value": "test"
      }
    ]
  }
}
```

## Error codes

The table below lists the business\-related error codes of the operation. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
