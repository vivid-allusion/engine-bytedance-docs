---
title: "BatchUpdateCdnConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/BatchUpdateCdnConfig_en-us"
---

Updates the configurations of multiple domains in BytePlus CDN.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">You cannot update a domain whose <code>Status</code> is <code>offline</code>. To get the status of a domain, call <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_en-us">DescribeCdnConfig</a>.</div>


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=BatchUpdateCdnConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `BatchUpdateCdnConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body

<span id="general-configurations"></span>
## General Configurations

<span id="domain-names"></span>
### Domain Names


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domains |String[] |Yes |Indicates the list of domains to be updated, containing up to 50 domains. |`["abc.example.com","zzz.example.com"]` |


<span id="aggregate"></span>
### Aggregate


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Aggregate |Boolean |No |This parameter has the following effects:<br><br><br>* Determines whether to display the configuration update result for each domain in the API response.<br><br>* Determines the behavior of CDN when it fails to update the configuration of a domain in the `Domains` list.<br><br><br>The parameter can have the following values:<br><br><br>* `true`: The API response does not display the configuration update result for each domain. In addition, if CDN fails to update the configuration of a domain, the API will abandon updating the configurations of all domains, and the response body will contain an `Error` structure. This structure contains the error information of the domain that failed to be updated. See Example 1.<br><br>* `false`: The API response displays the configuration update result for each domain. The response body will contain a `DeployResult` structure. This structure contains the configuration update result for each domain. See Example 2. In addition, if CDN fails to update the configuration of a domain, CDN will continue to update the configurations of other domains.<br><br><br>The default value of this parameter is `true`. |`false` |


<span id="ipv6"></span>
### IPv6


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|IPv6 |Object |No |Indicates the IPv6 configuration. | |
|Switch |Boolean |Yes |Indicates whether to enable IPv6 support for user requests. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling IPv6.<br><br>* `false`: Indicates disabling IPv6. |`true` |


<span id="standard-origins"></span>
### Standard Origins


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Origin |Object[] |No |Indicates the standard origin configuration. | |
|OriginAction |Object |Yes |Indicates the configuration of origins, which applies to all user requests. | |
|OriginLines |Object[] |Yes |Indicates an origin list. The list can contain up to 50 origins. | |
|Address |String |Yes |Indicates the address of an origin server in the list. This parameter has the following descriptions:<br><br><br>* If `InstanceType` is `ip`, you are specifying the IP address of the origin server. The IP address can be an IPv4 or IPv6 address.<br><br>* If `InstanceType` is `domain`, you are specifying the domain name of the origin server. The domain name cannot be a wildcard domain, nor can it be the same as the domain name to be bound to this policy.<br><br>* If `InstanceType` is `tos`, you are specifying the bucket domain name. The bucket domain name can be the one assigned by the cloud provider or a custom domain name you set for the bucket with the cloud provider. The bucket domain name cannot contain `https://` and its length cannot exceed 100 characters. The bucket can be from BytePlus TOS, Alibaba Cloud OSS, Tencent Cloud COS, AWS S3, or any third\-party object storage service that uses an S3\-compatible authentication method.<br><br><br>tip<br><br><br>* If the bucket is from the TOS service under your account, you need to open the configuration page for this domain name in the CDN console before calling this API. On this page, click **Authorize** to grant CDN access to the TOS service under your account.<br><br>* In Azure Blob Storage, an object storage bucket is called a container. |`www.example.com` |
|InstanceType |String |Yes |Indicates the type of the origin. This parameter has the following values:<br><br><br>* `ip`: indicates IP address.<br><br>* `domain`: indicates domain name.<br><br>* `tos`: indicates object storage bucket.<br><br><br>warning<br><br>When CDN sends origin requests to an object storage origin, the origin request uses the same method as the user request. By default, user requests can use DELETE, GET, HEAD, POST, PUT, PATCH, OPTIONS, CONNECT methods. If you don't want origin requests to use certain request methods, for example, if you don't want origin requests to use the DELETE method which might accidentally delete files on the origin, it's recommended to take the following steps:<br><br><br>1. Set permissions in the object storage service where the bucket is located to prevent unintended operations.<br><br>2. In CDN's `MethodDeniedRule` feature, specify the request methods that CDN doesn't support. |`ip` |
|OriginType |String |Yes |Indicates the role of this origin. This parameter has the following values:<br><br><br>* `primary`: indicates primary origin.<br><br>* `backup`: indicates secondary origin.<br><br><br>The origin list must contain at least one primary origin. Secondary origins are optional. |`primary` |
|HttpPort |String |No |Indicates the port that CDN uses to access this origin when using HTTP protocol. The value range is 1\-65535, with a default value of `80`. If the origin server hasn't opened this port, you don't need to specify this parameter.<br><br>This parameter is only valid when `InstanceType` is `ip` or `domain`. |`80` |
|HttpsPort |String |No |Indicates the port that CDN uses to access this origin when using HTTPS protocol. The value range is 1\-65535, with a default value of `443`. If the origin server hasn't opened this port, you don't need to specify this parameter.<br><br>This parameter is only valid when `InstanceType` is `ip` or `domain`. |`443` |
|OriginHost |String |No |Indicates the site domain that origin requests access, which is applicable when there are multiple sites on the origin server.<br><br><br>* The default value of this parameter is the same as the global `OriginHost`, but has a higher priority than the global `OriginHost` parameter.<br><br>* The length of this parameter's value cannot exceed 1,024 characters.<br><br>* If you do not modify `Address` or specify `OriginHost` when calling this API, `OriginHost` will not be overwritten by the default value but will retain its current value. |`img.example.com` |
|PrivateBucketAccess |Boolean |No |Specifies whether the bucket is private. This parameter is valid only when `InstanceType` is `tos`. Valid values:<br><br><br>* `true`: The bucket is private.<br><br>* `false`: The bucket is not private.<br><br><br>The default value is `false`. |`false` |
|PrivateBucketAuth |Object |No |Specifies the authentication configuration for accessing the bucket.<br><br>tip<br><br>If the bucket is a TOS bucket under the current account and you want to use cross\-service authorization to access the TOS bucket, you do not need to specify this parameter. Cross\-service authorization does not require an AccessKey. | |
|Switch |Boolean |Yes |Indicates whether credentials are required to access the bucket. This parameter has the following values:<br><br><br>* `true`: Indicates that credentials are required.<br><br>* `false`: Indicates that no credentials are required. |`false` |
|AuthType |String |No |Specifies the authentication method used by the object storage service of the bucket. Valid values:<br><br><br>* `tos`: BytePlus TOS. You use an AccessKey to access the TOS bucket.<br><br>* `cos`: Tencent Cloud COS.<br><br>* `oss`: Alibaba Cloud OSS.<br><br>* `azure`: Microsoft Azure.<br><br>* `aws_common`: AWS S3 and S3\-compatible authentication methods. |`cos` |
|TosAuthInformation |Object |No |Specifies the access credential (AccessKey) for the bucket. | |
|AccessKeyId |String |No |The AccessKey ID in the access credential, which is referred to as SecretId in Tencent Cloud. Its length is 5 to 100 characters. |`xxxxxxxx` |
|AccessKeySecret |String |No |The AccessKey Secret in the access credential, which is referred to as SecretKey in Tencent Cloud. Its length is 5 to 100 characters. |`xxxxxx` |
|AccountKey |String |No |Indicates your Azure storage account's shared key. This parameter is only valid when `AuthType` is `azure`. |`xxxxxx` |
|Region |String |No |Indicates information of the region where the bucket is located, which is the region code of the bucket. The region code is involved in signature calculation.<br><br>If `AuthType` is `aws_common` and `PrivateBucketAccess` is `true`, you must specify this parameter. |`us-east-1` |
|Weight |String |No |Indicates the weight of this origin, with a valid range of 1\-100, the default value is `1`. The higher the weight, the greater the likelihood that the origin will be selected by the CDN when sending an origin request.<br><br>This parameter is only valid when `InstanceType` is `ip` or `domain`. |`100` |
|BucketName |String |No |Indicates your Azure storage account name. This parameter is only valid when `AuthType` is `azure`. |`mystorageaccount` |


<span id="conditional-origins"></span>
### Conditional Origins


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ConditionalOrigin |Object |No |Indicates the configuration of the Conditional Origin feature. | |
|OriginRules |Object[] |No |Indicates a list of rules. Each rule in the list defines a set of matching conditions and the actions that CDN performs on requests that meet the matching conditions.<br><br>The list can contain up to 20 rules.<br><br>When a user request is received, CDN matches the rules with the request in order of priority, from high to low. If a rule matches the request, CDN stops processing the remaining rules. | |
|Actions |Object |No |Indicates the action configuration defined in a rule. | |
|OriginLines |Object[] |No |Indicates a list of origin servers. Currently, the list can only contain one origin server. | |
|Address |String |No |Indicates the address of an origin server.<br><br><br>* When `InstanceType` is `ip`, `Address` indicates an IPv4 or IPv6 address.<br><br>* When `InstanceType` is `domain`, `Address` indicates a domain name. The domain name cannot be a wildcard domain name.<br><br>* If `InstanceType` is `storage`, you specify the bucket domain name, which can be the bucket domain name assigned by the cloud vendor, or the custom domain name you set for the bucket in the cloud vendor. The bucket domain name cannot contain `https://` and the length cannot exceed 100 characters. The bucket can be from BytePlus TOS, Alibaba Cloud OSS, Tencent Cloud COS, AWS S3, or any third\-party object storage service that is compatible with S3 authentication, such as Qiniu Cloud, Huawei Cloud, etc. |`203.0.113.8` |
|HttpPort |String |No |Indicates the port that CDN uses when accessing the origin server using the HTTP protocol. The value range is 1\-65535, and the default value is `80`. If the origin server has not opened this port, you do not need to specify this parameter. |`80` |
|HttpsPort |String |No |Indicates the port that CDN uses when accessing the origin server using the HTTPS protocol. The value range is 1\-65535, and the default value is `443`. If the origin server has not opened this port, you do not need to specify this parameter. |`443` |
|InstanceType |String |No |Indicates the type of the origin server. This parameter has the following values:<br><br><br>* `ip`: Indicates an IP address.<br><br>* `domain`: Indicates a domain name.<br><br>* `storage`: Indicates an object storage bucket.<br><br><br>warning<br><br>When CDN sends an origin request to an object storage origin server, the method used for the origin request is the same as the user request. By default, the request methods that can be used for user requests are DELETE, GET, HEAD, POST, PUT, PATCH, OPTIONS, CONNECT. If you do not want the origin request to use certain request methods, for example, you do not want the origin request to use the DELETE method, which may cause accidental deletion of files on the origin server, it is recommended that you take the following steps:<br><br><br>1. Set permissions in the object storage service where the bucket is located to prevent unexpected operations.<br><br>2. In the `MethodDeniedRule` feature of CDN, specify the request methods that CDN does not support. |`ip` |
|OriginHost |String |No |Indicates the domain name of the site accessed by the origin request, which is applicable to the case where there are multiple sites on the origin server.<br><br><br>* The default value of this parameter is the same as the global `OriginHost`, but its priority is higher than the global `OriginHost` parameter.<br><br>* The length of this parameter value cannot exceed 1,024 characters.<br><br>* If you do not modify `Address` or specify `OriginHost` when calling this API, `OriginHost` will not be overwritten by the default value, but will remain its current value. |`img.example.com` |
|BucketSource |String |No |Specifies the authentication method used by the object storage service of the bucket. Valid values:<br><br><br>* `tos`: BytePlus TOS.<br><br>* `cos`: Tencent Cloud COS.<br><br>* `oss`: Alibaba Cloud OSS.<br><br>* `azure`: Microsoft Azure.<br><br>* `aws_common`: AWS S3 and S3\-compatible authentication methods. |`aws_common` |
|PrivateBucketAccess |Boolean |No |Specifies whether the bucket is private. This parameter is valid only when `InstanceType` is `storage`. Valid values:<br><br><br>* `true`: The bucket is private.<br><br>* `false`: The bucket is not private.<br><br><br>The default value is `false`. |`false` |
|TosAuthInformation |Object |No |Specifies the authentication configuration for accessing the bucket.<br><br>tip<br><br>If the bucket is a TOS bucket under the current account and you want to use cross\-service authorization to access the TOS bucket, you do not need to specify this parameter. Cross\-service authorization does not require an AccessKey. | |
|AccessKeyId |String |No |The AccessKey ID in the access credential, which is referred to as SecretId in Tencent Cloud. |`xxxxxxxx` |
|AccessKeySecret |String |No |The AccessKey Secret in the access credential, which is referred to as SecretKey in Tencent Cloud. |`xxxxxx` |
|Region |String |No |Indicates the region information of the bucket, that is, the region code of the bucket. The region code participates in the calculation of the signature.<br><br>If `BucketSource` is `aws_common` and `PrivateBucketAccess` is `true`, you must specify this parameter. |`ap-southeast-1` |
|AccountName |String |No |Indicates your Azure storage account's shared key. This parameter is only valid when `AuthType` is `azure`. |`xxxxxxxxxxxxxxxxxxxx` |
|OriginType |String |No |Indicates the role of this origin. This parameter has the following values:<br><br><br>* `primary`: indicates primary origin.<br><br>* `backup`: indicates secondary origin.<br><br><br>The origin list must contain at least one primary origin. Backup origins are optional. |`primary` |
|Weight |String |No |Indicates the weight of the origin. Valid values range from 1 to 100, and the default value is 1. An origin with a higher weight is more likely to be selected when CDN sends an origin request. |`1` |
|Condition |Object |No |Indicates the configuration of the matching conditions in this rule. | |
|ConditionGroups |Object[] |No |Indicates a list of matching conditions. The list can contain up to 50 matching conditions. | |
|Condition |Object |No |Indicates the configuration of a matching condition. | |
|Object |String |No |Indicates a matching object. This parameter has the following values:<br><br><br>* `path`: Indicates the full path in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `full_querystring`: Indicates all query parameters in the request URL.<br><br>* `client_ip`: Indicates the client's IP address.<br><br>* `query_name`: Indicates a query parameter in the request URL.<br><br>* `customize`: Indicates a header in the user request. |`path` |
|Operator |String |No |Indicates the matching type. For each `Object`, the specifiable `Operator` is as follows:<br><br><br>* `path`: You can specify `equal`, `not_equal`, `regex_match`, `regex_not_match`.<br><br>* `directory`: You can specify `equal`, `not_equal`.<br><br>* `filetype`: You can specify `equal`, `not_equal`.<br><br>* `full_querystring`: You can specify `regex_match`, `regex_not_match`.<br><br>* `client_ip`: You can specify `equal`, `not_equal`, `belong`, `not_belong`.<br><br>* `query_name`: You can specify `equal`, `not_equal`, `regex_match`, `regex_not_match`, `exist`, `not_exist`, `empty`, `not_empty`.<br><br>* `customize`: You can specify `equal`, `not_equal`, `empty`, `not_empty`.<br><br><br>Among the above values, the descriptions of `belong` and `not_belong` are as follows:<br><br><br>* `belong`: Indicates that if the client IP address's location is in the list of countries and regions represented by `Value`, the request meets this matching condition.<br><br>* `not_belong`: Indicates that if the client IP address's location is not in the list of countries and regions represented by `Value`, the request meets this matching condition. |`equal` |
|Value |String[] |No |Indicates one or more matching values, separated by semicolons (;). However, when `Object` is `customize`, multiple header values are separated by vertical bars (\\|). For the input requirements of the configuration value, see [Console Description Document](https://docs.byteplus.com/en/docs/byteplus-cdn/conditional_origins_en).<br><br>tip<br><br>When `Object` is `client_ip` and `Operator` is `belong` or `not_belong`, the matching value is the code of one or more countries or regions. You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to get the codes of all countries and regions supported by CDN. When calling `DescribeCdnRegionAndIsp`, please specify the request parameter `Area` as `Global`. |`/www/img/my*image.png;/doc` |
|Name |String |No |* When `Object` is `query_name`, this parameter indicates the name of the specified query parameter.<br><br>* When `Object` is `customize`, this parameter indicates the name of the specified request header.<br><br>* When `Object` is other values, this parameter does not need to be specified. |`myparam` |
|Type |String |No |* When `Object` is `query_name`, the value of this parameter must be `querystring`.<br><br>* When `Object` is `customize`, the value of this parameter must be `request_header`.<br><br>* When `Object` is other values, this parameter does not need to be specified. |`request_header` |
|Connective |String |No |Indicates the relationship between these matching conditions. This parameter has the following values:<br><br><br>* `or`: Indicates that the relationship is "or".<br><br>* `and`: Indicates that the relationship is "and".<br><br><br>The default value of this parameter is `or`. |`and` |
|IsGroup |Boolean |No |The value of this parameter must be `true`. |`true` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="origin-protocol"></span>
### Origin Protocol


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginProtocol |String |Yes |Indicates the configuration of the Origin Protocol feature. This parameter can take the following values:<br><br><br>* `http`: indicates that origin requests use the HTTP protocol.<br><br>* `https`: indicates that origin requests use the HTTPS protocol.<br><br>* `followclient`: indicates that the protocol used by origin requests is the same as user requests. |`http` |


<span id="origin-certificate-validation"></span>
### Origin Certificate Validation


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginCertCheck |Object |No |Indicates the configuration of the Origin Certificate Validation feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create).<br><br>After this feature is enabled, CDN validates the legitimacy of the origin server certificate, including whether the certificate has been revoked, whether the certificate is issued by a trusted CA, whether the certificate matches the origin server domain, and more. CDN has built\-in root certificates from common trusted CAs. If the origin server certificate fails validation, CDN performs an [origin request retry](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en). If the origin server certificate still fails validation during the retry, CDN determines that files cannot be obtained from this origin and responds to user requests with a 504 status code. | |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value for this parameter is `false`. |`true` |
|CertInfoList |Object[] |No |Indicates a list of CA certificates. The CA certificates in the list are hosted on CDN and cannot be SM certificates. CDN uses the CA certificates in this list to verify the server certificate from the origin.<br><br>Currently, this list can only contain one CA certificate. | |
|CertId |String |No |Indicates the ID of a CA certificate in the list, starting with `cert_hosting` .<br><br>You can call [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcertinfo) to query the list of CA certificates hosted on CDN to obtain the ID of the certificate you want to specify. |`cert_hosting-104663` |


