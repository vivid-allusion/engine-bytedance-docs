---
title: "CertificateDeleteInstance - Deleting a certificate instance"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateDeleteInstance_-_Deleting_a_certificate_instance"
---

Call this API to delete an SSL certificate instance.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Precautions

Only certificate instances that meet specific conditions can be deleted. For more information, see [Deleting a condition](https://docs.byteplus.com/en/docs/byteplus-certificate-center/docs-deleting-an-ssl-certificate#operation-steps).

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CertificateDeleteInstance`

Action to execute. Set the value to CertificateDeleteInstance.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**InstanceId ** string必选 `Example: cert-5fea76da5ec54e2999819ffc5aba****`

Certificate instance ID to be deleted.

> You can call the [CertificateGetInstanceList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificategetInstancelist) API to get all certificate instance IDs.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
POST /?Action=CertificateDeleteInstance&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260113T092810Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260113/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "cert-5fea76da5ec54e2999819ffc5aba****"
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202601131728201411872440271C81E8",
    "Action": "CertificateDeleteInstance",
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
|400 |MalformedRequest |The request is malformed |Request parameters format is invalid. |
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|400 |SystemBusy |The system is busy. Please try again later. |The system is busy. Please retry later. |
|400 |NotFound.CertificateInstance |The specified certificate was not found. |The specified certificate does not exist. |
|400 |Deployed.Certificate |Unable to do this operation because the certificate has been deployed. |This certificate has been deployed and does not support the current action |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
