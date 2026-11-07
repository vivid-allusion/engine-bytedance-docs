---
title: "DescribeCipherTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describeciphertemplate-f8c12"
---

Get the configuration details of an encryption policy in BytePlus CDN.


* If the policy has been published, the API returns the configuration details of the published version (with status `running`) by default.

* If the policy has not been published, the API returns the configuration details of the version with status `draft` by default.


You can also specify a version of the policy to get its configuration details.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCipherTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the ID of the encryption policy you want to query.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to obtain the ID of the encryption policy you want to query. |`tpl-c2PRDW` |
|TemplateVersion |String |No |Indicates a version of the policy. The API returns the configuration details of this version.<br><br>The default value of this parameter is as follows:<br><br><br>* If the policy has been published, the default value is the published version (with status `running`).<br><br>* If the policy has not been published, the default value is `draft`.<br><br><br>You can call [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us) to get all versions of the policy. |`P-250414.89520` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|BoundDomains |Object[] |For the encryption policy specified by `TemplateId`, this parameter indicates a list of domain names associated with the encryption policy.<br><br>If the policy is not bound to any domain names, the value of this parameter is `null`. | |
|BoundTime |Long |Indicates the time when the encryption policy was bound to the domain name specified by `Domain`, in Unix timestamp format. |`1709174039` |
|Domain |String |Indicates one of the domain names bound to the encryption policy. |`www.example.com` |
|CreateTime |Long |Indicates the creation time of this domain name, in Unix timestamp format. |`1636612244` |
|HTTPS |Object |Indicates the configuration of the HTTPS encryption service. | |
|DisableHttp |Boolean |Indicates whether to allow requests whose scheme in the request URL is `HTTP`. This parameter has the following values:<br><br><br>* `true`: Indicates that requests with the `HTTP` scheme are allowed.<br><br>* `false`: Indicates that requests with the `HTTP` scheme are not allowed. |`false` |
|ForcedRedirect |Object |Indicates the configuration of the Protocol Redirect feature. This feature is disabled by default.<br><br>tip<br><br>`ForcedRedirect` and `HttpForcedRedirect` are mutually exclusive. If you configure one, you cannot configure the other. | |
|EnableForcedRedirect |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled. After enabling, CDN will redirect received HTTP requests to HTTPS requests.<br><br>* `false`: Indicates that this feature is disabled. After disabling, CDN will not redirect HTTP requests to HTTPS requests. |`true` |
|StatusCode |String |Indicates the redirect response status code of the CDN when an HTTPS request is received. This parameter has the following values:<br><br><br>* `301`: Indicates that the returned status code is 301.<br><br>* `302`: Indicates that the returned status code is 302. |`301` |
|HTTP2 |Boolean |Indicates whether to enable HTTP/2 support for user requests. This parameter has the following values:<br><br><br>* `true`: Indicates that HTTP/2 is enabled.<br><br>* `false`: Indicates that HTTP/2 is disabled. |`true` |
|Hsts |Object |Indicates the configuration of the HSTS feature. | |
|Subdomain |String |Indicates whether the HSTS configuration also applies to the subdomains of the domain name. This parameter has the following values:<br><br><br>* `include`: Indicates that the HSTS configuration applies to subdomain sites.<br><br>* `exclude`: Indicates that the HSTS configuration does not apply to subdomain sites. |`include` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|Ttl |Long |Indicates the cache expiration time of the `Strict-Transport-Security` response header in the browser, in seconds.<br><br>If the value of this parameter is `0`, its effect is equivalent to disabling the HSTS setting. |`300` |
|OCSP |Boolean |Indicates whether to enable OCSP Stapling. This parameter can take the following values:<br><br><br>* `true`: Indicates to enable OCSP Stapling.<br><br>* `false`: Indicates to disable OCSP Stapling. |`true` |
|TlsVersion |String[] |Indicates a list that specifies the TLS versions supported by the domain name. This parameter can take the following values:<br><br><br>* `tlsv1.0`: Indicates TLS 1.0.<br><br>* `tlsv1.1`: Indicates TLS 1.1.<br><br>* `tlsv1.2`: Indicates TLS 1.2.<br><br>* `tlsv1.3`: Indicates TLS 1.3. |`["tlsv1.1","tlsv1.2"]` |
|CertCheck |Object |Indicates the configuration of the Mutual TLS feature. | |
|CertInfoList |Object[] |Indicates a list of CA certificates. The list can contain up to two CA certificates. The CA certificates must be hosted in CDN and can use either the RSA or ECC encryption algorithm. | |
|CertId |String |Indicates the ID of a CA certificate. The ID begins with `cert_hosting-`. |`cert_hosting-31869` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|HttpForcedRedirect |Object |Indicates the configuration of the Redirect HTTPS to HTTP feature.<br><br>tip<br><br>`HttpForcedRedirect` and `ForcedRedirect` are mutually exclusive. If you configure one, you cannot configure the other. | |
|EnableForcedRedirect |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled. After enabling, CDN will redirect received HTTPS requests to HTTP requests.<br><br>* `false`: Indicates that this feature is disabled. CDN will not redirect HTTPS requests to HTTP requests. |`true` |
|StatusCode |String |Indicates the redirect status code returned by the CDN when an HTTPS request is received. This parameter has the following values: **301**, **302**, **303**, **307**, **308**.<br><br>It should be noted that:<br><br><br>* For 301 and 302, if the method used in the original request is not GET, the method used in the new request may become GET when the client sends a request to the new URL.<br><br>* For 303, the method used in the new request is GET.<br><br>* For 307 and 308, the method used in the new request is the same as the original request and will not be changed. |`302` |
|Message |String |Indicates a new description for the policy, which should not exceed 120 characters in length. |`This is a test.` |
|Quic |Object |Indicates the HTTP/3 (QUIC) configuration. | |
|Switch |Boolean |Indicates whether to enable QUIC for user requests. This parameter has the following values:<br><br><br>* `true`: Indicates that QUIC is enabled.<br><br>* `false`: Indicates that QUIC is disabled. |`true` |
|Status |String |Indicates the status of this domain name. This parameter has the following values:<br><br><br>* `online`: Indicates that the status is running normally.<br><br>* `configuring`: Indicates that the status is configuring.<br><br>* `offline`: Indicates that the status is offline. |`offline` |
|TemplateId |String |Indicates the ID of the encryption policy. |`tpl-c2PRDW` |
|Title |String |Indicates a new name for the policy, which should not exceed 100 characters in length. |`Test-Policy` |
|Type |String |Indicates the type of the encryption policy. The value of this parameter is always `cipher`. |`cipher` |
|UpdateTime |Long |Indicates the last update time of this domain name configuration, in Unix timestamp format. If this domain name configuration has not been updated after creation, the value of this parameter is the same as the value of `CreateTime`. |`1639621409` |
|Exception |Boolean |Indicates whether the encryption policy contains special configurations. Special configurations refer to those not operated by users but by BytePlus engineers. This parameter can take the following values:<br><br><br>* `true`: Indicates it contains special configurations.<br><br>* `false`: Indicates it does not contain special configurations. |`false` |
|Project |String |Indicates the project to which this domain name belongs. |`default` |
|ProdVersion |String |Indicates the published version (with status `running`) of the policy. If there is no version with status `running`, this parameter value is empty (""). |`P-250414.89520` |
|DomainCount |Long |域名数量 | |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCipherTemplate&Version=2021-03-01
{
    "TemplateId": "tpl-c57pd62"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "20250825065108DF9658839E53B0AEB207",
        "Action": "DescribeCipherTemplate",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "BoundDomains": [
            {
                "BoundTime": 1755585664,
                "Domain": "www.example.com"
            }
        ],
        "CreateTime": 1755585663,
        "Exception": false,
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
        "Message": "This is a test message",
        "ProdVersion": "P-250819.88575",
        "Project": "default",
        "Quic": {
            "Switch": true
        },
        "Status": "locked",
        "TemplateId": "tpl-c57pd62",
        "Title": "My Policy",
        "Type": "cipher",
        "UpdateTime": 1755585664
    }
}
```


&nbsp;
