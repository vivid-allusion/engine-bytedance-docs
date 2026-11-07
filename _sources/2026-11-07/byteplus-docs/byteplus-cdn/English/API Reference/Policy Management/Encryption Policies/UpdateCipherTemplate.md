---
title: "UpdateCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateciphertemplate-ac087"
---

Modify a encryption policy configuration in BytePlus CDN.

In BytePlus CDN, if you need to modify a domain configuration, you can use any of the following methods:


* Method 1: Directly modify the configurations of the domain .

* Method 2: Modify the policy configurations bound to the domain.


This article describes how to implement the modifications of encryption policies in Method 2 through API.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">For the differences between these two methods, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/domain-management_en">Domain Configuration</a>.</div>


* <div data-tips="true" data-tips-type="tip">For how to implement the update of delivery policies in Method 2 through API, see <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/reference-updateservicetemplate">UpdateServiceTemplate</a>.</div>



Except for `Title` and `Message`, updating other parameters requires you to specify `TemplateVersion` as `draft` when calling `UpdateCipherTemplate`. This means the policy to be updated must have a Draft version. To ensure the policy to be updated has a Draft version, follow these steps:


1. Call the `DescribeTemplateReleaseVersions` API for this policy.

2. Check if the Draft version (`"Version": "draft"`) exists in the version list returned by the API.

* If the Draft version exists, you can call `UpdateCipherTemplate` for this policy.

* Otherwise, you need to first call `CreateTemplateVersion` for this policy to create a Draft version, then call `UpdateCipherTemplate`.


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This API performs an overwrite modification on the corresponding domain configuration module, with the following notes:</div>



* <div data-tips="true" data-tips-type="warning">When you create an API request, if a module is not specified, its existing configuration remains unchanged after you submit the API request.</div>


* <div data-tips="true" data-tips-type="warning">If you specify a module but don't specify an optional parameter within that module, the parameter will use its default value. After you submit the API request, the existing value of that parameter will be overwritten by the default value.</div>



<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UpdateCipherTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the ID of the encryption policy you wish to modify.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to get the ID of the encryption policy you want to modify. |`tpl-c2vy7q` |
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
|Message |String |No |Indicates a new description for the policy, which should not exceed 120 characters in length. |`This is a test.` |
|Quic |Object |No |Indicates the HTTP/3 (QUIC) configuration. | |
|Switch |Boolean |Yes |Indicates whether to enable HTTP/3 (QUIC) support for user requests. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling HTTP/3 (QUIC).<br><br>* `false`: Indicates disabling HTTP/3 (QUIC). |`true` |
|Title |String |No |Indicates a new name for the policy, which should not exceed 100 characters in length. |`Test-Policy` |
|TemplateVersion |String |No |Indicates the version of the policy to be updated.<br><br><br>* If the parameter to be updated is `Title` or `Message`, you don't need to specify this parameter. These two parameters are not related to policy versions.<br><br>* If the parameter to be updated is not `Title` or `Message`, you must specify this parameter as `draft`. See the description at the beginning of the document. |`draft` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=UpdateCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c2vy7q",
    "TemplateVersion": "draft",
    "HTTPS": {
        "DisableHttp": false,
        "ForcedRedirect": {
            "EnableForcedRedirect": true,
            "StatusCode": "302"
        },
        "HTTP2": true,
        "Hsts": {
            "Subdomain": "include",
            "Switch": true,
            "Ttl": 1800
        },
        "OCSP": true,
        "TlsVersion": [
            "tlsv1.2",
            "tlsv1.3"
        ]
    },
    "CertCheck": {
        "Switch": true,
        "CertInfoList": [
            {
                "CertId": "cert_hosting-1000034057"
            },
            {
                "CertId": "cert_hosting-1000009760"
            }
        ]
    },
    "HttpForcedRedirect": {
        "EnableForcedRedirect": false,
        "StatusCode": "302"
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
        "RequestId": "20210915182437010194100054410018B1",
        "Action": "UpdateCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    }
}
```


&nbsp;