<span id="ipv6-origin-fetch"></span>
### IPv6 Origin Fetch


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginIPv6 |String |No |Indicates the configuration of the IPv6 Origin Fetch feature. The parameter can have the following values:<br><br><br>* `ipv6_first` : CDN always attempts to retrieve the IPv6 address of the origin domain. If the IPv6 address cannot be retrieved, CDN then attempts to retrieve the IPv4 address.<br><br>* `ipv4_first` : CDN always attempts to retrieve the IPv4 address of the origin domain. If the IPv4 address cannot be retrieved, CDN then attempts to retrieve the IPv6 address.<br><br>* `followclient` : CDN attempts to retrieve an IP address of the same type as the user request.<br><br><br>The default value for this parameter is followclient .<br><br>Since some CDN regional nodes outside of Chinese Mainland do not support sending origin requests to IPv6 addresses, this feature is only available for regional nodes within Chinese Mainland. |`followclient` |


<span id="origin-host"></span>
### Origin Host


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginHost |String |No |Indicates the global Origin Host configuration.<br><br>If there are multiple sites on the origin server, this parameter indicates the domain name of the site that the origin request accesses. This parameter is effective for all origin configurations, but its priority is lower than the `OriginHost` parameter in the origin configuration.<br><br>The default value of this parameter is the same as `Domain`.<br><br>If the origin is an object storage bucket, you do not need to specify this parameter. Its default value is the same as the `Address` in the origin configuration. |`img.example.com` |


<span id="https"></span>
## HTTPS

<span id="https"></span>
### HTTPS


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|HTTPS |Object |No |Indicates the configuration of the HTTPS encryption service. | |
|Switch |Boolean |Yes |Indicates whether to enable the HTTPS encryption service. This parameter has the following values:<br><br><br>* `true`: Indicates enabling the HTTPS encryption service.<br><br>* `false`: Indicates disabling the HTTPS encryption service.<br><br><br>If `Switch` is `true`, you must specify `CertInfo`.<br><br>The certificate you specify can be hosted in BytePlus Certificate Center or in CDN. |`true` |
|CertInfo |Object |No |Indicates the certificate to be associated with the domain.<br><br><br>* If the certificate is already hosted in BytePlus Certificate Center or CDN, you must specify the ID of the certificate in `CertId`.<br><br>* Otherwise, you can call [AddCertificate](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-addcertificate) to upload your certificate or purchase a certificate in the Certificate Center console, and then call `UpdateCdnConfig` to associate the certificate. | |
|CertId |String |No |Indicates the certificate ID to be associated.<br><br>You can call [ListCertInfo](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-listcertinfo) to get the ID of the certificate you want to associate. |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
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


<span id="redirect-https-to-http"></span>
### Redirect HTTPS to HTTP

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">To configure HTTP protocol redirect to HTTPS, see the <code>ForcedRedirect</code> feature under <code>HTTPS</code>. <code>HttpForcedRedirect</code> and <code>ForcedRedirect</code> are mutually exclusive. In other words, if you configure either one of these features, you cannot configure the other.</div>



|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|HttpForcedRedirect |Object |No |Indicates the configuration of the Redirect HTTPS to HTTP feature.<br><br>tip<br><br>`HttpForcedRedirect` and `ForcedRedirect` are mutually exclusive. If you configure one, you cannot configure the other. | |
|EnableForcedRedirect |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature. Once enabled, the CDN will redirect received HTTPS requests to HTTP requests.<br><br>* `false`: Indicates disabling this feature. The CDN will not redirect HTTPS requests to HTTP requests. |`true` |
|StatusCode |String |Yes |Indicates the redirect response status code of the CDN when an HTTPS request is received. This parameter has the following values: **301**, **302**, **303**, **307**, **308**.<br><br>The default value of this parameter is `301`.<br><br>Please note that:<br><br><br>* For 301 and 302, if the original request method is not GET, the method used by the client when sending a request to the new URL may change to GET.\\|<br><br>* For 303, the method used for the new request is GET.\\|<br><br>* For 307 and 308, the method used for the new request is the same as the original request and will not be changed. |`302` |


<span id="http-3-quic"></span>
### HTTP/3 (QUIC)


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Quic |Object |No |Indicates the HTTP/3 (QUIC) configuration. | |
|Switch |Boolean |Yes |Indicates whether to enable HTTP/3 (QUIC) support for user requests. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling HTTP/3 (QUIC).<br><br>* `false`: Indicates disabling HTTP/3 (QUIC). |`true` |


<span id="access-restrictions"></span>
## Access Restrictions

<span id="websocket"></span>
### WebSocket


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Websocket |Object |No |Indicates the WebSocket configuration. | |
|Switch |Boolean |No |Indicates whether to enable WebSocket for user requests. This parameter has the following values:<br><br><br>* `true`: Indicates enabling WebSocket. When WebSocket is enabled, CDN can respond to WebSocket requests from clients.<br><br>* `false`: Indicates disabling WebSocket.<br><br><br>The default value of this parameter is `false`. |`true` |
|Timeout |Long |No |Indicates the timeout duration for WebSocket connections, in seconds, with a range of 1\-900.<br><br>The default value of this parameter is `60`. |`60` |


<span id="proxy-protocol"></span>
### PROXY Protocol


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ProxyProtocol |Object |No |Represents the configuration for the PROXY Protocol. | |
|Switch |Boolean |No |Indicates whether to enable PROXY Protocol support for user requests. This parameter has the following values:<br><br><br>* `true` : Enables the PROXY Protocol. After this feature is enabled, the CDN can parse the received PROXY protocol header to obtain the client's real IP address.<br><br>* `false` : Disables the PROXY Protocol.<br><br><br>The default value for this parameter is `false` . |`true` |


<span id="server-sent-events-sse"></span>
### Server\-Sent Events (SSE)


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ServerSentEvent |Object |No |Indicates the Server\-Sent Events (SSE) configuration. | |
|Switch |Boolean |No |Indicates whether to enable SSE for user requests. This parameter has the following values:<br><br><br>* `true`: Enables SSE. When this feature is enabled, for a received client SSE request, the CDN acts as an SSE proxy. In this role, the CDN passes the client request to the origin and pushes the SSE\-formatted data stream from the origin to the client.<br><br>* `false`: Disables SSE.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="url-normallization"></span>
### URL Normallization


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|UrlNormalize |Object |No |Indicates the configuration of the URL Normalization feature. | |
|NormalizeObject |String[] |No |Indicates a list of URL normalization options. This parameter is required when `Switch` is set to `true`. The list can include the following options:<br><br><br>* `dot_segments`: Indicates the following replacements in the request URL:<br><br>   * `/./`: Replaced with a single forward slash (/).<br><br>   * `/../`: If there is a directory level before `/../`, both `/../` and that directory will be removed. If there is no directory before `/../`, the original URL is preserved.<br><br>* `back_slashes`: Indicates that backslashes (\) in the request URL will be replaced with a single forward slash (/).<br><br>* `successive_slashes`: Indicates that double slash (//) in the request URL will be replaced with a single forward slash (/). |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="geographic-restrictions"></span>
### Geographic Restrictions


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|AreaAccessRule |Object |No |Indicates the configuration of the Geographic Restrictions feature. | |
|Area |String[] |No |Indicates a list of countries and regions to which geographic restrictions are applied. This parameter is required when `Switch` is set to `true`. Countries and regions are represented using abbreviations. You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/zh-CN/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) with `Area` set to `Global` to obtain the country/region abbreviations. |`["CHE","AZE"]` |
|RuleType |String |No |Indicates the type of `Area`. This parameter is required when `Switch` is set to `true`. The parameter accepts the following values:<br><br><br>* `deny`: Indicates `Area` is a blocklist. The CDN will block requests from these countries and regions.<br><br>* `allow`: Indicates `Area` is an allowlist. The CDN only allows requests from these countries and regions. |`allow` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="disabled-http-methods"></span>
### Disabled HTTP Methods


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|MethodDeniedRule |Object |No |Indicates the configuration of the Disallowed HTTP Methods feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|Methods |String |No |Indicates one or multiple HTTP request methods to be disabled. When `Switch` is `true`, this parameter is required. Multiple methods are separated by a comma (,). This parameter can take the following values:<br><br><br>* `get`: indicates disabling the GET request method.<br><br>* `post`: indicates disabling the POST request method.<br><br>* `delete`: indicates disabling the DELETE request method.<br><br>* `put`: indicates disabling the PUT request method.<br><br>* `head`: indicates disabling the HEAD request method.<br><br>* `patch`: indicates disabling the PATCH request method.<br><br>* `connect`: indicate diabling the CONNECT request method.<br><br>* `options`: indicates disabling the OPTIONS request method.<br><br><br>warning<br><br>When CDN sends an origin request to an object storage origin, the method used by the origin request is the same as the user request. By default, CDN supports the request methods used by user requests, including DELETE, GET, HEAD, POST, PUT, PATCH, CONNECT, and OPTIONS. If you do not want origin requests using specific request methods to access your origin, for example, if you do not want requests using the DELETE method to delete files on the origin, it is recommended that you perform all of the following actions:<br><br><br>1. For the cloud vendor account corresponding to the AK/SK you provided, set permissions with the cloud vendor to prohibit that account from performing specific operations on your object storage origin.<br><br>2. In the `MethodDeniedRule` settings of CDN, specify the request methods that CDN does not support for user requests. |`delete,put` |


<span id="ip-restrictions"></span>
### IP Restrictions


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|IpAccessRule |Object |No |Indicates the configuration of the IP Restrictions feature.<br><br>This feature provides two configuration methods:<br><br><br>* Regular configuration: Specify `RuleType` and `Ip` to configure the current policy.<br><br>* Universal catalog: Specify `SharedConfig` to use a universal catalog.<br><br><br>You can only choose one configuration method. | |
|Ip |String[] |Yes |Indicates the IP addresses in the allowlist or blocklist. When `Switch` is `true`, this parameter is required. You can specify one or more IP addresses and IP address segments. IP addresses and segments can be in IPv4 or IPv6 formats. You can input up to 1,000 addresses.<br><br>If you specify `SharedConfig`, you cannot specify this parameter. |`["xx.xxx.xx.xx","x.x.x.x"]` |
|RuleType |String |Yes |Indicates the type of the IP list. When `Switch` is `true`, this parameter is required. This parameter has the following values:<br><br><br>* `allow`: Indicates allowlist.<br><br>* `deny`: Indicates blocklist.<br><br><br>If you specify `SharedConfig`, you cannot specify this parameter. |`deny` |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|SharedConfig |Object |No |Indicates a universal catalog.<br><br>If you specify this parameter, you cannot specify `RuleType` and `Ip`. | |
|ConfigName |String |No |Indicates the name of the universal catalog. The `ConfigType` of this universal catalog must be `deny_ip_access_rule` or `allow_ip_access_rule`.<br><br><br>* `deny_ip_access_rule`: Indicates an IP blocklist.<br><br>* `allow_ip_access_rule`: Indicates an IP allowlist.<br><br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get the list of universal catalogs. |`my_whitelist` |
|DenyStatusCode |Long |No |Indicates the HTTP status code returned by CDN when it rejects a request. The value ranges from 200 to 999. If this parameter is not specified, CDN returns status code 403. |`402` |
|IpSource |Object |No |Indicates the configuration for how CDN obtains the client IP address. | |
|SourceList |String[] |No |Indicates one or more IP sources used when `Type` is `custom`.<br><br>Valid values:<br><br><br>* `x-real-ip`: Indicates the IP address obtained from the `X-Real-IP` request header.<br><br>* `x-forwarded-for`: Indicates the IP address obtained from the `X-Forwarded-For` request header.<br><br>* `client-ip`: Indicates the actual connection IP. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br><br>For an IP blocklist, CDN rejects the request if any IP address obtained from the selected sources matches a blocklist rule. For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match allowlist rules. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |No |Indicates the method used to determine the client IP address.<br><br>Valid values:<br><br><br>* `default`: Uses the actual connection IP.<br><br>* `custom`: Uses one or more sources specified in `SourceList`. If CDN cannot obtain an IP address from a selected request header, it uses the actual connection IP for that source.<br><br><br>The default value is `default`. |`custom` |


