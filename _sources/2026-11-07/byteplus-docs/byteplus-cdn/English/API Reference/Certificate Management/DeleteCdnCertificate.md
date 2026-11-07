---
title: "DeleteCdnCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DeleteCdnCertificate_en-us"
---

Deletes a certificate that is hosted on CDN. You can only delete certificates that are not associated with any domain names.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DeleteCdnCertificate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DeleteCdnCertificate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|CertId |String |Yes |The ID of the certificate to be deleted. The certificate ID starts with `cert_hosting`.<br><br>You can call [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcertinfo) to get the list of certificate IDs. |`cert_hosting-4041`<br><br> |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DeleteCdnCertificate&Version=2021-03-01
{
    "CertId": "cert_hosting-4041"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202207131500530102120352272280EC8F",
        "Action": "DeleteCdnCertificate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```
