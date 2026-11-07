---
title: "CertificateGetInstance - Querying the certificate instance details"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateGetInstance"
---

Call this API to query the details of the specified SSL certificate instance.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request Parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example value: CertificateGetInstance`

The action to be performed. The value is CertificateGetInstance.

**Version ** string必选 `Example value: 2024-10-01`

The API version. Value: 2024\-10\-01.

### Body

**InstanceId ** string必选 `Example value: cert-c88df6d4a1b348c3b714b746d3cc****`

The ID of the certificate instance.

> You can call the [CertificateGetInstanceList](https://www.volcengine.com/docs/6638/1413343) interface to get the IDs of all certificate instances.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**InstanceId ** string`Example value: cert-c88df6d4a1b348c3b714b746d3cc****`

Certificate Instance ID.

**AccountId ** string`Example value: 210000XXXX`

BytePlus Account ID.

**SourceId ** string`Example: cert-6d580ffd930e42239dad01b56654****`

For certificates obtained through renewal, this is the ID of the original certificate instance.

**Tag ** string`Example value: unnamed certificate`

Remarks for the certificate instance.

**Status ** string`Example value: Issued`

The status of the certificate instance. This parameter can take the following values:

* `NotSubmitted`: Draft

* `Pending`: Verifying

* `Issued`: Issued

* `Cancelling`: Cancelling

* `Canceled`: Cancelled

* `Revoking`: Revoking.

* `Revoked`: The certificate has been revoked.

* `Failed`: The request failed.

* `Unknown`: The status is unknown.

**InstanceType ** string`Example value: Paid`

The type of the certificate instance. This parameter can take the following values:

* `Free`: Free certificate

* `Test`: Test certificate (Paid)

* `Paid`: Official certificate (Paid)

* `Imported`: Uploaded certificate

**InstanceLevel ** stringExample value: dv

The type of the certificate. This parameter can take the following values:

* `dv`: Domain validation

* `ov`: Organization validation

* `ev`: Extended Validation

> This parameter is empty for uploaded certificates.

**OrderBrand ** string`Example value: digicert`

The brand of the certificate.

> This parameter is empty for uploaded certificates.

**OrderOrganizationId ** string`Example value: org-685e6a2bae5b46bcacbe3a82965e****`

The ID of the information template associated with the certificate order.

> This parameter is empty for uploaded certificates.

**OrderPeriod ** integer`Example value: 12`

The duration of the certificate service. Unit: months.

> For uploaded certificates, the value of this parameter is 0.

**OrderPlan ** string`Example value: digicert_wildcard_dv`

The specification of the certificate.

> This parameter is empty for uploaded certificates.

**CertificateDomainType ** string`Example: Wildcard`

Domain type of the certificate. This parameter can take the following values:

* `Single`: Single domain name

* `Wildcard`: Wildcard domain name

* `Multi`: Multiple domain names

> This parameter is empty for uploaded certificates.

**IsCertificateSm ** booleanExample value: false

Indicates whether the certificate is an SM certificate.

**IsCertificateRevoked ** boolean`Example: false`

Whether the certificate has been revoked.

**CommonName ** string`Example value: *.example.com`

Certificate common name (CN).

**San ** string[]`Example: *.example.com`

The certificate's Subject Alternative Name (SAN). The Subject Alternative Name contains all domain names that the certificate protects.

**NotBefore ** stringExample: 2024\-12\-26 08:00:00

The start time of the certificate validity period.

**NotAfter ** string`Example: 2025-01-25 07:59:59`

The end of the certificate's validity period.

**CertificateDetail ** object`Example: `

Certificate details.

**Subject ** objectExample:

The subject information of the certificate.

**CommonName ** string`Example: *.example.com`

Common Name (CN).

**Organization ** string`Example: Test Company`

Organization (O).

**OrganizationUnit ** string`Example: Systems Department`

Organizational Unit (OU).

**Country ** string`Example value: CN`

Country (C).

**Province ** string`Example value: Shanghai`

State or Province (ST).

**Locality ** string`Example value: Shanghai`

Locality (L).

**Address ** string`Example value: No. X, XX Street`

Address (Street).

**PostalCode ** string`Example: 310000`

Postal code (PostalCode).

**Issuer ** object`Example value: `

The issuer information for the certificate.

**CommonName ** stringExample value: \*.example.com

Common name (CN).

**Organization ** string`Example: Test Company`

Organization (O).

**OrganizationUnit ** string`Example value: Systems Department`

Department (OU).

**Country ** string`Example value: CN`

Country (C).

**Province ** string`Example value: Shanghai`

Province or state (ST).

**Locality ** string`Example value: Shanghai`

Locality (L).

**Address ** stringExample: No. XX, XX Street

Address (Street).

**PostalCode ** stringExample: 310000

Postal code.

**Chain ** string[]`Example value: `["

"\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-\nMIIEqzCC......mSD5gds=\n\-\-\-\-\-END CERTIFICATE\-\-\-\-\-\n",

"\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-\nMIIEszCC......../m8Fxw==\n\-\-\-\-\-END CERTIFICATE\-\-\-\-\-\n",

"\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-\nMIIDjjCC......fl\nMrY=\n\-\-\-\-\-END CERTIFICATE\-\-\-\-\-\n"

]``

Certificate chain (PEM format).

A certificate chain consists of a leaf certificate, an intermediate certificate, and a root certificate.

**PrivateKey ** string`Example: `\-\-\-\-\-BEGIN RSA PRIVATE KEY\-\-\-\-\-\nMIIEogIB......vhUorDg=\n\-\-\-\-\-END RSA PRIVATE KEY\-\-\-\-\-\n``

Private Key.

**SerialNumber ** string`Example value: 00000000089E14D489AC80161569F34A29D6CEA7`

Serial number.

**KeyAlgorithm ** string`Example value: RSA 2048`

Key algorithm.

**SignatureAlgorithm ** string`Example value: SHA256-RSA`

Signature algorithm.

**FingerPrintSha256 ** stringExample value: A53B846E14B33939E6CD7F9CF320FD9F96AB1D466A224CD28A38DC1388F51248

SHA\-256 fingerprint.

**FingerPrintSha1 ** string`Example value: AAB216FF78244113D199CB87A8FE62992DB56EF0`

SHA\-1 fingerprint.

**EncryptionCertificateDetail ** objectExample:

The details of the encryption certificate. This applies only to SM certificates.

**Subject ** object`Example value: `

Certificate subject information.

**CommonName ** string`Example value: *.example.com`

Common Name (CN).

**Organization ** stringExample value: Test Company

Organization (O).

**OrganizationUnit ** string`Example: Systems Department`

Organizational Unit (OU).

**Country ** string`Example value: CN`

Country (C).

**Province ** string`Example value: Shanghai`

The province or state (ST).

**Locality ** string`Example: Shanghai`

Locality (L).

**Address ** string`Example value: XX Street, No. XX`

Address (Street).

**PostalCode ** string`Example value: 310000`

Postal code (PostalCode).

**Issuer ** object`Example value:`

The issuer information of the certificate.

**CommonName ** string`Example: *.example.com`

Common Name (CN).

**Organization ** string`Example value: Test organization`

Organization name (O).

**OrganizationUnit ** string`Example: Systems Department`

Organizational Unit (OU).

**Country ** string`Example: CN`

Country (C).

**Province ** stringExample value: Shanghai

Province or state (ST).

**Locality ** string`Example value: Shanghai`

Locality (L).

**Address ** string`Example: 123 Main Street`

Address (Street).

**PostalCode ** string`Example value: 310000`

Postal Code (PostalCode).

**Chain ** string[]`Example value: `["

"\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-\nMIIEqzCC......mSD5gds=\n\-\-\-\-\-END CERTIFICATE\-\-\-\-\-\n",

"\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-\nMIIEszCC......../m8Fxw==\n\-\-\-\-\-END CERTIFICATE\-\-\-\-\-\n",

"\-\-\-\-\-BEGIN CERTIFICATE\-\-\-\-\-\nMIIDjjCC......fl\nMrY=\n\-\-\-\-\-END CERTIFICATE\-\-\-\-\-\n"

]``

Certificate chain (PEM format).

The certificate chain consists of the leaf certificate, intermediate CA certificate, and root certificate.

**PrivateKey ** string`Example: `\-\-\-\-\-BEGIN RSA PRIVATE KEY\-\-\-\-\-\nMIIEogIB......vhUorDg=\n\-\-\-\-\-END RSA PRIVATE KEY\-\-\-\-\-\n``

Private Key.

**SerialNumber ** stringExample value: 00000000089E14D489AC80161569F34A29D6CEA7

Serial number.

**KeyAlgorithm ** string`Example: RSA 2048`

The key algorithm.

**SignatureAlgorithm ** string`Example value: SHA256-RSA`

The signature algorithm.

**FingerPrintSha256 ** string`Example value: A53B846E14B33939E6CD7F9CF320FD9F96AB1D466A224CD28A38DC1388F51248`

SHA\-256 fingerprint.

**FingerPrintSha1 ** stringExample value: AAB216FF78244113D199CB87A8FE62992DB56EF0

SHA\-1 fingerprint.

**ProjectName ** string`Example: default`

The name of the BytePlus project for the certificate instance.

**Tags ** object[]`Example: `

A list of resource tags attached to the certificate instance.

**Key ** string`Example: env`

Tag key.

**Value ** string`Example value: test`

Tag value.

**CreatedTime ** string`Example value: 2024-12-26 19:15:11`

The creation time of the certificate instance.

## Request example

```json
POST /?Action=CertificateGetInstance&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20251031T085641Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251031/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "cert-c88df6d4a1b348c3b714b746d3cc****"
}
```

## Response example

```json
JSON
{
  "ResponseMetadata": {
    "RequestId": "20251031165646104225213040036FC1",
    "Action": "CertificateGetInstance",
    "Version": "2024-10-01",
    "Service": "certificate_service",
    "Region": "ap-singapore-1"
  },
  "Result": {
    "InstanceId": "cert-c88df6d4a1b348c3b714b746d3cc****",
    "AccountId": "210000XXXX",
    "SourceId": "cert-6d580ffd930e42239dad01b56654****",
    "Tag": "Untitled Certificate",
    "Status": "Issued",
    "InstanceType": "Paid",
    "InstanceLevel": "dv",
    "OrderBrand": "digicert",
    "OrderOrganizationId": "org-685e6a2bae5b46bcacbe3a82965e****",
    "OrderPeriod": 12,
    "OrderPlan": "digicert_wildcard_dv",
    "CertificateDomainType": "Wildcard",
    "IsCertificateSm": true,
    "IsCertificateRevoked": true,
    "CommonName": "*.example.com",
    "San": [
      "*.example.com"
    ],
    "NotBefore": "2024-12-26 08:00:00",
    "NotAfter": "2025-01-25 07:59:59",
    "CertificateDetail": {
      "Subject": {
        "CommonName": "*.example.com",
        "Organization": "Test Enterprise",
        "OrganizationUnit": "Systems Department",
        "Country": "CN",
        "Province": "Shanghai",
        "Locality": "Shanghai",
        "Address": "No. XX, XX Street",
        "PostalCode": "310000"
      },
      "Issuer": {
        "CommonName": "*.example.com",
        "Organization": "Test Enterprise",
        "OrganizationUnit": "Systems Department",
        "Country": "CN",
        "Province": "Shanghai",
        "Locality": "Shanghai",
        "Address": "No. XX, XX Street",
        "PostalCode": "310000"
      },
      "Chain": [
        "`[\n                \"-----BEGIN CERTIFICATE-----\\nMIIEqzCC......mSD5gds=\\n-----END CERTIFICATE-----\\n\",\n                \"-----BEGIN CERTIFICATE-----\\nMIIEszCC......../m8Fxw==\\n-----END CERTIFICATE-----\\n\",\n                \"-----BEGIN CERTIFICATE-----\\nMIIDjjCC......fl\\nMrY=\\n-----END CERTIFICATE-----\\n\"\n            ]`"
      ],
      "PrivateKey": "`-----BEGIN RSA PRIVATE KEY-----\\nMIIEogIB......vhUorDg=\\n-----END RSA PRIVATE KEY-----\\n`",
      "SerialNumber": "00000000089E14D489AC80161569F34A29D6CEA7",
      "KeyAlgorithm": "RSA 2048",
      "SignatureAlgorithm": "SHA256-RSA",
      "FingerPrintSha256": "A53B846E14B33939E6CD7F9CF320FD9F96AB1D466A224CD28A38DC1388F51248",
      "FingerPrintSha1": "AAB216FF78244113D199CB87A8FE62992DB56EF0"
    },
    "EncryptionCertificateDetail": {
      "Subject": {
        "CommonName": "*.example.com",
        "Organization": "Test Enterprise",
        "OrganizationUnit": "Systems Department",
        "Country": "CN",
        "Province": "Shanghai",
        "Locality": "Shanghai",
        "Address": "No. XX, XX Street",
        "PostalCode": "310000"
      },
      "Issuer": {
        "CommonName": "*.example.com",
        "Organization": "Test Enterprise",
        "OrganizationUnit": "Systems Department",
        "Country": "CN",
        "Province": "Shanghai",
        "Locality": "Shanghai",
        "Address": "No. XX, XX Street",
        "PostalCode": "310000"
      },
      "Chain": [
        "`[\n                \"-----BEGIN CERTIFICATE-----\\nMIIEqzCC......mSD5gds=\\n-----END CERTIFICATE-----\\n\",\n                \"-----BEGIN CERTIFICATE-----\\nMIIEszCC......../m8Fxw==\\n-----END CERTIFICATE-----\\n\",\n                \"-----BEGIN CERTIFICATE-----\\nMIIDjjCC......fl\\nMrY=\\n-----END CERTIFICATE-----\\n\"\n            ]`"
      ],
      "PrivateKey": "`-----BEGIN RSA PRIVATE KEY-----\\nMIIEogIB......vhUorDg=\\n-----END RSA PRIVATE KEY-----\\n`",
      "SerialNumber": "00000000089E14D489AC80161569F34A29D6CEA7",
      "KeyAlgorithm": "RSA 2048",
      "SignatureAlgorithm": "SHA256-RSA",
      "FingerPrintSha256": "A53B846E14B33939E6CD7F9CF320FD9F96AB1D466A224CD28A38DC1388F51248",
      "FingerPrintSha1": "AAB216FF78244113D199CB87A8FE62992DB56EF0"
    },
    "ProjectName": "default",
    "Tags": [
      {
        "Key": "env",
        "Value": "test"
      }
    ],
    "CreatedTime": "2024-12-26 19:15:11"
  }
```

## Error code

The following table lists the error codes related to the business logic for this API. For common error codes, see the [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) document.

|Status code |Error code |Error message |Description |
|---|---|---|---|
|400 |NotFound.CertificateInstance |The specified certificate was not found. |The specified certificate was not found. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error. |