<span id="referer-restrictions"></span>
### Referer Restrictions


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|RefererAccessRule |Object |No |Indicates the configuration of the Referer Restrictions feature. For information about how different configurations affect request matching results, see [Configuration examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-referer-restrictions#configuration-examples). | |
|AllowEmpty |Boolean |Yes |Specifies how CDN processes user requests that do not contain a Referer header. This parameter has the following values:<br><br><br>* `true`: Indicates that if a request does not contain a Referer header, the request is considered to match your configured Referer list.<br><br>* `false`: Indicates that if a request does not contain a Referer header, the request is considered not to match your configured Referer list.<br><br><br>The default value of this parameter is `false`. |`true` |
|Referers |String[] |Yes |Represents a Referer list. The input requirements for this parameter are the same as those for `Referers` of the `CommonType` type under `ReferersType`. We recommend that you use `ReferersType` to specify a Referer list.<br><br>Also, if you specify `SharedConfig`, you cannot specify this parameter. |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|ReferersType |Object |Yes |Represents a `ReferersType` object. It contains a `CommonType` object and a `RegularType` object, which represent a regular Referer list and a regular expression list for matching Referers, respectively. You can define both objects at the same time.<br><br>If you specify `SharedConfig`, you cannot specify this parameter. | |
|CommonType |Object |Yes |Represents a `CommonType` object, which contains a regular Referer list. | |
|IgnoreCase |Boolean |No |Indicates whether the `Referers` list under `CommonType` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`true` |
|Referers |String[] |Yes |Represents a regular Referer list. In this list, you can specify one or more IP addresses, CIDR blocks, domains, and wildcard domains. Domains can be second\-level domains. IP addresses can only be in IPv4 format. You can enter up to 1,000 IP addresses. The domains you enter cannot contain `http://` or `https://`. The length of this parameter value cannot exceed 30,000 characters. |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreScheme |Boolean |No |Indicates whether CDN verifies the scheme in the Referer, that is, whether the Referer contains `http://` or `https://`. This parameter has the following values:<br><br><br>* `true`: Indicates that CDN does not verify whether the Referer contains a scheme. In this case, regardless of whether the Referer contains a scheme, CDN will match the Referer against your configured list.<br><br>* `false`: Indicates that CDN first verifies whether the Referer contains a scheme. Only if the Referer contains a scheme will CDN match the Referer against your configured list. Otherwise, CDN determines that the request does not match your configured list.<br><br><br>The default value of this parameter is `false`.<br><br>Also, this configuration does not apply to the regular expression list under `RegularType`, because CDN relies on regular expressions to determine whether a Referer matches the regular expression list. |`false` |
|RegularType |Object |Yes |Represents a `RegularType` object, which contains a list of regular expressions for matching the Referer header in requests. To use this parameter, [submit a ticket](https://console.byteplus.com/workorder/create). | |
|Referers |String[] |Yes |Represents a list of regular expressions for matching Referers. The length of this parameter value cannot exceed 30,000 characters. |`^http://a.com` |
|RuleType |String |Yes |Indicates the type of the Referer list. When `Switch` is `true`, this parameter is required. This parameter has the following values:<br><br><br>* `allow`: Indicates allowlist.<br><br>* `deny`: Indicates blocklist. |`deny` |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|SharedConfig |Object |No |Represents a universal catalog.<br><br>If you specify this parameter, you cannot specify `Referers` or `ReferersType`. | |
|ConfigName |String |No |Represents the name of a universal catalog. The `ConfigType` of this global configuration must be `deny_referer_access_rule` or `allow_referer_access_rule`.<br><br><br>* `deny_referer_access_rule`: Indicates a Referer blocklist.<br><br>* `allow_referer_access_rule`: Indicates a Referer allowlist.<br><br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get a list of universal catalogs. |`my_allowlist` |


<span id="ua-restrictions"></span>
### UA Restrictions


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|UaAccessRule |Object |No |Indicates the configuration of the UA Restrictions feature. | |
|AllowEmpty |Boolean |Yes |Specifies how CDN processes user requests that do not contain a User\-Agent header. This parameter has the following values:<br><br><br>* `true`: Indicates that if a request does not contain a User\-Agent header, the request is considered to match your configured User\-Agent list.<br><br>* `false`: Indicates that if a request does not contain a User\-Agent header, the request is considered not to match your configured User\-Agent list.<br><br><br>The default value of this parameter is `false`. |`true` |
|IgnoreCase |Boolean |Yes |Indicates whether the UA string is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates the UA string is case\-insensitive.<br><br>* `false`: Indicates the UA string is case\-sensitive.<br><br><br>The default value for this parameter is `false`. |`true` |
|RuleType |String |Yes |Indicates the type of the UA list. When `Switch` is `true`, this parameter is required. This parameter has the following values:<br><br><br>* `deny`: Indicates blocklist.<br><br>* `allow`: Indicates allowlist. |`deny` |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|UserAgent |String[] |Yes |Indicates a list of UAs. This parameter is required when `Switch` is `true`. The list can contain up to 1,000 UAs. The following details describe this parameter:<br><br><br>* The length of the parameter value cannot exceed 30,000 characters.<br><br>* If `RuleType` is `allow`, it means only requests containing UAs from the list are allowed to access the domain name.<br><br>* If `RuleType` is `deny`, it means requests containing UAs from the list are not allowed to access the domain name.<br><br><br>There are restrictions on the characters that can be included in the UA:<br><br><br>* `*` can be used in the UA to represent one or more characters. `*` can only appear at the beginning and end of the UA.<br><br>* UA cannot consist only of `*` or spaces.<br><br>* If the UA contains symbols, the symbols must be HTML encoded. |`["*curl*","*Mozilla*"]` |


<span id="origin-restrictions"></span>
### Origin Restrictions


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginAccessRule |Object |No |Indicates the configuration of the Origin Restrictions feature. | |
|AllowEmpty |Boolean |Yes |Specifies how CDN processes user requests that do not contain an Origin header. This parameter has the following values:<br><br><br>* `true`: Indicates that if a request does not contain an Origin header, the request is considered to match your configured Origin list.<br><br>* `false`: Indicates that if a request does not contain an Origin header, the request is considered not to match your configured Origin list.<br><br><br>The default value of this parameter is `false`. |`true` |
|IgnoreCase |Boolean |Yes |Indicates whether the Origin list is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates that the Origin list is case\-insensitive.<br><br>* `false`: Indicates that the Origin list is case\-sensitive.<br><br><br>The default value of this parameter is `true`. |`true` |
|Origins |String[] |Yes |Represents an Origin list. The list can contain up to 100 Origins, with a total length not exceeding 3,000 characters. An Origin can be an IP address, CIDR block, domain name, or wildcard domain. Domain names can be second\-level domains. IP addresses can be in either IPv4 or IPv6 formats. |`["www.test.com"]` |
|RuleType |String |Yes |Indicates the type of the Origin list. This parameter has the following values:<br><br><br>* `allow`: Indicates allowlist.<br><br>* `deny`: Indicates blocklist. |`deny` |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |


<span id="custom-restrictions"></span>
### Custom Restrictions


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|RequestBlockRule |Object |No |Indicates the configuration of the Custom Restrictions feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|BlockRule |Object[] |Yes |Indicates a list of rules. The list can contain up to 10 rules. When `Switch` is `true`, this parameter is required.<br><br>The first rule in the list has the highest priority.<br><br>When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|BlockAction |Object |Yes |Indicates the configuration of CDN behavior in a rule. | |
|Action |String |Yes |Indicates how the CDN handles requests that match `Condition`. This parameter has the following values:<br><br><br>* `refuse`: Indicates that the CDN refuses the request and responds with a 4xx error code. The error code is specified in `StatusCode`.<br><br>* `redirect`: Indicates that the CDN redirects the request to the URL specified in `RedirectUrl`. |`refuse` |
|StatusCode |String |Yes |Indicates the CDN's response status code for user requests that match `Condition`.<br><br><br>* When `Action` is `refuse`, this parameter indicates an error code in the range of 400\-499.<br><br>* When `Action` is `redirect`, this parameter has the following values:<br><br>   * `301`: Indicates the response status code is 301.<br><br>   * `302`: Indicates the response status code is 302. |`403` |
|ErrorPage |String |No |* When `Action` is `refuse`, this parameter is optional and explained as follows:<br><br>   * If this parameter is specified, it indicates the name of a custom response page in the "Universal Catalog" feature. In other words, when the CDN refuses the request, it returns this custom page.<br><br>   * If not specified, it indicates that the CDN uses the standard response body of the error code specified in `StatusCode`.<br><br>* When `Action` is `redirect`, this parameter is invalid and can be omitted. |`GlobalConfigName` |
|RedirectUrl |String |No |* When `Action` is `redirect`, this parameter is required and indicates the redirect URL. The URL must start with `http://` or `https://` and cannot exceed 1,024 characters in length.<br><br>* When `Action` is `refuse`, this parameter is invalid and can be omitted. |`http://www.example.com` |
|Condition |Object |Yes |Indicates the definition of matching conditions in this rule. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions used to match the path and query parameters in the request URL, as well as the client IP address from which the request originates. The list can contain up to 5 matching conditions. Each matching condition includes a matching type, comparison type, and matching value. | |
|Object |String |Yes |Indicates a matching type.<br><br><br>* When `Type` is `url`, this parameter has the following values:<br><br>   * `path`: Indicates the path in the request URL.<br><br>   * `directory`: Indicates a directory in the path.<br><br>   * `filetype`: Indicates the extension at the end of the path.<br><br>   * `regex`: Indicates the path in the request URL, matched by a regular expression.<br><br>* When `Type` is `querystring`, this parameter has the following values:<br><br>   * `query_name`: Indicates a query parameter in the request URL.<br><br>   * `full_querystring`: Indicates the query string in the request URL.<br><br>* When `Type` is `client_ip`, this parameter has the following values:<br><br>   * `client_ip`: Indicates the client's IP address.<br><br>* When `Type` is `request_header`, this parameter has the following values:<br><br>   * `ua`: Indicates the User\-Agent header in the request.<br><br>   * `customize`: Indicates a custom header in the request. |`filetype` |
|Operator |String |Yes |Indicates a comparison type.<br><br><br>* When `Object` is `path`, `directory`, or `filetype`, this parameter has the following values:<br><br>   * `equal`: Indicates that if any value in `Value` matches, the request satisfies this matching condition.<br><br>   * `not_equal`: Indicates that if none of the values in `Value` match, the request satisfies this matching condition.<br><br>* When `Object` is `query_name`, this parameter has the following values:<br><br>   * `exist`: Indicates existence. The matching logic is the same as `equal`.<br><br>   * `not_exist`: Indicates non\-existence. The matching logic is the same as `not_equal`.<br><br>   * `belong_shared_config`: Indicates that if any value in the universal catalog represented by `Value` matches, the request satisfies this matching condition.<br><br>   * `not_belong_shared_config`: Indicates that if none of the values in the universal catalog represented by `Value` match, the request satisfies this matching condition.<br><br>   * `empty`: Indicates that the value is empty.<br><br>   * `not_empty`: Indicates that the value is not empty.<br><br>   * `equal`: See the above description.<br><br>   * `not_equal`: See the above description.<br><br>* When `Object` is `regex`, `full_querystring`, `client_ip`, or `ua`, this parameter has the following values:<br><br>   * `match`: Describes the same as `equal`.<br><br>   * `not_match`: Describes the same as `not_equal`.<br><br>* When `Object` is `ua` or `customize`, this parameter also has the following **additional** values:<br><br>   * `empty`: See the above description.<br><br>   * `not_empty`: See the above description. |`not_equal` |
|Type |String |Yes |Indicates the type of a matching object. This parameter has the following values:<br><br><br>* `url`: Indicates the request URL.<br><br>* `querystring`: Indicates the query string in the request URL.<br><br>* `request_header`: Indicates the headers in the request. |`url` |
|Value |String |Yes |Indicates one or more matching values.<br><br><br>* If `Type` is `request_header`, multiple matching values are separated by a vertical bar (\\|).<br><br>* If `Type` is not `request_header`, multiple matching values are separated by a semicolon (;).<br><br><br>The input requirements for this parameter are as follows:<br><br><br>* When `Object` is `path`, `directory`, or `filetype`, the total length of all matching values cannot exceed 1,024 characters and cannot contain the following characters:<br><br>   * Double slash (//), spaces, dollar signs ($), question marks (?), periods (.)<br><br>* When `Object` is `path`, this parameter has the following **additional** requirements:<br><br>   * Each matching value must start with a slash (/). You can use one or more asterisks (\*) in the matching value, each asterisk representing one or more characters. For example: `/www/img/my*image.png`.<br><br>* When `Object` is `directory`, this parameter has the following **additional** requirements:<br><br>   * Each matching value must start and end with a slash (/). For example: `/www/img/`.<br><br>* When `Object` is `filetype`, this parameter has the following **additional** requirements:<br><br>   * Each matching value does not need to start with a period (.). For example: `png;txt`.<br><br>* When `Object` is `query_name`,<br><br>   * If `Operator` is `equal` or `not_equal`, you can only specify one matching value, which represents the value of the query parameter indicated by `Name`. The length of this value cannot exceed 256 characters and can contain numbers, letters, percent signs (%), underscores (_), and hyphens (\-).<br><br>   * If `Operator` is `belong_shared_config` or `not_belong_shared_config`, you can only specify one matching value. This matching value is the name of a universal catalog.<br><br>   * If `Operator` is `exist`, `not_exist`, `empty`, or `not_empty`, this parameter is invalid and can be omitted.<br><br>* When `Object` is `full_querystring` or `regex`, each matching value is a regular expression. Multiple matching values are separated by a semicolon (;). The total length of all matching values cannot exceed 1,024 characters.<br><br>* When `Object` is `client_ip`, `Value` can contain up to 50 matching values, with a total length not exceeding 30,000 characters. Each matching value is an IP address. IP addresses can be IPv4 addresses, IPv4 CIDR addresses, IPv6 addresses, or IPv6 CIDR addresses.<br><br>* When `Object` is `custom` or `ua`, `Value` can contain up to 50 matching values, with a total length not exceeding 1,024 characters. Matching values can start and end with an asterisk ( *). An asterisk (* ) represents any consecutive characters.<br><br>   * If `Object` is `custom`, each matching value is the value of the header indicated by `Name`.<br><br>   * If `Object` is `ua`, each matching value is a User\-Agent header value.<br><br>   * If `Operator` is `empty` or `not_empty`, this parameter is invalid and can be omitted. |`png;txt` |
|Name |String |No |When `Object` is `query_name` or `customize`, this parameter is valid.<br><br><br>* If `Object` is `query_name`, this parameter indicates the name of a query parameter.<br><br>* If `Object` is `customize`, this parameter indicates the name of a custom request header.<br><br><br>The length of `Name` cannot exceed 256 characters and can contain numbers, letters, percent signs (%), underscores (_), and hyphens (\-). |`color` |
|Connective |String |Yes |Indicates the relationship between multiple `ConditionRule`. This parameter has the following values:<br><br><br>* `AND`: Indicates "and".<br><br>* `OR`: Indicates "or".<br><br><br>The default value of this parameter is `OR`. |`AND` |
|RuleName |String |Yes |Indicates the name of the rule, with a length not exceeding 20 characters. It can contain letters, numbers, underscores (_), hyphens (\-), and Chinese characters. One Chinese character occupies 3 characters. |`MyRule` |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="url-redirect"></span>
### URL Redirect


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|RedirectionRewrite |Object |No |Indicates the configuration of the URL Redirect feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|RedirectionRule |Object[] |No |Indicates a list of rules for URL redirect rewriting. When `Switch` is `true`, this parameter is required. The list can contain up to 50 rules.<br><br>The first rule in the list has the highest priority.<br><br>When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|RedirectionAction |Object |Yes |Indicates a rule for URL redirect rewriting. | |
|RedirectCode |String |Yes |Indicates the response status code for URL redirection. This parameter can take the following values:<br><br><br>* `301`: Indicates that the file has been moved permanently.<br><br>* `302`: Indicates that the file has been moved temporarily. |`301` |
|SourcePath |String |Yes |Indicates the original path of the file. That is the path included in the request. Paths must start with a slash (/) and not contain double slash (//), percent signs (%), or spaces. The length of this parameter value cannot exceed 1,024 characters. |`/img/image.png` |
|TargetHost |String |Yes |Indicates the domain name or IP address of the site to which the target path belongs. The IP address must be IPv4. The length of this parameter value cannot exceed 1,024 characters. The default value for this parameter is your domain name. |`www.test.com` |
|TargetPath |String |Yes |Indicates the target path after redirection. The path must start with a slash (/) and not contain double slash (//), percent signs (%), or spaces. The length of this parameter value cannot exceed 1,024 characters. |`/png/image.png` |
|TargetProtocol |String |Yes |Indicates the protocol used by the new request after URL redirection. This parameter can take the following values:<br><br><br>* `followclient`: Indicates that the protocol of the original request is used.<br><br>* `http`: Indicates that the new request is forced to use the HTTP protocol.<br><br>* `https`: Indicates that the new request is forced to use the HTTPS protocol. |`followclient` |
|TargetQueryComponents |Object |Yes |Indicates the handling of query parameters in the original request URL. | |
|Action |String |Yes |Indicates the handling of query parameters in the original request URL. This parameter can take the following values:<br><br><br>* `include`: Indicates that all query parameters from the original request URL are included in the redirected URL.<br><br>* `exclude`: Indicates that none of the query parameters from the original request URL are included in the redirected URL.<br><br>* `includePart`: Indicates that specific query parameters from the original request URL are included in the redirected URL.<br><br>* `excludePart`: Indicates that specific query parameters from the original request URL are not included in the redirected URL. |`include` |
|Value |String |Yes |Indicates the query parameters to retain or remove. Separate multiple parameters with a semicolon (;). Specified query parameters should not contain double slash (//), quotation marks ("), or spaces. The default value for `Value` is `*`, indicating all query parameters.<br><br><br>* If `Action` is `include` or `exclude`, then `Value` must be `*`.<br><br>* If `Action` is `includePart` or `excludePart`, you can specify one or multiple query parameters. In this case, your specified query parameters cannot be `*`. |`seq` |


<span id="signed-url-authentication"></span>
### Signed URL Authentication


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|SignedUrlAuth |Object |No |Indicates the configuration of the Signed URL Authentication feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|SignedUrlAuthRules |Object[] |No |Indicates a rule list. Each rule contains matching condition configuration and authentication configuration. Currently, the list can only contain one rule. This parameter is required when `Switch` is `true`. | |
|Condition |Object |Yes |Indicates the configuration of matching conditions. CDN performs authentication for user requests that meet the conditions. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions.<br><br><br>* When `URLAuthType` is `typea`, `typed`, or `typee`, you can create up to 10 conditions.<br><br>* When `URLAuthType` is `typeb` or `typec`, you can only create 1 condition. | |
|Object |String |Yes |Indicates the matching type in the matching condition. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension at the end of the URL path.<br><br>* `directory`: Indicates a directory in the URL path.<br><br>* `path`: Indicates the complete URL path.<br><br>* `regex`: Indicates the complete URL path, matched through regular expressions. To use this value, [submit a ticket](https://console.byteplus.com/workorder/create).<br><br><br>Please note that when `URLAuthType` is `typeb` or `typec`, you can only specify this parameter value as `filetype` or `directory`. |`directory` |
|Operator |String |Yes |Indicates the matching method in the matching condition. This parameter has the following values:<br><br><br>* `match`: Indicates that if `object` matches `Value`, the request meets this matching condition.<br><br>* `not_match`: Indicates that if `object` does not match `Value`, the request meets this matching condition.<br><br><br>The default value of this parameter is `match`.<br><br>Please note that when `URLAuthType` is `typeb` or `typec`, you can only specify this parameter value as `match`. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates the matching value in the matching condition. Multiple matching values are separated by semicolons (;), with a total length not exceeding 1,024 characters, and cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value is a file extension and cannot start with a period (.). For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value is a directory path and must start and end with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value is a URL path and must start with a slash (/). Matching values can contain asterisks (\*) to represent one or more arbitrary characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If `Object` is `regex`, each matching value is a regular expression used to match URL paths. For example: `^/a{1,2}.*g$`. |`png;jpg` |
|Connective |String |Yes |Indicates the logical relationship between multiple `ConditionRule`s. This parameter has the following values:<br><br><br>* `AND`: Indicates the logical relationship is "AND".<br><br>* `OR`: Indicates the logical relationship is "OR".<br><br><br>The default value of this parameter is `OR`.<br><br><br>* When `URLAuthType` is `typeb` or `typec`, this parameter value must be `OR`. |`OR` |
|SignedUrlAuthAction |Object |Yes |Indicates the configuration for signature calculation. | |
|Duration |Long |Yes |The valid duration of the signature, in seconds. This parameter is used in conjunction with the timestamp included in the request to calculate the expiration time of the signature. The value range of this parameter is `0-315,360,000`. The expiration time of the signature = timestamp + `Duration`. When CDN receives a request, if the expiration time of the signature is less than the current time, CDN determines the signature has expired. |`1000` |
|MasterSecretKey |String |Yes |Indicates the primary key. The length cannot exceed 120 characters. |`abcdefg` |
|URLAuthType |String |Yes |Signature type. This parameter can take the following values: `typea`, `typeb`, `typec`, `typed`, `typee`, with each type`s authentication explanation seen in [Configuring URL Authentication](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/overview).\|`typea`\| | |
|BackupSecretKey |String |No |Indicates the backup key. The length cannot exceed 120 characters. |`abcdefg` |
|CustomVariableRules |Object |No |Indicates custom signature calculation variables. | |
|CustomVariableInstances |Object[] |Yes |Indicates a list of variables. | |
|Operator |String |Yes |Indicates the matching method for the variable. The value of this parameter can only be `match`. |`match` |
|Type |String |Yes |Indicates the type of variable. This parameter can take the following values:<br><br><br>* `queryString`: Indicates that the variable is a query parameter in the user request.<br><br>* `requestHeader`: Indicates that the variable is a header field in the user request. |`queryString` |
|Value |String |Yes |Indicates the name of the variable, which must not exceed 100 characters in length. The requirements for the variable name are as follows:<br><br><br>* If the `Type` is `queryString`, the variable name can include letters, digits, hyphens (\-), commas (,), periods (.), and exclamation marks (!).<br><br>* If the `Type` is `requestHeader`, the variable name cannot include the following:<br><br>   * Underscore (_), space, double quotes ("), colon (:) |`myparam1` |
|KeepOriginArg |Boolean |No |Specifies whether CDN includes the signature parameter from the user request in origin requests. This parameter takes effect only when `URLAuthType` is `typea` or `typed`.<br><br>Valid values:<br><br><br>* `true`: CDN includes the signature parameter in origin requests.<br><br>* `false`: CDN does not include the signature parameter in origin requests.<br><br><br>The default value is `false`.<br><br>This parameter does not take effect when `URLAuthType` is `typeb`, `typec`, or `typee`.<br><br><br>* For `typeb` and `typec`, CDN does not include the signature parameter in origin requests.<br><br>* For `typee`, whether CDN includes the signature parameter in origin requests is determined by `DeleteAuthCacheAndOrigin`. |`true` |
|RewriteM3u8 |Boolean |No |For requests for HLS manifests (`.m3u8` files), specifies whether CDN rewrites the manifest by generating signatures for each video segment and appending the signatures to the segment URIs.<br><br>Valid values:<br><br><br>* `true`: CDN rewrites the manifest.<br><br>* `false`: CDN does not rewrite the manifest.<br><br><br>The default value is `false`.<br><br>tip<br><br>CDN does not rewrite compressed manifests. CDN does not rewrite a manifest in either of the following cases:<br><br><br>* The origin response contains the `Content-Encoding` header, which indicates that the manifest is compressed.<br><br>* The user request matches a rule configured for the Smart Compression feature. |`true` |
|SignName |String |No |Indicates the name of the signature parameter. The explanation for this parameter is as follows:<br><br><br>* Can include letters, digits, underscores (_), hyphens (\-), periods (.), commas (,), and exclamation marks (!).<br><br>* Length must not exceed 100 characters.<br><br>* Must include at least one letter.<br><br>* Must not be the same as `TimeName`.<br><br><br>When `URLAuthType` is `typea`, `typed`, or `typee`, this parameter is required. For other types, this parameter is not effective. |`sign` |
|SignatureRule |String[] |No |When `URLAuthType` is `typee` , this parameter is required and indicates the fields to be included in the signature calculation. The fields that must be included in the signature calculation are as follows:<br><br><br>* `key` : Indicates the key specified by `MasterSecretKey` or `BackupSecretKey`.<br><br>* `uri` : Indicates the URI of the user request, including only the path and query parameters. If the URI contains Chinese characters, you need to encode the URI.<br><br>* `TimeName` : Indicates the timestamp specified by `TimeFormat`.<br><br><br>The fields that can be optionally included in the signature calculation are as follows:<br><br><br>* `domain`: Indicates the domain name.<br><br>* `referer`: Indicates the referer value carried in the user request.<br><br>* `ua`: Indicates the User\-Agent value carried in the user request.<br><br>* `ip`: Indicates the client IP of the user request.<br><br>* `origin`: Indicates the Origin value carried in the user request.<br><br>* Custom variables: Indicates the value of the variables you defined in `CustomVariableInstances`.<br><br><br>CDN concatenates these fields into a string in the order of the fields in the list, and then calculates the MD5 value of the string. The MD5 value is the signature. |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |No |Specifies the time format used by `TimeName`. Valid values:<br><br><br>* `basicFormat2m`: Uses the `YYYYMMDDHHMM` format.<br><br>* `decimal`: Uses a decimal timestamp.<br><br>* `heximal`: Uses a hexadecimal timestamp.<br><br><br>Usage notes:<br><br><br>* When `URLAuthType` is `typea`, this parameter can be omitted and is always `decimal`.<br><br>* When `URLAuthType` is `typeb`, this parameter is required. Valid values are `decimal`, `heximal`, and `basicFormat2m`.<br><br>* When `URLAuthType` is `typec`, this parameter can be omitted and is always `heximal`.<br><br>* When `URLAuthType` is `typed` or `typee`, this parameter is required. Valid values are `decimal` and `heximal`. |`heximal` |
|TimeName |String |No |Indicates the name of the timestamp parameter. The value of `TimeName` can include letters, digits, underscores (_), hyphens (\-), periods (.), commas (,), and exclamation marks (!), with a length of `1-100` characters. `TimeName` cannot be the same as `SignName`.<br><br>When `URLAuthType` is `typed` or `typee`, this parameter is required. For other types, this parameter is not effective. |`TimeParam` |
|RewriteM3u8Rule |Object |No |Specifies the M3U8 rewriting configuration. This configuration takes effect only when `RewriteM3u8` is `true`. | |
|DeleteParam |Boolean |No |Specifies whether to retain the original query parameters in a segment URL when rewriting the URL.<br><br>Valid values:<br><br><br>* `true`: Deletes the original query parameters.<br><br>* `false`: Retains the original query parameters.<br><br><br>The default value is `false`.<br><br>Note that this setting affects signature calculation. |`true` |
|KeepM3u8Param |Boolean |No |Specifies whether to add the non\-signature query parameters from the M3U8 request URL to segment URLs.<br><br>Valid values:<br><br><br>* `true`: Adds the query parameters to segment URLs.<br><br>* `false`: Does not add the query parameters to segment URLs.<br><br><br>The default value is `false`.<br><br>Note that this setting affects signature calculation. |`true` |
|RewriteTag |Object |No |Specifies the Tag Rewriting configuration. You can define tags other than `EXTINF`. | |
|Switch |Boolean |No |Specifies whether to rewrite segment URIs associated with additional tags.<br><br>Valid values:<br><br><br>* `true`: Rewrites URIs associated with additional tags.<br><br>* `false`: Does not rewrite URIs associated with additional tags.<br><br><br>The default value is `false`. |`true` |
|Tags |String[] |No |Specifies a list of additional tags whose associated segment URIs need to be rewritten, in addition to the default tags.<br><br>The list can contain up to 20 tags. Each tag must be 1 to 100 characters long and cannot contain `#` or `:`. |`["EXT-X-MAP", "My-TAG"]` |
|AuthAlgorithm |String |No |Indicates the algorithm used to calculate the signature. Valid values:<br><br><br>* `md5`: Uses the MD5 algorithm.<br><br>* `sha256`: Uses the SHA\-256 algorithm.<br><br><br>The default value is `md5`. |`md5` |
|DeleteAuthCacheAndOrigin |Boolean |No |Specifies whether CDN includes the signature parameter from the user request in origin requests and cache keys. This parameter takes effect only when `URLAuthType` is `typee`.<br><br>Valid values:<br><br><br>* `true`: The signature parameter is excluded from both origin requests and cache keys.<br><br>* `false`: The signature parameter is included in both origin requests and cache keys.<br><br><br>The default value is `false`. |`true` |
|AuthRulesF |Object[] |No |Indicates the Type\-F configuration, which includes a list of rules. The list can contain a maximum of 5 rules. The first rule in the list has the highest priority.<br><br>When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|ArgumentRule |Object |No |Indicates configurations related to origin request parameters. | |
|KeepOriginArg |Boolean |No |Indicates whether to include the token calculated based on `AuthTokenCalRule` in origin requests. This parameter accepts the following values:<br><br><br>* `true`: Indicates including the token in origin requests. The token appears in the same position as specified in `SignCapRule`.<br><br>* `false`: Indicates not including the token in origin requests. |`true` |
|GeneralParamRule |Object |No |Specifies how CDN sets query parameters in the video fragment URI. | |
|ParentLinkParamInherit |String |No |Specifies whether the rewritten video fragment URI includes all query parameters from the user request URL except those representing the token and token timestamp. This parameter has the following values:<br><br><br>* `not_inherit`: The rewritten fragment URI will not include these query parameters.<br><br>* `inherit`: The rewritten fragment URI will include these query parameters. |`not_inherit` |
|SubLinkParamRule |Object |No |This structure contains additional query parameter settings. This structure contains additional query parameter settings. | |
|InheritMode |String |No |Specifies how CDN sets the parameter value in the video fragment URI when the same query parameter exists in both the video fragment URI and user request URL. You can set this parameter when `ParentLinkParamInherit` is set to `inherit`.<br><br>This parameter has the following values:<br><br><br>* `sub_link_first`: Uses the parameter value from the video fragment URI.<br><br>* `inherit_first`: Uses the parameter value from the user request URL. |`inherit_first` |
|KeepSubLinkArg |String |No |Specifies whether the rewritten video fragment URI retains the original query parameters in the URI. This parameter has the following values:<br><br><br>* `delete`: The rewritten fragment URI will not retain these query parameters.<br><br>* `keep`: The rewritten fragment URI will retain these query parameters. |`delete` |
|AuthTokenCalRule |Object |No |Indicates the token calculation settings. Please refer to the sample code to deploy token calculation logic on the client side and include the generated signature in user requests.<br><br>CDN uses `SignJoinSymbol` to concatenate objects in `SignParam`, then applies the algorithms specified in `ParamCalRules` to calculate the token for comparison with the token included in user requests. | |
|ParamCalRules |String[] |No |Indicates the list of algorithms used for token calculation, containing up to 5 algorithms. CDN generates the token calculation formula according to the order of algorithms in the list.<br><br>This parameter accepts the following values: `md5_bin`, `base64url`, `sha256`, `md5`, `base64_encode`, `sha1`, `sha224`, `sha384`, `sha512`, `sha3_224`, `sha3_256`, `sha3_384`, `sha3_512`, `upper_case`, `lower_case`.<br><br>tip<br><br>If you specify `md5_bin`, you must specify `base64url` as the next algorithm.<br><br><br>* Correct configuration: `sha1`, `md5_bin`, `base64url`<br><br>* Incorrect configuration: `sha1`, `md5_bin`, `base64url`, `base64url`, `md5_bin` |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |No |Indicates the connector used to join objects in `SignParam`. The default value is empty (""). |`00` |
|SignParam |Object[] |No |Indicates the list of objects used by CDN for token calculation. Each object consists of `ParamType` and related configurations. For example, the following example indicates that the object is a string with the value `str-for-token-calc`.<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|CookieToken |String |No |When `ParamType` is `Cookie`, you must specify this parameter. It represents the key of the cookie you want to specify. CDN will obtain the value of this cookie. |`mycookiekey` |
|ParamSource |String |No |When `RewriteMPD` or `RewriteM3U8` is enabled and the object's `ParamType` is `URI`, `URLParam`, or `FullURI`, you can specify this parameter.<br><br>For tokens added to the Manifest, this parameter indicates the source of the object when CDN calculates the token using this object.<br><br>This parameter accepts the following values:<br><br><br>* `ParentLink`: Indicates the object comes from the URL in the user request.<br><br>* `ChildLink`: Indicates the object comes from the URI of video fragments in the Manifest.<br><br><br>The default value is `ChildLink`. |`ParentLink` |
|ParamType |String |No |Indicates the object type. This parameter accepts the following values:<br><br><br>* `SecretKey`: Indicates `MasterSecretKey` or `BackupSecretKey` in the `SecretKey` structure. When authentication fails, CDN will recalculate the token using `BackupSecretKey` to re\-authenticate the user request.<br><br>* `SupString`: Indicates a string. Related configurations are specified in `SupContent`.<br><br>* `URI`: Indicates consecutive segments in the request path. The path excludes the query string. Related configurations are specified in `UriParamSup` and `ParamSource`.<br><br>* `URLParam`: Indicates certain objects in the request URL. Objects can be a query parameter or a directory. Related configurations are specified in `UriParam` and `ParamSource`.<br><br>* `ClientDomain`: Indicates the request domain.<br><br>* `Referer`: Indicates the value of the Referer header in the user request.<br><br>* `Origin`: Indicates the value of the Origin header in the user request.<br><br>* `ClientIP`: Indicates the client IP address that sends the user request.<br><br>* `UA`: Indicates the value of the User\-Agent header in the user request.<br><br>* `ReqHeader`: Indicates the value of a specific header in the user request. Related configurations are specified in `RequestHeader`.<br><br>* `Cookie`: Indicates a cookie in the request. Related configurations are specified in `CookieToken`.<br><br>* `FullURI`: Indicates the complete request path, excluding query strings. Related configurations are specified in `ParamSource`. |`URI` |
|RequestHeader |String |No |When `ParamType` is `ReqHeader`, you must specify this parameter. It represents the request header you want to specify. |`myheader2` |
|SupContent |String |No |When `ParamType` is `SupString`, you must specify this parameter. It represents the string you want to specify. |`123abc` |
|UriParamSup |Object |No |Indicates how to obtain consecutive segments from the request path. When `ParamType` is `URI`, you must specify this parameter.<br><br>This parameter is a structure that includes the following configurations:<br><br><br>* The delimiter used to split the request path.<br><br>* The start and end levels of the required consecutive path segments.<br><br>* The connector used to join these path segments. The joined path segments are used for token calculation. | |
|JoinSymbol |String |No |Indicates the connector used to join these path segments. Requirements are as follows:<br><br><br>* The length is 1 character and can a letter, a number, an underscore (_), a hyphen (\-), a forward slash (/), and an exclamation mark (!).<br><br><br>The default value is empty (""). |`00` |
|SplitSymbol |String |No |Indicates the delimiter used to split the request path. Requirements are as follows:<br><br><br>* The length is 1 character and can be a letter, a number, an underscore (_), a hyphen (\-), a forward slash (/), and an exclamation mark (!). |`-` |
|StartLevel |Long |No |Indicates the level where the starting segment is located. Requirements are as follows:<br><br><br>* Must be a positive integer.<br><br>* Cannot exceed the total number of levels.<br><br>* The path segment represented by `StartLevel` cannot be to the right of the path segment represented by `TermLevel`. |`2` |
|TermLevel |Long |No |Indicates the level where the ending segment is located. Requirements are as follows:<br><br><br>* Must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If `TermLevel` is a negative integer, it counts from right to left starting from the rightmost segment. |`3` |
|UrlParam |Object |No |Indicates how to obtain the required objects from the URL. When `ParamType` is `URLParam`, you must specify this parameter.<br><br>This parameter is a structure that contains the object's source and related configurations. | |
|ArgSegment |Object |No |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a specific level. This segment is the object you need to obtain. | |
|Level |Long |No |Indicates the level where your required object is located after the obtained content is split into multiple segments. Requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost segment.<br><br>When `Switch` is `true`, you must specify this parameter. |`2` |
|SplitSymbol |String |No |Indicates the delimiter used to split the content.<br><br>When `Switch` is `true`, you must specify this parameter. |`-` |
|Switch |Boolean |No |Indicates whether the obtained content needs to be split. This parameter accepts the following values:<br><br><br>* `true`: Indicates the content needs to be split.<br><br>* `false`: Indicates the content does not need to be split.<br><br><br>The default value is `false`. |`true` |
|CapMode |String |No |Indicates the source of the object. This parameter accepts the following values:<br><br><br>* `name`: Indicates query parameters. Related configurations are specified in `ParamName` and `ArgSegment`.<br><br>* `uri`: Indicates a directory in the request path. Related configurations are specified in `UriLevel` and `ArgSegment`. |`uri` |
|ParamName |String |No |When `ParamType` is `name`, you must specify this parameter. It represents the query parameter you want to specify. |`myparam3` |
|UriLevel |Long |No |When `ParamType` is `uri`, you must specify this parameter. It represents the directory you want to specify.<br><br>Requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost directory. |`2` |
|CustomRewrite |Object |No |Indicates the custom URL signing configuration for video Manifest. When enabled, CDN uses [custom URL signing logic](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#custom-url-signing-logic-for-video-manifests) to override the [default URL signing logic](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#default-url-signing-logic-for-video-manifests). | |
|RewriteParam |Object[] |No |Indicates a list of objects. CDN concatenates these objects to generate tokens and adds them to video fragment URIs. | |
|ParamType |String |No |Indicates the object type. This parameter accepts the following values:<br><br><br>* `ParentLinkUrlParam`: Indicates certain objects in the user request URL. Objects can be a query parameter or a path directory. Related configurations are specified in the `ParentLinkUrlParam` structure.<br><br>* `SupString`: Indicates a string. Related configurations are specified in `SupContent`.<br><br>* `ParentLinkURI`: Indicates consecutive segments in the user request path. The path excludes query strings. Related configurations are specified in `ParentLinkUriParamSup`.<br><br>* `ParentLinkExpire`: Indicates the token timestamp in the user request. See the description of the `Duration` parameter under `ExpireTimeRule`.<br><br>* `AuthToken`: Indicates the token calculated based on `AuthTokenCalRule`.<br><br>* `ParentFullURI`: Indicates the complete path of the user request, excluding the query string. |`ParentLinkURI` |
|SupContent |String |No |When `ParamType` is `SupString`, you must specify this parameter. It represents the string you want to specify. |`abc-13343` |
|ParentLinkUriParamSup |Object |No |Indicates how to obtain objects from the user request path. You must specify this parameter when `ParamType` is `ParentLinkURI`.<br><br>This parameter is a structure that includes the following configurations:<br><br><br>* The delimiter used to split the request path.<br><br>* The start and end levels of consecutive path segments.<br><br>* The joining string used to concatenate these path segments. The concatenated path segments are used to generate the token. | |
|JoinSymbol |String |No |Indicates the joining string used to concatenate these path segments. The requirements are as follows:<br><br><br>* The length is 1 character and can be a letter, a number, an underscore (_), a hyphen (\-), a forward slash (/), and an exclamation mark (!). |`00` |
|SplitSymbol |String |No |Indicates the delimiter used to split the request path, which must be identical to `JoinSymbol`. |`-` |
|StartLevel |Long |No |Indicates the level of the starting segment. The requirements are as follows:<br><br><br>* Must be a positive integer.<br><br>* Cannot exceed the total number of levels.<br><br>* The path segment indicated by `StartLevel` cannot be to the right of the path segment indicated by `TermLevel`. |`1` |
|TermLevel |Long |No |Indicates the level of the ending segment. The requirements are as follows:<br><br><br>* Must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If `TermLevel` is a negative integer, it counts from the rightmost segment towards the left. |`3` |
|ParentLinkUrlParam |Object |No |Indicates how to obtain objects from the URL. You must specify this parameter when `ParamType` is `ParentLinkUrlParam`.<br><br>This parameter is a structure that contains the object source and related configurations. | |
|ArgSegment |Object |No |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a certain level. This segment is the object you need to obtain. | |
|Level |Long |No |After splitting the obtained content into segments at multiple levels, this parameter indicates the level of the segment you need. The requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from the rightmost segment towards the left.<br><br>You must specify this parameter when `Switch` is `true`. |`2` |
|SplitSymbol |String |No |Indicates the delimiter used to split the content.<br><br>You must specify this parameter when `Switch` is `true`. |`-` |
|Switch |Boolean |No |Indicates whether the obtained content needs to be split. This parameter accepts the following values:<br><br><br>* `true`: Indicates the content needs to be split.<br><br>* `false`: Indicates the content does not need to be split.<br><br><br>The default value of this parameter is `false`. |`true` |
|CapMode |String |No |Indicates the source of the object. This parameter accepts the following values:<br><br><br>* `name`: Indicates query parameters. Related configurations are specified in `ParamName` and `ArgSegment`.<br><br>* `uri`: Indicates the directory in the request path. Related configurations are specified in `UriLevel` and `ArgSegment`. |`name` |
|ParamName |String |No |You must specify this parameter when `CapMode` is `name`. This parameter indicates the query parameter you want to specify. |`myparam5` |
|UriLevel |Long |No |You must specify this parameter when `CapMode` is `uri`. This parameter indicates the directory you want to specify.<br><br>The requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from the rightmost directory towards the left. |`4` |
|RewriteRule |Object |No |Indicates how CDN adds tokens to video fragment URIs. | |
|CapMode |String |No |Indicates how CDN adds the generated token to video fragment URIs. This parameter accepts the following values:<br><br><br>* `name`: Indicates setting the specified query parameter as the token. Related configurations are specified in `ParamName`.<br><br>* `uri`: Indicates inserting a directory in the URL path and setting this directory as the token. Related configurations are specified in `UriLevel`. |`name` |
|ParamName |String |No |When `CapMode` is `name`, you must specify this parameter. It represents the query parameter you want to specify. |`myparam4` |
|UriLevel |Long |No |When `CapMode` is `uri`, you must specify this parameter. It represents the directory you want to specify.<br><br>Requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost directory. |`2` |
|SignJoinSymbol |String |No |Indicates the connector used to join objects in `RewriteParam`. |`00` |
|Switch |Boolean |No |Indicates whether to enable the custom URL signing configuration. This parameter accepts the following values:<br><br><br>* `true`: Indicates to enable the custom URL signing configuration.<br><br>* `false`: Indicates to disable the custom URL signing configuration.<br><br><br>The default value is `false`. |`true` |
|ExpireTimeRule |Object |No |Indicates settings related to token expiration time. | |
|Duration |Long |No |Indicates the token's Time To Live (TTL) in seconds, ranging from 0\-315,360,000, with a default value of `0`.<br><br><br>* Token expiration time = Token timestamp obtained based on `ExpTimeCapRule` + `Duration` |`20` |
|ExpTimeCapRule |Object |No |Indicates how to obtain the token timestamp. The token timestamp is a Unix timestamp. | |
|ArgSegment |Object |No |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a specific level. This segment is the token timestamp you need to obtain. | |
|Level |Long |No |Indicates the level where the token timestamp is located after the content is split into multiple segments. Requirements are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost segment.<br><br>When `Switch` is `true`, you must specify this parameter. |`2` |
|SplitSymbol |String |No |Indicates the delimiter used to split the content.<br><br>When `Switch` is `true`, you must specify this parameter. |`-` |
|Switch |Boolean |No |Indicates whether the obtained content needs to be split. This parameter accepts the following values:<br><br><br>* `true`: Indicates the content needs to be split.<br><br>* `false`: Indicates the content does not need to be split.<br><br><br>The default value is `false`. |`true` |
|CapMode |String |No |Indicates the source of the token timestamp. This parameter accepts the following values:<br><br><br>* `name`: Indicates query parameters. Related configurations are specified in `ParamName` and `ArgSegment`.<br><br>* `uri`: Indicates a directory in the request path. Related configurations are specified in `UriLevel` and `ArgSegment`.<br><br>* `header`: Indicates a header in the request. Related configurations are specified in `CustomValue`.<br><br>* `cookie`: Indicates a cookie in the request. Related configurations are specified in `CustomValue`. |`header` |
|CustomValue |String |No |This parameter has the following meanings:<br><br><br>* When `CapMode` is `header`, you must specify this parameter. It represents the request header you want to specify.<br><br>* When `CapMode` is `cookie`, you must specify this parameter. It represents the key of the cookie you want to specify, and CDN will obtain the corresponding value. |`myheader1` |
|ParamName |String |No |When `ParamType` is `ReqHeader`, you must specify this parameter. It represents the query parameter you want to specify. |`myparm1` |
|UriLevel |Long |No |When `ParamType` is `uri`, you must specify this parameter. It represents the directory you want to specify.<br><br>Requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost directory. |`2` |
|TimeFormat |String |No |Indicates the format of the token timestamp.<br><br><br>* `octal`: Indicates octal format. For example: `14751410031`.<br><br>* `decimal`: Indicates decimal format. For example: `1738936345`.<br><br>* `heximal`: Indicates hexadecimal format. For example: `67a61019`. |`heximal` |
|RewriteM3U8 |Object |No |Indicates the configuration of HLS Manifest modification, that is, configuring how to add tokens to the video segment URIs in the Manifest.<br><br>If `CapMode` under `SignCapRule` is `header` or `cookie`, you cannot set this parameter. | |
|RewriteM3U8Tag |Object |No |Indicates additional tags. For tags included in `Tags`, CDN will add tokens to URIs under these tags. See [Examples of this setting](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#example-of-applying-url-signing-to-extra-tags). | |
|Switch |Boolean |No |Indicates whether to set additional tags. This parameter accepts the following values:<br><br><br>* `true`: Indicates additional tags need to be set.<br><br>* `false`: Indicates additional tags do not need to be set.<br><br><br>The default value is `false`. |`true` |
|Tags |String[] |No |Indicates the list of additional tags. |`["tag1","tag2","tag3"]` |
|Switch |Boolean |No |Indicates whether to modify the HLS Manifest. This parameter accepts the following values:<br><br><br>* `true`: Indicates the Manifest needs to be modified.<br><br>* `false`: Indicates the Manifest does not need to be modified.<br><br><br>By default, CDN only adds tokens to video fragment URIs under the `EXTINF` tag in the Manifest. |`true` |
|RewriteMPD |Object |No |Indicates the configuration of HLS Manifest modification, that is, configuring how to add tokens to the video segment URIs in the Manifest.<br><br>If `CapMode` under `SignCapRule` is `header` or `cookie`, you cannot set this parameter. | |
|MpdVarExpand |Boolean |No |Indicates whether to replace parameters in URIs under `SegmentTemplate` with actual values. `MpdVarExpand` has the following values:<br><br><br>* `true`: Indicates to enable this configuration. When enabled, CDN first replaces parameters in the video segment URI with actual values, then generates a token based on the URI containing actual values, and finally adds the token to the URI.<br><br>* `false`: Indicates not to enable this configuration. The variable names themselves are used as fixed strings for token generation.<br><br><br>The default value of this parameter is `false`.<br><br>When this configuration is enabled, only parameters that meet all of the following conditions will be replaced with actual values:<br><br><br>* The variable is `$RepresentationID$`.<br><br>* Under `SegmentTemplate`, there is at least one URI that meets the following condition:<br><br>   * In this URI, at least one occurrence of `$RepresentationID$` is not in the last segment of the URI path.<br><br>* No other content can appear between `<SegmentTemplate ... />` and `<Representation .../>`.<br><br><br>Additionally, in the rewritten DASH Manifest, the original `SegmentTemplate` will be preserved.<br><br>See [Examples](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#template-parameter-substitution-examples). |`true` |
|Switch |Boolean |No |Indicates whether to modify the DASH Manifest. This parameter accepts the following values:<br><br><br>* `true`: Indicates the Manifest needs to be modified.<br><br>* `false`: Indicates the Manifest does not need to be modified. |`true` |
|SecretKey |Object |No |Indicates the keys used for token calculation. Includes a primary key and a secondary key. | |
|BackupSecretKey |String |No |Indicates the secondary key, with length between 6\-40 characters. When authentication fails, CDN will recalculate the token using `BackupSecretKey` to re\-authenticate the user request. |`secondary-key-456` |
|MasterSecretKey |String |No |Indicates the primary key, with length between 6\-40 characters. |`primary-key-123` |
|SignCapRule |Object |No |Indicates how to obtain the token from user requests. | |
|ArgSegment |Object |No |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a specific level. This segment is the token you need to obtain. | |
|Level |Long |No |Indicates the level where the token is located after the content is split into multiple segments. Requirements are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost segment.<br><br>When `Switch` is `true`, you must specify this parameter. |`2` |
|SplitSymbol |String |No |Indicates the delimiter used to split the content.<br><br>When `Switch` is `true`, you must specify this parameter. |`//` |
|Switch |Boolean |No |Indicates whether the obtained content needs to be split. This parameter accepts the following values:<br><br><br>* `true`: Indicates the content needs to be split.<br><br>* `false`: Indicates the content does not need to be split.<br><br><br>The default value is `false`. |`true` |
|CapMode |String |No |Indicates the source of the token. This parameter accepts the following values:<br><br><br>* `name`: Indicates query parameters. Related configurations are specified in `ParamName`.<br><br>* `uri`: Indicates a directory in the request path. Related configurations are specified in `UriLevel`.<br><br>* `header`: Indicates a header in the request. Related configurations are specified in `CustomValue`.<br><br>* `cookie`: Indicates a cookie in the request. Related configurations are specified in `CustomValue`. |`name` |
|CustomValue |String |No |This parameter has the following meanings:<br><br><br>* When `CapMode` is `header`, you must specify this parameter. It represents the request header you want to specify.<br><br>* When `CapMode` is `cookie`, you must specify this parameter. It represents the key of the cookie you want to specify, and CDN will obtain the corresponding value. |`myheader` |
|ParamName |String |No |When `CapMode` is `name`, you must specify this parameter. It represents the query parameter you want to specify. |`myparam` |
|UriLevel |Long |No |When `CapMode` is `uri`, you must specify this parameter. It represents the directory you want to specify.<br><br>Requirements for this parameter are as follows:<br><br><br>* The level must be a non\-zero integer.<br><br>* The absolute value cannot exceed the total number of levels.<br><br><br>If the level is a negative integer, it counts from right to left starting from the rightmost directory. |`3` |
|Condition |Object |No |Indicates the configuration for matching conditions. If a request meets the matching conditions, CDN performs URL authentication for this request. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. The list can contain up to 10 matching conditions. | |
|Object |String |Yes |Indicates the matching object. This parameter accepts the following values:<br><br><br>* `filetype`: Indicates the file extension of the request.<br><br>* `directory`: Indicates a directory in the request path.<br><br>* `path`: Indicates the complete path of the request, excluding the query string.<br><br>* `regex`: Indicates a regular expression for matching the complete path. |`directory` |
|Operator |String |Yes |Indicates the matching operator. This parameter accepts the following values:<br><br><br>* `match`: Indicates that the request meets this matching condition if `Value` matches the `Object` in the request.<br><br>* `not_match`: Indicates that the request meets this matching condition if `Value` does not match the `Object` in the request. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), or question marks (?).<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a file extension without starting with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a path directory that starts and ends with a forward slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a complete path excluding the query string. The complete path starts with a forward slash (/). Additionally, each matching value can contain wildcards (\*) to represent one or more arbitrary characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If `Object` is `regex`, each matching value represents a regular expression. For example: `/a{1,2}(.*)g`. |`/chs/foods/;/us/birds/` |
|Connective |String |Yes |Indicates the relationship between matching conditions. This parameter accepts the following values:<br><br><br>* `OR`: Indicates an "OR" relationship.<br><br>* `AND`: Indicates an "AND" relationship.<br><br><br>The default value is `OR`. |`OR` |
|RuleName |String |No |Indicates the name of a rule in the rule list. The name cannot exceed 120 characters and can contain Chinese characters, letters, numbers, hyphens (\-), underscores (_), and spaces. Each Chinese character counts as 3 characters. |`Authentication rule A` |
|RewriteFormat |String |No |Indicates the format of the rewritten video fragment URI. This parameter accepts the following values:<br><br><br>* `default`: This value has the same meaning as `absolute`.<br><br>* `relative`: Maintains the current URI format. Note that if `CapMode` under `ExpireTimeRule` or `SignCapRule` is set to `uri`, you cannot set `RewriteFormat` to `relative`.<br><br>* `absolute`: If the URI format is a relative path, CDN converts it to an absolute path. If the URI is already an absolute path or a complete URL, the current format is maintained.<br><br>* `full`: If the URI format is an absolute path or a relative path, CDN converts it to a complete URL.<br><br><br>The default value of this parameter is `default`. |`default` |


<span id="remote-authentication"></span>
### Remote Authentication


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|RemoteAuth |Object |No |Indicates the configuration of the Remote Authentication feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|RemoteAuthRules |Object[] |No |Indicates a list of authentication rules. Currently only one rule can be included in the list. The rule includes matching condition configuration and authentication configuration. This parameter is required when `Switch` is `true`. | |
|Condition |Object |Yes |Indicates the configuration of matching conditions. If a request meets the matching conditions, CDN performs the operation specified in `RemoteAuthRuleAction` for this request. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. The list can contain up to 50 matching conditions.<br><br>The relationship between these matching conditions is "or", which means if a request meets any matching condition, CDN performs the operation specified in `RemoteAuthRuleAction` for this request. | |
|Object |String |Yes |Indicates a matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL. |`filetype` |
|Operator |String |Yes |Indicates a matching type. This parameter has the following values:<br><br><br>* `match`: Indicates that if `Value` matches the `Object` in the request, the request meets this matching condition.<br><br>* `not_match`: Indicates that if `Value` does not match the `Object` in the request, the request meets this matching condition.<br><br><br>Note that the `Operator` in all matching conditions must be the same. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`png;jpg` |
|RemoteAuthRuleAction |Object |Yes |Indicates the authentication\-related configuration.<br><br>When a request meets the matching conditions in `Condition`, CDN sends it to the authentication server for authentication and accepts or rejects the request based on the authentication result. | |
|AuthModeConfig |Object |Yes |Indicates the configuration of the authentication server. | |
|MasterRemoteAddr |String |Yes |Indicates the primary address of the authentication server. The format of the primary address is `<scheme>://<domain>` or `<scheme>://<ip>`. The value for `<scheme>` can be either `http` or `https`. The value of `<domain>` cannot be `localhost`. The value of `<ip>` cannot be `127.0.0.1`. The length of this parameter value should not exceed 100 characters. |`https://primary.example.com` |
|PathType |String |Yes |Indicates the path used in the authentication request. The authentication address and request path form the complete authentication URL. CDN will forward the user request to this authentication URL. This parameter has the following values:<br><br><br>* `constant`: Indicates that the path in the authentication request is the same as in the user`s request.<br><br><br>\|\|<br><br><br>* `variable`: Indicates that you need to specify a path for the authentication request in the `pathValue` parameter. |`constant` |
|RequestMethod |String |Yes |Indicates the method used by the CDN when sending an authentication request. This parameter has the following values:<br><br><br>* `default`: Indicates that the method used for the authentication request is the same as the user`s request.<br><br><br>\|\|<br><br><br>* `get`: Indicates that the authentication request uses the GET method.<br><br>* `post`: Indicates that the authentication request uses the POST method.<br><br>* `head`: Indicates that the authentication request uses the HEAD method. |`get` |
|BackupRemoteAddr |String |No |Indicates the backup address of the authentication server. The address format and requirements are the same as the primary address. |`https://secondary.example.com` |
|PathValue |String |No |Indicates a path for an authentication request, which should not exceed 100 characters. The path must start with a slash (/) and cannot include the following:<br><br><br>* Double slash (//), percent sign (%), dollar sign ($), space, question mark (?) |`/auth` |
|AuthResponseConfig |Object |Yes |CDN needs to process the authentication status codes returned by the authentication server. This parameter indicates the relevant configuration. | |
|CacheAction |Object |No |CDN can cache the authentication status codes. This parameter indicates the relevant configuration. | |
|Action |String |Yes |Indicates whether CDN caches the authentication status codes. The parameter has the following values:<br><br><br>* `nocache`: Indicates that CDN does not cache the authentication status codes.<br><br>* `cache`: Indicates that CDN caches the authentication status codes. |`nocache` |
|Ttl |Long |Yes |Indicates the caching time for the authentication status codes in seconds. The range is 1\-86400. 86400 seconds is equivalent to 24 hours. |`5` |
|CacheKey |String[] |No |The cache key specifies the query parameters used to differentiate between different request URIs. Each parameter must start with a `$`. You may also specify parameters described in [Variable Field Descriptions](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/remote-authentication_1#77280519). |`[$URI,$host]` |
|ResponseAction |Object |No |Indicates how CDN responds to the user when authentication fails. | |
|StatusCode |String |No |Indicates the status code with which CDN responds to the user when authentication fails. You may specify any status code between 400\-499. The default value of this parameter is `403`. |`403` |
|StatusCodeAction |Object |No |Indicates how CDN processes authentication status codes. | |
|DefaultAction |String |Yes |Indicates how CDN processes the authentication request when the status code is neither `FailCode` nor `SuccessCode`. The parameter has the following values:<br><br><br>* `reject`: Indicates that CDN considers the authentication to have failed.<br><br>* `pass`: Indicates that CDN considers the authentication to have succeeded. |`pass` |
|FailCode |String |Yes |Indicates the authentication status code when authentication fails. You may specify one or more status codes between 400\-499. Multiple status codes are separated by a semicolon (;). You may also specify 4xx to represent any status code between 400\-499. |`403` |
|SuccessCode |String |Yes |Indicates the authentication status code when the authentication is successful. You may specify one or more status codes between 200\-299. Multiple status codes are separated by a semicolon (;). You may also specify 2xx to represent any status code between 200\-299. |`200` |
|TimeOutAction |Object |No |Indicates how CDN handles authentication requests after a timeout. | |
|Action |String |Yes |Indicates the policy of CDN in handling authentication requests after a timeout. The parameter has the following values:<br><br><br>* `reject`: Indicates that CDN considers the authentication to have failed.<br><br>* `pass`: Indicates that CDN considers the authentication to have succeeded. |`reject` |
|Time |Long |Yes |Indicates the timeout duration for authentication, in milliseconds, and the range is 200 \- 3600. |`200` |
|QueryStringRules |Object |Yes |Indicates the parameter settings for authentication requests. | |
|QueryStringComponents |Object |No |Indicates the policy settings for authentication request parameters. | |
|Action |String |No |Indicates whether the authentication request includes query parameters from the user request URL. The parameter has the following values:<br><br><br>* `exclude`: Indicates that the authentication request does not include any query parameters.<br><br>* `include`: Indicates that the authentication request includes all query parameters.<br><br>* `includePart`: Indicates that the authentication request includes specified query parameters. |`exclude` |
|Value |String |No |Indicates the corresponding value for the `Action` parameter, which should not exceed 1,024 characters. This parameter has the following values:<br><br><br>* If `Action` is `exclude` or `include`, `Value` must be `*`.<br><br>* If `Action` is `includePart`, you need to specify one or more query parameters from the user request URL in the `Value` parameter, separated by semicolons (;). You cannot specify `*`. Query parameters are case\-sensitive and cannot contain the following:<br><br>   * Double quotes ("), space<br><br><br>The default value of this parameter is `*`. |`*` |
|QueryStringInstances |Object[] |No |Indicates extra parameter settings in the authentication request. You can set up to 50 parameters. | |
|Action |String |No |Indicates how to set authentication request parameters. Currently, you can only set the `Action` to `set`. `set` indicates setting parameters. You need to specify the authentication request parameter you want to set in `Key`. If the authentication request parameter you specify does not exist, CDN will add that parameter to the authentication request. If the authentication request parameter already exists, CDN will use the value of `Value` as the value for that authentication request parameter. |`set` |
|Key |String |No |Indicates the authentication request parameter you need to set, which cannot exceed 1,024 characters in length. Authentication request parameters cannot contain the following:<br><br><br>* Double quotation marks (")、spaces |`sign` |
|Value |String |No |Indicates the value of the authentication request parameter, which cannot exceed 1,024 characters in length and is case\-sensitive. `Value` has the following values:<br><br><br>* When `ValueType` is `constant`, it indicates that the value of the authentication request parameter is a constant. You need to specify the value of the constant. The constant value cannot start with a dollar sign ($) and cannot contain double quotation marks (").<br><br>* When `ValueType` is `variable`, it indicates that the value of the authentication request parameter comes from a variable. You can specify a variable from this [list of variables](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/remote-authentication_1#77280519). |`1235565` |
|ValueType |String |No |Indicates the type of authentication request parameter you have set in `Key`. `ValueType` has the following values:<br><br><br>* `constant`: Indicates that the authentication request parameter is a constant. In this case, you need to specify the value of the constant in `Value`.<br><br>* `variable`: Indicates that the value of the authentication request parameter comes from a variable. See the explanation for `Value`. |`variable` |
|RequestHeaderRules |Object |Yes |Indicates the settings for the authentication request headers. You can set up to 50 request headers. | |
|RequestHeaderComponents |Object |No |Indicates the policy for setting authentication request headers. | |
|Action |String |Yes |Indicates whether the authentication request headers include user request headers. This parameter has the following values:<br><br><br>* `exclude`: Indicates that the authentication request headers do not include any user request headers.<br><br>* `include`: Indicates that the authentication request headers include all user request headers.<br><br>* `includePart`: Indicates that the authentication request headers include specified user request headers. |`exclude` |
|Value |String |No |Indicates the parameter value corresponding to the `Action` parameter, which cannot exceed 1,024 characters in length. This parameter has the following explanations:<br><br><br>* If `Action` is `exclude` or `include`, `Value` must be `*`.<br><br>* If `Action` is `includePart`, the `Value` parameter is one or more headers from the user request. Multiple headers are separated by a semicolon (;). Its value cannot just be `*` and cannot contain the following:<br><br>   * Underscores (_)、Spaces、Double quotation marks (")<br><br><br>The default value of this parameter is `*`. |`*` |
|RequestHeaderInstances |Object[] |No |Indicates a set of settings for authentication request headers.<br><br>Note that the following headers may already be included in the CDN`s authentication request:<br><br>\|\|<br><br><br>* `X-Forwarded-Protocol`, `X-Forwarded-Proto`, `X-Client-Scheme`: All three headers indicate the protocol used by the user request with no difference.<br><br>* `X-Real-IP`: Indicates the user`s real IP address. The value of this header is not affected by proxy servers.<br><br><br>\|\|<br><br><br>* `X-Forwarded-For`: Indicates the user`s IP address. If the user`s request goes through a proxy server, the value of this header becomes the IP address of the proxy server.<br><br><br>It is not recommended to set these headers in this parameter. If you set these headers, their original values will be overwritten. | |
|Action |String |Yes |Indicates how to set the authentication request headers. Currently, you can only set this parameter value to `set`. `set` means setting request headers. At this time, you need to specify the request header you want to set in `Key`. If the request header you set does not exist, CDN will add that request header to the authentication request. If the request header you set already exists, CDN will use the value of `Value` as the value for that request header. |`set` |
|Key |String |Yes |Indicates the request header you need to set. The request header cannot be `host`, cannot exceed 1,024 characters in length, and is case\-insensitive. Request headers cannot contain the following:<br><br><br>* Underscores (_)、Double quotation marks (")、Spaces |`x-test-header` |
|ValueType |String |Yes |Indicates the type of request header. This parameter has the following values:<br><br><br>* `constant`: Indicates that the value of the request header is a constant. You need to specify the value of the constant in the `Value` parameter.<br><br>* `variable`: Indicates that the value of the request header comes from a variable. See the explanation for `Value`. |`variable` |
|Value |String |No |Indicates the value of the request header. This parameter has the following values:<br><br><br>* When `ValueType` is `constant`, you need to specify a constant value. The length of this constant value cannot exceed 1,024 characters and is case\-sensitive. Also, the constant value cannot start with a dollar sign ($), and cannot contain double quotation marks (").<br><br>* When `ValueType` is `variable`, it indicates that the value of the request header comes from a variable. You can specify a variable from this [list of variables](https://docs.byteplus.com/zh-CN/byteplus-cdn/docs/remote-authentication_1#77280519). |`1234fdf` |
|RequestHost |String |No |Indicates the value of the HOST header in the authentication request. The default value of this parameter is `default`, which means that the value of the HOST header is the same as your domain name. |`www.example.com` |


<span id="data-rate-limiting"></span>
### Data Rate Limiting


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|DownloadSpeedLimit |Object |No |Indicates the configuration of the Data Rate Limiting feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|DownloadSpeedLimitRules |Object[] |No |Indicates a list of limiting rules. When `Switch` is `true`, this parameter is required. Other notes about this parameter are as follows:<br><br><br>* Each rule includes matching condition configuration and limiting configuration.<br><br>* The list can contain up to 50 rules.<br><br>* The order of rules in the list represents the priority order of rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|DownloadSpeedLimitAction |Object |Yes |Indicates the limiting configuration. | |
|SpeedLimitRate |Long |Yes |Indicates the maximum data transfer rate when CDN responds to a single request, in `B/S`, using a base of `1,024`. The value range of this parameter is 1\-1,073,741,824,000,000. `1,073,741,824,000,000` is 1,000,000 Gbps. |`500000` |
|SpeedLimitRateAfter |Long |No |Indicates an initial data amount, in `bytes`, using a base of `1,024`. The value range of this parameter is 0\-1,073,741,824,000,000.<br><br>When CDN starts transmitting data for a request, this limiting rule will not be enabled until the amount of transmitted data reaches this initial data amount.<br><br>If this parameter value is `0`, it means that this limiting rule is enabled when CDN starts transmitting the first byte for a request. |`1000` |
|SpeedLimitTime |Object |No |Indicates the dates and time periods when the limiting rule is enabled. | |
|DayWeek |String |Yes |Indicates the dates when this limiting rule is enabled, with the following values: `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `unlimited`. `unlimited` means every day.<br><br>You can specify one or more dates, separated by semicolons (;). |`monday;friday` |
|BeginTime |String |No |Indicates the start time when this limiting rule is enabled, in the format of `mm:ss`.<br><br>If `DayWeek` is `unlimited`, `BeginTime` will be set to `00:00`, which you cannot change. |`05:08` |
|EndTime |String |No |Indicates the end time when this limiting rule is enabled, in the format of `mm:ss`.<br><br>If `DayWeek` is `unlimited`, `EndTime` will be set to `23:59`, which you cannot change. |`16:48` |
|Condition |Object |No |Indicates the configuration of matching conditions. If a request matches a condition, CDN performs the operation specified in `DownloadSpeedLimitAction` for this request.<br><br>If this parameter is not specified, CDN performs the operation specified in `DownloadSpeedLimitAction` for all requests. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates a matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete request path.<br><br>* `unlimited`: Indicates all files under the domain.<br><br>* `regex`: Indicates the complete request path, matched through regular expressions. |`filetype` |
|Operator |String |Yes |Indicates a matching type. This parameter value can only be `match`, which means that if `Value` matches the `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If `Object` is `unlimited`, this parameter value must be empty ("").<br><br>* If `Object` is `regex`, it represents one or more regular expressions. Multiple regular expressions are separated by semicolons (;). For example: `/a/*.jpg`. |`/www/img/f1/;/www/doc/` |


<span id="request-rate-limiting"></span>
### Request Rate Limiting


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|IpFreqLimit |Object |No |Indicates the configuration of the Request Rate Limiting feature. This feature is disabled by default. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|IpFreqLimitRules |Object[] |No |Indicates a set of rules for this feature. When `Switch` is `true`, this parameter is required. Currently, only one rule can be specified. | |
|IpFreqLimitAction |Object |Yes |Indicates the content of the Request Rate Limiting rule. | |
|Action |String |Yes |Indicates the CDN's action when the QPS of an IP reaches `FreqLimitRate`. Currently, you can only set this parameter to `deny`, which means the CDN will refuse new requests from that IP address. |`deny` |
|FreqLimitRate |Long |Yes |Indicates the QPS limit for each IP. The value range for this parameter is 1\-1,000,000. |`5000` |
|StatusCode |String |Yes |Indicates the CDN's response status code when it refuses requests from an IP address. Currently, this parameter can only be set to `403`. |`403` |


<span id="caching"></span>
## Caching

<span id="cache-key"></span>
### Cache Key


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|CacheKey |Object[] |No |Indicates the configuration of the Cache Key feature. In this feature, you can create a list of rules, described below:<br><br><br>* Each rule contains matching condition configuration and operation configuration.<br><br>* The list can contain up to 50 rules.<br><br>* The order in which rules appear in the list indicates the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules.<br><br><br>You **must** add the following default rule at the end of the rule list. This default rule is used to match any user request that does not match other rules. In the default rule, you can adjust the settings in `CacheKeyAction` but cannot modify the configuration in `Condition`.<br><br>```json```<br>```{```<br>```            "CacheKeyAction": {```<br>```                "CacheKeyComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "IgnoreCase": true,```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Name": "",```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|CacheKeyAction |Object |Yes |When a request meets the matching conditions in `Condition`, CDN sets a cache key for the requested file. This parameter represents the configuration of the cache key. | |
|CacheKeyComponents |Object[] |Yes |Cache keys are composed of the host, path and query string in the request. This parameter indicates the configuration of each component. Currently, you can only configure query strings contained in cache keys. | |
|Action |String |Yes |Specifies how the CDN handles query strings in the cache key for requested files. This parameter has the following values:<br><br><br>* `exclude`: Indicates that the cache key does not contain any query parameters from the request.<br><br>* `include`: Indicates that the cache key contains all query parameters from the request. The order of the query parameters in the cache key is the same as their order in the request URL.<br><br>* `includePart`: Indicates that the cache key contains only the query parameters specified in `Subobject`. The CDN sorts the query parameters included in the cache key alphabetically before generating the cache key.<br><br>* `excludePart`: Indicates that the cache key contains all query parameters from the request except those specified in `Subobject`. The CDN sorts the query parameters included in the cache key alphabetically before generating the cache key.<br><br><br>tip<br><br>The order of query parameters in the cache key affects cache matching. If the order of query parameters in the request URL differs from the order in the cache key, the CDN determines that the request is a cache miss. |`excludePart` |
|IgnoreCase |Boolean |Yes |Indicates whether `Subobject` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `false`, and it is valid only when `Action` is `includePart` or `excluePart`. |`true` |
|Object |String |Yes |Indicates a component in the cache key. Currently, the value of this parameter can only be `querystring`, which represents the query string. |`queryString` |
|Subobject |String |Yes |This parameter corresponds to the `Action` and indicates the specific query parameters that the CDN includes in the cache key. The description of this parameter is as follows:<br><br><br>* If `Action` is `include` or `exclude`, `Subobject` must be `*`, indicating all query parameters in the request.<br><br>* If `Action` is `includePart` or `excludePart`, it indicates the query parameters that need to be retained or not retained. Use semicolons (;) to separate multiple query parameters. The query parameters you specify cannot be `*`, nor can they contain double slash (//), percent signs (%), or spaces. |`sign;testParams` |
|Condition |Object |Yes |Indicates the configuration of matching conditions. If a request matches a condition, CDN performs the operation specified in `CacheKeyAction` for this request.<br><br>The `Condition` of the last rule in `CacheKey` must be the following settings. See the example request.<br><br>```json```<br>```"Condition": {```<br>```  "ConditionRule": [```<br>```    {```<br>```      "Object": "directory",```<br>```      "Operator": "match",```<br>```      "Type": "url",```<br>```      "Value": "/"```<br>```    }```<br>```  ]```<br>```}```<br> | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates a matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL.<br><br>* `regex`: Indicates the path in the request URL, matched by a regular expression. |`directory` |
|Operator |String |Yes |Indicates a matching type. This parameter value can only be `match`, which means that if `Value` matches the `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`png` |
|IgnoreCase |Boolean |No |Indicates whether `Value` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="caching-rules"></span>
### Caching Rules


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Cache |Object[] |No |Indicates the configuration for the Caching Rules feature. This feature is disabled by default, meaning no custom rules are created.<br><br><br>* The list can contain up to 50 rules.<br><br>* The order of rules in the list defines their priority. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules.<br><br><br>CDN has a [default cache rule](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules#default-caching-rule) that matches any user request that does not match other rules. This default rule is always effective and has the lowest priority. You do **not** need to specify this default rule when configuring this feature. | |
|CacheAction |Object |Yes |When a request meets the matching conditions in `Condition`, CDN performs the specified operation on the requested file. This parameter defines the configuration related to that operation. | |
|Action |String |Yes |Indicates the operations performed by the CDN. Currently, the value of this parameter can only be `cache`, which means caching the requested file. How requested files are cached is specified in `DefaultPolicy`. |`cache` |
|IgnoreCase |Boolean |Yes |Indicates whether `Value` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `false`. |`true` |
|Ttl |Long |Yes |Indicates the cache duration of the requested file, unit is `seconds`, range is `0-315,360,000`. `315,360,000` is 10 years.<br><br>If the parameter value is `0`, CDN processes requests that match the rule in the following ways:<br><br><br>* If the file has not been cached, CDN will not cache the file.<br><br>* If the file has been cached, the file expires immediately, and subsequent requests for the file will trigger [origin validation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules#origin-validation). This situation typically occurs when you modify the caching rule to change the cache duration of a cached file from a non\-zero value to `0`. |`100` |
|DefaultPolicy |String |No |Indicates the CDN's caching behavior for requested files. This parameter has the following values:<br><br><br>* `force_cache`: Corresponds to the combination of **CDN Cache** + **Force Caching (On)**  in the CDN console.<br><br>* `default`: Corresponds to the combination of **CDN Cache** + **Force Caching (Off)**  in the CDN console.<br><br>* `origin_first`: Corresponds to the combination of **Follow Origin** + **Supplementary Caching (On)**  in the CDN console.<br><br>* `origin_first_Replenish`: Corresponds to the combination of **Follow Origin** + **Supplementary Caching (Off)**  in the CDN console.<br><br>* `no_cache`: Corresponds to the **Disable Caching** configuration in the CDN console.<br><br><br>The default value for this parameter is `default`. For descriptions of these cache policies, see [Cache Rules](https://docs.byteplus.com/en-US/byteplus-cdn/docs/caching-rules). |`force_cache` |
|SetCookieNoCache |Boolean |No |Specifies whether to cache origin responses that contain the Set\-Cookie header. This parameter can take the following values:<br><br><br>* `true`: CDN caches such responses.<br><br>* `false`: CDN does not cache such responses.<br><br><br>The default value is `false`.<br><br>tip<br><br>If `DefaultPolicy` is set to `force_cache`, `SetCookieNoCachedoes` not take effect. |`false` |
|Condition |Object |Yes |Indicates the configuration of matching conditions. If a request matches a condition, CDN performs the operation specified in `CacheAction` for this request. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates a matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL.<br><br>* `regex`: Indicates the path in the request URL, matched by a regular expression. |`directory` |
|Operator |String |Yes |Indicates a matching type. This parameter value can only be `match`, which means that if `Value` matches the `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`png` |


<span id="negative-caching"></span>
### Negative Caching


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|NegativeCache |Object[] |No |Indicates the configuration of the Negative Caching feature. In this feature, you can create a list of rules, as described below:<br><br><br>* Each rule contains matching condition configuration and operation configuration.<br><br>* The list can contain up to 50 rules.<br><br>* The order in which rules appear in the list indicates the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|NegativeCacheRule |Object |Yes |When a request meets the matching conditions in `Condition`, CDN performs the specified operation on the requested file. This parameter defines the configuration related to that operation. | |
|Action |String |Yes |Represents the operations performed by the CDN. Currently, the value of this parameter can only be `cache`, which means caching the response status code of the origin site. |`cache` |
|StatusCode |String |Yes |Indicates the status code that needs to be cached, the range is `400-599`. You can specify a single status code, or you can specify `4xx` or `5xx`.<br><br><br>* `4xx`: Indicates any status code between 400 and 499.<br><br>* `5xx`: Indicates any status code between 500 and 599. |`404` |
|Ttl |Long |Yes |Indicates the cache duration of the status code, the unit is `seconds`, and the range is `1-315,360,000`. `315,360,000` is 10 years. |`100` |
|IgnoreCase |Boolean |No |Indicates whether `Value` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `false`. |`true` |
|Condition |Object |No |Indicates the configuration of matching conditions. If a request matches a condition, CDN performs the operation specified in `NegativeCacheRule` for this request. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates a matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL.<br><br>* `regex`: Indicates the path in the request URL, matched by a regular expression. |`directory` |
|Operator |String |Yes |Indicates a matching type. This parameter value can only be `match`, which means that if `Value` matches the `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`png` |


<span id="browser-caching"></span>
### Browser Caching


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|BrowserCache |Object[] |No |Indicates the configuration of the Browser Caching feature. In this feature, you can create a list of rules, described below:<br><br><br>* Each rule contains matching condition configuration and operation configuration.<br><br>* The list can contain up to 50 rules.<br><br>* The order in which rules appear in the list indicates the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|CacheAction |Object |Yes |When a request meets the matching conditions in `Condition`, CDN performs the specified operation on the requested file. This parameter defines the configuration related to that operation. | |
|Action |String |Yes |Indicates the operation that the browser needs to perform. Currently, the value of this parameter can only be `cache`, which means caching the requested file. How requested files are cached is specified in `DefaultPolicy`. |`cache` |
|IgnoreCase |Boolean |Yes |Indicates whether `Value` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitive.<br><br>* `false`: Indicates case\-sensitive.<br><br><br>The default value of this parameter is `false`. |`true` |
|Ttl |Long |Yes |Indicates the duration for which the browser needs to cache the requested file, in seconds. The CDN will include the `Cache-Control: max-age` header in the response, and the header value is the value of this parameter. |`100` |
|DefaultPolicy |String |No |Indicates how the browser should cache requested files. This parameter has the following values:<br><br><br>* `cache`: Indicates that the requested file needs to be cached.<br><br>* `origin_first`: Indicates that the caching policy from the origin is followed. This policy will be included in the CDN's response.<br><br>* `no_cache`: Indicates that the requested file does not need to be cached.<br><br><br>For detailed information about browser caching policies, see [Browser Caching Policies](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-browser-caching). |`cache` |
|SetCookieNoCache |Boolean |No |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |Yes |Indicates the configuration of matching conditions. If a request matches a condition, CDN performs the operation specified in `CacheAction` for this request. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates a matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL. |`directory` |
|Operator |String |Yes |Indicates a matching type. This parameter value can only be `match`, which means that if `Value` matches the `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`png` |


<span id="client-response-headers"></span>
### Client Response Headers


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|ResponseHeader |Object[] |No |Indicates the configuration of the Client Response Headers feature. | |
|ResponseHeaderAction |Object |Yes |Indicates the operation on response headers by CDN when responding to user requests. | |
|ResponseHeaderInstances |Object[] |Yes |Indicates a list of configuration rules for a response header. Each rule includes settings related to the operation on a header. You can add up to 50 rules. | |
|Action |String |Yes |Specify the operation on response headers. Available values for this parameter are:<br><br><br>* `set`: indicates setting a header. The setting operation includes addition and modification. If the origin response already contains the header, its value will be overwritten. If the origin response does not include the header, it will be added.<br><br>* `delete`: indicates the deletion of a header. |`set` |
|Key |String |Yes |Specify the name of a header. The name cannot exceed 1,024 characters, and it is case\-insensitive. It cannot contain the following:<br><br><br>* Underscore (_), space, double quotes (")<br><br><br>Additionally, header names cannot use these [specific names](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers#notes). |`Content-Disposition` |
|ValueType |String |Yes |Specify the value type for `Key`. This parameter is only valid when `Action` is `set`. If `Action` is not `set`, this parameter is not applicable. The parameter has the following values:<br><br><br>* `constant`: indicates that the value of `Key` is a string.<br><br>* `variable`: indicates that the value of `Key` is sourced from a variable.<br><br>* `customize`: indicates that the value of `Key` is a string concatenated from variables and strings. |`constant` |
|AccessOriginControl |Boolean |No |Indicates whether the CDN needs to verify the Origin header in the request.<br><br>This parameter has the following values:<br><br><br>* `true`: Indicates that the CDN will verify the Origin header. If the verification is successful, the CDN will include the Access\-Control\-Allow\-Origin header in the response. The value of this header is the same as the value of the Origin header. If the verification fails, the response will not include the Access\-Control\-Allow\-Origin header.<br><br>* `false`: Indicates that the CDN will not verify the Origin header. In the response, the CDN will include the Access\-Control\-Allow\-Origin header. The value of this header is the content you configured for Access\-Control\-Allow\-Origin.<br><br><br>The default value for this parameter is `false`.<br><br>This parameter is only valid under the following conditions:<br><br><br>* `Action` is `set`.<br><br>* `Key` is `Access-Control-Allow-Origin`.<br><br>* `ValueType` is `constant`. |`true` |
|Value |String |No |Indicate the value of `Key`. This parameter is only valid when `Action` is `set`. If `Action` is not `set`, this parameter is not applicable. When `ValueType` is `constant`, you must specify a string as the value for the header. The header`s value length cannot exceed 1,024 characters and cannot contain dollar signs ($).<br><br>\|`attachment;filename=FileName.xls`\|<br><br>When `ValueType` is `variable`, the value for `Key` can be sourced from [a variable in this list](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-cdn-response-headers#variable-list).<br><br>When `ValueType` is `customize`, it indicates that the value of `Key` is a concatenated string of variables from the list and strings. Variables are denoted by `${variable name}` in the concatenated string. Example value: `${remote_addr}aaa${host}ccc` | |


<span id="custom-error-pages"></span>
### Custom Error Pages


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|CustomErrorPage |Object |No |Indicates the configuration of the Custom Error Pages feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|ErrorPageRule |Object[] |No |Indicates a collection of configuration rules. You can add up to 50 rules. | |
|ErrorPageAction |Object |Yes |Related configuration for the rule. | |
|Action |String |No |Indicates the actual operation. Currently, you can only specify this parameter value as `redirect`. Indicates that the client`s request is redirected.\|`redirect`\| | |
|RedirectCode |String |Yes |Indicates the response status code for the redirect. You can choose the appropriate status code according to your needs. Available values for this parameter are:<br><br><br>* `301`: Indicates that the content is permanently moved.<br><br>* `302`: Indicates that the content is temporarily moved. |`302` |
|RedirectUrl |String |Yes |Indicates the target address for redirection, length cannot exceed 1,024 characters. The address must include protocol, domain name, and path, and must comply with the URL specifications. |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |Yes |Indicates a status code, with a range of 400\-599. You can enter 4xx or 5xx. 4xx indicates all status codes between 400\-499. 5xx indicates all status codes between 500\-599. |`4xx` |


<span id="multi-range"></span>
### Multi Range


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|MultiRange |Object |No |Indicates the configuration of the Multi Range feature. | |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature. When this feature is enabled, CDN allows Range requests that specify multiple ranges.<br><br>* `false`: Indicates disabling this feature. If CDN receives a Range request that specifies multiple ranges, CDN will reject the request and return a 416 response status code.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="serve-stale"></span>
### Serve Stale


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OfflineCache |Object |No |Indicates the configuration for the Serve Stale feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|Object |String |No |Indicates the trigger condition for this feature. The parameter can have the following values:<br><br><br>* `request_error`: Indicates an origin request error. When an origin request error occurs, CDN does not receive response from the origin.<br><br>* `error_code`: Indicates that the response status code from the origin is 5xx.<br><br>* `request_error,error_code`: Indicates that both of the above conditions are included. |`error_code` |
|StatusCode |String |No |Indicates one or more response status codes, ranging from 500 to 599. Multiple status codes are separated by semicolons (;). You can also enter `5xx` to represent any status code starting with the number 5.<br><br>This parameter is valid only when `Object` is `error_code` or `request_error,error_code`. |`504;505` |
|Switch |Boolean |No |Indicates whether to enable this feature. The parameter can have the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |


<span id="origin-fetch"></span>
## Origin Fetch

<span id="range-origin-fetch"></span>
### Range Origin Fetch


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginRange |Boolean |No |Indicates the configuration of the Range Origin Fetch feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. The default fragment size for Range GET requests is 1 MB.<br><br>tip<br><br>If `Switch` in the `Range` structure is `true`, the feature is enabled, even if `OriginRange` is `false`. |`true` |
|Range |Object |No |Indicates the settings for fragment size. | |
|RangeSize |Long |No |Indicates the size of the fragments.<br><br><br>* If `Unit` is `MB`, the value range of this parameter is 1\-40.<br><br>* If `Unit` is `KB`, the value of this parameter can only be `512`.<br><br><br>The default value of this parameter is `1`. |`512` |
|Switch |Boolean |No |Indicates whether to enable this setting. The parameter can be one of the following values:<br><br><br>* `true`: Indicates enabling this setting.<br><br>* `false`: Indicates disabling this setting.<br><br><br>The default value of this parameter is `false`. |`true` |
|Unit |String |No |Indicates the unit of `RangeSize`. The parameter can be one of the following values:<br><br><br>* `KB`<br><br>* `MB`<br><br><br>The default value of this parameter is `MB`. |`KB` |


<span id="origin-fetch-timeouts"></span>
### Origin Fetch Timeouts


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Timeout |Object |No |Indicates the configuration of the Origin Fetch Timeouts feature. | |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. In this case, the timeout settings for TCP requests and HTTP requests use the system default values, which are 2 seconds and 60 seconds, respectively. |`true` |
|TimeoutRules |Object[] |No |Indicates a set of timeout settings. Currently, you can only specify one configuration. This parameter is required when `Switch` is `true`. | |
|TimeoutAction |Object |No |Indicates the configuration for the timeout period. | |
|HttpTimeout |Long |No |Indicates the maximum time, in seconds, that a CDN point of presence (POP) waits for subsequent response body data after receiving the first byte from the origin server. The connection is closed if no response body data is received within this period. |`60` |
|TcpTimeout |Long |No |Indicates the maximum time, in seconds, that a CDN POP waits to establish a TCP connection with the origin server. The connection attempt times out if the connection is not established within this period. |`2` |
|HttpFirstByteTimeout |Long |No |Indicates the maximum time, in seconds, that a CDN POP waits for the first byte of the response after sending an HTTP request to the origin server. The connection is closed if the first byte is not received within this period. |`90` |


<span id="redirect-follow"></span>
### Redirect Follow


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|FollowRedirect |Boolean |No |Indicates the configuration of the Redirect Follow feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="origin-retry"></span>
### Origin Retry


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginRetry |Object |No |Indicates the configuration of the Origin Retry feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|StatusCode |String |No |Indicates one or more HTTP status codes between 400 and 599, inclusive. Separate multiple status codes with semicolons (`;`). You can specify `4xx` or `5xx` to match all 4xx or 5xx status codes, respectively. |`404;408;5xx` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`false` |


<span id="origin-request-headers"></span>
### Origin Request Headers


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|RequestHeader |Object[] |No |Indicates the configuration of the Origin Request Headers feature. | |
|RequestHeaderAction |Object |Yes |Indicates a list of configuration rules for a request header. Each rule contains settings related to the operation of a header. You can add up to 50 rules. | |
|RequestHeaderInstances |Object[] |Yes |Indicates a list of configuration rules for a request header. Each rule contains settings related to the operation of a header. You can add up to 50 rules. | |
|Action |String |Yes |Specify the operation on request headers. This parameter has the following values:<br><br><br>* `set`: indicates setting a header. The setting operation includes adding and modifying. If the request already includes the header, its value will be overwritten. If the request does not include the header, the header will be added.<br><br>* `delete`, indicates deleting a header. |`set` |
|Key |String |Yes |Specify a header name. The length of the name cannot exceed 1,024 characters, and is case\-insensitive. Also, the name cannot contain the following:<br><br><br>* Underscore (_), space, double quotes (")<br><br><br>Also, header names cannot use these [specific names](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers#notes). |`Cdn-provider` |
|ValueType |String |Yes |Specify the value type of `Key`. This parameter is only valid when `Action` is `set`. If `Action` is not `set`, this parameter is invalid. This parameter has the following values:<br><br><br>* `constant`: indicates that the value of `Key` is a string.<br><br>* `variable`: indicates that the value of `Key` comes from a variable.<br><br>* `customize`: indicates that the value of `Key` is a string concatenated from variables and strings. |`constant` |
|Value |String |No |Indicates the value of `Key`. This parameter is only valid when `Action` is `set`. If `Action` is not `set`, this parameter is invalid. When `ValueType` is `constant`, you need to specify a string as the value of the header. This header value cannot exceed 1,024 characters and cannot contain dollar signs ($).<br><br>When `ValueType` is `variable`, the value of `Key` can be from [a variable in this list](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-request-headers#variable-list).<br><br>When `ValueType` is `customize`, it indicates that the value of `Key` is the concatenated string of variables from the list and strings. In the concatenated string, variables are indicated by `${variable name}`. Sample value: `aaa${http_host}bbb${msec}ccc` |`bp-cdn` |


<span id="origin-request-parameters"></span>
### Origin Request Parameters


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginArg |Object[] |No |Indicates the rule list of the Origin Request Parameters feature.<br><br><br>* The list can contain up to 50 rules.<br><br>* Each rule consists of a matching condition (`Condition`) and the action CDN performs (`OriginArgAction`).<br><br>* The order of rules in the list defines their priority. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules.<br><br><br>You **must** add the following default rule at the end of the rule list. This default rule is used to match any user request that does not match other rules. You cannot modify the `Condition` in this rule, but you can modify the configuration in `OriginArgAction`.<br><br>```json```<br>```{```<br>```            "Condition": {```<br>```                "ConditionRule": [```<br>```                    {```<br>```                        "Object": "directory",```<br>```                        "Operator": "match",```<br>```                        "Type": "url",```<br>```                        "Value": "/"```<br>```                    }```<br>```                ]```<br>```            },```<br>```            "OriginArgAction": {```<br>```                "OriginArgComponents": [```<br>```                    {```<br>```                        "Action": "include",```<br>```                        "Object": "queryString",```<br>```                        "Subobject": "*"```<br>```                    }```<br>```                ]```<br>```            }```<br>```        }```<br> | |
|Condition |Object |Yes |Indicates the configuration of matching conditions. If a request meets this matching condition, CDN performs the operation specified in `OriginArgAction`. Currently, you must and can only specify one condition. | |
|ConditionRule |Object[] |Yes |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates a matching type. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL.<br><br>* `regex`: Indicates the complete path in the request URL, matched through regular expressions. |`directory` |
|Operator |String |Yes |Indicates a matching type. Currently, this parameter value can only be `match`, which means that only a successful match is considered to meet the matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, does not need to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a directory path, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`.<br><br>* If `Object` is `regex`, each matching value represents a regular expression. For examples of regular expressions, see [Configuration Examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-query-parameters_1#url-regex-configuration-examples). |`/` |
|OriginArgAction |Object |Yes |Indicates the action CDN performs when the request meets the `Condition`. | |
|OriginArgComponents |Object[] |Yes |Indicates a list of actions. These actions define how CDN handles query parameters in the origin request.<br><br>Currently, the list can only contain one action. | |
|Action |String |Yes |Indicates the action CDN performs. This parameter has the following values:<br><br><br>* `include`: Indicates that the origin request URL includes all query parameters from the user request URL.<br><br>* `exclude`: Indicates that the origin request URL does not include any query parameters from the user request URL.<br><br>* `addPart`: Indicates that the origin request URL includes all query parameters from the user request URL, and additionally includes the query parameters specified in `Subobject`.<br><br>* `includePart`: Indicates that if the user request URL contains the query parameters specified in `Subobject`, the origin request URL includes these specified query parameters.<br><br>* `excludePart`: Indicates that the origin request URL includes all query parameters from the user request URL, except for the query parameters specified in `Subobject`.<br><br>* `set`: Indicates that the origin request URL includes all query parameters from the user request URL. Additionally, for the query parameters and values you specify in `Subobject`, CDN performs the following actions:<br><br>   * If these query parameters are in the user request URL, CDN sets their values in the origin request URL to the values you specified.<br><br>   * If the user request URL does not contain these query parameters, CDN adds these query parameters to the origin request URL. |`exclude` |
|Object |String |Yes |Indicates which object CDN performs the `Action` on. Currently, this parameter value can only be `queryString`, representing the query string in the request URL. |`queryString` |
|Subobject |String |Yes |Indicates one or more query parameters. Multiple query parameters are separated by semicolons (;), with a total length not exceeding 1,024 characters. `Subobject` can only contain letters, numbers, underscores (_), commas (,), hyphens (\-), periods (.), and exclamation marks (!).<br><br>When matching query parameters in the request URL, the parameters in `Subobject` are case\-sensitive.<br><br>Additional notes for `Subobject`:<br><br><br>* When `Action` is `include` or `exclude`, `Subobject` must be `*`, representing all query parameters in the request URL.<br><br>* When `Action` is `includePart` or `excludePart`, `Subobject` represents one or more query parameters. For example, `param1;param2`.<br><br>* When `Action` is `addPart` or `set`, `Subobject` represents one or more query parameters and their values, in the format `key=value`. For example, `param1=val1;param2=val2;param3=val3`. |`*` |


<span id="origin-sni"></span>
### Origin SNI


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginSni |Object |No |Indicates the configurations of the Origin SNI feature. | |
|SniDomain |String |No |Specifies the domain name for origin SNI. When `Switch` is `true`, this parameter is required. The length of this parameter value cannot exceed 1,024 characters. |`img.example.com` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="origin-url-rewrite"></span>
### Origin URL Rewrite


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginRewrite |Object |No |Indicates the configurations of the Origin URL Rewrite feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|OriginRewriteRule |Object[] |No |Indicates a set of rules for the origin path rewrite. When `Switch` is `true`, this parameter is required. | |
|OriginRewriteAction |Object |No |Indicates a rule configuration for rewriting the origin path. | |
|SourcePath |String |No |Indicates a regular expression, with a maximum length of 1,024 characters, used to match the path in the user request URL. See [examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1#path-rewrite-configuration-examples). |`^/img/food.png$` |
|TargetPath |String |No |Indicates the rewrite path, with a maximum length of 1,024 characters.<br><br>You can use variables such as `$1` , `$2` , and `$3` in `TargetPath` to capture groups defined in `SourcePath`.<br><br>See [examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1#path-rewrite-configuration-examples). |`/png/food.webp` |
|RewriteType |String |No |Indicates the rewrite type. Valid values:<br><br><br>* `rewrite_path`: Rewrites the path in the request URL.<br><br>* `rewrite_url`: Rewrites the path and query string in the request URL.<br><br><br>The default value is `rewrite_path`. |`rewrite_path` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="origin-response-headers"></span>
### Origin Response Headers


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginResponseHeader |Object[] |No |Indicates the configuration of the Origin Response Headers feature. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create). | |
|OriginResponseHeaderAction |Object |No |Indicates the operations that CDN can perform on response headers upon receiving an origin response. | |
|OriginResponseHeaderInstances |Object[] |No |Indicates a list of response header rules. Each rule defines an operation for a response header. You can configure up to 50 rules. | |
|Action |String |No |Indicates the operation that CDN performs on a response header. Valid values:<br><br><br>* `set`: Sets a response header. This operation can add or modify a header. If the origin response already contains the specified header, CDN overwrites its value. Otherwise, CDN adds the header.<br><br>* `delete`: Deletes a response header. |`set` |
|Key |String |No |Indicates the name of a response header. The name can contain up to 1,024 characters. Header names are case\-insensitive and cannot contain Chinese characters, underscores (`_`), spaces, double quotation marks (`"`), or colons (`:`).<br><br>For more information, see [Common Headers](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-headers_en-us#common-headers). |`MyHeader` |
|Value |String |No |Indicates the value of `Key`. This parameter is applicable only when `Action` is `set` and is ignored otherwise.<br><br><br>* When `ValueType` is `constant`, specify a fixed string as the header value. The header value can contain up to 1,024 characters and cannot contain dollar signs (`$`).<br><br>* When `ValueType` is `variable`, the value of `Key` can be a variable selected from the [variable list](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-headers_en-us#variables). A variable whose name does not contain an underscore can be used as `Key` and assigned a fixed string that replaces its existing value.<br><br>* When `ValueType` is `customize`, the value of `Key` is a string formed by concatenating variables from the [variable list](https://docs.byteplus.com/en/docs/byteplus-cdn/origin-response-headers_en-us#variables) and fixed strings. In the concatenated string, represent each variable as `${variable_name}`. Example: `${remote_addr}aaa${host}ccc` |`hello` |
|ValueType |String |No |Indicates the value type of `Key`. This parameter is applicable only when `Action` is `set` and is ignored otherwise. Valid values:<br><br><br>* `constant`: The value of `Key` is a fixed string.<br><br>* `variable`: The value of `Key` is obtained from a variable.<br><br>* `customize`: The value of `Key` is a string formed by concatenating variables and fixed strings. |`constant` |
|Object |String |No |Indicates the origin\-response status codes to which the rule applies. Valid values:<br><br><br>* `default`: The rule applies only to requests with origin responses that have one of the following status codes:<br><br>   * 200, 201, 204, 206, 301, 302, 303, 304, 307, or 308<br><br>* `all_request`: The rule applies to all requests, regardless of the origin\-response status code.<br><br><br>The default value is `default`. When `Action` is `delete`, this parameter can only be set to `all_request`. |`default` |


<span id="content-optimization"></span>
## Content Optimization

<span id="file-compression"></span>
### File Compression


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Compression |Object |No |Indicates the configuration of the File Compression feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|CompressionRules |Object[] |No |Indicates a set of rules. Each rule includes matching condition configuration and operation configuration. | |
|CompressionAction |Object |Yes |Indicates the configuration of the compression operation performed by the CDN on the requested file when the user's request meets the `Condition`. | |
|CompressionType |String[] |Yes |Indicates the compression algorithm used by the CDN. This parameter has the following values:<br><br><br>* `br`: Indicates the Brotli compression algorithm.<br><br>* `gzip`: Indicates the Gzip compression algorithm.<br><br><br>You can specify both algorithms simultaneously.<br><br>Note that the CDN decides whether to compress the requested file and which compression algorithm to use based on the `Accept-Encoding` header in the user's request. |`["gzip","br"]` |
|CompressionFormat |String |No |Indicates that the CDN matches requests based on the `Content-Type` header in the request. This parameter has the following values:<br><br><br>* `default`: Indicates that if the `Content-Type` header value is in the default list below, the CDN performs the operation configured in `CompressionAction` on the requested file.<br><br>* `customize`: Indicates that if the `Content-Type` header value is in the header values specified by `CompressionFormat`, the CDN performs the operation configured in `CompressionAction` on the requested file.<br><br><br>If you need CDN to match requests based on the matching conditions in `Condition`, you do not need to specify `CompressionFormat` or you can specify `CompressionFormat` as `all`.<br><br>**Default list**<br><br>text/html, text/xml, text/plain, text/css, application/javascript, application/x\-javascript, application/rss+xml, text/javascript, image/tiff, image/svg+xml, application/json, application/xml, text/plain; charset=utf\-8If the matching condition is based on the Content\-Type header (in this case, `Condition` is `null` or unspecified), this parameter specifies the matching condition for the Content\-Type. Available values are:<br><br><br>* `default`: Indicates that the matching condition is for file types included in the default Content\-Type list.<br><br>* `customize`: Indicates that the matching condition is for custom file types defined by the user.<br><br><br>If `Condition` is not `null`, it indicates that the matching condition is defined in `ConditionRule`. In this case, this parameter must be set to `all`. |`customize` |
|CompressionTarget |String |No |Indicates the filter value of `Content-Type`.<br><br><br>* If `CompressionFormat` is `default` or `all`, this parameter must be `*`.<br><br>* If `CompressionFormat` is `customize`, you need to specify one or more file types. Multiple file types are separated by commas (,). |`application/xml,hello/world` |
|MinFileSizeKB |Long |No |Indicates the minimum value of the file size range. CDN only compresses files within the range represented by `MinFileSizeKB` and `MaxFileSizeKB`. The value range for this parameter is 0 \- 2,147,483,647, the unit is KB, and the base used is 1,024. The default value for this parameter is `0`. |`10` |
|MaxFileSizeKB |Long |No |文件范围（最大值） |`1000` |
|Condition |Object |No |Indicates the configuration of matching conditions. If a request matches a condition, CDN performs the operation specified in `CompressionAction` for that request.<br><br>Please note that if you specify `CompressionFormat`, `Condition` must be `null` or not specified. | |
|ConditionRule |Object[] |Yes |Indicates the list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Yes |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `path`: Indicates the complete path in the request URL. |`directory` |
|Operator |String |Yes |Indicates the matching type. The value of this parameter can only be `match`, indicating that if `Value` matches the `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |Yes |This parameter can only be `url`, indicating the request URL. |`url` |
|Value |String |Yes |Indicates one or more matching values, with a total length not exceeding 1,024 characters. Multiple matching values are separated by semicolons (;). Matching values cannot contain the following characters:<br><br><br>* Double slash (//), spaces, dollar signs ($), question marks (?)<br><br><br>Additionally,<br><br><br>* If `Object` is `filetype`, each matching value represents a request URL extension, without needing to start with a period (.), and can only contain letters and numbers. For example: `png;txt`.<br><br>* If `Object` is `directory`, each matching value represents a URL Path Directory, starting and ending with a slash (/). For example: `/chs/foods/;/us/birds/`.<br><br>* If `Object` is `path`, each matching value represents a URL Path, starting with a slash (/). Each matching value can contain wildcards (\*) representing one or more characters. For example: `/chs/foods/local*sets;/us/birds/chickadee`. |`/img/` |


<span id="file-minification"></span>
### File Minification


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|PageOptimization |Object |No |Indicates the configuration of the File Minification feature. | |
|OptimizationType |String[] |Yes |Indicates the object for optimization. This parameter can take the following values:<br><br><br>* `html`: Indicates HTML pages.<br><br>* `js`: Indicates Javascript code.<br><br>* `css`: Indicates CSS code.<br><br><br>The default value for this parameter is `html`. If you specify `js` or `css`, `html` must also be specified. |`["html","js"]` |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |


<span id="video-seeking"></span>
### Video Seeking


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|VideoDrag |Object |No |Indicates the configuration of the Video Seeking feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |


<span id="performance-optimization"></span>
## Performance Optimization

<span id="smart-routing"></span>
### Smart Routing


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|SmartOriginRouting |Object |No |Indicates the configuration of the Smart Routing feature. | |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`true` |


<span id="origin-keep-alive"></span>
### Origin Keep\-Alive


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|OriginPreconnect |Object |No |Indicates the configuration of the Origin Keep\-Alive feature. | |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`true` |


<span id="pro-settings"></span>
## Pro Settings

<span id="cache-sharing"></span>
### Cache Sharing


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|CacheHost |Object |No |Indicates the configuration of the Cache Sharing feature. This feature is disabled by default. To use this feature, please [submit a ticket](https://console.byteplus.com/workorder/create).<br><br>If you want to configure Cache Sharing for multiple domains, you need to call this API to configure the caching domain for each domain. | |
|CacheHostRule |Object[] |No |Indicates a set of Cache Sharing configurations. This parameter is required when `Switch` is `true`. | |
|CacheHostAction |Object |No |Indicates the details of a configuration. | |
|CacheHost |String |No |Indicates the caching domain. The caching domain must be a domain under your account. This parameter indicates that `Domain` shares the CDN cache of `CacheHost`. |`www.test.com` |
|Switch |Boolean |No |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value of this parameter is `false`. |`true` |


<span id="ai-traffic-management"></span>
## AI Traffic Management

<span id="convert-html-to-markdown"></span>
### Convert HTML to Markdown


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|HTMLToMarkdown |Object |No |Indicates the configuration of the Convert HTML to Markdown feature. | |
|Switch |Boolean |Yes |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`true` |


<span id="response-parameters"></span>
## Response Parameters

<span id="update-result"></span>
## Update result

<span id="update-result-for-each-domain"></span>
### Update result for each domain


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|DeployResult |Object[] |Indicates the configuration update result for each domain in the `Domains` list. This parameter appears only when `Aggregate` is `false`. | |
|Domain |String |Represents a domain in the `Domains` list. |`www.example.com` |
|ErrorMsg |String |Indicates the reason for the update failure. This parameter appears only when `Status` is `fail`. |`some error` |
|Status |String |Indicates the configuration update result for the domain. This parameter can have the following values:<br><br><br>* `success`: The configuration of the domain was updated successfully.<br><br>* `fail`: The configuration of the domain failed to be updated. |`fail` |


<span id="sample-request-1"></span>
## Sample Request 1

```json
POST https://cdn.byteplusapi.com/?Action=BatchUpdateCdnConfig&Version=2021-03-01
{
    "Domains": [
        "www.example.com",
        "img.example.com",
        "videos.example.com"
    ],
    "OriginProtocol": "http",
    "HTTPS": {
        "Switch": true,
        "OCSP": true
    },
    "Aggregate": true
}
```


<span id="sample-response-1"></span>
## Sample Response 1

```json
{
    "ResponseMetadata": {
        "RequestId": "202410091237542EE1A0C61B73114E0B08",
        "Action": "BatchUpdateCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1",
        "Error": {
            "Code": "InvalidParameter.Domain.xxxxx",
            "Message": "some error"
        }
    }
}
```


<span id="sample-request-2"></span>
## Sample Request 2

```json
POST https://cdn.byteplusapi.com/?Action=BatchUpdateCdnConfig&Version=2021-03-01
{
    "Domains": [
        "www.example.com",
        "img.example.com",
        "videos.example.com"
    ],
    "OriginProtocol": "http",
    "HTTPS": {
        "Switch": true,
        "OCSP": true
    },
    "Aggregate": false
}
```


<span id="sample-response-2"></span>
## Sample Response 2

```json
{
    "ResponseMetadata": {
        "RequestId": "20241009141640E5DE873D9A01D9F72861",
        "Action": "BatchUpdateCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DeployResult": [
            {
                "Domain": "www.example.com",
                "Status": "success"
            },
            {
                "Domain": "img.example.com",
                "ErrorMsg": "error message 1",
                "Status": "fail"
            },
            {
                "Domain": "videos.example.com",
                "ErrorMsg": "error message 2",
                "Status": "fail"
            }
        ]
    }
}
```
