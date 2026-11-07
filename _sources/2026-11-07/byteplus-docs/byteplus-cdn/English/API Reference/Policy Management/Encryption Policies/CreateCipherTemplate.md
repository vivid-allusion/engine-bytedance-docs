---
title: "CreateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-createciphertemplate-cf232"
---

Create an encryption policy in BytePlus CDN.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=CreateCipherTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `CreateCipherTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Title |String |Yes |Indicates the name of the encryption policy you want to create. The name must not exceed 100 characters. |`TestPolicy` |
|HTTPS |Object |No |Indicates the configuration of the HTTPS encryption service. | |
|DisableHttp |Boolean |No |Indicates whether the CDN accepts HTTP user requests. This parameter can take the following values:<br><br><br>* `true`: Indicates that it does not accept. If an HTTP request is received, the CDN will reject the request.<br><br>* `false`: Indicates that it accepts.<br><br><br>The default value for this parameter is `false`. |`false` |
|ForcedRedirect |Object |No |Indicates the configuration of the Protocol Redirect feature. This feature is disabled by default.<br><br>tip<br><br>`ForcedRedirect` and `HttpForcedRedirect` are mutually exclusive. If you configure one, you cannot configure the other. | |
|EnableForcedRedirect |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled. Once enabled, the CDN will redirect received HTTP requests to HTTPS requests.<br><br>* `false`: Indicates that this feature is disabled. The CDN will not redirect HTTP requests to HTTPS requests. |`true` |
|StatusCode |String |Yes |Indicates the redirect response status code of the CDN when an HTTP request is received. This parameter has the following values: **301**, **302**, **303**, **307**, **308**.<br><br>The default value of this parameter is `301`.<br><br>Please note that:<br><br><br>* For 301 and 302, if the original request method is not GET, the method used by the client when sending a request to the new URL may change to GET.\\|<br><br>* For 303, the method used for the new request is GET.\\|<br><br>* For 307 and 308, the method used for the new request is the same as the original request and will not be changed. |`301` |
|HTTP2 |Boolean |No |Indicates whether to enable HTTP/2 support for user requests. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling HTTP/2.<br><br>* `false`: Indicates disabling HTTP/2.<br><br><br>The default value for this parameter is `true`. |`true` |
|Hsts |Object |No |Indicates the HSTS feature. This feature is disabled by default. | |
|Subdomain |String |No |Indicates whether the HSTS configuration should also be applied to the subdomains of the domain name. This parameter can take the following values:<br><br><br>* `include`: Indicates that HSTS settings apply to subdomains.<br><br>* `exclude`: Indicates that HSTS settings do not apply to subdomains.<br><br><br>The default value for this parameter is `exclude`. |`include` |
|Switch |Boolean |No |Indicates whether to enable HSTS. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling HSTS.<br><br>* `false`: Indicates disabling HSTS.<br><br><br>The default value for this parameter is `false`. |`true` |
|Ttl |Long |No |Indicates the expiration time for the `Strict-Transport-Security` response header in the browser cache, in seconds.<br><br>If `Switch` is `true`, this parameter is required. The value range for this parameter is 0 \- 31,536,000 seconds, where 31,536,000 seconds represents 365 days.<br><br>If the value of this parameter is `0`, it is equivalent to disabling the HSTS settings. |`300` |
|OCSP |Boolean |No |Indicates whether to enable OCSP Stapling. This parameter can take the following values:<br><br><br>* `true`: Indicates to enable OCSP Stapling.<br><br>* `false`: Indicates to disable OCSP Stapling.<br><br><br>The default value for this parameter is `false`. |`true` |
|TlsVersion |String[] |No |Indicates a list that specifies the TLS versions supported by the domain name. This parameter can take the following values:<br><br><br>* `tlsv1.0`: Indicates TLS 1.0.<br><br>* `tlsv1.1`: Indicates TLS 1.1.<br><br>* `tlsv1.2`: Indicates TLS 1.2.<br><br>* `tlsv1.3`: Indicates TLS 1.3.<br><br><br>The default value for this parameter is `["tlsv1.1", "tlsv1.2", "tlsv1.3"]` |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |No |Indicates the configuration of the Mutual TLS feature. | |
|CertInfoList |Object[] |No |Indicates a list of CA certificates. The list can contain up to two CA certificates. The CA certificates must be hosted in CDN and can use either the RSA or ECC encryption algorithm.<br><br>If the certificate to associate has not been uploaded, call [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addcertificate) to upload it to CDN first. | |
|CertId |String |No |Indicates the ID of a CA certificate. The ID begins with `cert_hosting-`.<br><br>Call [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcertinfo) to obtain the ID of the certificate to associate. |`cert_hosting-31869` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |
|HttpForcedRedirect |Object |No |Indicates the configuration of the Redirect HTTPS to HTTP feature.<br><br>tip<br><br>`HttpForcedRedirect` and `ForcedRedirect` are mutually exclusive. If you configure one, you cannot configure the other. | |
|EnableForcedRedirect |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature. Once enabled, the CDN will redirect received HTTPS requests to HTTP requests.<br><br>* `false`: Indicates disabling this feature. The CDN will not redirect HTTPS requests to HTTP requests. |`true` |
|StatusCode |String |Yes |Indicates the redirect response status code of the CDN when an HTTPS request is received. This parameter has the following values: **301**, **302**, **303**, **307**, **308**.<br><br>The default value of this parameter is `301`.<br><br>Please note that:<br><br><br>* For 301 and 302, if the original request method is not GET, the method used by the client when sending a request to the new URL may change to GET.\\|<br><br>* For 303, the method used for the new request is GET.\\|<br><br>* For 307 and 308, the method used for the new request is the same as the original request and will not be changed. |`302` |
|Message |String |No |Indicates the description of the encryption policy, which must not exceed 120 characters. |`This is a test.` |
|Quic |Object |No |Indicates the HTTP/3 (QUIC) configuration. | |
|Switch |Boolean |Yes |Indicates whether to enable HTTP/3 (QUIC) support for user requests. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling HTTP/3 (QUIC).<br><br>* `false`: Indicates disabling HTTP/3 (QUIC). |`true` |
|Project |String |No |Indicates the project to which this encryption policy belongs. The default value of the parameter is `default`, indicating the Default project. |`default` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|TemplateId |String |Indicates the ID of the created encryption policy. |`tpl-cqwYjZ` |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=CreateCipherTemplate&Version=2021-03-01
{
    "Title": "My Policy",
    "Message": "This is a test.",
    "Project": "default",
    "HTTPS": {
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "303"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 50
        },
        "OCSP": true,
        "TlsVersion": [
            "tlsv1.1",
            "tlsv1.2"
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "301"
    },
    "Quic": {
        "Switch": true
    }
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "2025082506361220B64EDF1EC3CBBB1ADE",
        "Action": "CreateCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "TemplateId": "tpl-ceg0x7z"
    }
}
```


&nbsp;
