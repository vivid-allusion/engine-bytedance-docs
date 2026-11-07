---
title: "CertificateGetInstanceList - Getting the certificate instance list"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificategetInstancelist"
---

Call this API to get a list of SSL certificate instances.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example value: CertificateGetInstanceList`

The action to perform. The value is CertificateGetInstanceList.

**Version ** string必选 `Example value: 2024-10-01`

The API version. Value: 2024\-10\-01.

### Body

**InstanceIds ** string[]`Optional` `Example: ["cert-310a6640e2ef4c1dbe5065c62821****"]`

The ID of the certificate instance.

**Status ** string[]`Optional` `Example: ["Issued"]`

Specifies the status of the certificate instance. The certificate status has the following values:

* `NotSubmitted`: Draft

* `Pending`: Verifying

* `Issued`: Issued

* `Cancelling`: Cancelling

* `Canceled`: Cancelled

* `Revoking`: Revoking

* `Revoked`: Revoked

* `Failed`: Request failed

* `Unknown`: Unknown

**Tag ** string`Optional` `Example value: Unnamed certificate`

The remarks for the certificate instance. Supports fuzzy matching.

**CommonName ** string`Optional` `Example: example.com`

The Common Name (CN) of the certificate. Supports fuzzy matching.

**Domain ** string`Optional` `Example value: www.example.com`

Specifies the Subject Alternative Name (SAN) of the certificate. Supports fuzzy match.

**InstanceType ** string`Optional` `Example value: Free`

The type of the certificate instance. This parameter can take the following values:

* `Free`: Free certificate

* `Test`: Test certificate (paid)

* `Paid`: Paid certificate (paid)

* `Imported`: Uploaded certificate

**IsRevoked ** boolean`Optional` `Example value: false`

Whether to return only revoked certificates. Default value: false.

**IsValid ** boolean`Optional` `Example value: true`

Specifies whether to return only valid certificates. Default: false.

A valid certificate is one that has been issued, is within its validity period, and has not been revoked.

**CertificateExpireBefore ** string`Optional` `Example value: 2024-11-24 07:59:59`

Specifies the expiration end time of the certificate. The format is `yyyy-mm-dd hh:mm:ss`.

**CertificateExpireAfter ** string`Optional` `Example value: 2024-10-25 08:00:00`

Specifies the start of the certificate expiration period. The time format is `yyyy-mm-dd hh:mm:ss`.

**PageNumber ** integer`Optional` `Example: 1`

Specifies the page number to return. Default: 1.

**PageSize ** integer`Optional` `Example value: 10`

The maximum number of certificate instances on a single page. Default value: 10. Maximum value: 100.

**ProjectName ** string`Optional` `Example value: default`

The name of the BytePlus project that the certificate instance belongs to.

**TagFilters ** object[]`Optional` `Example: `

Specifies the resource tags attached to the certificate instance.

**Key ** string必选 `Example: env`

Tag key.

**Values ** string[]必选 `Example value: test`

The tag value.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**PageNumber ** integer`Example value: 1`

Current page number.

**PageSize ** integer`Example value: 10`

The maximum number of certificate instances per page.

**TotalCount ** integer`Example value: 1`

The number of certificate instances that meet the query conditions.

**Instances ** object[]`Example value:`

A list of certificate instance objects.

**AccountId ** string`Example value: 210000XXXX`

BytePlus Account ID.

**SourceId ** string`Example: cert-6d580ffd930e42239dad01b56654****`

For certificates obtained through renewal, this represents the ID of the old certificate instance that was renewed.

**Tag ** string`Example value: Unnamed certificate`

Remarks for the certificate instance.

**Status ** string`Example value: Issued`

The state of the certificate instance. This parameter can take the following values:

* `NotSubmitted`: Draft

* `Pending`: Verifying

* `Issued`: Issued

* `Cancelling`: Cancelling

* `Canceled`: Cancelled

* `Revoking`: Revoking

* `Revoked`: Revoked

* `Failed`: Request failed

* `Unknown`: Unknown

**InstanceType ** string`Example: Paid`

The type of the certificate instance. This parameter can take the following values:

* `Free`: Free certificate

* `Test`: Test certificate (Paid)

* `Paid`: Paid certificate

* `Imported`: Uploaded certificate

**InstanceId ** string`Example value: cert-c88df6d4a1b348c3b714b746d3cc****`

Certificate instance ID.

**CommonName ** string`Example value: *.example.com`

The common name (CN) of the certificate.

**Issuer ** stringExample: RapidSSL TLS RSA CA G1

The common name (CN) of the certificate issuer.

**San ** string[]`Example value: *.example.com`

The certificate's Subject Alternative Name (SAN). The Subject Alternative Name includes all domain names that the certificate can protect.

**IsCertificateRevoked ** boolean`Example value: false`

Whether the certificate is revoked.

**IsCertificateSm ** boolean`Example value: false`

Indicates whether the certificate is an SM certificate.

**OrderPeriod ** integerExample value: 12

The duration of the certificate service. The unit is months.

> For an uploaded certificate, the value of this parameter is 0.

**OrderBrand ** stringExample: digicert_free

The brand of the certificate.

> This parameter is empty for uploaded certificates.

**InstanceLevel ** string`Example value: dv`

The type of the certificate. This parameter can take the following values:

* `dv`: Domain Validation

* `ov`: Organization Validation

* `ev`: Extended Validation

> For uploaded certificates, this parameter is empty.

**CertificateDomainType ** string`Example value: Wildcard`

The domain type of the certificate. This parameter can take the following values:

* `Single`: Single domain name

* `Wildcard`: Wildcard domain

* `Multi`: Multi\-domain

> This parameter is empty for uploaded certificates.

**CertificateKeyAlgorithm ** string`Example: RSA 2048`

The key algorithm of the certificate.

**NotBefore ** string`Example value: 2024-12-26 08:00:00`

The start of the certificate's validity period.

**NotAfter ** string`Example: 2025-01-25 07:59:59`

The end time of the certificate's validity period.

**ProjectName ** string`Example value: default`

The name of the BytePlusect to which the certificate instance belongs.

**Tags ** object[]`Example value:`

The list of resource tags attached to the certificate instance.

**Key ** string`Example value: env`

Tag key.

**Value ** string`Example value: test`

Tag value.

**CreatedTime ** string`Example value: 2024-12-26 19:15:11`

The creation time of the certificate instance.

## Request example

```json
POST /?Action=CertificateGetInstanceList&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260113T092343Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260113/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceIds": [
    "cert-310a6640e2ef4c1dbe5065c62821****"
  ],
  "Status": [
    "Issued"
  ],
  "Tag": "Unnamed certificate",
  "CommonName": "example.com",
  "Domain": "www.example.com",
  "InstanceType": "Free",
  "IsRevoked": true,
  "IsValid": true,
  "CertificateExpireBefore": "2024-11-24 07:59:59",
  "CertificateExpireAfter": "2024-10-25 08:00:00",
  "PageNumber": 1,
  "PageSize": 10,
  "ProjectName": "default",
  "TagFilters": [
    {
      "Key": "env",
      "Values": [
        "test"
      ]
    }
  ]
}
```

## Response example

```json
{
  "ResponseMetadata": {
    "RequestId": "20260113172445052069235216AA8C5A",
    "Action": "CertificateGetInstanceList",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "ap-southeast-1"
  },
  "Result": {
    "PageNumber": 1,
    "PageSize": 10,
    "TotalCount": 1,
    "Instances": [
      {
        "AccountId": "210000XXXX",
        "SourceId": "cert-6d580ffd930e42239dad01b56654****",
        "Tag": "Unnamed certificate",
        "Status": "Issued",
        "InstanceType": "Paid",
        "InstanceId": "cert-c88df6d4a1b348c3b714b746d3cc****",
        "CommonName": "*.example.com",
        "Issuer": "RapidSSL TLS RSA CA G1",
        "San": [
          "*.example.com"
        ],
        "IsCertificateRevoked": true,
        "IsCertificateSm": true,
        "OrderPeriod": 12,
        "OrderBrand": "digicert_free",
        "InstanceLevel": "dv",
        "CertificateDomainType": "Wildcard",
        "CertificateKeyAlgorithm": "RSA 2048",
        "NotBefore": "2024-12-26 08:00:00",
        "NotAfter": "2025-01-25 07:59:59",
        "ProjectName": "default",
        "Tags": [
          {
            "Key": "env",
            "Value": "test"
          }
        ],
        "CreatedTime": "2024-12-26 19:15:11"
      }
    ]
  }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) documentation.

|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |MalformedRequest |The request is malformed |The request parameter format is invalid. |
|400 |InvalidParameter |The specified parameter %s is invalid. |The specified parameter value is invalid. |
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error. |
