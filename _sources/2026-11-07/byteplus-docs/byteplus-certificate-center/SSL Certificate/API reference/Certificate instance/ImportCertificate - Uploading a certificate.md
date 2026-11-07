---
title: "ImportCertificate - Uploading a certificate"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/reference-uploadcertificate"
---

Upload a certificate to the BytePlus Certificate Center.

## Instructions

* Certificates using the following key algorithms are allowed to be uploaded to the certificate center: RSA and ECC.

* The certificate to be uploaded must be valid (not expired and not revoked).

* The certificate file and private key file must be uploaded together.

* Upload up to 500 certificates.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For mor information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: ImportCertificate`

Action to execute. Set the value to `ImportCertificate`.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**Tag ** string`optional` `Example: uploaded-cert`

Add a remark for the certificate instance.

**ProjectName ** string`optional` `Example: default`

The name of the BytePlus project to which the certificate instance belongs. If this parameter is not specified, the certificate instance will belong to the `default` project.

> Project is a resource management tool provided by BytePlus. You can use projects to group cloud resources, and then set access control policies or query billing statements based on projects. For more information, see [Project overview](https://docs.byteplus.com/en/docs/resourcemanagement/Project_Overview).

**Repeatable ** boolean`optional` `Example: false`

Allow uploading an identical certificate. Default value: `false`.

By default, the BytePlus Certificate Center checks whether the certificate you are uploading is identical to an existing certificate (determined by the certificate fingerprint). If an identical certificate already exists, the new certificate cannot be uploaded, and the API will return the ID of the existing certificate.

**NoVerifyAndFixChain ** boolean`optional` `Example: false`

Ignore the certificate integrity check. Default value: `false`.

* By default, the BytePlus Certificate Center performs an integrity check on certificates to be uploaded to ensure they can be used properly.

* It is recommended to keep the default setting and do not change it. Ignoring the integrity check may allow you to upload and use certificates with security risks, which could affect your production services.

* The certificate integrity check covers the following: verifying whether the certificate chain is complete, whether each certificate in the chain is issued by the next certificate, and whether the certificates use insecure digest algorithms.

   * If the certificate chain is incomplete, the BytePlus Certificate Center will automatically complete it before uploading;

   * If the certificate issuance relationship verification fails, or if the certificate uses an insecure algorithm, the certificate cannot be uploaded.

**CertificateInfo ** object`optional` `Example:`

Used to upload certificates that use RSA or ECC algorithms.

> CertificateInfo must include both CertificateChain and PrivateKey.

**CertificateChain ** string`optional` `Example: -----BEGIN CERTIFICATE-----\n......\n-----END CERTIFICATE-----`

Content of the certificate (or certificate chain).

Cannot contain line breaks. If line breaks are required, use `\n`.

**PrivateKey ** string`optional` `Example: -----BEGIN RSA PRIVATE KEY-----\n......\n-----END RSA PRIVATE KEY-----`

The content of the private key corresponding to the certificate.

Cannot contain line breaks. If line breaks are required, use `\n`.

**Tags ** object[]`optional` `Example:`

The resource tags bound to the certificate instance.

**Key ** string必选 `Example: env`

The tag key.

**Value ** string必选 `Example: test`

The tag value.

## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**InstanceId ** string`Example: cert-5fea76da5ec54e2999819ffc5aba****`

Certificate instance ID.

> This parameter will have a value only when the certificate is uploaded successfully.

**RepeatId ** string`Example: cert-5fea76da5ec54e2999819ffc5aba****`

If the uploaded certificate is identical to an existing certificate in the certificate center, the certificate cannot be uploaded, and this parameter will return the instance ID of the identical certificate. If there are multiple identical certificates, the instance ID of the certificate with the earliest creation time is returned.

> If the request parameter `repeatable` is `true`, this parameter will always return empty.

## Request example

```json
POST /?Action=ImportCertificate&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20241105T031307Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20241105/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
    "Tag": "uploaded-cert",
    "ProjectName": "default",
    "Repeatable": true,
    "NoVerifyAndFixChain": false,
    "CertificateInfo": {
        "CertificateChain": "-----BEGIN CERTIFICATE-----\n...\n-----END CERTIFICATE-----",
        "PrivateKey": "-----BEGIN RSA PRIVATE KEY-----\n......\n-----END RSA PRIVATE KEY-----"
    }
}
```

## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "2024110511135900003918523121038B",
        "Action": "ImportCertificate",
        "Version": "2024-10-01",
        "Service": "certificate_service",
        "Region": "ap-southeast-1"
    },
    "Result": {
        "InstanceId": "cert-5fea76da5ec54e2999819ffc5aba****",
        "RepeatId": ""
    }
}
```

## Error codes

The following table lists the error codes related to the business logic for this API. For details, see [Common error codes](https://docs.byteplus.com/en/docs/ecs/Public-error-codes).

|HTTP code |Error code |Error message |Description |
|---|---|---|---|
|400 |SystemBusy |The system is busy. Please try again later. |The system is busy. Try again later. |
|400 |MalformedRequest |The request is malformed |The request parameters are invalid or improperly formatted. |
|400 |QuotaExceeded |%s has exceeded the quota. example: The memory size of the specified disk has exceeded the quota. |The resource quota has been exceeded. |
|400 |NotFound.Project |The specified project is not found |The specified project does not exist. |
|400 |Expired.Certificate |Unable to do this operation because the certificate has expired. |The operation cannot be performed on an expired certificate. |
|400 |Unsupported.PrivateKeyAlgorithm |The private key algorithm is not supported. |The private key uses an unsupported algorithm. |
|400 |Malformed.PrivateKey |Failed to decode private key. |Failed to parse the private key. |
|400 |NotMatch.KeyPair |Failed to verify the public and private key. |The public and private keys do not match. |
|400 |NotMatch.CertificateKeyUsage |The KeyUsage of the signature certificate chain and/or encryption certificate chain is illegal. |The KeyUsage extension in the signing or encryption certificate is invalid. |
|400 |Malformed.Certificate |Failed to decode the certificate. |Failed to parse the certificate. |
|400 |UnknownError.ObtainCertChain |Failed to obtain the certificate chain. |Unable to reconstruct or complete the certificate chain. |
|500 |InternalError |The request has failed due to an unknown error. |An unexpected internal error occurred. |
