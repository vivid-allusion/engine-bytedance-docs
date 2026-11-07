---
title: "CancelInstance - Canceling a certificate order"
product: "BytePlus Certificate Center"
product_code: "byteplus-certificate-center"
source: "https://docs.byteplus.com/en/docs/byteplus-certificate-center/CancelInstance"
---

Call this API to cancel an SSL certificate order.

## Instructions

When you successfully cancel a paid certificate order, the fee you paid for the order will be refunded to you via the original payment method.

## Precautions

* Within 5 calendar days after the certificate is issued, you can cancel the order.

* If you have not yet submitted the certificate application, or have submitted it but the certificate has not yet been issued, you can also cancel the order.

* Request frequency: Up to 20 requests per second per tenant.

## Request parameters

The following only details request parameters specific to this API and key common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

### Query

**Action ** string必选 `Example: CancelInstance`

Action to execute. Set the value to CancelInstance.

**Version ** string必选 `Example: 2024-10-01`

Current API version is 2024\-10\-01.

### Body

**Reason ** string`optional` `Example: wrong information`

Reason for canceling this certificate order.

**InstanceId ** string必选 `Example: cert-5fea76da5ec54e2999819ffc9354****`

ID of the certificate instance order to be canceled.

> You can call the [CertificateGetInstanceList](https://docs.byteplus.com/en/docs/byteplus-certificate-center/certificategetInstancelist) API to get all certificate instance IDs.

## Response parameters

This API does not have specific response parameters. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

## Request example

```json
POST /?Action=CancelInstance&Version=2024-10-01 HTTP/1.1
Host: open.byteplusapi.com
Content-Type: application/json; charset=UTF-8
X-Date: 20241105T061409Z
X-Content-Sha256: 287e874e******d653b44d21e
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20241105/ap-southeast-1/certificate_service/request, SignedHeaders=host;x-content-sha256;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f

{
    "Reason": "wrong information",
    "InstanceId": "cert-5fea76da5ec54e2999819ffc9354****"
}
```

## Response examples

```json
{
  "ResponseMetadata": {
    "RequestId": "202501091759071352441511639171A5",
    "Action": "CancelInstance",
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
|400 |NotFound.CertificateInstance |The specified certificate was not found. |The specified certificate does not exist. |
|400 |Expired.Certificate |Unable to do this operation because the certificate has expired. |Certificate already expired. Operation not supported. |
|400 |InvalidStatus.Instance |Unable to do this operation because the certificate status not meeting the requirements. |The current certificate status does not support this operation. |
|400 |Revoked.Certificate |Unable to do this operation because the certificate has been revoked. |Certificate already revoked. Operation not supported. |
|400 |OperationDenied.InvalidCancelPeriod |Unable to cancel this order because more than 5 calendar days have passed since the certificate was successfully issued. |The certificate has been issued and the cancellation period has expired; cancellation is not supported. |
|500 |InternalError |The request has failed due to an unknown error. |Unknown error |
