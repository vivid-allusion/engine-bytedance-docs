---
title: "AddCertificate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addcertificate"
---

Upload a server certificate in BytePlus CDN, used to configure HTTPS for a domain.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `AddCertificate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Source |String |No |Specifies where the certificate is stored. This parameter can take one of the following values:<br><br><br>* `cert_center`: The BytePlus Certificate Center.<br><br>* `cdn_cert_hosting`: BytePlus CDN certificate hosting. To host a certificate in CDN, submit a [support ticket](https://console.byteplus.com/workorder/create?_vtm_=a78999.b69280.0_0.0_0.0.1016_7659971919328183861).<br><br><br>The default value is `cdn_cert_hosting`. |`cert_center` |
|Certificate |String |Yes |Indicates the content of the certificate file. It is recommended to include the complete certificate chain. Line breaks in the content need to be replaced with `\r\n`. The certificate file extension is .crt or .pem. |`-----BEGIN CERTIFICATE-----\r\n......\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\n.......\r\n-----END CERTIFICATE-----` |
|PrivateKey |String |Yes |Indicates the content of the certificate private key file. The line breaks in the content should be replaced with `\r\n`. The certificate private key file must have an extension of either `.key` or `.pem`. |`-----BEGIN RSA PRIVATE KEY-----\r\n.....\r\n-----END RSA PRIVATE KEY-----` |
|Desc |String |No |Indicates the remarks of this certificate, with a length not exceeding 64 characters. |`Note` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|CertId |String |Indicates the ID of the certificate in the `origin` after it has been uploaded. |`cert-17f1d965a11342eb80d9a0ecfef35713` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=AddCertificate&Version=2021-03-01
{
    "Source": "cert_center",
    "Certificate": "-----BEGIN CERTIFICATE-----\r\nMIGrhI\r\nmg==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIIE ==\r\n-----END CERTIFICATE-----\r\n-----BEGIN CERTIFICATE-----\r\nMIID \r\nMrY=\r\n-----END CERTIFICATE-----",
    "PrivateKey": "-----BEGIN RSA PRIVATE KEY-----\r\nMIIjQVx9Q==\r\n-----END RSA PRIVATE KEY-----"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20240402082809CAFB8B06254524ECDFF3",
        "Action": "AddCertificate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "CertId": "cert-c6424725984f4c69b671e119aa0ffa69"
    }
}
```


&nbsp;
