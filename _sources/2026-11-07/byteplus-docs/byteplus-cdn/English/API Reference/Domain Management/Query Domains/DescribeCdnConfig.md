---
title: "DescribeCdnConfig"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnConfig_en-us"
---

Retrieves the configuration of a domain name in BytePlus CDN.

<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `DescribeCdnConfig`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|Domain |String |Yes |Indicates a domain name and retrieves its configuration. |`www.example.com` |


<span id="response-parameters"></span>
## Response Parameters


|Parameter |Data Type |Description |Value |
|---|---|---|---|
|DomainConfig |Object |Indicates the configuration of `Domain`. | |
|Domain |String |Indicates `Domain` in the request parameters. |`www.example.com` |
|Origin |Object[] |Indicates the standard origin configuration. | |
|OriginAction |Object |Indicates the origin configuration, which is applied to all user requests. | |
|OriginLines |Object[] |Indicates a list of origins. | |
|Address |String |Indicates the address of an origin in the list. |`www.example.com` |
|InstanceType |String |Indicates the type of the origin. This parameter has the following values:<br><br><br>* `ip`: Indicates an IP address.<br><br>* `domain`: Indicates a domain name.<br><br>* `tos`: Indicates an object storage bucket. |`ip` |
|OriginType |String |Indicates the type of the origin. This parameter has the following values:<br><br><br>* `primary`: Indicates a primary origin.<br><br>* `backup`: Indicates a backup origin. |`primary` |
|HttpPort |String |Indicates the port that CDN uses to access the origin using the HTTP protocol. |`80` |
|HttpsPort |String |Indicates the port that CDN uses to access the origin using the HTTPS protocol. |`443` |
|OriginHost |String |Indicates the site domain that the origin request accesses, which has a higher priority than the global `OriginHost` parameter. |`img.example.com` |
|PrivateBucketAccess |Boolean |Indicates whether the bucket is a private bucket. This parameter is valid only when `InstanceType` is `tos`. This parameter has the following values:<br><br><br>* `true`: Indicates that the bucket is a private bucket.<br><br>* `false`: Indicates that the bucket is not a private bucket. |`false` |
|PrivateBucketAuth |Object |Specifies the authentication configuration for accessing the bucket. | |
|Switch |Boolean |Indicates whether credentials are required to access the bucket. This parameter has the following values:<br><br><br>* `true`: Indicates that credentials are required.<br><br>* `false`: Indicates that no credentials are required. |`false` |
|AuthType |String |Indicates the authentication method provided by the object storage service that the bucket uses. This parameter has the following values:<br><br><br>* `tos`: Represents BytePlus TOS.<br><br>* `cos`: Represents Tencent Cloud COS.<br><br>* `oss`: Represents AlibabaCloud OSS.<br><br>* `azure`: Represents Microsoft Azure.<br><br>* `aws_common`: Represents AWS S3 or other third\-party object storage services that use an S3\-compatible authentication method. |`cos` |
|TosAuthInformation |Object |Specifies the access credential (AccessKey) for the bucket. | |
|AccessKeyId |String |The AccessKey ID in the access credential, which is referred to as SecretId in Tencent Cloud. Its length is 5 to 100 characters. |`xxxxxxxx` |
|AccessKeySecret |String |The AccessKey Secret in the access credential, which is referred to as SecretKey in Tencent Cloud. Its length is 5 to 100 characters. |`xxxxxx` |
|AccountKey |String |Indicates the shared key of your Azure storage account. This parameter is valid only when `AuthType` is `azure`. |`xxxxxx` |
|Region |String |Indicates the region information where the bucket is located, that is, the region code of the bucket. The region code participates in the calculation of the signature. |`us-east-1` |
|Weight |String |Indicates the weight of the origin. The greater the weight, the greater the probability that the origin will be selected when the CDN sends an origin request.<br><br>This parameter is valid only when `InstanceType` is `ip` or `domain`. |`100` |
|BucketName |String |Indicates the name of your Azure storage account. This parameter is valid only when `AuthType` is `azure`. |`mystorageaccount` |
|OriginProtocol |String |Indicates the protocol used for origin requests. This parameter has the following values:<br><br><br>* `http`: Indicates that origin requests use the HTTP protocol.<br><br>* `https`: Indicates that origin requests use the HTTPS protocol.<br><br>* `followclient`: Indicates that the origin request protocol is the same as the protocol used by the user request. |`http` |
|AreaAccessRule |Object |Indicates the configuration of the Geographic Restrictions feature. | |
|Area |String[] |Indicates a list of countries and regions to which geographic access restrictions are applied. The names of countries and regions are represented by abbreviations. You can call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) and specify `Area` as `Global` to get the abbreviations of countries and regions. |`["CHE","AZE"]` |
|RuleType |String |Indicates the type of `Area`. This parameter has the following values:<br><br><br>* `deny`: Represents that `Area` is a blocklist. CDN will block requests from these countries and regions.<br><br>* `allow`: Represents that `Area` is a whitelist. CDN will only allow requests from these countries and regions. |`allow` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|BrowserCache |Object[] |Indicates the configuration of the Browser Caching feature. In this feature, you can create a list of rules, described below:<br><br><br>* Each rule contains matching condition configuration and action configuration.<br><br>* The order of the rules in the list represents the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|CacheAction |Object |When a request satisfies the matching conditions in `Condition`, the CDN will perform the specified action on the requested file. This parameter defines the configuration related to this action. | |
|Action |String |Indicates the action that the browser needs to perform. Currently, the value of this parameter can only be `cache`, which means to cache the requested file. `DefaultPolicy` specifies how to cache the requested file. |`cache` |
|IgnoreCase |Boolean |Indicates whether `Value` is case\-sensitive.<br><br><br>* `true`: Indicates case\-insensitivity.<br><br>* `false`: Indicates case\-sensitivity. |`true` |
|Ttl |Long |Indicates the duration for which the browser needs to cache the requested file, in seconds. The CDN will include the `Cache-Control: max-age` header in the response, and the header value is the value of this parameter. |`100` |
|DefaultPolicy |String |Indicates how the browser should cache the requested file. This parameter has the following values:<br><br><br>* `cache`: Indicates that the requested file needs to be cached.<br><br>* `origin_first`: Indicates that the caching policy from the origin should be followed. This policy will be included in the CDN's response.<br><br>* `no_cache`: Indicates that the requested file does not need to be cached.<br><br><br>For detailed information about browser caching policies, see [Browser Caching Policy](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-browser-caching). |`cache` |
|SetCookieNoCache |Boolean |是否设置cookie不缓存，仅支持节点缓存规则 | |
|Condition |Object |Indicates the configuration of matching conditions. If a request matches a certain condition, the CDN performs the action specified in `CacheAction` on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. Currently, the list can only contain one matching condition. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a certain directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL. |`directory` |
|Operator |String |Indicates the matching type. The value of this parameter can only be `match`, which means that if `Value` matches `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by semicolons (;). |`png` |
|Cache |Object[] |Indicates the configuration for the Caching Rules feature. This feature is disabled by default, meaning no custom rules are created.<br><br><br>* The order of the rules in the list defines the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|CacheAction |Object |When a request satisfies the matching conditions in `Condition`, the CDN will perform the specified action on the requested file. This parameter defines the configuration related to this action. | |
|Action |String |Indicates the action performed by the CDN. Currently, the value of this parameter can only be `cache`, which means to cache the requested file. `DefaultPolicy` specifies how to cache the requested file. |`cache` |
|IgnoreCase |Boolean |Indicates whether `Value` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitivity.<br><br>* `false`: Indicates case\-sensitivity. |`true` |
|Ttl |Long |Indicates the cache duration of the requested file in `seconds`.<br><br>If the parameter value is `0`, CDN processes requests that match the rule in the following ways:<br><br><br>* If the file has not been cached, CDN will not cache the file.<br><br>* If the file has been cached, the file expires immediately, and subsequent requests for the file will trigger [origin validation](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules#origin-validation). This situation typically occurs when you modify the caching rule to change the cache duration of a cached file from a non\-zero value to `0`. |`100` |
|DefaultPolicy |String |Indicates the caching behavior of the CDN for the requested file. This parameter has the following values:<br><br><br>* `force_cache`: Corresponds to the configuration combination of **CDN Cache** + **Force Cache (On)**  in the CDN console.<br><br>* `default`: Corresponds to the configuration combination of **CDN Cache** + **Force Cache (Off)**  in the CDN console.<br><br>* `origin_first`: Corresponds to the configuration combination of **Follow Origin** + **Supplementary Cache (On)**  in the CDN console.<br><br>* `origin_first_Replenish`: Corresponds to the configuration combination of **Follow Origin** + **Supplementary Cache (Off)**  in the CDN console.<br><br>* `no_cache`: Corresponds to the **Disable Caching** configuration in the CDN console.<br><br><br>For a description of these caching policies, see [Caching Rules](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-caching-rules). |`force_cache` |
|SetCookieNoCache |Boolean |Indicates whether to cache origin responses that contain the Set\-Cookie header. This parameter can take the following values:<br><br><br>* `true`: CDN caches such responses.<br><br>* `false`: CDN does not cache such responses.<br><br><br>tip<br><br>If `DefaultPolicy` is set to `force_cache`, `SetCookieNoCachedoes` not take effect. |`true` |
|Condition |Object |Indicates the configuration of matching conditions. If a request matches a certain condition, the CDN performs the action specified in `CacheAction` on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a certain directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL. |`directory` |
|Operator |String |Indicates the matching type. The value of this parameter can only be `match`, which means that if `Value` matches `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by semicolons (;). |`png` |
|CacheHost |Object |Indicates the configuration of the Cache Sharing feature. | |
|CacheHostRule |Object[] |Indicates a set of shared cache configurations. | |
|CacheHostAction |Object |Indicates the details of a certain configuration. | |
|CacheHost |String |Indicates the target domain name. The target domain name must be another domain name under your account. This parameter indicates that `Domain` shares the CDN cache of `CacheHost`. |`www.test.com` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|CacheKey |Object[] |Indicates the configuration of the Cache Key feature. In this feature, you can create a list of rules, described below:<br><br><br>* Each rule contains matching condition configuration and action configuration.<br><br>* The order of the rules in the list represents the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|CacheKeyAction |Object |When a request satisfies the matching conditions in `Condition`, the CDN sets a cache key for the requested file. This parameter represents the configuration of the cache key. | |
|CacheKeyComponents |Object[] |A cache key is composed of parts such as the host, path, and query string in the request. This parameter represents the configuration of each of these components. | |
|Action |String |Specifies how the CDN handles query strings in the cache key for requested files. This parameter has the following values:<br><br><br>* `exclude`: Indicates that the cache key does not contain any query parameters from the request.<br><br>* `include`: Indicates that the cache key contains all query parameters from the request. The order of the query parameters in the cache key is the same as their order in the request URL.<br><br>* `includePart`: Indicates that the cache key contains only the query parameters specified in `Subobject`. The CDN sorts the query parameters included in the cache key alphabetically before generating the cache key.<br><br>* `excludePart`: Indicates that the cache key contains all query parameters from the request except those specified in `Subobject`. The CDN sorts the query parameters included in the cache key alphabetically before generating the cache key.<br><br><br>tip<br><br>The order of query parameters in the cache key affects cache matching. If the order of query parameters in the request URL differs from the order in the cache key, the CDN determines that the request is a cache miss. |`excludePart` |
|IgnoreCase |Boolean |Indicates whether `Subobject` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitivity.<br><br>* `false`: Indicates case\-sensitivity. |`true` |
|Object |String |Indicates a component of the cache key. Currently, the value of this parameter can only be `querystring`, which represents the query string. |`queryString` |
|Subobject |String |This parameter corresponds to `Action` and indicates the specific query parameters that the CDN includes in the cache key. The description of this parameter is as follows:<br><br><br>* If `Action` is `include` or `exclude`, `Subobject` is `*`, which represents all query parameters in the request.<br><br>* If `Action` is `includePart` or `excludePart`, it represents the query parameters to be retained or not retained. Multiple query parameters are separated by semicolons (;). |`sign;testParams` |
|Condition |Object |Indicates the configuration of matching conditions. If a request matches a certain condition, the CDN performs the action specified in `CacheKeyAction` on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. The list can only contain one matching condition. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a certain directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL. |`directory` |
|Operator |String |Indicates the matching type. The value of this parameter can only be `match`, which means that if `Value` matches `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by semicolons (;). |`png` |
|IgnoreCase |Boolean |Indicates whether `Value` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitivity.<br><br>* `false`: Indicates case\-sensitivity. |`true` |
|Compression |Object |Indicates the configuration of the File Compression feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|CompressionRules |Object[] |Indicates a set of rules. Each rule contains matching condition configuration and action configuration. | |
|CompressionAction |Object |Indicates the configuration of the compression operation that the CDN performs on the requested file when the user request satisfies `Condition`. | |
|CompressionType |String[] |Indicates one or more compression algorithms used by the CDN. This parameter has the following values:<br><br><br>* `br`: Represents the Brotli compression algorithm.<br><br>* `gzip`: Represents the Gzip compression algorithm.<br><br><br>It should be noted that the CDN decides whether to compress the requested file and which compression algorithm to use based on the `Accept-Encoding` header in the user request. |`["gzip","br"]` |
|CompressionFormat |String |Indicates that the CDN matches the request based on the `Content-Type` header in the request. This parameter has the following values:<br><br><br>* `default`: Indicates that if the `Content-Type` header value is in the default list below, the CDN performs the operation configured in `CompressionAction` on the requested file.<br><br>* `customize`: Indicates that if the `Content-Type` header value is in the header values specified by `CompressionFormat`, the CDN performs the operation configured in `CompressionAction` on the requested file.<br><br><br>**Default List**<br><br>text/html,text/xml,text/plain,text/css,application/javascript,application/x\-javascript,application/rss+xml,text/javascript,image/tiff,image/svg+xml,application/json,application/xml,text/plain; charset=utf\-8 |`customize` |
|CompressionTarget |String |Indicates the filter value of `Content-Type`.<br><br><br>* If `CompressionFormat` is `default` or `all`, this parameter is `*`.<br><br>* If `CompressionFormat` is `customize`, this parameter contains one or more file types. Multiple file types are separated by commas (,). |`application/xml,hello/world` |
|MinFileSizeKB |Long |Indicates the minimum file size. The CDN only compresses files whose size is within the range represented by `MinFileSizeKB` and `MaxFileSizeKB`. The unit of this parameter is KB, and the base used is 1,024. |`10` |
|MaxFileSizeKB |Long |Indicates the maximum file size, in KB, using a base of 1,024. If this parameter is not specified, there is no upper limit on the file size. |`1000` |
|Condition |Object |Indicates the configuration of matching conditions. If a request matches a certain condition, the CDN performs the action specified in `CompressionAction` on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a certain directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL. |`directory` |
|Operator |String |Indicates the matching type. The value of this parameter can only be `match`, which means that if `Value` matches `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by semicolons (;). |`/img/` |
|CustomErrorPage |Object |Indicates the configuration of the Custom Error Pages feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|ErrorPageRule |Object[] |Indicates a list of configuration rules. | |
|ErrorPageAction |Object |Indicates the relevant configuration of the rule. | |
|Action |String |Indicates the configuration of the action. Currently, the value of this parameter can only be `redirect`. It indicates that the client request is redirected. |`redirect` |
|RedirectCode |String |Indicates the response status code for the redirection. The possible values for this parameter are `301`, `302`, `303`, `307`, and `308`.<br><br>It should be noted that:<br><br><br>* For 301 and 302, if the method used in the original request is not GET, the method used in the new request sent by the client to the new URL may become GET.<br><br>* For 303, the method used in the new request is GET.<br><br>* For 307 and 308, the method used in the new request is the same as the original request and will not be changed. |`302` |
|RedirectUrl |String |Indicates the target address for the redirect. |`http://www.test.com/friendlyurl.html` |
|StatusCode |String |Indicates a status code, which can be 4xx or 5xx. 4xx represents all status codes between 400 and 499. 5xx represents all status codes between 500 and 599. |`4xx` |
|DownloadSpeedLimit |Object |Indicates the configuration of the Data Rate Limiting feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|DownloadSpeedLimitRules |Object[] |Indicates a list of rate limit rules. Other descriptions of this parameter are as follows:<br><br><br>* Each rule contains matching condition configuration and rate limit configuration.<br><br>* The order of the rules in the list represents the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|DownloadSpeedLimitAction |Object |Indicates the limiting configuration. | |
|SpeedLimitRate |Long |Indicates the maximum data transfer rate of the CDN when responding to a single request, in `B/S`, using a base of `1,024`. |`500000` |
|SpeedLimitRateAfter |Long |Indicates an initial data volume, in `bytes`, using a base of `1,024`.<br><br>When the CDN starts transferring data for a request, this rate limit rule will not be enabled until the transferred data volume reaches this initial data volume.<br><br>If the value of this parameter is `0`, it means that the rate limit rule is enabled when the CDN starts transferring the first byte for a request. |`1000` |
|SpeedLimitTime |Object |Indicates the date and time period when the rate limit rule is enabled. | |
|DayWeek |String |Indicates the date on which the rate limit rule is enabled, with the following possible values: `monday`, `tuesday`, `wednesday`, `thursday`, `friday`, `saturday`, `sunday`, `unlimited`.<br><br>`unlimited` means every day. Multiple dates are separated by semicolons (;). |`monday;friday` |
|BeginTime |String |Indicates the start time for enabling the rate limit rule, in the format `mm:ss`. |`05:08` |
|EndTime |String |Indicates the end time for enabling the rate limit rule, in the format `mm:ss`. |`16:48` |
|Condition |Object |Indicates the configuration of matching conditions. If a request matches a certain condition, the CDN performs the action specified in `DownloadSpeedLimitAction` on the request.<br><br>If this parameter does not appear or is `null`, the CDN performs the action specified in `DownloadSpeedLimitAction` on all requests. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a certain directory in the request URL.<br><br>* `path`: Represents the complete request path.<br><br>* `unlimited`: Represents all files under the domain name.<br><br>* `regex`: Represents the complete request path, matched by regular expression. |`filetype` |
|Operator |String |Indicates the matching type. The value of this parameter can only be `match`, which means that if `Value` matches `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by semicolons (;). |`/www/img/f1/;/www/doc/` |
|FollowRedirect |Boolean |Indicates the configuration of the Redirect Follow feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|HTTPS |Object |Indicates the configuration of the HTTPS encryption service. | |
|Switch |Boolean |Indicates whether to enable the HTTPS encryption service. This parameter has the following values:<br><br><br>* `true`: Indicates that the HTTPS encryption service is enabled.<br><br>* `false`: Indicates that the HTTPS encryption service is disabled. |`true` |
|CertInfo |Object |Indicates the certificate to be associated with the domain name. | |
|CertId |String |Indicates the ID of the certificate to be associated. |`cert-eb5d99026753499a8a34d2a4f0a08d92` |
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
|IPv6 |Object |Indicates IPv6 configuration. | |
|Switch |Boolean |Indicates whether to enable IPv6 support for user requests. This parameter has the following values:<br><br><br>* `true`: Indicates that IPv6 is enabled.<br><br>* `false`: Indicates that IPv6 is disabled. |`true` |
|IpAccessRule |Object |Indicates the configuration of the IP Restrictions feature.<br><br>This feature provides two configuration methods:<br><br><br>* Regular configuration: Specify `RuleType` and `Ip` to configure the current domain name.<br><br>* Universal catalog: Specify `SharedConfig` to use a universal catalog. | |
|Ip |String[] |Indicates the IP addresses in the blocklist or allowlist. |`["xx.xxx.xx.xx","x.x.x.x"]` |
|RuleType |String |Indicates the type of IP list. This parameter has the following values:<br><br><br>* `allow`: Represents a allowlist.<br><br>* `deny`: Represents a blocklist. |`deny` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|SharedConfig |Object |Indicates a universal catalog. | |
|ConfigName |String |Indicates the name of a universal catalog. The `ConfigType` of this universal catalog must be `deny_ip_access_rule` or `allow_ip_access_rule`.<br><br><br>* `deny_ip_access_rule`: Represents an IP blocklist.<br><br>* `allow_ip_access_rule`: Represents an IP allowlist.<br><br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get a list of universal catalogs. |`my_whitelist` |
|DenyStatusCode |Long |Indicates the HTTP status code returned by CDN when it rejects a request. |`403` |
|IpSource |Object |Indicates the configuration for how CDN obtains the client IP address. | |
|SourceList |String[] |Indicates one or more IP sources used when `Type` is `custom`.<br><br>Valid values:<br><br><br>* `x-real-ip`: Indicates the IP address obtained from the `X-Real-IP` request header.<br><br>* `x-forwarded-for`: Indicates the IP address obtained from the `X-Forwarded-For` request header.<br><br>* `client-ip`: Indicates the actual connection IP. The actual connection IP is the IP address of the peer that directly establishes a network connection with the CDN node.<br><br><br>For an IP blocklist, CDN rejects the request if any IP address obtained from the selected sources matches a blocklist rule. For an IP allowlist, CDN allows the request only if all IP addresses obtained from the selected sources match allowlist rules. |`["x-real-ip", "x-forwarded-for"]` |
|Type |String |Indicates the method used to determine the client IP address.<br><br>Valid values:<br><br><br>* `default`: Uses the actual connection IP.<br><br>* `custom`: Uses one or more sources specified in `SourceList`. If CDN cannot obtain an IP address from a selected request header, it uses the actual connection IP for that source. |`custom` |
|IpFreqLimit |Object |Indicates the configuration of the Request Rate Limiting feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|IpFreqLimitRules |Object[] |Indicates a set of rules for this feature. | |
|IpFreqLimitAction |Object |Indicates the content of the Request Rate Limiting rule. | |
|FreqLimitRate |Long |Indicates the QPS Limit for each IP. The value range for this parameter is 1\-1,000,000. |`5000` |
|StatusCode |String |Indicates the CDN's response status code when it refuses requests from an IP address. Currently, this parameter can only be set to `403`. |`403` |
|MethodDeniedRule |Object |Indicates the configuration of the Disabled HTTP Methods feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|Methods |String |Indicates one or more disabled HTTP request methods. Multiple methods are separated by commas (,). This parameter has the following values:<br><br><br>* `get`: Disables the GET request method.<br><br>* `post`: Disables the POST request method.<br><br>* `delete`: Disables the DELETE request method.<br><br>* `put`: Disables the PUT request method.<br><br>* `head`：Indicates that the HEAD request method is disabled.<br><br>* `patch`: Represents the PATCH request method.<br><br>* `connect`: Represents the CONNECT request method.<br><br>* `options`: Represents the OPTIONS request method. |`delete,put` |
|NegativeCache |Object[] |Indicates the configuration of the Negative Caching feature, which contains a list of rules, as described below:<br><br><br>* Each rule contains matching condition configuration and action configuration.<br><br>* The order of the rules in the list represents the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|NegativeCacheRule |Object |When a request satisfies the matching conditions in `Condition`, the CDN will perform the specified action on the requested file. This parameter defines the configuration related to this action. | |
|Action |String |Indicates the action performed by the CDN. Currently, the value of this parameter can only be `cache`, which means to cache the response status code of the origin. |`cache` |
|StatusCode |String |Indicates a status code to be cached, in the range of `400-599`, which can be `4xx` or `5xx`. `4xx` represents all status codes between 400 and 499. `5xx` represents all status codes between 500 and 599. |`404` |
|Ttl |Long |Indicates the cache duration of the status code, in `seconds`. |`100` |
|IgnoreCase |Boolean |Indicates whether `Value` is case\-sensitive.<br><br><br>* `true`: Indicates case\-insensitivity.<br><br>* `false`: Indicates case\-sensitivity. |`true` |
|Condition |Object |Indicates the configuration of matching conditions. If a request matches a certain condition, the CDN performs the action specified in `NegativeCacheRule` on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a certain directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL. |`directory` |
|Operator |String |Indicates the matching type. The value of this parameter can only be `match`, which means that if `Value` matches `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by semicolons (;). |`png` |
|OriginAccessRule |Object |Indicates the configuration of the Origin Restrictions feature. | |
|AllowEmpty |Boolean |Indicates how CDN handles a request when the user request does not contain an Origin header. This parameter has the following values:<br><br><br>* `true`: Indicates that if the request does not contain an Origin header, the request is considered to match the configured Origin list.<br><br>* `false`: Indicates that if the request does not contain an Origin header, the request is considered not to match the configured Origin list. |`true` |
|IgnoreCase |Boolean |Indicates whether the Origin list is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates that the Origin list is case\-insensitive.<br><br>* `false`: Indicates that the Origin list is case\-sensitive. |`true` |
|Origins |String[] |Indicates an Origin list. |`["www.test.com"]` |
|RuleType |String |Indicates the type of Origin list. This parameter has the following values:<br><br><br>* `allow`: Represents an allowlist.<br><br>* `deny`: Represents a blocklist. |`deny` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|OriginArg |Object[] |Indicates a list of rules for the Origin Request Parameters feature.<br><br><br>* Each rule consists of a matching condition (`Condition`) and an action performed by CDN (`OriginArgAction`).<br><br>* The order of the rules in the list defines the priority of the rules. The first rule in the list has the highest priority.<br><br>* When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|Condition |Object |Indicates the configuration of matching conditions. If a request satisfies the matching condition, CDN performs the action specified in `OriginArgAction`. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching type. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL.<br><br>* `regex`: Represents the complete path in the request URL, matched by a regular expression. |`directory` |
|Operator |String |Indicates the matching type. Currently, the value of this parameter can only be `match`, which means that a match is considered successful only if the match is successful. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by a semicolon (;). |`/` |
|OriginArgAction |Object |Indicates the action performed by CDN when the request satisfies `Condition`. | |
|OriginArgComponents |Object[] |Indicates a list of actions. These actions define how CDN handles the query parameters in the origin request. | |
|Action |String |Indicates the action performed by CDN. This parameter has the following values:<br><br><br>* `include`: Indicates that the origin request URL includes all query parameters from the user request URL.<br><br>* `exclude`: Indicates that the origin request URL does not include any query parameters from the user request URL.<br><br>* `addPart`: Indicates that the origin request URL includes all query parameters from the user request URL, and additionally includes the query parameters specified in `Subobject`.<br><br>* `includePart`: Indicates that if the user request URL includes the query parameters specified in `Subobject`, then the origin request URL includes these specified query parameters.<br><br>* `excludePart`: Indicates that the origin request URL includes all query parameters from the user request URL, except for the query parameters specified in `Subobject`.<br><br>* `set`: Indicates that the origin request URL includes all query parameters from the user request URL. At the same time, for the query parameters and parameter values specified in `Subobject`, CDN performs the following operations:<br><br>   * If these query parameters are in the user request URL, CDN sets the values of these parameters to the specified values in the origin request URL.<br><br>   * If the user request URL does not include these query parameters, CDN adds these query parameters to the origin request URL. |`exclude` |
|Object |String |Indicates the object on which CDN performs the `Action`. Currently, the value of this parameter can only be `queryString`, which represents the query string in the request URL. |`queryString` |
|Subobject |String |Indicates one or more query parameters. Multiple query parameters are separated by a semicolon (;).<br><br>When matching query parameters in the request URL, the parameters in `Subobject` are case\-sensitive.<br><br>If `Subobject` is `*`, it represents all query parameters in the request URL. |`*` |
|OriginHost |String |If there are multiple sites on the origin server, this parameter represents the site domain that the origin request accesses. This parameter takes effect for all origin configurations, but has a lower priority than the `OriginHost` parameter in the origin configuration. |`img.example.com` |
|OriginRange |Boolean |Indicates the configuration of the Range Origin Fetch feature. This parameter has the following values:<br><br><br>* `true`: Indicates that the feature is enabled.<br><br>* `false`: Indicates that the feature is disabled.<br><br><br>The default fragment size for Range GET requests is 1 MB. |`true` |
|OriginRewrite |Object |Indicates the configurations of the Origin URL Rewrite feature. | |
|OriginRewriteRule |Object[] |Indicates a set of rules for the origin path rewrite. | |
|OriginRewriteAction |Object |Indicates a rule configuration for rewriting the origin path. | |
|SourcePath |String |Indicates a regular expression, with a maximum length of 1,024 characters, used to match the path in the user request URL. See [examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1#path-rewrite-configuration-examples). |`^/img/food.png$` |
|TargetPath |String |Indicates the rewrite path, with a maximum length of 1,024 characters.<br><br>You can use variables such as `$1` , `$2` , and `$3` in `TargetPath` to capture groups defined in `SourcePath`.<br><br>See [examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-origin-path-rewrite_1#path-rewrite-configuration-examples). |`/png/food.webp` |
|RewriteType |String |Indicates the rewrite type. Valid values:<br><br><br>* `rewrite_path`: Rewrites the path in the request URL.<br><br>* `rewrite_url`: Rewrites the path and query string in the request URL. |`rewrite_path` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`true` |
|OriginSni |Object |Indicates the configurations of the Origin SNI feature. | |
|SniDomain |String |Specifies the domain name for the origin SNI. |`img.example.com` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|PageOptimization |Object |Indicates the configuration of the File Minification feature. | |
|OptimizationType |String[] |Indicates the object to be optimized. This parameter has the following values:<br><br><br>* `html`: Represents an HTML page.<br><br>* `js`: Represents Javascript code.<br><br>* `css`: Represents CSS code. |`["html","js"]` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|Quic |Object |Indicates the HTTP/3 (QUIC) configuration. | |
|Switch |Boolean |Indicates whether to enable QUIC for user requests. This parameter has the following values:<br><br><br>* `true`: Indicates that QUIC is enabled.<br><br>* `false`: Indicates that QUIC is disabled. |`true` |
|RedirectionRewrite |Object |Indicates the configuration of the URL Redirect feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|RedirectionRule |Object[] |Indicates a list of URL redirect rules. The first rule in the list has the highest priority.<br><br>When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|RedirectionAction |Object |Indicates a URL redirect rule. | |
|RedirectCode |String |Indicates the response status code for the URL redirect. The possible values for this parameter are `301`, `302`, `303`, `307`, and `308`.<br><br>Please note:<br><br><br>* For 301 and 302, if the method used in the original request is not GET, the method used in the new request to the new URL may become GET.<br><br>* For 303, the method used in the new request is GET.<br><br>* For 307 and 308, the method used in the new request is the same as the original request and will not be changed. |`301` |
|SourcePath |String |Indicates the original path of the file. This is the path included in the request. |`/img/image.png` |
|TargetHost |String |Indicates the domain name or IP address to which the target path belongs. |`www.test.com` |
|TargetPath |String |Indicates the target path after the redirect. |`/png/image.png` |
|TargetProtocol |String |Indicates the protocol used by the new request after the URL redirect. This parameter has the following values:<br><br><br>* `followclient`: Indicates that the protocol of the original request is used.<br><br>* `http`: Indicates that the new request is forced to use the HTTP protocol.<br><br>* `https`: Indicates that the new request is forced to use the HTTPS protocol. |`followclient` |
|TargetQueryComponents |Object |Indicates how to handle the query parameters in the original request URL. | |
|Action |String |Indicates how to handle the query parameters in the original request URL. This parameter has the following values:<br><br><br>* `include`: Indicates that all query parameters from the original request URL are included in the redirected URL.<br><br>* `exclude`: Indicates that no query parameters from the original request URL are included in the redirected URL.<br><br>* `includePart`: Indicates that specific query parameters from the original request URL are included in the redirected URL.<br><br>* `excludePart`: Indicates that specific query parameters from the original request URL are not included in the redirected URL. |`include` |
|Value |String |Indicates the query parameters to be retained or deleted. Multiple query parameters are separated by a semicolon (;). If `Value` is `*`, it represents all query parameters. |`seq` |
|RefererAccessRule |Object |Indicates the configuration of the Referer Restrictions feature. For information on how different configurations affect request matching results, see [Configuration Examples](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-referer-restrictions#configuration-examples). | |
|AllowEmpty |Boolean |Indicates whether requests with an empty Referer header ("") or without a Referer header are allowed. This parameter has the following values:<br><br><br>* `true`: Indicates allowed.<br><br>* `false`: Indicates not allowed. If the Referer header of the request is empty ("") or does not contain a Referer header, BytePlus CDN rejects the request. |`true` |
|Referers |String[] |Indicates a list of Referers. Referers can also be specified in `ReferersType`. |`["www.test.com","xxx.xx.x.x","xx.xx.xx.x/24"]` |
|ReferersType |Object |Indicates a `ReferersType` object. It contains a `CommonType` object and a `RegularType` object, which represent a regular Referer list and a list of regular expressions for matching Referers, respectively. `CommonType` and `RegularType` can exist at the same time. | |
|CommonType |Object |Indicates a `CommonType` object, which contains a regular Referer list. | |
|IgnoreCase |Boolean |Indicates whether the `Referers` list under `CommonType` is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: Indicates case\-insensitivity.<br><br>* `false`: Indicates case\-sensitivity. |`true` |
|Referers |String[] |Indicates a regular Referer list. |`["www.test.com","xxx.xxx.xx.xxx","1xx.xx.xx.x/24"]` |
|IgnoreScheme |Boolean |Indicates whether CDN verifies the scheme in the Referer, that is, whether the Referer contains `http://` or `https://`. This parameter has the following values:<br><br><br>* `true`: Indicates that CDN does not verify whether the Referer contains a scheme. In this case, regardless of whether the Referer contains a scheme, CDN will match the Referer against the configured list.<br><br>* `false`: Indicates that CDN will first verify whether the Referer contains a scheme. Only if the Referer contains a scheme will CDN match the Referer against the configured list. Otherwise, CDN determines that the request does not match the configured list.<br><br><br>This configuration does not take effect for the list of regular expressions under `RegularType`, because CDN relies on regular expressions to determine whether the Referer matches the regular expression list. |`false` |
|RegularType |Object |Indicates a `RegularType` object, which contains a list of regular expressions used to match the Referer header in the request. | |
|Referers |String[] |Indicates a list of regular expressions for matching Referers. |`^http://a.com` |
|RuleType |String |Indicates the type of the Referer list. This parameter has the following values:<br><br><br>* `allow`: Represents an allowlist.<br><br>* `deny`: Represents a blocklist. |`deny` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|SharedConfig |Object |Indicates a universal catalog. | |
|ConfigName |String |Indicates the name of a universal catalog. The `ConfigType` of this universal catalog must be `deny_referer_access_rule` or `allow_referer_access_rule`.<br><br><br>* `deny_referer_access_rule`: Represents a Referer blocklist.<br><br>* `allow_referer_access_rule`: Represents a Referer allowlist.<br><br><br>You can call [ListSharedConfig](https://docs.byteplus.com/en/docs/byteplus-cdn/ListSharedConfig_en) to get a list of universal catalogs. |`my_allowlist` |
|RemoteAuth |Object |Indicates the configuration of the Remote Authentication feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|RemoteAuthRules |Object[] |Indicates a list of authentication rules. Each rule contains matching condition configuration and authentication configuration. | |
|Condition |Object |Indicates the configuration of matching conditions. If a request satisfies the matching conditions, CDN performs the action specified in `RemoteAuthRuleAction` on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions.<br><br>The relationship between these matching conditions is "OR", which means that if a request satisfies any of the matching conditions, CDN performs the action specified in `RemoteAuthRuleAction` on the request. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension in the request URL.<br><br>* `directory`: Represents a directory in the request URL.<br><br>* `path`: Represents the complete path in the request URL. |`filetype` |
|Operator |String |Indicates the matching type. This parameter has the following values:<br><br><br>* `match`: Indicates that if `Value` matches `Object` in the request, the request satisfies this matching condition.<br><br>* `not_match`: Indicates that if `Value` does not match `Object` in the request, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by a semicolon (;). |`png;jpg` |
|RemoteAuthRuleAction |Object |Indicates authentication\-related configurations.<br><br>When a request satisfies the matching conditions in `Condition`, CDN sends it to the authentication server for authentication, and accepts or rejects the request based on the authentication result. | |
|AuthModeConfig |Object |Indicates the configuration of the authentication server. | |
|MasterRemoteAddr |String |Indicates the primary address of the authentication server. |`https://primary.example.com` |
|PathType |String |Indicates the path of the authentication request. The authentication address and request path form the complete authentication URL. CDN forwards the user's request to this authentication URL. This parameter has the following values:<br><br><br>* `constant`: Indicates that the path in the authentication request is the same as the path in the user request.<br><br>* `variable`: Represents the path specified in `pathValue`. |`constant` |
|RequestMethod |String |Indicates the request method used by CDN when sending an authentication request. This parameter has the following values:<br><br><br>* `default`: Indicates that the method used for the authentication request is the same as the user's request.<br><br>* `get`: Indicates that the authentication request uses the GET method.<br><br>* `post`: Indicates that the authentication request uses the POST method.<br><br>* `head`: Indicates that the authentication request uses the HEAD method. |`get` |
|BackupRemoteAddr |String |Indicates the backup address of the authentication server. |`https://secondary.example.com` |
|PathValue |String |Indicates the path of an authentication request. |`/auth` |
|AuthResponseConfig |Object |CDN needs to process the authentication status code returned by the authentication server. This parameter represents the relevant configuration. | |
|CacheAction |Object |CDN can cache authentication status codes. This parameter represents the relevant configuration. | |
|Action |String |Indicates whether CDN caches authentication status codes. This parameter has the following values:<br><br><br>* `nocache`: Indicates that CDN does not cache authentication status codes.<br><br>* `cache`: CDN caches authentication status codes. |`nocache` |
|Ttl |Long |Indicates the cache time of the authentication status code, in seconds. |`5` |
|CacheKey |String[] |The cache key specifies the query parameters used to distinguish different request URIs. Each parameter must start with `$`. See the parameter in [Variable Field Description](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-remote-authentication_1#authentication-parameters). |`[$URI,$host]` |
|ResponseAction |Object |Indicates how CDN responds to the user when authentication fails. | |
|StatusCode |String |Indicates the status code that CDN responds to the user when authentication fails. |`403` |
|StatusCodeAction |Object |Indicates how CDN handles authentication status codes. | |
|DefaultAction |String |Indicates how CDN handles the authentication request if the authentication status code is neither `FailCode` nor `SuccessCode`. This parameter has the following values:<br><br><br>* `reject`: Indicates that CDN considers the authentication to have failed.<br><br>* `pass`: Indicates that CDN considers the authentication to have succeeded. |`pass` |
|FailCode |String |Indicates the authentication status codes for authentication failure. Multiple status codes are separated by a semicolon (;). |`403` |
|SuccessCode |String |Indicates the authentication status codes for authentication success. Multiple status codes are separated by a semicolon (;). |`200` |
|TimeOutAction |Object |Indicates how CDN handles the authentication request after an authentication timeout. | |
|Action |String |Indicates the policy for CDN to handle authentication requests after an authentication timeout. This parameter has the following values:<br><br><br>* `reject`: Indicates that CDN considers the authentication to have failed.<br><br>* `pass`: Indicates that CDN considers the authentication to have succeeded. |`reject` |
|Time |Long |Indicates the authentication timeout time, in milliseconds. |`200` |
|QueryStringRules |Object |Indicates the parameter settings for the authentication request. | |
|QueryStringComponents |Object |Indicates the setting policy for authentication request parameters. | |
|Action |String |Indicates whether the authentication request includes the query parameters from the user request URL. This parameter has the following values:<br><br><br>* `exclude`: Indicates that the authentication request does not include any query parameters.<br><br>* `include`: Indicates that the authentication request includes all query parameters.<br><br>* `includePart`: Indicates that the authentication request includes the specified query parameters. |`exclude` |
|Value |String |Indicates the parameter value corresponding to the `Action` parameter. `*` represents all query parameters. |`*` |
|QueryStringInstances |Object[] |Indicates additional parameter settings in the authentication request. | |
|Action |String |Indicates how to set the authentication request parameters. The current parameter value can only be `set`. `set` means to set the parameters. `Key` specifies the authentication request parameters to be set.<br><br><br>* If the specified authentication request parameter does not exist, CDN will add the parameter to the authentication request.<br><br>* If the specified authentication request parameter already exists, CDN will use the value of `Value` as the value of the authentication request parameter. |`set` |
|Key |String |Indicates the authentication request parameters to be set. |`sign` |
|Value |String |Indicates the value of the authentication request parameter. It is case\-sensitive. |`1235565` |
|ValueType |String |Indicates the type of the authentication request parameter specified by Key. ValueType has the following values:<br><br><br>* `constant`: Indicates that the authentication request parameter is a constant.<br><br>* `variable`: Indicates that the value of the authentication request parameter comes from a variable. See the description of `Value`.<br><br>* `customize`: Indicates that the value of the authentication request parameter is a string concatenated from a variable and a fixed string. |`variable` |
|RequestHeaderRules |Object |Indicates the settings for the authentication request header. | |
|RequestHeaderComponents |Object |Indicates the setting policy for the authentication request header. | |
|Action |String |Indicates whether the authentication request header includes the user request header. This parameter has the following values:<br><br><br>* `exclude`: Indicates that the authentication request header does not include any user request headers.<br><br>* `include`: Indicates that the authentication request header includes all user request headers.<br><br>* `includePart`: Indicates that the authentication request header includes the specified user request headers. |`exclude` |
|Value |String |Indicates the parameter value corresponding to the Action parameter. If the parameter value is \*, it represents all request headers. |`*` |
|RequestHeaderInstances |Object[] |Indicates a set of authentication request header settings.<br><br>Note that when the CDN initiates an authentication request, the request may already contain the following headers:<br><br><br>* `X-Forwarded-Protocol`, `X-Forwarded-Proto`, `X-Client-Scheme`: These three headers all represent the protocol used by the user request, and there is no difference.<br><br>* `X-Real-IP`: Represents the user's real IP address. The value of this header is not affected by proxy servers.<br><br>* `X-Forwarded-For`: Represents the user's IP address. If the user's request passes through a proxy server, the value of this header will become the IP address of the proxy server. | |
|Action |String |Indicates how to set the authentication request header. Currently, this parameter can only be set, which means to set the request header. `Key` specifies the request header to be set.<br><br><br>* If the set request header does not exist, the CDN will add the request header to the authentication request.<br><br>* If the set request header already exists, the CDN will use the value of `Value` as the value of the request header. |`set` |
|Key |String |Indicates the request header to be set. |`x-test-header` |
|ValueType |String |Indicates the type of the request header. This parameter has the following values:<br><br><br>* `constant`: Indicates that the value of the request header is a constant.<br><br>* `variable`: Indicates that the value of the request header comes from a variable.<br><br>* `customize`: Indicates that the value of the request header is a string concatenated from a variable and a fixed string. |`variable` |
|Value |String |Indicates the value of the request header. |`1234fdf` |
|RequestHost |String |Indicates the value of the HOST header in the authentication request. The default value of this parameter is default, which means that the value of the HOST header is the same as the domain name. |`www.example.com` |
|RequestHeader |Object[] |Indicates the configuration of the Origin Request Headers feature. | |
|RequestHeaderAction |Object |Indicates a list of request header configuration rules. Each rule contains the relevant operation settings for a header. | |
|RequestHeaderInstances |Object[] |Indicates a list of request header configuration rules. Each rule contains the relevant operation settings for a header. | |
|Action |String |Indicates the operation on the request header. This parameter has the following values:<br><br><br>* `set`: Indicates setting a header. The setting operation includes adding and modifying. If the request already contains the header, the value of the header will be overwritten. If the request does not contain the header, the header will be added.<br><br>* `delete`: Indicates deleting a header. |`set` |
|Key |String |Indicates the name of a header, case\-insensitive. |`Cdn-provider` |
|ValueType |String |Indicates the value type of Key. This parameter is valid only when Action is set. This parameter has the following values:<br><br><br>* `constant`: Indicates that the value of `Key` is a fixed string.<br><br>* `variable`: Indicates that the value of `Key` comes from a variable.<br><br>* `customize`: Indicates that the value of `Key` is a string concatenated from a variable and a fixed string. |`constant` |
|Value |String |Indicates the value of Key. |`bp-cdn` |
|ResponseHeader |Object[] |Indicates the configuration of the Client Response Headers feature. | |
|ResponseHeaderAction |Object |Indicates the operation on the response header when the CDN responds to a user request. | |
|ResponseHeaderInstances |Object[] |Indicates a list of response header configuration rules. Each rule contains the relevant operation settings for a header. | |
|Action |String |Indicates the operation on the response header. This parameter has the following values:<br><br><br>* `set`: Indicates setting a header. The setting operation includes adding and modifying. If the origin response already contains the header, the value of the header will be overwritten. If the origin response does not contain the header, the header will be added.<br><br>* `delete`: Indicates deleting a header. |`set` |
|Key |String |Indicates the name of a header. |`Content-Disposition` |
|ValueType |String |Indicates the value type of `Key`. This parameter is valid only when Action is set. This parameter has the following values:<br><br><br>* `constant`: Indicates that the value of `Key` is a string.<br><br>* `variable`: Indicates that the value of `Key` comes from a variable.<br><br>* `customize`: Indicates that the value of `Key` is a string concatenated from a variable and a string. |`constant` |
|AccessOriginControl |Boolean |Indicates whether to verify the Origin header in the request when the CDN responds to a user request.<br><br>This parameter has the following values:<br><br><br>* `true`: Indicates that the CDN will verify the Origin header. If the verification is successful, the CDN will include the Access\-Control\-Allow\-Origin header in the response. The header value is the same as the Origin header value. If the verification fails, the response will not include the Access\-Control\-Allow\-Origin header.<br><br>* `false`: Indicates that the CDN will not verify the Origin header. In the response, the CDN will include the Access\-Control\-Allow\-Origin header. The header value is the set content of Access\-Control\-Allow\-Origin.<br><br><br>This parameter is valid only when the following conditions are met:<br><br><br>* `Action` is `set`.<br><br>* `Key` is `Access-Control-Allow-Origin`.<br><br>* `ValueType` is `constant`. |`true` |
|Value |String |Indicates the value of Key. |`attachment;filename=FileName.xls` |
|ServiceRegion |String |Indicates the service area of the domain name. This parameter has the following values:<br><br><br>* `chinese_mainland`: Represents Chinese Mainland.<br><br>* `global`: Represents Global.<br><br>* `outside_chinese_mainland`: Represents Global (excluding Chinese mainland). |`outside_chinese_mainland` |
|SignedUrlAuth |Object |Indicates the configuration of the Signed URL Authentication feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|SignedUrlAuthRules |Object[] |Indicates a list of rules. Each rule contains matching condition configuration and authentication configuration. | |
|Condition |Object |Indicates the configuration of matching conditions. CDN authenticates user requests that meet the conditions. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching type in the matching condition. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension at the end of the URL path.<br><br>* `directory`: Represents a directory in the URL path.<br><br>* `path`: Represents the complete URL path.<br><br>* `regex`: Represents the complete URL path, matched by regular expression. |`directory` |
|Operator |String |Indicates the matching method in the matching condition. This parameter has the following values:<br><br><br>* `match`: Indicates that if `object` matches `Value`, the request satisfies this matching condition.<br><br>* `not_match`: Indicates that if `object` does not match `Value`, the request satisfies this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates the matching value in the matching condition. |`png;jpg` |
|Connective |String |Indicates the logical relationship between multiple `ConditionRule`s. This parameter has the following values:<br><br><br>* `AND`: Represents the logical relationship is "AND".<br><br>* `OR`: Represents the logical relationship is "OR". |`OR` |
|SignedUrlAuthAction |Object |Indicates the configuration for signature calculation. | |
|Duration |Long |Indicates the validity period of the signature in seconds. This parameter is used in conjunction with the timestamp contained in the request to calculate the expiration time of the signature. The expiration time of the signature = timestamp + `Duration`. When the CDN receives a request, if the expiration time of the signature is earlier than the current time, the CDN determines that the signature has expired. |`1000` |
|MasterSecretKey |String |Indicates the primary key. |`abcdefg` |
|URLAuthType |String |Signature type. This parameter has the following values: `typea`, `typeb`, `typec`, `typed`, `typee`. For the authentication description of each type, see [Configure URL Authentication](https://docs.byteplus.com/en/docs/byteplus-cdn/docs-overview). |`typea` |
|BackupSecretKey |String |Indicates the backup key. |`abcdefg` |
|CustomVariableRules |Object |Indicates custom signature variables. | |
|CustomVariableInstances |Object[] |Indicates a list of variables. | |
|Operator |String |Indicates the matching method of the variable. The value of this parameter can only be `match`. |`match` |
|Type |String |Indicates the type of the variable. This parameter has the following values:<br><br><br>* `queryString`: Indicates that the variable is a query parameter in the request.<br><br>* `requestHeader`: Indicates that the variable is a header field in the request. |`queryString` |
|Value |String |Indicates the name of the variable. |`myparam1` |
|KeepOriginArg |Boolean |Indicates whether the CDN includes the signature parameters from the user request in the origin request.<br><br>This parameter has the following values:<br><br><br>* `true`: Indicates that the CDN includes the signature parameters in the origin request.<br><br>* `false`: Indicates that the CDN does not include the signature parameters in the origin request. |`true` |
|RewriteM3u8 |Boolean |For HLS Manifest (.m3u8) requests, this parameter indicates whether the CDN should modify the Manifest, thereby generating a signature for each video segment and adding the signature to the URI.<br><br>This parameter has the following values:<br><br><br>* `true`: Indicates that the Manifest needs to be modified.<br><br>* `false`: Indicates that the Manifest does not need to be modified. |`true` |
|SignName |String |Indicates the name of the signature parameter. |`sign` |
|SignatureRule |String[] |This parameter is valid when `URLAuthType` is `typee` and indicates the fields to be included in the signature calculation. The fields that must be included in the signature calculation are as follows:<br><br><br>* `key` : Indicates the key specified by `MasterSecretKey` or `BackupSecretKey`.<br><br>* `uri` : Indicates the URI of the user request, including only the path and query parameters.<br><br>* `TimeName` : Indicates the timestamp specified by `TimeFormat`.<br><br><br>The fields that can be optionally included in the signature calculation are as follows:<br><br><br>* `domain` : Indicates the domain name.<br><br>* `referer` : Indicates the referer value carried in the user request.<br><br>* `ua` : Indicates the User\-Agent value carried in the user request.<br><br>* `ip` : Indicates the client IP of the user request.<br><br>* `origin` : Indicates the Origin value carried in the user request.<br><br>* Custom variables: Indicates the value of the variables you defined in `CustomVariableInstances` .<br><br><br>CDN concatenates these fields into a string in the order of the fields in the list, and then calculates the MD5 value of the string. The MD5 value is the signature. |`["domain","ip","key","TimeName","uri"]` |
|TimeFormat |String |Specifies the time format used by `TimeName`. Valid values:<br><br><br>* `basicFormat2m`: Uses the `YYYYMMDDHHMM` format.<br><br>* `decimal`: Uses a decimal timestamp.<br><br>* `heximal`: Uses a hexadecimal timestamp. |`heximal` |
|TimeName |String |Indicates the name of the timestamp parameter. |`TimeParam` |
|RewriteM3u8Rule |Object |Indicates the configuration of the "M3U8 Modify" feature. | |
|DeleteParam |Boolean |Indicates whether to retain the original parameters in the URL when modifying the segment URL. This parameter has the following values:<br><br><br>* `true`: Indicates deleting the original parameters.<br><br>* `false`: Indicates retaining the original parameters.<br><br><br>Note that the setting of this parameter affects the calculation of the signature. |`true` |
|KeepM3u8Param |Boolean |Specifies whether to add the non\-signature query parameters from the M3U8 request URL to segment URLs.<br><br>Valid values:<br><br><br>* `true`: Adds the query parameters to segment URLs.<br><br>* `false`: Does not add the query parameters to segment URLs.<br><br><br>Note that this setting affects signature calculation. |`true` |
|RewriteTag |Object |Specifies the Tag Rewriting configuration. You can define tags other than `EXTINF`. | |
|Switch |Boolean |Specifies whether to rewrite segment URIs associated with additional tags.<br><br>Valid values:<br><br><br>* `true`: Rewrites URIs associated with additional tags.<br><br>* `false`: Does not rewrite URIs associated with additional tags. |`true` |
|Tags |String[] |Specifies a list of additional tags whose associated segment URIs need to be rewritten, in addition to the default tags. |`["EXT-X-MAP", "My-TAG"]` |
|AuthAlgorithm |String |Indicates the algorithm used for signature calculation. This configuration has the following values:<br><br><br>* `md5`: Represents the MD5 algorithm.<br><br>* `sha256`: Represents the SHA\-256 algorithm. |`md5` |
|DeleteAuthCacheAndOrigin |Boolean |Specifies whether CDN includes the signature parameter from the user request in origin requests and cache keys.<br><br>Valid values:<br><br><br>* `true`: The signature parameter is excluded from both origin requests and cache keys.<br><br>* `false`: The signature parameter is included in both origin requests and cache keys. |`true` |
|AuthRulesF |Object[] |Indicates the Type\-F configuration, which includes a list of rules. The list can contain a maximum of 5 rules. The first rule in the list has the highest priority.<br><br>When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|RuleName |String |Indicates the name of a rule in the rule list. |`Authentication rule A` |
|Condition |Object |Indicates the configuration of matching conditions. If a request meets the matching conditions, the CDN performs URL authentication on the request. | |
|ConditionRule |Object[] |Indicates a list of matching conditions. | |
|Object |String |Indicates the matching object. This parameter has the following values:<br><br><br>* `filetype`: Represents the extension of the requested file.<br><br>* `directory`: Represents a certain directory in the request path.<br><br>* `path`: Represents the complete path of the request, excluding the query string.<br><br>* `regex`: Represents a regular expression used to match the complete path. |`directory` |
|Operator |String |Indicates the matching operator. This parameter has the following values:<br><br><br>* `match`: Indicates that if `Value` matches `Object` in the request, the request meets this matching condition.<br><br>* `not_match`: Indicates that if `Value` does not match `Object` in the request, the request meets this matching condition. |`match` |
|Type |String |The value of this parameter can only be `url`, which represents the request URL. |`url` |
|Value |String |Indicates one or more matching values. Multiple matching values are separated by a semicolon (;). |`/chs/foods/;/us/birds/` |
|Connective |String |Indicates the relationship between matching conditions. This parameter has the following values:<br><br><br>* `OR`: Represents the relationship is "or".<br><br>* `AND`: Represents the relationship is "and". |`OR` |
|SecretKey |Object |Indicates the key used to calculate the token. It includes a primary key and a backup key. | |
|MasterSecretKey |String |Indicates the primary key. |`primary-key-123` |
|BackupSecretKey |String |Indicates the backup key. |`secondary-key-456` |
|SignCapRule |Object |Indicates the method of obtaining the token from the user request. | |
|ArgSegment |Object |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a certain level. This segment is the token to be obtained. | |
|Switch |Boolean |Indicates whether the obtained content needs to be split. This parameter has the following values:<br><br><br>* `true`: Indicates that the content needs to be split.<br><br>* `false`: Indicates that the content does not need to be split. |`true` |
|Level |Long |Indicates the level where the token is located after the content is split into multiple segments.<br><br>If the level is a negative integer, it means counting from the rightmost segment to the left. |`2` |
|SplitSymbol |String |Indicates the delimiter used to split the content. |`//` |
|CapMode |String |Indicates the source of the token. This parameter has the following values:<br><br><br>* `name`: Represents a query parameter. The relevant configuration is specified in `ParamName`.<br><br>* `uri`: Represents a directory in the request path. The relevant configuration is specified in `UriLevel`.<br><br>* `header`: Represents a header in the request. The relevant configuration is specified in `CustomValue`.<br><br>* `cookie`: Represents a cookie in the request. The relevant configuration is specified in `CustomValue`. |`name` |
|CustomValue |String |The meaning of this parameter is as follows:<br><br><br>* When `CapMode` is `header`, this parameter represents the specified request header.<br><br>* When `CapMode` is `cookie`, this parameter represents the key of the specified cookie, and CDN will obtain the value of this cookie. |`myheader` |
|ParamName |String |When `CapMode` is `name`, this parameter represents the query parameter to be specified. |`myparam` |
|UriLevel |Long |When `CapMode` is `uri`, this parameter represents the specified directory level.<br><br>If the level is a negative integer, it means counting from the rightmost directory in the path to the left. |`3` |
|ExpireTimeRule |Object |Indicates the settings related to the token expiration time. | |
|Duration |Long |Indicates the valid duration (TTL) of the token, in seconds.<br><br><br>* Token expiration time = Token timestamp obtained based on `ExpTimeCapRule` + `Duration` |`20` |
|ExpTimeCapRule |Object |Indicates the method of obtaining the token timestamp. The token timestamp is a Unix timestamp. | |
|CapMode |String |Indicates the source of the token timestamp. This parameter has the following values:<br><br><br>* `name`: Represents a query parameter. The relevant configuration is specified in `ParamName` and `ArgSegment`.<br><br>* `uri`: Represents a directory in the request path. The relevant configuration is specified in `UriLevel` and `ArgSegment`.<br><br>* `header`: Represents a header in the request. The relevant configuration is specified in `CustomValue`.<br><br>* `cookie`: Represents a cookie in the request. The relevant configuration is specified in `CustomValue`. |`header` |
|ParamName |String |When `ParamType` is `ReqHeader`, this parameter represents the specified query parameter. |`myparm1` |
|UriLevel |Long |When `ParamType` is `uri`, this parameter represents the specified directory level.<br><br>If the level is a negative integer, it means counting from the rightmost directory in the path to the left. |`2` |
|ArgSegment |Object |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a certain level. This segment is the token timestamp to be obtained. | |
|Switch |Boolean |Indicates whether the obtained content needs to be split. This parameter has the following values:<br><br><br>* `true`: Indicates that the content needs to be split.<br><br>* `false`: Indicates that the content does not need to be split. |`true` |
|Level |Long |Indicates the level where the token timestamp is located after the content is split into multiple segments.<br><br>If the level is a negative integer, it means counting from the rightmost segment to the left. |`2` |
|SplitSymbol |String |Indicates the delimiter used to split the content. |`-` |
|CustomValue |String |The meaning of this parameter is as follows:<br><br><br>* When `CapMode` is `header`, this parameter represents the specified request header.<br><br>* When `CapMode` is `cookie`, this parameter represents the key of the specified cookie, and CDN will obtain the value of this cookie. |`myheader1` |
|TimeFormat |String |Indicates the format of the token timestamp.<br><br><br>* `octal`: Indicates octal format. For example: `14751410031`.<br><br>* `decimal`: Indicates decimal format. For example: `1738936345`.<br><br>* `heximal`: Indicates hexadecimal format. For example: `67a61019`. |`heximal` |
|AuthTokenCalRule |Object |Indicates the settings for token calculation.<br><br>CDN uses `SignJoinSymbol` to concatenate the objects in `SignParam`, and then applies the algorithm specified in `ParamCalRules` to the concatenated object to calculate the token, which is used for comparison with the token contained in the user request. | |
|ParamCalRules |String[] |Indicates the list of algorithms used to calculate the token. CDN generates the calculation formula for the token in the order of the algorithms in the list.<br><br>This parameter has the following values: `md5_bin`, `base64url`, `sha256`, `md5`, `base64_encode`, `sha1`, `sha224`, `sha384`, `sha512`, `sha3_224`, `sha3_256`, `sha3_384`, `sha3_512`, `upper_case`, `lower_case`. |`["sha1"、"md5_bin"、"base64url"]` |
|SignJoinSymbol |String |Indicates the delimiter used to concatenate the objects in `SignParam`. |`00` |
|SignParam |Object[] |Indicates the list of objects used by CDN when calculating the token. Each object consists of `ParamType` and related configurations. For example, the following example shows that the object is a string with the value `str-for-token-calc`.<br><br>```json```<br>```{```<br>```    "ParamType": "SupString",```<br>```    "SupContent": "str-for-token-calc"```<br>```}```<br> | |
|ParamType |String |Indicates the type of the object. This parameter has the following values:<br><br><br>* `SecretKey`: Represents `MasterSecretKey` or `BackupSecretKey` in the `SecretKey` structure. When authentication fails, CDN will use `BackupSecretKey` to calculate the token and re\-authenticate the user request.<br><br>* `SupString`: Represents a string. The relevant configuration is specified in `SupContent`.<br><br>* `URI`: Represents a continuous segment in the request path. The path does not include a query string. The relevant configuration is specified in `UriParamSup` and `ParamSource`.<br><br>* `URLParam`: Represents a certain type of object in the request URL. The object can be a query parameter or a directory. The relevant configuration is specified in `UriParam` and `ParamSource`.<br><br>* `ClientDomain`: Represents the request domain name.<br><br>* `Referer`: Represents the value of the Referer header in the user request.<br><br>* `Origin`: Represents the value of the Origin header in the user request.<br><br>* `ClientIP`: Represents the client IP address that sent the user request.<br><br>* `UA`: Represents the value of the User\-Agent header in the user request.<br><br>* `ReqHeader`: Represents the value of a certain header in the user request. The relevant configuration is specified in `RequestHeader`.<br><br>* `Cookie`: Represents a cookie in the request. The relevant configuration is specified in `CookieToken`.<br><br>* `FullURI`: Represents the complete path of the request, without the query string. The relevant configuration is specified in `ParamSource`. |`URI` |
|CookieToken |String |When `ParamType` is `Cookie`, this parameter represents the key of the specified cookie. CDN will obtain the value of this cookie. |`mycookiekey` |
|RequestHeader |String |When `ParamType` is `ReqHeader`, this parameter represents the specified request header. |`myheader2` |
|SupContent |String |When `ParamType` is `SupString`, this parameter represents the specified string. |`123abc` |
|UriParamSup |Object |Indicates the method of obtaining a continuous segment from the request path.<br><br>This parameter is a structure containing the following configurations:<br><br><br>* The delimiter used to split the request path.<br><br>* The start and end levels of the required continuous path segment.<br><br>* The delimiter used to concatenate these path segments. The concatenated path segment is used to calculate the token. | |
|SplitSymbol |String |Indicates the delimiter used to split the request path. |`-` |
|StartLevel |Long |Indicates the level where the starting segment is located. |`2` |
|TermLevel |Long |Indicates the level where the ending segment is located.<br><br>If `TermLevel` is a negative integer, it means counting from the rightmost segment to the left. |`3` |
|JoinSymbol |String |Indicates the delimiter used to concatenate these path segments. |`00` |
|UrlParam |Object |Indicates the method of obtaining the required object from the URL.<br><br>This parameter is a structure containing the source of the object and related configurations. | |
|CapMode |String |Indicates the source of the object. This parameter has the following values:<br><br><br>* `name`: Represents a query parameter. The relevant configuration is specified in `ParamName` and `ArgSegment`.<br><br>* `uri`: Represents a specified directory in the request path. The relevant configuration is specified in `UriLevel` and `ArgSegment`. |`uri` |
|ParamName |String |When `ParamType` is `name`, this parameter represents the specified query parameter. |`myparam3` |
|UriLevel |Long |When `ParamType` is `uri`, this parameter represents the specified directory level.<br><br>If the level is a negative integer, it means counting from the rightmost directory in the path to the left. |`2` |
|ArgSegment |Object |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a certain level. This segment is the object to be obtained. | |
|Switch |Boolean |Indicates whether the obtained content needs to be split. This parameter has the following values:<br><br><br>* `true`: Indicates that the content needs to be split.<br><br>* `false`: Indicates that the content does not need to be split. |`true` |
|Level |Long |Indicates the level where the required object is located after the obtained content is split into multiple segments.<br><br>If the level is a negative integer, it means counting from the rightmost segment to the left. |`2` |
|SplitSymbol |String |Indicates the delimiter used to split the content. |`-` |
|ParamSource |String |For tokens added to the Manifest, this parameter indicates the source of the object when CDN uses this object to calculate the token.<br><br>This parameter has the following values:<br><br><br>* `ParentLink`: Indicates that the object comes from the URL in the user request.<br><br>* `ChildLink`: Indicates that the object comes from the URI of the video segment in the Manifest. |`ParentLink` |
|RewriteM3U8 |Object |Indicates the configuration of HLS Manifest modification, that is, configuring how to add tokens to the video segment URIs in the Manifest. | |
|Switch |Boolean |Indicates whether to modify the HLS Manifest. This parameter has the following values:<br><br><br>* `true`: Indicates that the Manifest needs to be modified.<br><br>* `false`: Indicates that the Manifest does not need to be modified.<br><br><br>By default, CDN only adds tokens to the video segment URIs under the `EXTINF` tag in the Manifest. |`true` |
|RewriteM3U8Tag |Object |Indicates additional tags. For tags included in `Tags`, CDN will add tokens to the URLs under these tags. See [Example of this setting](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#example-of-applying-url-signing-to-extra-tags). | |
|Switch |Boolean |Indicates whether to set additional tags. This parameter has the following values:<br><br><br>* `true`: Indicates that additional tags need to be set.<br><br>* `false`: Indicates that additional tags do not need to be set. |`true` |
|Tags |String[] |Indicates a list of additional tags. |`["tag1","tag2","tag3"]` |
|RewriteMPD |Object |Indicates the configuration of DASH Manifest modification, that is, configuring how to add tokens to the video segment URIs in the Manifest. | |
|Switch |Boolean |Indicates whether to modify the DASH Manifest. This parameter has the following values:<br><br><br>* `true`: Indicates that the Manifest needs to be modified.<br><br>* `false`: Indicates that the Manifest does not need to be modified. |`true` |
|MpdVarExpand |Boolean |Indicates whether to replace the variables in the URI under `SegmentTemplate` with actual values. This parameter has the following values:<br><br><br>* `true`: Enables this configuration. After this configuration is enabled, CDN will first replace the variables in the video segment URI with actual values, then generate a token based on the URI containing the actual values, and finally add the token to the URI.<br><br>* `false`: Does not enable this configuration. The variable name itself will be used as a fixed string to generate the token.<br><br><br>After this configuration is enabled, only variables that meet all the following conditions will be replaced with actual values:<br><br><br>* The variable is `$RepresentationID$`.<br><br>* There is at least one URI under `SegmentTemplate` that meets the following conditions:<br><br>   * In this URI, at least one `$RepresentationID$` does not appear as the last segment of the URI path.<br><br>* There can be no other content between `<SegmentTemplate ... />` and `<Representation .../>`.<br><br><br>In addition, in the modified DASH Manifest, the original `SegmentTemplate` will be retained.<br><br>See [Example](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#template-parameter-substitution-examples). |`true` |
|CustomRewrite |Object |Indicates the extended modify configuration for the video Manifest. After this configuration is enabled, CDN uses [special modify logic](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#custom-url-signing-logic-for-video-manifests) to override the [default modify logic](https://docs.byteplus.com/en/docs/byteplus-cdn/typef_en-us#default-url-signing-logic-for-video-manifests). | |
|Switch |Boolean |Indicates whether to enable the extended modify configuration. This parameter has the following values:<br><br><br>* `true`: Indicates that the extended modify configuration is enabled.<br><br>* `false`: Indicates that the extended modify configuration is not enabled. |`true` |
|RewriteParam |Object[] |Indicates a list of objects. CDN concatenates these objects to generate a token and adds it to the URL of the video segment. | |
|ParamType |String |Indicates the type of the object. This parameter has the following values:<br><br><br>* `ParentLinkUrlParam`: Represents a certain type of object in the user request URL. The object can be a query parameter or a path directory at a certain level. The relevant configuration is specified in the `ParentLinkUrlParam` structure.<br><br>* `SupString`: Represents a string. The relevant configuration is specified in `SupContent`.<br><br>* `ParentLinkURI`: Represents a continuous segment in the user request path. The path does not include a query string. The relevant configuration is specified in `ParentLinkUriParamSup`.<br><br>* `ParentLinkExpire`: Represents the timestamp of the token in the user request. See the description of the `Duration` parameter under `ExpireTimeRule`.<br><br>* `AuthToken`: Represents the token calculated based on `AuthTokenCalRule`.<br><br>* `ParentFullURI`: Represents the complete path of the user request, without the query string. |`ParentLinkURI` |
|SupContent |String |When `ParamType` is `SupString`, this parameter represents the specified string. |`abc-13343` |
|ParentLinkUriParamSup |Object |Indicates the method of obtaining an object from the user request path.<br><br>This parameter is a structure containing the following configurations:<br><br><br>* The delimiter used to split the request path.<br><br>* The start and end levels of the continuous path segment.<br><br>* The delimiter used to concatenate these path segments. The concatenated path segment is used to generate the token. | |
|SplitSymbol |String |Indicates the delimiter used to split the request path, which is required to be the same as `JoinSymbol`. |`-` |
|StartLevel |Long |Indicates the level where the starting segment is located. |`1` |
|TermLevel |Long |Indicates the level where the ending segment is located, with the following requirements:<br><br><br>* It can only be a non\-zero integer.<br><br>* The absolute value cannot be greater than the total number of levels.<br><br><br>If `TermLevel` is a negative integer, it means counting from the rightmost segment to the left. |`3` |
|JoinSymbol |String |Indicates the delimiter used to concatenate these path segments. |`00` |
|ParentLinkUrlParam |Object |Indicates the method of obtaining an object from the URL.<br><br>This parameter is a structure containing the source of the object and related configurations. | |
|CapMode |String |Indicates the source of the object. This parameter has the following values:<br><br><br>* `name`: Represents a query parameter. The relevant configuration is specified in `ParamName` and `ArgSegment`.<br><br>* `uri`: Represents a specified directory in the request path. The relevant configuration is specified in `UriLevel` and `ArgSegment`. |`name` |
|ParamName |String |When `CapMode` is `name`, this parameter represents the specified query parameter. |`myparam5` |
|UriLevel |Long |When `CapMode` is `uri`, this parameter represents the specified directory level.<br><br>If the level is a negative integer, it means counting from the rightmost directory in the path to the left. |`4` |
|ArgSegment |Object |Indicates whether the content obtained based on `ParamName` or `UriLevel` needs to be split to extract a segment at a certain level. This segment is the object to be obtained. | |
|Switch |Boolean |Indicates whether the obtained content needs to be split. This parameter has the following values:<br><br><br>* `true`: Indicates that the content needs to be split.<br><br>* `false`: Indicates that the content does not need to be split. |`true` |
|Level |Long |Indicates the level where the required segment is located after the obtained content is split into multiple segments.<br><br>If the level is a negative integer, it means counting from the rightmost segment to the left. |`2` |
|SplitSymbol |String |Indicates the delimiter used to split the content. |`-` |
|RewriteRule |Object |Indicates the method by which CDN adds a token to the video segment URI. | |
|CapMode |String |Indicates how CDN adds the generated token to the video segment URI. This parameter has the following values:<br><br><br>* `name`: Indicates that the specified query parameter in the URI is set to the token. The relevant configuration is specified in `ParamName`.<br><br>* `uri`: Indicates that a directory is inserted at the specified directory level in the URI, and this directory is set to the token. The relevant configuration is specified in `UriLevel`. |`name` |
|ParamName |String |When `CapMode` is `name`, it represents the specified query parameter. |`myparam4` |
|UriLevel |Long |When `CapMode` is `uri`, it represents the specified directory level.<br><br>If the level is a negative integer, it means counting from the rightmost directory to the left. |`2` |
|SignJoinSymbol |String |Indicates the delimiter used to concatenate the objects in `RewriteParam`. |`00` |
|ArgumentRule |Object |Indicates the configuration related to origin request parameters. | |
|KeepOriginArg |Boolean |Indicates whether to include the token calculated based on `AuthTokenCalRule` in the origin request. This parameter has the following values:<br><br><br>* `true`: Indicates that the token is included in the origin request. The position of the token in the origin request is the same as the setting in `SignCapRule`.<br><br>* `false`: Indicates that the token is not included in the origin request. |`true` |
|GeneralParamRule |Object |Indicates the method by which CDN sets the query parameters in the video segment URI. | |
|ParentLinkParamInherit |String |Indicates whether the modified video segment URI includes all query parameters from the user request URL except for the parameters representing the token and token timestamp. This parameter has the following values:<br><br><br>* `not_inherit`: Indicates that the modified segment URI will not include these query parameters.<br><br>* `inherit`: Indicates that the modified segment URI will include these query parameters. |`not_inherit` |
|SubLinkParamRule |Object |This structure contains additional query parameter settings. This structure contains additional query parameter settings. | |
|InheritMode |String |Indicates how CDN sets the value of a query parameter in the video segment URI when the same query parameter exists in both the video segment URI and the user request URL.<br><br>This parameter has the following values:<br><br><br>* `sub_link_first`: Indicates that the value of the parameter in the video segment URI is used.<br><br>* `inherit_first`: Indicates that the value of the parameter in the user request URL is used. |`inherit_first` |
|KeepSubLinkArg |String |Indicates whether the modified video segment URI retains the original query parameters in the URI. This parameter has the following values:<br><br><br>* `delete`: Indicates that the modified segment URI will not retain these query parameters.<br><br>* `keep`: Indicates that the modified segment URI will retain these query parameters. |`delete` |
|RewriteFormat |String |Indicates the format of the modified video segment URI. This parameter has the following values:<br><br><br>* `default`: The meaning of this parameter value is the same as `absolute`.<br><br>* `relative`: Keeps the current format of the URI.<br><br>* `absolute`: If the format of the URI is a relative path, CDN converts the format to an absolute path. If the URI is an absolute path or a full URL, the current format is kept.<br><br>* `full`: If the format of the URI is an absolute path or a relative path, CDN converts the format to a full URL. |`default` |
|Timeout |Object |Indicates the configuration of the Origin Fetch Timeouts feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. In this case, the timeout for TCP requests and HTTP requests uses the default values, which are 2 seconds and 60 seconds, respectively. |`true` |
|TimeoutRules |Object[] |Indicates a set of timeout configurations. | |
|TimeoutAction |Object |Indicates the timeout configuration. | |
|HttpTimeout |Long |Indicates the maximum time, in seconds, that a CDN point of presence (POP) waits for subsequent response body data after receiving the first byte from the origin server. |`60` |
|TcpTimeout |Long |Indicates the maximum time, in seconds, that a CDN POP waits to establish a TCP connection with the origin server. |`2` |
|HttpFirstByteTimeout |Long |Indicates the maximum time, in seconds, that a CDN POP waits for the first byte of the response after sending an HTTP request to the origin server. |`90` |
|UaAccessRule |Object |Indicates the configuration for the UA Restrictions feature. | |
|AllowEmpty |Boolean |Indicates whether requests with an empty User\-Agent header ("") or without a User\-Agent header are allowed. This parameter has the following values:<br><br><br>* `true`: Indicates allowed.<br><br>* `false`: Indicates not allowed. If the User\-Agent header of the request is empty ("") or does not contain a User\-Agent header, BytePlus CDN rejects the request. |`true` |
|IgnoreCase |Boolean |Indicates whether the UA string is case\-sensitive. This parameter has the following values:<br><br><br>* `true`: The UA string is case\-insensitive.<br><br>* `false`: The UA string is case\-sensitive. |`true` |
|RuleType |String |Indicates the type of the UA list. This parameter is required when `Switch` is `true`. This parameter has the following values:<br><br><br>* `allow`: Allowlist.<br><br>* `deny`: Blocklist. |`deny` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Enable this feature.<br><br>* `false`: Disable this feature. |`true` |
|UserAgent |String[] |Indicates a list of UAs. The description of this parameter is as follows:<br><br><br>* If `RuleType` is `allow`, only requests containing UAs in the list are allowed to access the domain.<br><br>* If `RuleType` is `deny`, requests containing UAs in the list are not allowed to access the domain.<br><br><br>The `*` in the UA represents one or more characters. |`["*curl*","*Mozilla*"]` |
|VideoDrag |Object |Indicates the configuration for the Video Seeking feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Enable this feature.<br><br>* `false`: Disable this feature. |`true` |
|OriginIPv6 |String |Indicates the configuration of the IPv6 Origin Fetch feature. The parameter can have the following values:<br><br><br>* `ipv6_first` : CDN always attempts to retrieve the IPv6 address of the origin domain. If the IPv6 address cannot be retrieved, CDN then attempts to retrieve the IPv4 address.<br><br>* `ipv4_first` : CDN always attempts to retrieve the IPv4 address of the origin domain. If the IPv4 address cannot be retrieved, CDN then attempts to retrieve the IPv6 address.<br><br>* `followclient` : CDN attempts to retrieve an IP address of the same type as the user request.<br><br>   The default value for this parameter is followclient .<br><br><br>Since some CDN regional nodes outside of Chinese Mainland do not support sending origin requests to IPv6 addresses, this feature is only available for regional nodes within Chinese Mainland. |`followclient` |
|UrlNormalize |Object |Indicates the configuration for the URL Normalization feature. | |
|NormalizeObject |String[] |Indicates a list of URL normalization options. This parameter is required when `Switch` is `true`. The list can contain the following options:<br><br><br>* `dot_segments`: Replaces the following in the request URL:<br><br>   * `/./`: Replaced with a single slash (/).<br><br>   * `/../`: If there is a directory level before `/../`, both `/../` and the directory are removed. If there is no directory before `/../`, the original URL is retained.<br><br>* `back_slashes`: Replaces backslashes () in the request URL with a single slash (/).<br><br>* `successive_slashes`: Replaces consecutive slashes (//) in the request URL with a single slash (/). |`["dot_segments","back_slashes","successive_slashes"]` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Enable this feature.<br><br>* `false`: Disable this feature. |`true` |
|RequestBlockRule |Object |Indicates the configuration for the Custom Restrictions feature. | |
|BlockRule |Object[] |Indicates a list of rules. The first rule in the list has the highest priority.<br><br>When a user request is received, CDN matches the request with rules in order of priority, from highest to lowest. If a rule matches the request, CDN stops processing the remaining rules. | |
|BlockAction |Object |Indicates the configuration of CDN behavior in a rule. | |
|Action |String |Indicates how CDN handles requests that match `Condition`. This parameter has the following values:<br><br><br>* `refuse`: CDN rejects the request and responds with a 4xx error code specified in `StatusCode`.<br><br>* `redirect`: CDN redirects the request to the URL specified in `RedirectUrl`. |`refuse` |
|StatusCode |String |Indicates the response status code for user requests that match `Condition`.<br><br><br>* When `Action` is `refuse`, this parameter represents an error code in the range of 400\-499.<br><br>* When `Action` is `redirect`, this parameter has the following values:<br><br>   * `301`: The response status code is 301.<br><br>   * `302`: The response status code is 302. |`403` |
|ErrorPage |String |* When `Action` is `refuse`, this parameter is optional, as described below:<br><br>   * If specified, this parameter represents the name of a custom response page in the "Universal Catalog" feature. That is, when CDN rejects a request, it returns this custom page.<br><br>   * If not specified, CDN uses the standard response body for the error code specified in `StatusCode`. |`GlobalConfigName` |
|RedirectUrl |String |* When `Action` is `redirect`, it represents the redirect URL.<br><br>* When `Action` is `refuse`, this parameter is invalid. |`http://www.example.com` |
|Condition |Object |Indicates the definition of matching conditions in this rule. | |
|ConditionRule |Object[] |Indicates a list of matching conditions used to match the path and query parameters in the request URL, as well as the client IP address from which the request originates. Each matching condition includes a match type, a comparison type, and a match value. | |
|Object |String |Indicates a match type.<br><br><br>* When `Type` is `url`, this parameter has the following values:<br><br>   * `path`: Represents the path in the request URL.<br><br>   * `directory`: Represents a directory in the path.<br><br>   * `filetype`: Represents the extension at the end of the path.<br><br>   * `regex`: Represents the path in the request URL, matched by a regular expression.<br><br>* When `Type` is `querystring`, this parameter has the following values:<br><br>   * `query_name`: Represents a query parameter in the request URL.<br><br>   * `full_querystring`: Represents the query string in the request URL.<br><br>* When `Type` is `client_ip`, this parameter has the following values:<br><br>   * `client_ip`: Represents the client's IP address.<br><br>* When `Type` is `request_header`, this parameter has the following values:<br><br>   * `ua`: Represents the User\-Agent header in the request.<br><br>   * `customize`: Represents a custom header in the request. |`filetype` |
|Operator |String |Indicates a comparison type.<br><br><br>* When `Object` is `path`, `directory`, or `filetype`, this parameter has the following values:<br><br>   * `equal`: If any value in `Value` is matched, the request meets this matching condition.<br><br>   * `not_equal`: Only if all values in `Value` are not matched, the request meets this matching condition.<br><br>* When `Object` is `query_name`, this parameter has the following values:<br><br>   * `exist`: Exists. The matching logic is the same as `equal`.<br><br>   * `not_exist`: Does not exist. The matching logic is the same as `not_equal`.<br><br>   * `belong_shared_config`: If any value contained in the universal catalog represented by `Value` is matched, the request meets this matching condition.<br><br>   * `not_belong_shared_config`: Only if all values in the universal catalog represented by `Value` are not matched, the request meets this matching condition.<br><br>   * `empty`: The value is empty.<br><br>   * `not_empty`: The value is not empty.<br><br>   * `equal`: See the description above.<br><br>   * `not_equal`: See the description above.<br><br>* When `Object` is `regex`, `full_querystring`, `client_ip`, or `ua`, this parameter has the following values:<br><br>   * `match`: The description is the same as `equal`.<br><br>   * `not_match`: The description is the same as `not_equal`.<br><br>* When `Object` is `ua` or `customize`, this parameter also has the following **additional** values:<br><br>   * `empty`: See the description above.<br><br>   * `not_empty`: See the description above. |`not_equal` |
|Type |String |Indicates the type of a matching object. This parameter has the following values:<br><br><br>* `url`: Represents the request URL.<br><br>* `querystring`: Represents the query string in the request URL.<br><br>* `request_header`: Represents a header in the request. |`url` |
|Value |String |Indicates one or more match values.<br><br><br>* If `Type` is `request_header`, multiple match values are separated by a vertical bar (\|).<br><br>* If `Type` is not `request_header`, multiple match values are separated by a semicolon (;). |`png;txt` |
|Name |String |This parameter is valid when `Object` is `query_name` or `customize`.<br><br><br>* If `Object` is `query_name`, this parameter represents the name of a query parameter.<br><br>* If `Object` is `customize`, this parameter represents the name of a custom request header. |`color` |
|Connective |String |Indicates the relationship between multiple `ConditionRule`s. This parameter has the following values:<br><br><br>* `AND`: Represents "and".<br><br>* `OR`: Represents "or". |`AND` |
|RuleName |String |Indicates the name of the rule. |`MyRule` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Enable this feature.<br><br>* `false`: Disable this feature. |`true` |
|OriginCertCheck |Object |Indicates the configuration for the Origin Certificate Validation feature.<br><br>After this feature is enabled, CDN validates the legitimacy of the origin certificate, including whether the certificate has been revoked, whether it is issued by a trusted CA, and whether it matches the origin domain. CDN has built\-in root certificates of common trusted CAs. If the origin certificate fails validation, CDN performs an [origin retry](https://docs.byteplus.com/en/docs/byteplus-cdn/origin_retry-en). If the origin certificate still fails validation during the retry, CDN determines that it cannot fetch the file from this origin and responds to the user request with a 504 status code. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Enable this feature.<br><br>* `false`: Disable this feature. |`true` |
|CertInfoList |Object[] |Indicates a list of CA certificates. CDN uses the CA certificates in this list to verify the server certificate from the origin. | |
|CertId |String |Indicates the ID of a CA certificate in the list, starting with `cert_hosting`. |`cert_hosting-104663` |
|ConditionalOrigin |Object |Indicates the configuration of the Conditional Origins feature. | |
|OriginRules |Object[] |Indicates a list of rules. Each rule in the list defines a set of matching conditions and the actions that CDN performs on requests that meet the matching conditions.<br><br>When a user request is received, CDN matches the rules with the request from high to low priority. If a rule matches the request, CDN stops processing the remaining rules. | |
|Actions |Object |Indicates the action configuration defined in a rule. | |
|OriginLines |Object[] |Indicates a list of origin servers. | |
|Address |String |Indicates the address of an origin server.<br><br><br>* When `InstanceType` is `ip`, `Address` indicates an IPv4 or IPv6 address.<br><br>* When `InstanceType` is `domain`, `Address` indicates a domain name.<br><br>* When `InstanceType` is `storage`, `Address` indicates the bucket domain name, which can be the bucket domain name assigned by the cloud vendor or the custom domain name you set for the bucket in the cloud vendor. |`203.0.113.8` |
|HttpPort |String |Indicates the port that CDN uses to access the origin server using the HTTP protocol. |`80` |
|HttpsPort |String |Indicates the port that CDN uses to access the origin server using the HTTPS protocol. |`443` |
|InstanceType |String |Indicates the type of the origin server. This parameter has the following values:<br><br><br>* `ip`: Indicates an IP address.<br><br>* `domain`: Indicates a domain name.<br><br>* `storage`: Indicates an object storage bucket. |`ip` |
|OriginHost |String |Indicates the site domain name accessed by the origin request, which is applicable to the case where there are multiple sites on the origin server.<br><br>This parameter has a higher priority than the global `OriginHost` parameter. |`img.example.com` |
|BucketSource |String |Indicates which object storage service's authentication method is used by the bucket. This parameter has the following values:<br><br><br>* `tos`: Indicates BytePlus TOS.<br><br>* `cos`: Indicates Tencent Cloud COS.<br><br>* `oss`: Indicates Alibaba Cloud OSS.<br><br>* `azure`: Indicates Microsoft Azure.<br><br>* `aws_common`: Indicates AWS S3 or other third\-party object storage services that use S3\-compatible authentication methods. |`aws_common` |
|PrivateBucketAccess |Boolean |Specifies whether the bucket is private. This parameter is valid only when `InstanceType` is `storage`. Valid values:<br><br><br>* `true`: The bucket is private.<br><br>* `false`: The bucket is not private. |`true` |
|TosAuthInformation |Object |Specifies the access credential (AccessKey) for the bucket. | |
|AccessKeyId |String |Indicates the AccessKey ID in the access credential, which is called SecretId in Tencent Cloud. |`xxxxxxxxxxxxxxxxxx` |
|AccessKeySecret |String |Indicates the AccessKey Secret in the access credential, which is called SecretKey in Tencent Cloud. |`xxxxxxxxxxxx` |
|Region |String |Indicates the region information of the bucket, that is, the region code of the bucket. The region code participates in the calculation of the signature. |`us-east-1` |
|AccountName |String |Indicates your Azure storage account's shared key. This parameter is only valid when `BucketSource` is `azure`. |`xxxxxxxxxxxxxxxxxxxxx` |
|OriginType |String |Indicates the role of this origin. This parameter has the following values:<br><br><br>* `primary`: indicates primary origin.<br><br>* `backup`: indicates secondary origin. |`primary` |
|Weight |String |Indicates the weight of the origin. Valid values range from 1 to 100, and the default value is 1. An origin with a higher weight is more likely to be selected when CDN sends an origin request. |`1` |
|Condition |Object |Indicates the configuration of the matching conditions in the rule. | |
|ConditionGroups |Object[] |Indicates a list of matching conditions. | |
|Condition |Object |Indicates the configuration of a matching condition. | |
|Object |String |Indicates a matching object. This parameter has the following values:<br><br><br>* `path`: Indicates the full path in the request URL.<br><br>* `directory`: Indicates a directory in the request URL.<br><br>* `filetype`: Indicates the extension in the request URL.<br><br>* `full_querystring`: Indicates all query parameters in the request URL.<br><br>* `client_ip`: Indicates the client's IP address.<br><br>* `query_name`: Indicates a query parameter in the request URL.<br><br>* `customize`: Indicates a header in the user request. |`path` |
|Operator |String |Indicates the matching type. |`equal` |
|Value |String[] |Indicates one or more matching values. |`/www/img/my*image.png;/doc` |
|Name |String |* When `Object` is `query_name`, this parameter indicates the name of the specified query parameter.<br><br>* When `Object` is `customize`, this parameter indicates the name of the specified request header.<br><br>* When `Object` is other values, this parameter is invalid. |`param` |
|Type |String |* When `Object` is `query_name`, the value of this parameter must be `querystring`.<br><br>* When `Object` is `customize`, the value of this parameter must be `request_header`.<br><br>* When `Object` is other values, this parameter is invalid. |`querystring` |
|Connective |String |Indicates the relationship between these matching conditions. This parameter has the following values:<br><br><br>* `or`: Indicates that the relationship is "or".<br><br>* `and`: Indicates that the relationship is "and". |`and` |
|IsGroup |Boolean |The value of this parameter is `true`. |`true` |
|Switch |Boolean |Indicates whether the feature is enabled. This parameter has the following values:<br><br><br>* `true`: Indicates that the feature is enabled.<br><br>* `false`: Indicates that the feature is not enabled. |`true` |
|OriginRetry |Object |Indicates the configuration of the Origin Retry feature. | |
|StatusCode |String |Indicates one or more HTTP status codes between 400 and 599, inclusive. |`404;408;5xx` |
|Switch |Boolean |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature. |`false` |
|Websocket |Object |Indicates WebSocket configuration. | |
|Switch |Boolean |Indicates whether to enable WebSocket support for user requests. This parameter has the following values:<br><br><br>* `true`: Indicates that WebSocket is enabled. After this configuration is enabled, CDN can respond to Websocket requests from clients.<br><br>* `false`: Indicates that WebSocket is disabled. |`true` |
|Timeout |Long |Indicates the timeout time of the WebSocket connection, in seconds. |`60` |
|MultiRange |Object |Indicates the configuration of the Multi Range feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled. After this feature is enabled, CDN allows Range requests with multiple ranges specified.<br><br>* `false`: Indicates that this feature is not enabled. If a Range request with multiple ranges specified is received, CDN will reject the request and return a 416 response status code. |`true` |
|OfflineCache |Object |Indicates the configuration for the Serve Stale feature. | |
|Object |String |Indicates the trigger condition for this feature. The parameter can have the following values:<br><br><br>* `request_error`: Indicates an origin request error. When an origin request error occurs, CDN does not receive any response from the origin.<br><br>* `error_code`: Indicates that the response status code from the origin is 5xx.<br><br>* `request_error,error_code`: Indicates that both of the above conditions are included. |`request_error,error_code` |
|StatusCode |String |Indicates one or more response status codes, ranging from 500 to 599. Multiple status codes are separated by semicolons (;). `5xx` represents any status code starting with the number 5.<br><br>This parameter is valid only when `Object` is `error_code` or `request_error,error_code`. |`504;505` |
|Switch |Boolean |Indicates whether this feature is enabled. This parameter has the following values:<br><br><br>* `true`: Indicates that this feature is enabled.<br><br>* `false`: Indicates that this feature is disabled. |`true` |
|OriginResponseHeader |Object[] |Indicates the configuration of the Origin Response Headers feature. | |
|OriginResponseHeaderAction |Object |Indicates the operation on the response header when CDN receives a response from the origin server. | |
|OriginResponseHeaderInstances |Object[] |Indicates a list of response header configuration rules. Each rule contains the relevant operation settings for a header. You can add up to 50 rules. | |
|Action |String |Indicates the operation of CDN on the response header. This parameter has the following values:<br><br><br>* `set`: Indicates setting a header. The setting operation includes adding and modifying. If the origin response already contains this header, the value of the header will be overwritten. If the origin response does not contain this header, the header will be added.<br><br>* `delete`: Indicates deleting a header. |`set` |
|Key |String |Indicates the name of a header. The name cannot exceed 1,024 characters, is case\-insensitive, and cannot contain Chinese characters and the following characters:<br><br><br>* Chinese characters, underscores (_), spaces, double quotes ("), colons (:)<br><br><br>See [Common Headers](https://www.volcengine.com/docs/6454/1319866#%E5%B8%B8%E7%94%A8%E5%A4%B4%E9%83%A8). |`MyHeader` |
|Value |String |Indicates the value of `Key`. |`hello` |
|ValueType |String |Indicates the value type of `Key`.<br><br>Valid values:<br><br><br>* `constant`: The value of `Key` is a fixed string.<br><br>* `variable`: The value of `Key` is obtained from a variable.<br><br>* `customize`: The value of `Key` is a string formed by concatenating variables and fixed strings. |`constant` |
|Object |String |Indicates which user requests this rule takes effect on. This parameter has the following values:<br><br><br>* `default`: Indicates that this rule only takes effect for user requests whose origin response contains the following response codes:<br><br>   * 200, 201, 204, 206, 301, 302, 303, 304, 307, 308<br><br>* `all_request`: Indicates that this rule takes effect for all user requests. |`default` |
|Cname |String |Indicates the CNAME assigned to this domain name by CDN. |`www.example.com.bplslb.com` |
|CreateTime |Long |Indicates the creation time of this domain name, in Unix timestamp format. |`1636612244` |
|Project |String |Indicates the project to which this domain name belongs. |`default` |
|Status |String |Indicates the status of this domain name. This parameter has the following values:<br><br><br>* `online`: Indicates that the status is running normally.<br><br>* `configuring`: Indicates that the status is configuring.<br><br>* `offline`: Indicates that the status is offline. |`offline` |
|UpdateTime |Long |Indicates the last update time of this domain name configuration, in Unix timestamp format. If this domain name configuration has not been updated after creation, the value of this parameter is the same as the value of `CreateTime`. |`1639621409` |
|ResourceTags |Object[] |Indicates the tags of the domain. | |
|Key |String |Indicates the key of a tag. |`key1` |
|Value |String |Indicates the value of the tag. |`value1` |
|ProxyProtocol |Object |Represents the configuration for the PROXY Protocol. | |
|Switch |Boolean |Indicates whether PROXY Protocol support is enabled. This parameter has the following values:<br><br><br>* `true` : Indicates that the PROXY Protocol is enabled. The CDN parses the received PROXY protocol header to obtain the client's real IP address.<br><br>* `false` : Indicates that the PROXY Protocol is disabled. | |
|Range |Object |Indicates the settings for fragment size. | |
|RangeSize |Long |Indicates the fragment size. |`512` |
|Switch |Boolean |Indicates whether the setting is enabled. The parameter can be one of the following values:<br><br><br>* `true` : Indicates the setting is enabled.<br><br>* `false` : Indicates the setting is disabled. |`true` |
|Unit |String |Indicates the unit of `RangeSize`. The parameter can be one of the following values:<br><br><br>* `KB`<br><br>* `MB` |`KB` |
|ServerSentEvent |Object |Indicates the Server\-Sent Events (SSE) configuration. | |
|Switch |Boolean |Indicates whether the setting is enabled. This parameter has the following values:<br><br><br>* `true`: Indicates that the setting is enabled.<br><br>* `false`: Indicates that the setting is disabled. |`true` |
|HTMLToMarkdown |Object |Indicates the configuration of the Convert HTML to Markdown feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`true` |
|OriginPreconnect |Object |Indicates the configuration of the Origin Keep\-Alive feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`true` |
|SmartOriginRouting |Object |Indicates the configuration of the Smart Routing feature. | |
|Switch |Boolean |Indicates whether to enable this feature. This parameter can take the following values:<br><br><br>* `true`: Indicates enabling this feature.<br><br>* `false`: Indicates disabling this feature.<br><br><br>The default value is `false`. |`true` |
|AccessOptimise |Object |中国大陆访问优化配置 | |
|AccOptimiseCname |String |无 | |
|Switch |Boolean |无 | |
|VideoPreview |Object |视频试看 | |
|Switch |Boolean |视频试看开关 | |
|PreviewParam |String |试看时长参数 | |


<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

```json
POST https://cdn.byteplusapi.com/?Action=DescribeCdnConfig&Version=2021-03-01
{
    "Domain": "test111.example.com"
}
```


<span id="sample-response"></span>
### Sample response

```json
{
    "ResponseMetadata": {
        "RequestId": "202508160551554488555F346DC5A960D4",
        "Action": "DescribeCdnConfig",
        "Version": "2021-03-01",
        "Service": "CDN",
        "Region": "ap-singapore-1"
    },
    "Result": {
        "DomainConfig": {
            "AreaAccessRule": {
                "Area": [
                    "CHN",
                    "HKG",
                    "MAC",
                    "TWN",
                    "CHE"
                ],
                "RuleType": "allow",
                "Switch": true
            },
            "ProxyProtocol": {
                "Switch": true
            },
            "BrowserCache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": true,
                        "Ttl": 216000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "no_cache",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "cache",
                        "IgnoreCase": false,
                        "Ttl": 3000
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cache": [
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "default",
                        "IgnoreCase": true,
                        "Ttl": 50
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "force_cache",
                        "IgnoreCase": false,
                        "Ttl": 80
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first",
                        "IgnoreCase": false,
                        "Ttl": 40
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheAction": {
                        "Action": "cache",
                        "DefaultPolicy": "origin_first_Replenish",
                        "IgnoreCase": false,
                        "Ttl": 0
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "CacheKey": [
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png",
                                "IgnoreCase": true
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "exclude",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "includePart",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "excludePart",
                                "IgnoreCase": false,
                                "Object": "queryString",
                                "Subobject": "param3;param4"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    }
                },
                {
                    "CacheKeyAction": {
                        "CacheKeyComponents": [
                            {
                                "Action": "include",
                                "IgnoreCase": true,
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    },
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    }
                }
            ],
            "Cname": "test111.example.com.bplslb.com",
            "Compression": {
                "CompressionRules": [
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip",
                                "br"
                            ],
                            "MinFileSizeKB": 10240
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "gzip"
                            ],
                            "MinFileSizeKB": 10000
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        }
                    },
                    {
                        "CompressionAction": {
                            "CompressionFormat": "all",
                            "CompressionTarget": "*",
                            "CompressionType": [
                                "br"
                            ],
                            "MinFileSizeKB": 12345
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        }
                    }
                ],
                "Switch": true
            },
            "ConditionalOrigin": {
                "OriginRules": [
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "203.0.113.6",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": ""
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Name": "myparam",
                                        "Object": "query_name",
                                        "Operator": "equal",
                                        "Type": "querystring",
                                        "Value": [
                                            "myvalue"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.s3-ap-southeast-1.amazonaws.com",
                                    "BucketSource": "aws_common",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx",
                                        "Region": "ap-southeast-1"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Name": "myheader",
                                        "Object": "customize",
                                        "Operator": "match",
                                        "Type": "request_header",
                                        "Value": [
                                            "myvalue"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                    "BucketSource": "cos",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "belong",
                                        "Value": [
                                            "HKG",
                                            "CHE"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "banana-health.tos-ap-southeast-1.bytepluses.com",
                                    "BucketSource": "tos",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "banana-health.tos-ap-southeast-1.bytepluses.com",
                                    "PrivateBucketAccess": true
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "filetype",
                                        "Operator": "equal",
                                        "Value": [
                                            "png"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "www.example.com",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "domain",
                                    "OriginHost": "non-img.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "directory",
                                        "Operator": "not_equal",
                                        "Value": [
                                            "/img/"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "198.51.100.5",
                                    "HttpPort": "80",
                                    "HttpsPort": "443",
                                    "InstanceType": "ip",
                                    "OriginHost": "img.example.com"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "full_querystring",
                                        "Operator": "regex_match",
                                        "Value": [
                                            "^/a{1,2}.*g$"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "and",
                            "IsGroup": true
                        }
                    },
                    {
                        "Actions": {
                            "OriginLines": [
                                {
                                    "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                    "BucketSource": "oss",
                                    "HttpPort": "",
                                    "HttpsPort": "",
                                    "InstanceType": "storage",
                                    "OriginHost": "",
                                    "PrivateBucketAccess": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxx"
                                    }
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionGroups": [
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file1",
                                            "/docs/file2/"
                                        ]
                                    },
                                    "IsGroup": false
                                },
                                {
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "equal",
                                        "Value": [
                                            "/docs/file3",
                                            "/docs/file4/"
                                        ]
                                    },
                                    "IsGroup": false
                                }
                            ],
                            "Connective": "or",
                            "IsGroup": true
                        }
                    }
                ],
                "Switch": true
            },
            "CreateTime": 1755314680,
            "CustomErrorPage": {
                "ErrorPageRule": [
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "301",
                            "RedirectUrl": "http://www.example.com/newpage1",
                            "StatusCode": "405"
                        }
                    },
                    {
                        "ErrorPageAction": {
                            "Action": "redirect",
                            "RedirectCode": "307",
                            "RedirectUrl": "http://www.example.com/newpage2",
                            "StatusCode": "504"
                        }
                    }
                ],
                "Switch": true
            },
            "Domain": "test111.example.com",
            "DownloadSpeedLimit": {
                "DownloadSpeedLimitRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "unlimited",
                                    "Operator": "match",
                                    "Type": "url"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 100,
                            "SpeedLimitRateAfter": 50,
                            "SpeedLimitTime": {
                                "BeginTime": "01:00",
                                "DayWeek": "unlimited",
                                "EndTime": "02:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 200,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "monday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 300,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "tuesday",
                                "EndTime": "06:00"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 400,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "wednesday",
                                "EndTime": "13:59"
                            }
                        }
                    },
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "DownloadSpeedLimitAction": {
                            "SpeedLimitRate": 500,
                            "SpeedLimitRateAfter": 90,
                            "SpeedLimitTime": {
                                "BeginTime": "04:00",
                                "DayWeek": "thursday",
                                "EndTime": "05:59"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "FollowRedirect": true,
            "HTTPS": {
                "CertInfo": {
                    "CertId": "cert-7fade0eb4f8d4aadbde5dd25f2ffdf35",
                    "CertName": "1000011991",
                    "EncryType": "inter_cert",
                    "ExpireTime": 1763086346,
                    "Source": "cert_center"
                },
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
                "Switch": true,
                "TlsVersion": [
                    "tlsv1.1",
                    "tlsv1.2"
                ]
            },
            "HttpForcedRedirect": {
                "EnableForcedRedirect": false,
                "StatusCode": "301"
            },
            "IPv6": {
                "Switch": true
            },
            "IpAccessRule": {
                "Switch": true,
                "DenyStatusCode": 402,
                "RuleType": "allow",
                "Ip": [
                    "xxx.xxx.xx.xx",
                    "xxx.xxx.xx.xxx"
                ],
                "IpSource": {
                    "SourceList": [
                        "x-forwarded-for",
                        "x-real-ip"
                    ],
                    "Type": "custom"
                }
            },
            "MethodDeniedRule": {
                "Methods": "POST,DELETE,CONNECT,OPTIONS",
                "Switch": true
            },
            "MultiRange": {
                "Switch": false
            },
            "NegativeCache": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "jpg;png"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "400",
                        "Ttl": 60
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": true,
                        "StatusCode": "401",
                        "Ttl": 59
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "402",
                        "Ttl": 70
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "NegativeCacheRule": {
                        "Action": "cache",
                        "IgnoreCase": false,
                        "StatusCode": "404",
                        "Ttl": 60
                    }
                }
            ],
            "OfflineCache": {
                "Object": "request_error,error_code",
                "StatusCode": "504;505",
                "Switch": true
            },
            "Origin": [
                {
                    "OriginAction": {
                        "OriginLines": [
                            {
                                "Address": "203.0.113.8",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginHost": "myorigin.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginHost": "myorigin2.example.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "InstanceType": "tos",
                                "OriginHost": "bpcntest.tos-ap-southeast-3.bytepluses.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "tos",
                                    "Switch": true
                                },
                                "Region": "ap-southeast-3",
                                "Weight": "1"
                            },
                            {
                                "Address": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.oss-ap-southeast-1.aliyuncs.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "oss",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxx"
                                    }
                                },
                                "Region": "oss-ap-southeast-1",
                                "Weight": "2"
                            },
                            {
                                "Address": "mybucket.cos.ap-singapore.myqcloud.com",
                                "InstanceType": "tos",
                                "OriginHost": "mybucket.cos.ap-singapore.myqcloud.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "cos",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-singapore",
                                "Weight": "3"
                            },
                            {
                                "Address": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "InstanceType": "tos",
                                "OriginHost": "my-bucket.s3.ap-southeast-1.amazonaws.com",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "aws_common",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccessKeyId": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
                                        "AccessKeySecret": "xxxxxxxxxx"
                                    }
                                },
                                "Region": "ap-southeast-1",
                                "Weight": "5"
                            },
                            {
                                "Address": "myazstorage.blob.core.windows.net",
                                "BucketName": "myazstorage",
                                "InstanceType": "tos",
                                "OriginHost": "myazstorage.blob.core.windows.net",
                                "OriginType": "primary",
                                "PrivateBucketAccess": true,
                                "PrivateBucketAuth": {
                                    "AuthType": "azure",
                                    "Switch": true,
                                    "TosAuthInformation": {
                                        "AccountKey": "xxxxxxxxxxxxxxxx"
                                    }
                                },
                                "Weight": "1"
                            },
                            {
                                "Address": "203.0.113.9",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "ip",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            },
                            {
                                "Address": "img2.example.com",
                                "HttpPort": "80",
                                "HttpsPort": "443",
                                "InstanceType": "domain",
                                "OriginType": "backup",
                                "PrivateBucketAccess": false,
                                "Weight": "1"
                            }
                        ]
                    }
                }
            ],
            "OriginAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "Origins": [
                    "test.example.net",
                    "my.example.net"
                ],
                "RuleType": "deny",
                "Switch": true
            },
            "OriginArg": [
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "regex",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "^/a{1,2}(.*)g$"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "set",
                                "Object": "queryString",
                                "Subobject": "key3=val3;key4=val4"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "filetype",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "png;jpg"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "excludePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/foods/;/dogs/ragdolls/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "includePart",
                                "Object": "queryString",
                                "Subobject": "param1;param2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file3;/docs/file4"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "addPart",
                                "Object": "queryString",
                                "Subobject": "key1=val1;key2=val2"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "path",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/docs/file1;/docs/file2"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "exclude",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                },
                {
                    "Condition": {
                        "ConditionRule": [
                            {
                                "Object": "directory",
                                "Operator": "match",
                                "Type": "url",
                                "Value": "/"
                            }
                        ],
                        "Connective": "OR"
                    },
                    "OriginArgAction": {
                        "OriginArgComponents": [
                            {
                                "Action": "include",
                                "Object": "queryString",
                                "Subobject": "*"
                            }
                        ]
                    }
                }
            ],
            "OriginCertCheck": {
                "Switch": true
            },
            "OriginHost": "superhost.example.com",
            "OriginIPv6": "ipv6_first",
            "OriginProtocol": "https",
            "OriginRange": true,
            "Range": {
                "Switch": true,
                "RangeSize": "2",
                "Unit": "MB"
            },
            "OriginRewrite": {
                "Switch": false
            },
            "OriginSni": {
                "SniDomain": "superhost.example.com",
                "Switch": true
            },
            "PageOptimization": {
                "OptimizationType": [
                    "html",
                    "js",
                    "css"
                ],
                "Switch": true
            },
            "Project": "default",
            "Quic": {
                "Switch": true
            },
            "RedirectionRewrite": {
                "RedirectionRule": [
                    {
                        "RedirectionAction": {
                            "RedirectCode": "302",
                            "SourcePath": "^/a{1,2}(.*)g$",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food$1g",
                            "TargetProtocol": "https",
                            "TargetQueryComponents": {
                                "Action": "includePart",
                                "Value": "param1"
                            }
                        }
                    },
                    {
                        "RedirectionAction": {
                            "RedirectCode": "307",
                            "SourcePath": "aaa(.*)",
                            "TargetHost": "www.example.com",
                            "TargetPath": "/food/$1g",
                            "TargetProtocol": "followclient",
                            "TargetQueryComponents": {
                                "Action": "include",
                                "Value": "*"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RefererAccessRule": {
                "AllowEmpty": true,
                "Referers": [
                    "www.example.org",
                    "docs.example.com",
                    "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                ],
                "ReferersType": {
                    "CommonType": {
                        "IgnoreCase": true,
                        "IgnoreScheme": true,
                        "Referers": [
                            "www.example.org",
                            "docs.example.com"
                        ]
                    },
                    "RegularType": {
                        "Referers": [
                            "^https://test.example.com/a{1,2}bc/.*\\.jpg$"
                        ]
                    }
                },
                "RuleType": "allow",
                "Switch": true
            },
            "RemoteAuth": {
                "RemoteAuthRules": [
                    {
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "bmp;pdf"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RemoteAuthRuleAction": {
                            "AuthModeConfig": {
                                "BackupRemoteAddr": "https://myendpoint2.com",
                                "MasterRemoteAddr": "https://myendpoint1.com",
                                "PathType": "variable",
                                "PathValue": "/sign",
                                "RequestMethod": "post"
                            },
                            "AuthResponseConfig": {
                                "CacheAction": {
                                    "Action": "cache",
                                    "CacheKey": [
                                        "URI",
                                        "content_type"
                                    ],
                                    "IgnoreCase": false,
                                    "Ttl": 40
                                },
                                "ResponseAction": {
                                    "StatusCode": "403"
                                },
                                "StatusCodeAction": {
                                    "DefaultAction": "pass",
                                    "FailCode": "401",
                                    "SuccessCode": "200"
                                },
                                "TimeOutAction": {
                                    "Action": "pass",
                                    "Time": 200
                                }
                            },
                            "QueryStringRules": {
                                "QueryStringComponents": {
                                    "Action": "includePart",
                                    "Value": "size;color"
                                },
                                "QueryStringInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "param1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "param2",
                                        "Value": "content_type",
                                        "ValueType": "variable"
                                    }
                                ]
                            },
                            "RequestBodyRules": "default",
                            "RequestHeaderRules": {
                                "RequestHeaderComponents": {
                                    "Action": "includePart",
                                    "Value": "header1;header2"
                                },
                                "RequestHeaderInstances": [
                                    {
                                        "Action": "set",
                                        "Key": "hd1",
                                        "Value": "val1",
                                        "ValueType": "constant"
                                    },
                                    {
                                        "Action": "set",
                                        "Key": "hd2",
                                        "Value": "client_ip",
                                        "ValueType": "variable"
                                    }
                                ],
                                "RequestHost": "test.example.com"
                            }
                        }
                    }
                ],
                "Switch": true
            },
            "RequestBlockRule": {
                "BlockRule": [
                    {
                        "BlockAction": {
                            "Action": "refuse",
                            "StatusCode": "404"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "path",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "filetype",
                                    "Operator": "equal",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Name": "param1",
                                    "Object": "query_name",
                                    "Operator": "equal",
                                    "Type": "querystring",
                                    "Value": "val1"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "RuleName": "myrule1"
                    },
                    {
                        "BlockAction": {
                            "Action": "redirect",
                            "RedirectUrl": "https://www.example.com/helloworld",
                            "StatusCode": "301"
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "full_querystring",
                                    "Operator": "not_match",
                                    "Type": "querystring",
                                    "Value": ".*size=.*\\&.*"
                                },
                                {
                                    "Object": "client_ip",
                                    "Operator": "match",
                                    "Type": "client_ip",
                                    "Value": "203.0.113.2;203.0.113.5"
                                },
                                {
                                    "Object": "ua",
                                    "Operator": "not_empty",
                                    "Type": "request_header"
                                },
                                {
                                    "Name": "myheader",
                                    "Object": "customize",
                                    "Operator": "match",
                                    "Type": "request_header",
                                    "Value": "value1"
                                }
                            ],
                            "Connective": "AND"
                        },
                        "RuleName": "myrule2"
                    }
                ],
                "Switch": true
            },
            "RequestHeader": [
                {
                    "RequestHeaderAction": {
                        "RequestHeaderInstances": [
                            {
                                "Action": "set",
                                "Key": "header1",
                                "Value": "val1",
                                "ValueType": "constant"
                            },
                            {
                                "Action": "set",
                                "Key": "header2",
                                "Value": "uri",
                                "ValueType": "variable"
                            },
                            {
                                "Action": "set",
                                "Key": "header3",
                                "Value": "myval${http_host}is${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "Action": "delete",
                                "Key": "header4"
                            }
                        ]
                    }
                }
            ],
            "ResourceTags": [
                {
                    "Key": "key1",
                    "Value": "value1"
                },
                {
                    "Key": "key2",
                    "Value": "value2"
                }
            ],
            "ResponseHeader": [
                {
                    "ResponseHeaderAction": {
                        "ResponseHeaderInstances": [
                            {
                                "AccessOriginControl": true,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Origin",
                                "Value": "myval",
                                "ValueType": "constant"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Allow-Headers",
                                "Value": "raw_uri",
                                "ValueType": "variable"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "set",
                                "Key": "Access-Control-Expose-Headers",
                                "Value": "my${host}data${query_string}",
                                "ValueType": "customize"
                            },
                            {
                                "AccessOriginControl": false,
                                "Action": "delete",
                                "Key": "Access-Control-Max-Age"
                            }
                        ]
                    }
                }
            ],
            "RuleEngine": {
                "Rules": [],
                "Switch": false
            },
            "ServiceRegion": "outside_chinese_mainland",
            "ServiceType": "web",
            "SignedUrlAuth": {
                "AuthRulesF": [
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "inherit_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": true
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "md5_bin",
                                "base64url",
                                "sha256",
                                "md5",
                                "base64_encode"
                            ],
                            "SignJoinSymbol": "abc",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "fixstring"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "URI",
                                    "UriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 3,
                                        "TermLevel": 5
                                    }
                                },
                                {
                                    "ParamSource": "ParentLink",
                                    "ParamType": "URLParam",
                                    "UrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "uri",
                                        "UriLevel": 3
                                    }
                                },
                                {
                                    "ParamType": "ClientDomain"
                                },
                                {
                                    "ParamType": "Referer"
                                },
                                {
                                    "ParamType": "Origin"
                                },
                                {
                                    "ParamType": "ClientIP"
                                },
                                {
                                    "ParamType": "UA"
                                },
                                {
                                    "ParamType": "ReqHeader",
                                    "RequestHeader": "myheader1"
                                },
                                {
                                    "CookieToken": "mycookie1",
                                    "ParamType": "Cookie"
                                },
                                {
                                    "ParamSource": "ChildLink",
                                    "ParamType": "FullURI"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "filetype",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "jpg;png"
                                },
                                {
                                    "Object": "directory",
                                    "Operator": "not_match",
                                    "Type": "url",
                                    "Value": "/docs/foods/;/dogs/ragdolls/"
                                },
                                {
                                    "Object": "path",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/docs/file1;/docs/file2"
                                },
                                {
                                    "Object": "regex",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "^/a{1,2}(.*)g$"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "CustomRewrite": {
                            "RewriteParam": [
                                {
                                    "ParamType": "ParentLinkUrlParam",
                                    "ParentLinkUrlParam": {
                                        "ArgSegment": {
                                            "Level": 0,
                                            "Switch": false
                                        },
                                        "CapMode": "name",
                                        "ParamName": "param23"
                                    }
                                },
                                {
                                    "ParamType": "SupString",
                                    "SupContent": "string2"
                                },
                                {
                                    "ParamType": "ParentLinkURI",
                                    "ParentLinkUriParamSup": {
                                        "JoinSymbol": "/",
                                        "SplitSymbol": "-",
                                        "StartLevel": 4,
                                        "TermLevel": 6
                                    }
                                },
                                {
                                    "ParamType": "ParentLinkExpire"
                                },
                                {
                                    "ParamType": "AuthToken"
                                },
                                {
                                    "ParamType": "ParentFullURI"
                                }
                            ],
                            "RewriteRule": {
                                "CapMode": "name",
                                "ParamName": "myparam1"
                            },
                            "SignJoinSymbol": "/",
                            "Switch": true
                        },
                        "ExpireTimeRule": {
                            "Duration": 30,
                            "ExpTimeCapRule": {
                                "ArgSegment": {
                                    "Level": 0,
                                    "Switch": false
                                },
                                "CapMode": "name",
                                "ParamName": "param1"
                            },
                            "TimeFormat": "heximal"
                        },
                        "RewriteFormat": "default",
                        "RewriteM3U8": {
                            "RewriteM3U8Tag": {
                                "Switch": true,
                                "Tags": [
                                    "tag1",
                                    "tag2"
                                ]
                            },
                            "Switch": true
                        },
                        "RewriteMPD": {
                            "MpdVarExpand": true,
                            "Switch": true
                        },
                        "RuleName": "Authentication rule A",
                        "SecretKey": {
                            "BackupSecretKey": "secondarykey",
                            "MasterSecretKey": "primarykey"
                        },
                        "SignCapRule": {
                            "ArgSegment": {
                                "Level": 2,
                                "SplitSymbol": "-",
                                "Switch": true
                            },
                            "CapMode": "uri",
                            "UriLevel": 2
                        }
                    },
                    {
                        "ArgumentRule": {
                            "GeneralParamRule": {
                                "ParentLinkParamInherit": "not_inherit",
                                "SubLinkParamRule": {
                                    "InheritMode": "sub_link_first",
                                    "KeepSubLinkArg": "keep"
                                }
                            },
                            "KeepOriginArg": false
                        },
                        "AuthTokenCalRule": {
                            "ParamCalRules": [
                                "base64url"
                            ],
                            "SignJoinSymbol": "45yu",
                            "SignParam": [
                                {
                                    "ParamType": "SecretKey"
                                }
                            ]
                        },
                        "Condition": {
                            "ConditionRule": [
                                {
                                    "Object": "directory",
                                    "Operator": "match",
                                    "Type": "url",
                                    "Value": "/"
                                }
                            ],
                            "Connective": "OR"
                        },
                        "ExpireTimeRule": {
                            "Duration": 67,
                            "ExpTimeCapRule": {
                                "CapMode": "cookie",
                                "CustomValue": "mycookie56"
                            },
                            "TimeFormat": "octal"
                        },
                        "RewriteFormat": "default",
                        "RuleName": "Authentication rule B",
                        "SecretKey": {
                            "BackupSecretKey": "sk",
                            "MasterSecretKey": "pk"
                        },
                        "SignCapRule": {
                            "CapMode": "header",
                            "CustomValue": "myheader56"
                        }
                    }
                ],
                "Switch": true
            },
            "Status": "online",
            "Timeout": {
                "Switch": true,
                "TimeoutRules": [
                    {
                        "TimeoutAction": {
                            "HttpTimeout": 10,
                            "TcpTimeout": 5,
                            "HttpFirstByteTimeout": 90
                        }
                    }
                ]
            },
            "UaAccessRule": {
                "AllowEmpty": true,
                "IgnoreCase": true,
                "RuleType": "deny",
                "Switch": true,
                "UserAgent": [
                    "*curl*",
                    "*firefox*"
                ]
            },
            "UpdateTime": 1755323476,
            "UrlNormalize": {
                "NormalizeObject": [
                    "back_slashes",
                    "successive_slashes",
                    "dot_segments"
                ],
                "Switch": true
            },
            "VideoDrag": {
                "Switch": true
            },
            "Websocket": {
                "Switch": true,
                "Timeout": 60
            }
        }
    }
}
```
