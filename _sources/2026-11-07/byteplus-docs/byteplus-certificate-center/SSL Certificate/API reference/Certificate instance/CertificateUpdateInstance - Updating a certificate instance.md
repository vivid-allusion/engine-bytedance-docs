---
title: "CertificateUpdateInstance - Updating a certificate instance"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CertificateUpdateInstance"
---

Call this API to update the configuration of an SSL certificate instance, including modifying the certificate remark and enabling or disabling certificate expiration alerts.

## Precautions

Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CertificateUpdateInstance`

Action to execute. Set the value to CertificateUpdateInstance.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**InstanceId ** string必选 `Example: cert-76c529256aba4a66bedd1d2ec862****`

The ID of the certificate instance to be operated on.

> You can call the [CertificateGetInstanceList](https://www.volcengine.com/docs/6638/1413343) API to get all certificate instance IDs.

**Tag ** string`optional` `Example: doc-test`

Set remarks for the certificate.

**Options ** object`optional` `Example:`

Actions.

**ExpiredNotice ** string`optional` `Example: Enabled`

Set the status of the certificate expiration alert. This parameter can take the following values:

* `Enabled`: Enable

* `Disabled`: Disable

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
POST /?Action=CertificateUpdateInstance&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20260113T092703Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20260113/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
  "InstanceId": "cert-76c529256aba4a66bedd1d2ec862****",
  "Tag": "doc-test",
  "Options": {
    "ExpiredNotice": "Enabled"
  }
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "20260113172709015041153234FBFC98",
    "Action": "CertificateUpdateInstance",
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
|400 |SystemBusy |The system is busy. Please try again later. |The system is busy. Please retry later. |
|400 |MissingParameter |The required parameter %s is missing. |Missing required parameter. |
|400 |InvalidParameter |The specified parameter %s is invalid. |The specified parameter value is invalid. |
|400 |Expired.Certificate |Unable to do this operation because the certificate has expired. |Operations on expired certificates are not supported. |
|400 |NotFound.CertificateInstance |The specified certificate was not found. |The specified certificate does not exist. |
|400 |InvalidStatus.Instance |Unable to do this operation because the certificate status not meeting the requirements. |The current certificate status does not support this operation. |
|400 |Revoked.Certificate |Unable to do this operation because the certificate has been revoked. |Certificate already revoked. Operation not supported. |
|400 |AlreadyDisabled.ExpireNotice |The certificate expiration reminder has been turned off |Certificate expiration reminder is disabled. Do not repeat the action. |
|400 |AlreadyEnabled.ExpireNotice |The certificate expiration reminder has been turned on |Certificate expiration reminder is enabled. Do not repeat the action. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
