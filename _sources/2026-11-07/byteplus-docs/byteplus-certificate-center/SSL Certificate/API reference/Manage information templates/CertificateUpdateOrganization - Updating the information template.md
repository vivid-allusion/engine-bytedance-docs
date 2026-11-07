---
title: "CertificateUpdateOrganization - Updating the information template"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateUpdateOrganization"
---

Call this API to update the content of the specified information template.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action** string 必选 `Example: CertificateUpdateOrganization`

Action to execute. Set the value to CertificateUpdateOrganization.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**Contact ** object`optional` `Example:`

Set the certificate contact information.

**Email** string `optional` `Example: zhangsan@example.com`

Contact email.

**Phone ** string`optional` `Example: +6581234567`

Contact phone number.

**IdCardNo ** string`optional` `Example: 310000202010202020`

Contact ID card number.

**FirstName ** string`optional` `Example: San`

Contact's first name.

**LastName ** string`optional` `Example: Zhang`

Contact's last name.

**OrganizationId ** string必选 `Example: org-879f6502723b4e0f8762cf3528f4****`

ID of the information template to be updated.

> You can call the [CertificateGetOrganizationList](https://www.volcengine.com/docs/6638/1365584) API to obtain the IDs of all information templates.

**Type ** string`optional` `Example: Enterprise`

Set the type of the information template. This parameter can take the following values:

* `Individual`: Personal type template, which can only be used to apply for DV certificates

* `Enterprise`: Enterprise type template, which can be used to apply for DV, OV, and EV certificates

**Tag ** string`optional` `Example: doc-test`

Set the name of the information template.

**Name ** string`optional` `Example: Test Enterprise`

Set the enterprise name.

> This parameter is required when Type is `Enterprise`.

**Address ** string`optional` `Example: 10 Anson Road, #20-01`

Set the enterprise address.

> This parameter is required when Type is `Enterprise`.

**City** string `optional` `Example: Singapore`

Set the city where the enterprise resides.

> This parameter is required when Type is `Enterprise`.

**Province ** string`optional` `Example: Singapore`

Set the province or state where the enterprise is located.

> This parameter is required when Type is `Enterprise`.

**Country ** string`optional` `Example: SG`

Set the two\-letter country code of the enterprise, e.g., SG for Singapore and US for the United States.

> This parameter is required when Type is `Enterprise`.

**PostalCode ** string`optional` `Example: 079903`

Set the postal code of the enterprise location.

**Department ** string`optional` `Example: System department`

Set the enterprise department.

**Email ** string`optional` `Example: doc-test@example.com`

Set the company e\-mail.

**BusinessLicenseNo ** string`optional` `Example: 11100000000000000R`

Set the enterprise's Unified Social Credit Code.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
POST /?Action=CertificateUpdateOrganization&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20241031T060232Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20241031/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
    "OrganizationId": "org-879f6502723b4e0f8762cf3528f4****",
    "Type": "Enterprise",
    "Tag": "doc-test-updated",
    "Name": "Test Enterprise",
    "Address": "10 Anson Road, #20-01",
    "City": "Singapore",
    "Province": "Singapore",
    "Country": "SG",
    "PostalCode": "079903",
    "Department": "System department",
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
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20241108170306E25CAC3871567504CDEF",
        "Action": "CertificateUpdateOrganization",
        "Version": "2024-10-01",
        "Service": "certificate_service",
        "Region": "ap-southeast-1"
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes).
