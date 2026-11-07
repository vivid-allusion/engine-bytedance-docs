---
title: "UpdateRuleEngineTemplate"
product: "BytePlus CDN"
product_code: "byteplus-cdn"
source: "https://docs.byteplus.com/en/docs/byteplus-cdn/UpdateRuleEngineTemplate_en-us"
---

Update the configuration in the rules engine template.

Except for `Title` and `Message`, updates to other parameters require you to specify `TemplateVersion` as `draft` when calling `UpdateRuleEngineTemplate`. This means that the policy to be updated already has a Draft version. To ensure that the policy to be updated already has a Draft version, follow these steps:


1. Call the [DescribeTemplateReleaseVersions](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeTemplateReleaseVersions_en-us) API for that policy.

2. In the version list returned by the API, check if the Draft version (`"Version": "draft"`) exists.

   * If the Draft version exists, you can call `UpdateRuleEngineTemplate` for that policy.

   * Otherwise, you need to first call [CreateTemplateVersion](https://docs.byteplus.com/en/docs/byteplus-cdn/CreateTemplateVersion_en-us) for that policy to create a Draft version, and then call `UpdateRuleEngineTemplate`.


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This API has been integrated into BytePlus SDK for Python v1.0.40 and later versions. Get the <a href="https://github.com/byteplus-sdk/byteplus-sdk-python">latest version of BytePlus SDK for Python</a>.</div>


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">The update method for the rule engine configuration is a full overwrite. When updating the rule engine configuration, if an existing configuration in the rule is not specified, that configuration will be removed. You can call <a href="https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeRuleEngineTemplate_en-us">DescribeRuleEngineTemplate</a> to get the current configuration of the rule.</div>


<span id="usage-limits"></span>
## Usage Limits

API throttling: You can submit up to 20 API requests per second.

<span id="usage"></span>
## Usage


* Request Method: POST

* Request URL: https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021\-03\-01


<span id="request-parameters"></span>
## Request Parameters

<span id="query-parameters"></span>
### Query Parameters


|Parameter |Data Type |Required |Description |
|---|---|---|---|
|Action |String |Yes |The action of this API operation. The action is: `UpdateRuleEngineTemplate`. |
|Version |String |Yes |The version of this API operation. Current version: `2021-03-01`. |


<span id="request-body"></span>
### Request Body


|Parameter |Data Type |Required |Description |Value |
|---|---|---|---|---|
|TemplateId |String |Yes |Indicates the ID of the rules engine policy you want to modify.<br><br>You can use [DescribeTemplates](https://docs.byteplus.com/en/docs/byteplus-cdn/reference-describetemplates) to get the ID of the rules engine policy you want to modify. |`tpl-rev6j89` |
|Message |String |No |Indicates a new policy description, which cannot exceed 120 characters. |`new-desc` |
|Rule |Object |No |Indicates the configuration of the rule. The actual data type of this parameter is String. When submitting an API request, you need to serialize the `Rule` structure to convert the JSON format to a string format. The steps are as follows:<br><br><br>1. Remove the outermost `[]`.<br><br>2. Remove line breaks and spaces.<br><br>3. Replace `"` with `\"`.<br><br>4. Set the processed content as a string value for `Rule`. | |
|IfBlock |Object |Yes |Indicates the IF expression in the rule, including the `Condition`, `Actions`, and `SubRules` structures. These structures demonstrate the following request processing logic:<br><br><br>* If the user request meets the matching conditions under `Condition`, CDN first executes the operations under `Actions` in the `IfBlock`, then processes the sub\-rules under `SubRules` in the `IfBlock`.<br><br>* Otherwise, CDN first executes the operations under `Actions` in the `ElseBlock`, then processes the sub\-rules under `SubRules` in the `ElseBlock`. |`See Sample Request 1 below` |
|SubRules |Object[] |No |Indicates the list of sub\-rules under the IF expression. The list can contain up to 10 sub\-rules. | |
|Desc |String |No |Indicates the description of the sub\-rule. |`Sub-rule1` |
|IfBlock |Object |Yes |Indicates the IF expression under the sub\-rule, with the same meaning and parameters as the parent rule's `IfBlock`. Note that sub\-rules cannot be nested within sub\-rules. Therefore, the value of the `SubRules` structure under the `IfBlock` in the sub\-rule must be empty (`[]`). | |
|ElseBlock |Object |No |Indicates the ELSE expression under the sub\-rule, with the same meaning and parameters as the parent rule's `ElseBlock`. | |
|Actions |Object[] |Yes |Indicates the list of actions executed by CDN. Each action is a CDN feature configuration.<br><br>Currently, some CDN features cannot be configured in the rules engine, but will be supported in the future. For CDN features supported by the rules engine, see the description of the `Action` parameter. | |
|Action |String |No |Indicates the CDN feature. Valid values:<br><br><br>* `redirect_request`: Origin URL Rewrite.<br><br>* `allow_access`: Allow Access.<br><br>* `redirect_protocol`: Protocol Redirect.<br><br>* `download_speed_limit`: Data Rate Limiting.<br><br>* `request_header`: Client Request Headers.<br><br>* `deny_access`: Deny Access.<br><br>* `url_auth`: Signed URL Authentication.<br><br>* `cache_key`: Cache Key.<br><br>* `compression`: File Compression.<br><br>* `video_drag`: Video Seeking.<br><br>* `cache_time`: Caching Rules.<br><br>* `response_header`: Client Response Headers.<br><br>* `browser_cache`: Browser Caching.<br><br>* `http_code`: HTTP Status Code Rewrite.<br><br>* `custom_page`: Custom Error Pages.<br><br>* `origin_range`: Range Origin Fetch.<br><br>* `origin_follow`: Redirect Follow.<br><br>* `origin_tcp_timeout`: TCP Timeout.<br><br>* `origin_http_timeout`: HTTP Timeout.<br><br>* `origin_rewrite`: Origin URL Rewrite.<br><br>* `origin_sni`: Origin SNI.<br><br>* `origin_protocol`: Origin Protocol.<br><br>* `origin_request_header`: Origin Request Headers.<br><br>* `origin_host`: Origin Host.<br><br><br>warning<br><br>If any condition in the condition list has an `Object` value of `response_header` or `http_code`, the action list can contain only one action whose [Stage is client_response](https://docs.byteplus.com/en/docs/18/47580#client-response-stage). |`response_header` |
|Groups |Object[] |No |Indicates the CDN feature configuration corresponding to `Action`, including the `Dimension` parameter and the `GroupParameters` structure.<br><br><br>* The `Dimension` parameter indicates the configuration object. Some CDN features may include multiple configuration objects.<br><br>* The `GroupParameters` structure contains configurations corresponding to `Dimension`. Different values for certain configurations may produce different configuration combinations, so `GroupParameters` represents a configuration group. For example, in "Client Request Header Settings", you can set and delete operations for request headers. These operations produce different configuration combinations, defined in their respective configuration groups. Additionally, for `GroupParameters`, each configuration group contains a `Parameters` structure. The `Parameters` structure is a list of parameters, each representing a specific configuration.<br><br><br>See [Action Parameter Configuration for Each Stage](https://docs.byteplus.com/en/docs/18/47580#action-parameter-configurations-by-stage). | |
|Dimension |String |No |Indicates the configuration object. |`response_header` |
|GroupParameters |Object[] |No |Indicates the configuration corresponding to `Dimension`. | |
|Parameters |Object[] |Yes |Indicates a list of parameters. | |
|Name |String |Yes |Indicates the name of a parameter in the list. |`action` |
|Values |String[] |Yes |Indicates the value of the parameter. | |
|Condition |Object |Yes |Indicates the matching condition definition under the IF expression. | |
|IsGroup |Boolean |Yes |This parameter value must be `true`. |`true` |
|Connective |String |Yes |This parameter value must be `and`. |`and` |
|ConditionGroups |Object[] |Yes |Indicates a list of condition groups. | |
|IsGroup |Boolean |Yes |Indicates whether each list item is a condition group. This parameter value must be `true`, indicating that each list item is a condition group. |`true` |
|Connective |String |Yes |Indicates the logical relationship between condition groups. This parameter has the following values:<br><br><br>* `and`: Indicates the relationship is `AND`.<br><br>* `or`: Indicates the relationship is `OR`.<br><br><br>The default value of this parameter is `and`. |`and` |
|ConditionGroups |Object[] |Yes |Indicates the list of matching conditions in the condition group. | |
|IsGroup |Boolean |Yes |Indicates whether this matching condition is a condition group. This parameter value must be `false`. The rules engine does not support nested condition groups. |`false` |
|Condition |Object |Yes |Indicates the definition of a matching condition in the list. Each matching condition includes:<br><br><br>* `Object`: Indicates the matching object.<br><br>* `Operator`: Indicates the matching operator.<br><br>* `Value`: Indicates the list of matching values. Unless `Operator` is `exist` or `not_exist`, each matching condition needs to specify a list of matching values.<br><br>* `IgnoreCase`: Indicates whether the matching value is case\-sensitive. Only applicable when the matching value is a string.<br><br>* `TimeZone`: Indicates the time zone, only applicable when `Object` is `request_time`.<br><br>* `Name`:<br><br>   * Indicates the parameter name. Applies when `Object` is `query_string`, `request_header`, `response_header`, or `client_cert_info`.<br><br>   * Indicates the time\-range type. Applies when `Object` is `request_time`.<br><br><br>For the Operators that can be used with each `Object`, as well as information such as `IgnoreCase`, see the description in the [Input Requirements for Each Matching Object](https://docs.byteplus.com/en/docs/18/47580#input-requirements-for-each-match-object) section below. | |
|Object |String |Yes |Indicates the matching object. This parameter has the following values:<br><br><br>* `always`: Indicates all requests.<br><br>* `path`: Indicates the request path, excluding query strings.<br><br>* `path_and_param`: Indicates the request path and query string.<br><br>* `url`: Indicates the complete request URL.<br><br>* `query_string`: Indicates the query string in the request URL.<br><br>* `http_referer`: Indicates the Referer header in the request.<br><br>* `client_ip`: Indicates the IP address of the client sending the request.<br><br>* `http_origin`: Indicates the Origin header in the request.<br><br>* `http_ua`: Indicates the User\-Agent header in the request.<br><br>* `request_header`: Indicates a header in the request other than Origin, Referer, and User\-Agent.<br><br>* `client_area`: Indicates the country or region from which the client IP address originates.<br><br>* `http_method`: Indicates the method used in the request.<br><br>* `request_time`: Indicates the time when CDN received the user request.<br><br>* `protocol`: Indicates the protocol used in the request.<br><br>* `response_header`: Indicates a header in the origin server response.<br><br>* `http_code`: Indicates the status code in the origin server response. |`always` |
|Operator |String |Yes |Indicates the match operator. Valid values:<br><br><br>* `prefix_match`: Matches the specified prefix.<br><br>* `prefix_not_match`: Does not match the specified prefix.<br><br>* `suffix_match`: Matches the specified suffix.<br><br>* `suffix_not_match`: Does not match the specified suffix.<br><br>* `match`: Matches the specified value.<br><br>* `not_match`: Does not match the specified value.<br><br>* `regex_match`: Matches the specified regular expression.<br><br>* `regex_not_match`: Does not match the specified regular expression.<br><br>* `equal`: Equals the specified value.<br><br>* `not_equal`: Does not equal the specified value.<br><br>* `exist`: Checks whether the specified object exists.<br><br>* `not_exist`: Checks whether the specified object does not exist.<br><br>* `belong_to`: Matches the specified Universal Catalog.<br><br>* `not_belong_to`: Does not match the specified Universal Catalog. |`suffix_match` |
|IgnoreCase |Boolean |Yes |Indicates whether `Value` is case\-sensitive. |`true` |
|Value |String[] |Yes |Indicates the list of matching values.<br><br>For the input requirements of the matching values, see the description in the [Input Requirements for Each Matching Object](https://docs.byteplus.com/en/docs/18/47580#input-requirements-for-each-match-object) section below. |`["png","gif"]` |
|Name |String |No |* When `Object` is `request_header`, `response_header`, or `query_string`, this parameter specifies the header or query parameter.<br><br>* When `Object` is `request_time`, valid values include:<br><br>   * `weekday`: Fixed days of the week.<br><br>   * `period`: A fixed time period.<br><br>   * `everyday`: A fixed time range each day.<br><br>* When `Object` is `client_cert_info`, valid values include:<br><br>   * `common_name`: The Common Name (CN) in the certificate subject.<br><br>   * `serial_number`: The certificate serial number.<br><br>   * `country_name`: The country or region code in the certificate subject.<br><br>   * `locality_name`: The city or locality in the certificate subject.<br><br>   * `organization_name`: The organization or company name in the certificate subject.<br><br>   * `organizational_unit_name`: The organizational unit or department name in the certificate subject. |`myparam` |
|TimeZone |String |No |When `Object` is `request_time`, this parameter indicates the time zone corresponding to the request time. Currently, you can only specify the time zone as UTC+08:00, with the parameter value as `+0800`. |`+0800` |
|ElseBlock |Object |Yes |Indicates the ELSE expression in the rule, including the `Actions` and `SubRules` structures.<br><br>If the user request does not meet the matching conditions under `Condition` in the `IfBlock`, CDN first executes the operations under `Actions` in the `ElseBlock`, then processes the sub\-rules under `SubRules` in the `ElseBlock`. | |
|SubRules |Object[] |No |Indicates the list of sub\-rules under the `ElseBlock` expression, with the same meaning and parameters as the `SubRules` structure under `IfBlock`. The list can contain up to 10 sub\-rules. | |
|Desc |String |No |Indicates the description of the sub\-rule. |`规则名称` |
|IfBlock |Object |Yes |Indicates the IF expression under the sub\-rule, with the same meaning and parameters as the parent rule's `IfBlock`. Note that sub\-rules cannot be nested within sub\-rules. Therefore, the value of the `SubRules` structure under the `IfBlock` in the sub\-rule must be empty (`[]`). | |
|ElseBlock |Object |No |Indicates the ELSE expression under the sub\-rule, with the same meaning and parameters as the parent rule's `ElseBlock`. | |
|Actions |Object[] |No |Indicates the `Actions` structure under the `ElseBlock` expression, with the same meaning and parameters as the `Actions` in the `IfBlock`. | |
|TemplateVersion |String |No |Indicates the policy version to be updated.<br><br><br>* If the parameter to be updated is `Title` or `Message`, you do not need to specify this parameter. These two parameters are not related to the policy version.<br><br>* If the parameter to be updated is not `Title` or `Message`, you must specify this parameter as `draft`. See the description at the beginning of the document. |`draft` |
|Title |String |No |Indicates a new policy name, which cannot exceed 100 characters. |`new-title` |


<span id="action-parameter-configurations-by-stage"></span>
## Action Parameter Configurations by Stage

<span id="client-request-stage"></span>
### client_request Stage


|**Action** |**Configuration Parameters** |**Example** |
|---|---|---|
|`redirect_request` |* `source_path`: The original path, matched by a regular expression.<br><br>* `status_code`: The redirect status code. Valid values: `301`, `302`, `303`, `307`, and `308`.<br><br>* `protocol`: The redirect protocol. Valid values: `follow_client`, `http`, and `https`.<br><br>* `target_host`: The domain name or IP address of the target site. The port is optional.<br><br>* `target_path`: The target path. Use `$n` to reference a capture group in the original path.<br><br>* `target_query_action`: Specifies how query parameters in the client request URL are handled. Valid values: `include_part`, `include_all`, `exclude_part`, and `exclude_all`.<br><br>* `target_query_values`: Parameters to include or remove. Applies when `target_query_action` is `include_part` or `exclude_part`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_269c25d2888e08f8eba903f3f8d810c1.json" name="redirect_request">redirect_request</Attachment><br> |
|`redirect_protocol` |* `status_code`: The redirect status code. Valid values: `301`, `302`, `303`, `307`, and `308`.<br><br>* `protocol`: The redirect protocol. Valid values: `http` and `https`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_cc69f446b49ee968718afdfc8fc9c994.json" name="redirect_protocol">redirect_protocol</Attachment><br> |
|`allow_access` |* `effective_scope`: The scope in which this action takes effect. Valid values: `rule_engine`, `method_denied_rule`, `area_access_rule`, and `request_block_rule`. Access control rules in the effective scope no longer block requests that meet the Rules Engine conditions. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_1cb30425b540afd3d3cce038f4d0fe92.json" name="allow_access.json">allow_access.json</Attachment><br> |
|`download_speed_limit` |* `limit_type`: Specifies the Throttling Method. Valid values: `normal` and `dynamic_limit`.<br><br>* `rate`: Specifies the Rate Limit, which is the data transfer rate threshold.<br><br>* `query_name`: Specifies the query parameter used to set the Rate Limit. Applies when `limit_type` is `dynamic_limit`.<br><br>* `dynamic_rate_unit`: Specifies the unit of the Rate Limit in the query parameter. Valid values: `KB/s`, `B/s`, and `MB/s`. Applies when `limit_type` is `dynamic_limit`.<br><br>* `rate_unit`: Specifies the unit of the Rate Limit. Valid values: `KB/s`, `B/s、MB/s`.<br><br>* `after_size`: Specifies Effective After, the amount of data that can be transferred before the Rate Limit takes effect.<br><br>* `after_size_unit`: Specifies the unit of Effective After. Valid values: `B`, `KB`, and `MB`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_30784db7f6e71524b69af14c020ecc2d.json" name="download_speed_limit.json">download_speed_limit.json</Attachment><br> |
|`request_header` |* `action`: The Client Request Headers operation. Valid values: `set` and `delete`.<br><br>* `header_name`: The header name.<br><br>* `header_value`: The header value. Applies when `action` is `set`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_13c911a67e9d16e54b479d9e20113613.json" name="request_header">request_header</Attachment><br> |
|`deny_access` |* `status_code`: The CDN response status code, in the range 100–599. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_90022a80c3c7d9204a21ccadddececca.json" name="deny_access">deny_access</Attachment><br> |
|`url_auth` |* `auth_type`: Specifies the Signed URL Authentication type. Valid values: `type_a`, `type_b`, `type_c`, `type_d`, and `type_e`.<br><br><br>**Type A Configuration Parameters**<br><br><br>* `master_secret_key`: The Primary Key used to generate and validate signatures.<br><br>* `backup_secret_key`: The Backup Key used when validation with the Primary Key fails.<br><br>* `sign_name`: Specifies the name of the signature parameter.<br><br>* `duration`: Specifies the Signature Validity Period in seconds.<br><br>* `time_format`: Specifies the timestamp format. The value is `dec`, a decimal Unix timestamp in seconds.<br><br>* `algorithm`: Specifies the Signing Algorithm. Valid values: `md5` and `sha256`.<br><br>* `origin_keep_auth_query`: Determines whether signature parameters are retained in Origin requests and the cache key. Valid values: `true` and `false`.<br><br>* `rewrite_m3u8`: Determines whether to enable HLS Manifest Signing for M3U8 playlists. Valid values: `true` and `false`.<br><br>* `keep_slice_query`: Determines whether existing query parameters in playlist resource URIs are retained. Valid values: `true` and `false`.<br><br>* `m3u8_keep_query`: Determines whether non\-authentication query parameters in the M3U8 request URL are added to playlist resource URIs. Valid values: `true` and `false`.<br><br>* `rewrite_m3u8_tag`: Specifies additional tags whose child resource URIs are rewritten.<br><br><br>**Type B Configuration Parameters**<br><br><br>* `master_secret_key`, `backup_secret_key`, `duration`, `algorithm`, `rewrite_m3u8`, `keep_slice_query`, `m3u8_keep_query`, `rewrite_m3u8_tag`<br><br>* `time_format`: Specifies the timestamp format. Valid values: `dec`, `hex`, and `basicFormat2m`. `basicFormat2m` uses the `YYYYMMDDHHMM` format.<br><br><br>**Type C Configuration Parameters**<br><br><br>* `master_secret_key`, `backup_secret_key`, `duration`, `algorithm`, `rewrite_m3u8`, `keep_slice_query`, `m3u8_keep_query`, `rewrite_m3u8_tag`<br><br>* `time_format`: Specifies the timestamp format. The value is `hex`, a hexadecimal Unix timestamp in seconds.<br><br><br>**Type D Configuration Parameters**<br><br><br>* `master_secret_key`, `backup_secret_key`, `sign_name`, `time_name`, `duration`, `algorithm`, `origin_keep_auth_query`, `rewrite_m3u8`, `keep_slice_query`, `m3u8_keep_query`, `rewrite_m3u8_tag`<br><br>* `time_format`: Specifies the timestamp format. Valid values: `dec` and `hex`.<br><br>* `time_name`: Specifies the name of the timestamp parameter.<br><br><br>**Type E Configuration Parameters**<br><br><br>* `master_secret_key`, `backup_secret_key`, `sign_name`, `time_name`, `duration`, `algorithm`, `rewrite_m3u8`, `keep_slice_query`, `m3u8_keep_query`, `rewrite_m3u8_tag`<br><br>* `time_format`: Specifies the timestamp format. Valid values: `dec` and `hex`.<br><br>* `custom_headers`: Specifies custom request headers to include in signature calculation. You can specify up to 50 headers.<br><br>* `custom_queries`: Specifies query parameters to include in signature calculation. You can specify up to 50 parameters.<br><br>* `signature_rules`: Defines the order of items in signature calculation. `signature_rules` can include `referer`, `origin`, `secret_key`, `domain`, `uri`, `ip`, `ua`, `time_name`, and the request headers and query parameters defined in `custom_headers` and `custom_queries`. `uri` is the request URL path, excluding query parameters. `time_name` is the timestamp parameter. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_3ae398c73b502830e7d5c3bb7917a718.json" name="type-a.json">type-a.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b5fe383bbfaae4c4f390346f6bf84439.json" name="type_b.json">type_b.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_4f8930053c49164c8dc3d8208da23e69.json" name="type_c.json">type_c.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_b61a3d5d2a1cf109e90c979f86960bc8.json" name="type_d.json">type_d.json</Attachment><br><br><br>&nbsp;<br><br><Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_a33dba9f893d5c7f61b2db3714f94d4f.json" name="type-e.json">type-e.json</Attachment><br> |


<span id="cache-stage"></span>
### cache Stage


|**Action** |**Configuration Parameters** |**Example** |
|---|---|---|
|`cache_key` |When `Dimension` is `query_string`, this setting specifies how query parameters in the request URL are handled. The cache key includes all query parameters by default. The following configuration parameters are available:<br><br><br>* `query_action`: Specifies which query parameters to include. Valid values: `include_part`, `include_all`, `exclude_part`, and `exclude_all`.<br><br>* `query_names`: Parameters to include or remove. Applies when `query_action` is `include_part` or `exclude_part`.<br><br>* `ignore_case`: Whether query parameter names are case\-sensitive.<br><br><br>&nbsp;<br><br>When `Dimension` is `request_header`, this specifies how headers in the request are handled. The cache key does not include any headers by default. The following configuration parameters are available:<br><br><br>* `header_names`: The list of headers to include.<br><br>* `ignore_case`: Whether header names are case\-sensitive. The value must be `true`.<br><br><br>&nbsp;<br><br>When `Dimension` is `cookie`, this specifies how cookies in the request are handled. The cache key does not include any cookies by default. The following configuration parameters are available:<br><br><br>* `cookie_action`: How cookies in the Client request are handled. Valid values: `include_part`, `include_all`, `exclude_part`, and `exclude_all`.<br><br>* `cookie_names`: The list of cookies to include. The list contains the keys of the cookies.<br><br>* `ignore_case`: Whether cookie keys are case\-sensitive.<br><br><br>&nbsp;<br><br>When `Dimension` is `request_path`, this specifies whether the original path is rewritten. The original path is not rewritten by default. The following configuration parameters are available:<br><br><br>* `source_path`: The original path, matched by a regular expression.<br><br>* `target_path`: The rewritten path. Use `$n` to reference a capture group in the original path.<br><br><br>&nbsp;<br><br>When `Dimension` is `path_ignore_case`, this specifies whether the path in the cache key is case\-sensitive. It is case\-insensitive by default. The following configuration parameters are available:<br><br><br>* `ignore_case`: Whether the path in the cache key is case\-sensitive.<br><br><br> |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_03ae9096555995f285cb21a33f24e239.json" name="cache_key">cache_key</Attachment><br> |
|`compression` |* `methods`: The compression algorithm. Valid values: `br` and `gzip`.<br><br>* `min_file_size`: The minimum file size. Files smaller than this size are not compressed.<br><br>* `min_file_size_unit`: The size unit. Valid values: `KB` and `MB`.<br><br>* `format`: The file type configuration. The CDN compresses only files of the specified types. Valid values: `default` and `customize`. `default` indicates all types in the `content_types` list.<br><br>* `content_types`: The specified file types. Applies when `format` is `customize`. Valid values: `text/html`, `text/plain`, `text/xml`, `text/css`, `application/javascript`, `application/x-javascript`, `application/rss+xml`, `application/json`, `image/tiff`, `text/javascript`, `image/svg+xml`, `application/xml`, `text/plain; charset=utf-8`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_ea52d7a5b797b0adf65c90403fa4cedd.json" name="compression">compression</Attachment><br> |
|`video_drag` |* `switch`: Whether to enable video seeking. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_5c85937d97bbf2841da168c5f33d0e6d.json" name="video_drag">video_drag</Attachment><br> |
|`cache_time` |* `ttl`: Specifies the cache lifetime (TTL). Applies when `cache_policy` is `default`.<br><br>* `ttl_unit`: Specifies the unit of the cache lifetime. Valid values: `sec`, `min`, `hour`, and `day`. Applies when `cache_policy` is `default`.<br><br>* `cache_policy`: Specifies the caching behavior. Valid values: `default`, `origin_first`, and `no_cache`.<br><br>* `force_cache`: Determines whether to enable Force Cache. Applies when `cache_policy` is `default`.<br><br>* `replenish`: Determines whether CDN uses the configured cache lifetime when the Origin response includes neither `Cache-Control` nor `Expires`. Applies when `cache_policy` is `origin_first`.<br><br>* `set_cookie_no_cache`: Determines whether to cache Origin responses that include the `Set-Cookie` header. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f5b20c40df5a15b2396da1c7cd6dceab.json" name="cache_time">cache_time</Attachment><br> |


<span id="client-response-stage"></span>
### client_response Stage


|**Action** |**Configuration Parameters** |**Example** |
|---|---|---|
|`response_header` |* `action`: The Client Response Headers operation performed when the CDN responds to a client request. Valid values: `set` and `delete`.<br><br>* `header_name`: The header name.<br><br>* `header_value`: The header value. Applies when `action` is `set`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_19c29be2af0dd5a170d32f19d8d095ff.json" name="response_header">response_header</Attachment><br> |
|`browser_cache` |* `cache_policy`: The Browser Caching policy. Valid values: `cache`, `origin_first`, and `no_cache`.<br><br><br>When `cache_policy` is `cache`, you must also configure:<br><br><br>* `ttl`: The cache duration, up to 10 years.<br><br>* `ttl_unit`: The duration unit. Valid values: `sec`, `min`, `hour`, and `day`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_3803a1f675d2d36d62c4011e422d043a.json" name="browser_cache.json">browser_cache.json</Attachment><br> |
|`http_code` |* `status_code`: A custom CDN response status code, in the range 100–999. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_fec6c7abf0691beff86c81c0f1d2eab3.json" name="http_code.json">http_code.json</Attachment><br> |
|`custom_page` |* `page_mode`: The value must be `redirection`, which indicates page redirection.<br><br>* `status_code`: The CDN response status code. Valid values: `301`, `302`, `303`, `307`, and `308`.<br><br>* `location`: The redirect URL. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload\_4db381c7252d3a785e97184575561aaa.json" name="custom_page.json">custom_page.json</Attachment><br> |


<span id="origin-request-stage"></span>
### origin_request Stage


|**Action** |**Configuration Parameters** |**Example** |
|---|---|---|
|`origin_range` |* `switch`: Whether to enable Range Origin Fetch.<br><br>* `range_type`: The segment type. The only valid value is `fixed`, which indicates fixed\-size segments.<br><br>* `range_size`: The segment size.<br><br>   * If `unit` is `KB`, `range_size` can only be `512`.<br><br>   * If `unit` is `MB`, the valid range of `range_size` is 1–40.<br><br>* `unit`: The segment unit. Valid values: `KB` and `MB`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_64df7cb3754d8b9bd5eac4dc2060d894.json" name="origin_range.json">origin_range.json</Attachment><br> |
|`origin_follow` |* `switch`: Whether to enable Redirect Follow for Origin requests. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7bff59be74c35e9cbe81238f9167fa1d.json" name="origin_follow">origin_follow</Attachment><br> |
|`origin_tcp_timeout` |* `connect_timeout`: The timeout period for TCP connection establishment. The default value is `2`.<br><br>* `connect_timeout_unit`: The timeout unit. The only valid value is `sec`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_08d39bc3afcddaa53d1a1830e572425c.json" name="origin_tcp_timeout">origin_tcp_timeout</Attachment><br> |
|`origin_http_timeout` |* `connect_timeout`: The timeout period for HTTP requests. The default value is `60`.<br><br>* `connect_timeout_unit`: The timeout unit. The only valid value is `sec`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_7749919155603107989f0d97cacd02ce.json" name="origin_http_timeout.json">origin_http_timeout.json</Attachment><br> |
|`origin_rewrite` |* `action`: Specifies the rewrite type. Valid values:<br><br>   * `path_rewrite`: Rewrites the path, excluding query parameters.<br><br>   * `url_rewrite`: Rewrites the path, including query parameters.<br><br>* `source_path`: A regular expression, up to 1,024 characters long, that matches the path in the client request URL.<br><br>* `target_path`: The rewritten path in the Origin request URL, up to 1,024 characters long. You can use `$1`, `$2`, `$3`, and similar references to capture groups defined in `source_path`.<br><br>* `mode`: Specifies what happens after a rewrite rule matches. The only valid value is `break`, which stops matching subsequent rewrite rules. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_10c7424a8861b203467208c34865f69f.json" name="origin_rewrite.json">origin_rewrite.json</Attachment><br> |
|`origin_sni` |* `domain`: The custom SNI domain name. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_502d9ab2b1b7addcc7c54fa31498cf82.json" name="origin_sni.json">origin_sni.json</Attachment><br> |
|`origin_protocol` |* `origin_protocol`: The protocol used for Origin requests. Valid values: `follow_client`, `http`, and `https`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_bdfdaaa95f0a0efe41a87f6d54ca2991.json" name="origin_protocol.json">origin_protocol.json</Attachment><br> |
|`origin_request_header` |* `action`: The Origin Request Headers operation. Valid values: `set` and `delete`.<br><br>* `header_name`: The header name.<br><br>* `header_value`: The header value. Applies when `action` is `set`. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_9879c889c26a7ceda887251af1a7e1a8.json" name="origin_request_header.json">origin_request_header.json</Attachment><br> |
|`origin_host` |* `host`: The Host header value in the Origin request. |<Attachment link="https://portal.volccdn.com/obj/volcfe/cloud-universal-doc/upload_f7fcb1327bda9210a128a8361054f62d.json" name="origin_host.json">origin_host.json</Attachment><br> |


<span id="input-requirements-for-each-match-object"></span>
## Input Requirements for Each Match Object


|**Match Object** |**IgnoreCase** |**Supported Operators** |**Name Input Requirements** |**Value Input Requirements** |**Example Values** |
|---|---|---|---|---|---|
|`always` |Not applicable |Not applicable |Not applicable |Not applicable | |
|`path` |Applicable |`equal` `not_equal` |Not applicable |* Must start with `/`.<br><br>* The total number of entries cannot exceed 100, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%). |`["/www/img/myimage.png", "/docs/file"]` |
|||`prefix_match` `prefix_not_match` ||* Must start with `/`.<br><br>* The total number of entries cannot exceed 100, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%) |`["/www", "/docs/f"]` |
|||`suffix_match` `suffix_not_match` ||* The total number of entries cannot exceed 100, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%).<br><br>* Cannot start with a period (.). |`["png","docx"]` |
|||`regex_match` `regex_not_match` ||* The total number of entries cannot exceed 50, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%). |`["^/a{1,2}(.*)g$"]` |
|||`belong_to` `not_belong_to` ||Specify a Universal Catalog that meets the following conditions:<br><br><br>* `ConfigType` is `common_match_list`.<br><br>* `CommonListType` is `exact_match` or `regex_match`. |`["MySharedList"]` |
|`path_and_param` |Applicable |Same as `path`. |Not applicable |Same as `path`. | |
|`url` |Applicable |`equal` `not_equal` |Not applicable |* Must start with `http://` or `https://`.<br><br>* The total number of entries cannot exceed 100, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%). |`["https://www.example.com/www/img/myimage.png","https://www.example.com/docs/file"]` |
|||`prefix_match` `prefix_not_match` ||* Must start with `http://` or `https://`.<br><br>* The total number of entries cannot exceed 100, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%). |`["https://www.example.com/www", "https://www.example.com/docs/f"]` |
|||`suffix_match` `suffix_not_match` ||* The total number of entries cannot exceed 100, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%). |`["png","docx"]` |
|||`regex_match` `regex_not_match` ||* The total number of entries cannot exceed 50, and the total length cannot exceed 300 characters.<br><br>* Cannot contain spaces or percent signs (%). |`["^/a{1,2}(.*)g$"]` |
|||`belong_to` `not_belong_to` ||Specify a Universal Catalog that meets the following conditions:<br><br><br>* `ConfigType` is `common_match_list`.<br><br>* `CommonListType` is `exact_match` or `regex_match`. |`["MySharedList"]` |
|`http_referer` |Applicable |`equal` `not_equal` |Not applicable |* The total number of entries cannot exceed 100.<br><br>* Each entry cannot exceed 200 characters in length. |`["https://www.example.com/image.png", "a.example.com","*.exampe.net","203.0.113.8"]` |
|||`exist` `not_exist` ||Not applicable | |
|||`regex_match` `regex_not_match` ||* The total number of entries cannot exceed 50.<br><br>* Each entry cannot exceed 200 characters in length. |`["^/a{1,2}(.*)g$"]` |
|||`belong_to` `not_belong_to` ||Specify a Universal Catalog that meets the following conditions:<br><br><br>* `ConfigType` is `common_match_list`.<br><br>* `CommonListType` is `exact_match` or `regex_match`. |`["MySharedList"]` |
|`client_ip` |Not applicable |`match` `not_match` |Not applicable |* Supports IP addresses and CIDR blocks.<br><br>* Supports IPv4 and IPv6 addresses.<br><br>* The total number of entries cannot exceed 100. |`["203.0.113.8","203.0.113.9"]` |
|||`belong_to` `not_belong_to` ||Specify a Universal Catalog that meets the following conditions:<br><br><br>* `ConfigType` is `common_match_list`.<br><br>* `CommonListType` is `ip_match`. |`["MySharedList"]` |
|`http_origin` |Applicable |Same as `http_referer`. |Not applicable |Same as `http_referer`. | |
|`http_ua` |Applicable |Same as `http_referer`. |Not applicable |Same as `http_referer`. | |
|`request_header` |Applicable |Same as `http_referer`. |* Cannot contain Chinese characters, underscores（_）, spaces, double quotation marks（"）, or colons（:）.<br><br>* Cannot exceed 100 characters in length. |Same as `http_referer`. |**Name**<br><br>`myheader`<br><br>**Value**<br><br>`["value1","value2"]` |
|`client_area` |Not applicable |`match` `not_match` |Not applicable |* Specify up to 30 Alpha\-3 codes for countries or regions. Call [DescribeCdnRegionAndIsp](https://docs.byteplus.com/en/docs/byteplus-cdn/DescribeCdnRegionAndIsp-en) to obtain Alpha\-3 codes. |`["PNG","FSM","FSM"]` |
|`http_method` |Not applicable |`equal` `not_equal` |Not applicable |* Includes one or more of the following values: `post`, `head`, `get`, `put`, `options`, `delete`, `connect`, and `patch`. |`["post","options"]` |
|`request_time` |Not applicable |`match` `not_match` |`weekday`: Specific days of the week. |* Includes one or more of the following values: `mon`, `tue`, `wed`, `thur`, `fri`, `sat`, and `sun`. |`["mon","fri"]` |
||||`period`: Any time period. |The start and end times are specified to the second. |`["2025-05-07 14:21:21", "2025-06-13 14:21:24"]` |
||||`everyday`: A time period within a day. ||`["02:02:02","06:04:04"]` |
|`protocol` |Not applicable |`equal` `not_equal` |Not applicable |Specify `http` or `https`. |`["http"]` |
|`client_cert_info` |Applicable |`match` `not_match` |`common_name`: The Common Name in the certificate subject. |The total number of entries cannot exceed 100, each entry cannot exceed 64 characters in length, and wildcards `*` are supported at the beginning and end. |`["www.example.com"]` |
||||`serial_number`: The certificate serial number. ||`["03A7F2C91B4E6D8A"]` |
||||`country_name`: The code for the country or region of the certificate subject. ||`["CN"]` |
||||`locality_name`: The city or locality of the certificate subject. ||`["Beijing"]` |
||||`organization_name`: The organization or company name of the certificate subject. ||`["Example Co., Ltd."]` |
||||`organizational_unit_name`: The organizational unit or department name of the certificate subject. ||`["IT Department"]` |
|`response_header` |Applicable |Same as `http_referer`. |* Cannot contain Chinese characters, underscores（_）, spaces, double quotation marks（"）, or colons（:）.<br><br>* Cannot exceed 100 characters in length. |Same as `http_referer`. |**Name**<br><br>`myheader`<br><br>**Value**<br><br>`["value1","value2"]` |
|`http_code` |Not applicable |`match` `not_match` |Not applicable |* Includes up to 30 status codes.<br><br>* Status codes range from 100 to 599.<br><br>* Supports values such as `2xx` and `3xx`. |`["405","5xx"]` |


<span id="response-parameters"></span>
## Response Parameters

<span id="samples"></span>
## Samples

<span id="sample-request"></span>
### Sample request

<span id="sample-1"></span>
#### Sample 1

```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
    "Rule": "{\"IfBlock\":{\"SubRules\":[],\"Actions\":[{\"Action\":\"origin_tcp_timeout\",\"Groups\":[{\"Dimension\":\"origin_tcp_timeout\",\"GroupParameters\":[{\"Parameters\":[{\"Name\":\"connect_timeout\",\"Values\":[\"30\"]},{\"Name\":\"connect_timeout_unit\",\"Values\":[\"sec\"]}]}]}]}],\"Condition\":{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":true,\"Connective\":\"and\",\"ConditionGroups\":[{\"IsGroup\":false,\"Condition\":{\"Object\":\"always\"}}]}]}}}"
}
```


<span id="sample-2"></span>
#### Sample 2

This sample focuses on the configuration of `Condition`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This sample cannot be used directly. You need to process the parameter configuration in the <code>Rule</code> structure first. See the description of the <code>Rule</code> parameter.</div>


```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine-actions",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
    "Rule": [
        {
            "Desc": "myDesc",
            "IfBlock": {
                "SubRules": [
                    {
                        "Desc": "Sub-rule1",
                        "IfBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "set"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader2"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_value",
                                                            "Values": [
                                                                "myheadervalue"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "Condition": {
                                "IsGroup": true,
                                "Connective": "and",
                                "ConditionGroups": [
                                    {
                                        "IsGroup": true,
                                        "Connective": "and",
                                        "ConditionGroups": [
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "always"
                                                }
                                            },
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "path",
                                                    "Operator": "suffix_match",
                                                    "IgnoreCase": true,
                                                    "Value": [
                                                        "param=value"
                                                    ]
                                                }
                                            }
                                        ]
                                    }
                                ]
                            }
                        },
                        "ElseBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "delete"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader3"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "Actions": [
                    {
                        "Action": "response_header",
                        "Groups": [
                            {
                                "Dimension": "response_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "set"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            },
                                            {
                                                "Name": "header_value",
                                                "Values": [
                                                    "myheadervalue"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader1"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "Condition": {
                    "IsGroup": true,
                    "Connective": "and",
                    "ConditionGroups": [
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "always"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "suffix_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "jpg",
                                            "png"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path_and_param",
                                        "Operator": "prefix_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/docs1/",
                                            "/docs2/"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "url",
                                        "Operator": "equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "https://www.example.com/abc/file"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "query_string",
                                        "Name": "myparam",
                                        "Operator": "equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "myvalue",
                                            "myvalue2"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_referer",
                                        "Operator": "not_equal",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "myreferer1",
                                            "myreferere2"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "client_ip",
                                        "Operator": "match",
                                        "Value": [
                                            "1.1.1.1",
                                            "2.2.2.2"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_origin",
                                        "Operator": "exist"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_ua",
                                        "Operator": "not_exist"
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_header",
                                        "Name": "myhttpheader",
                                        "Operator": "regex_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "^abc$",
                                            "^cde$"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "client_area",
                                        "Operator": "not_match",
                                        "Value": [
                                            "PNG",
                                            "FSM"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_method",
                                        "Operator": "equal",
                                        "Value": [
                                            "post",
                                            "head",
                                            "get",
                                            "put",
                                            "options",
                                            "delete",
                                            "connect",
                                            "patch"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "everyday",
                                        "Operator": "match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "02:02:02",
                                            "06:04:04"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "weekday",
                                        "Operator": "not_match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "mon",
                                            "tue",
                                            "wed",
                                            "thur",
                                            "fri",
                                            "sat",
                                            "sun"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "request_time",
                                        "Name": "period",
                                        "Operator": "not_match",
                                        "TimeZone": "+0800",
                                        "Value": [
                                            "2025-05-07 14:21:21",
                                            "2025-06-13 14:21:24"
                                        ]
                                    }
                                }
                            ]
                        },
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "protocol",
                                        "Operator": "equal",
                                        "Value": [
                                            "http"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "response_header",
                                        "Name": "myresponseheader",
                                        "Operator": "regex_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "^resheader1$",
                                            "^resheader2$"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "http_code",
                                        "Operator": "match",
                                        "Value": [
                                            "400",
                                            "500"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "prefix_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/abc/"
                                        ]
                                    }
                                },
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "path",
                                        "Operator": "suffix_not_match",
                                        "IgnoreCase": true,
                                        "Value": [
                                            "/def/"
                                        ]
                                    }
                                }
                            ]
                        }
                    ]
                }
            },
            "ElseBlock": {
                "SubRules": [
                    {
                        "Desc": "规则名称",
                        "IfBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "set"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader6"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_value",
                                                            "Values": [
                                                                "1111"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ],
                            "Condition": {
                                "IsGroup": true,
                                "Connective": "and",
                                "ConditionGroups": [
                                    {
                                        "IsGroup": true,
                                        "Connective": "and",
                                        "ConditionGroups": [
                                            {
                                                "IsGroup": false,
                                                "Condition": {
                                                    "Object": "http_referer",
                                                    "Operator": "exist"
                                                }
                                            }
                                        ]
                                    }
                                ]
                            }
                        },
                        "ElseBlock": {
                            "SubRules": [],
                            "Actions": [
                                {
                                    "Action": "response_header",
                                    "Groups": [
                                        {
                                            "Dimension": "response_header",
                                            "GroupParameters": [
                                                {
                                                    "Parameters": [
                                                        {
                                                            "Name": "action",
                                                            "Values": [
                                                                "delete"
                                                            ]
                                                        },
                                                        {
                                                            "Name": "header_name",
                                                            "Values": [
                                                                "myheader7"
                                                            ]
                                                        }
                                                    ]
                                                }
                                            ]
                                        }
                                    ]
                                }
                            ]
                        }
                    }
                ],
                "Actions": [
                    {
                        "Action": "response_header",
                        "Groups": [
                            {
                                "Dimension": "response_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "MyHeader"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```


<span id="sample-3"></span>
#### Sample 3

This sample focuses on the configuration of `Action`.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This sample cannot be used directly. You need to process the parameter configuration in the <code>Rule</code> structure first. See the description of the <code>Rule</code> parameter.</div>


```json
POST https://cdn.byteplusapi.com/?Action=UpdateRuleEngineTemplate&Version=2021-03-01
{
    "Title": "rulesengine-actions",
    "Message": "new_desc",
    "TemplateId": "tpl-rejjo23",
    "TemplateVersion": "draft",
    "Rule": [
        {
            "Desc": "myDesc",
            "IfBlock": {
                "SubRules": [],
                "Actions": [
                    {
                        "Action": "redirect_request",
                        "Groups": [
                            {
                                "Dimension": "redirect_request",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "source_path",
                                                "Values": [
                                                    "^/docs/file1$"
                                                ]
                                            },
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "301"
                                                ]
                                            },
                                            {
                                                "Name": "protocol",
                                                "Values": [
                                                    "follow_client"
                                                ]
                                            },
                                            {
                                                "Name": "target_host",
                                                "Values": [
                                                    "www.example.com"
                                                ]
                                            },
                                            {
                                                "Name": "target_path",
                                                "Values": [
                                                    "^/cos1/file2$"
                                                ]
                                            },
                                            {
                                                "Name": "target_query_action",
                                                "Values": [
                                                    "include_all"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "allow_access",
                        "Groups": [
                            {
                                "Dimension": "allow_access",
                                "GroupParameters": [
                                    {
                                        "Parameters": []
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "download_speed_limit",
                        "Groups": [
                            {
                                "Dimension": "download_speed_limit",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "rate",
                                                "Values": [
                                                    "100"
                                                ]
                                            },
                                            {
                                                "Name": "rate_unit",
                                                "Values": [
                                                    "B/s"
                                                ]
                                            },
                                            {
                                                "Name": "after_size",
                                                "Values": [
                                                    "15"
                                                ]
                                            },
                                            {
                                                "Name": "after_size_unit",
                                                "Values": [
                                                    "MB"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "request_header",
                        "Groups": [
                            {
                                "Dimension": "request_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "set"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            },
                                            {
                                                "Name": "header_value",
                                                "Values": [
                                                    "myvalue"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "action",
                                                "Values": [
                                                    "delete"
                                                ]
                                            },
                                            {
                                                "Name": "header_name",
                                                "Values": [
                                                    "myheader"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "deny_access",
                        "Groups": [
                            {
                                "Dimension": "deny_access",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "465"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "cache_key",
                        "Groups": [
                            {
                                "Dimension": "query_string",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "exclude_part"
                                                ]
                                            },
                                            {
                                                "Name": "query_names",
                                                "Values": [
                                                    "myparam1",
                                                    "myparam2"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "include_part"
                                                ]
                                            },
                                            {
                                                "Name": "query_names",
                                                "Values": [
                                                    "ff"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "include_all"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    },
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "query_action",
                                                "Values": [
                                                    "exclude_all"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "request_header",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "header_names",
                                                "Values": [
                                                    "myheader",
                                                    "myheader2"
                                                ]
                                            },
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "request_path",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "source_path",
                                                "Values": [
                                                    "^/path1/$"
                                                ]
                                            },
                                            {
                                                "Name": "target_path",
                                                "Values": [
                                                    "^/path2/$"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            },
                            {
                                "Dimension": "path_ignore_case",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "ignore_case",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "compression",
                        "Groups": [
                            {
                                "Dimension": "compression",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "methods",
                                                "Values": [
                                                    "gzip",
                                                    "brotli"
                                                ]
                                            },
                                            {
                                                "Name": "min_file_size",
                                                "Values": [
                                                    "563"
                                                ]
                                            },
                                            {
                                                "Name": "min_file_size_unit",
                                                "Values": [
                                                    "KB"
                                                ]
                                            },
                                            {
                                                "Name": "format",
                                                "Values": [
                                                    "default"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "video_drag",
                        "Groups": [
                            {
                                "Dimension": "video_drag",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "cache_time",
                        "Groups": [
                            {
                                "Dimension": "cache_time",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "ttl",
                                                "Values": [
                                                    "56"
                                                ]
                                            },
                                            {
                                                "Name": "ttl_unit",
                                                "Values": [
                                                    "day"
                                                ]
                                            },
                                            {
                                                "Name": "cache_policy",
                                                "Values": [
                                                    "origin_first"
                                                ]
                                            },
                                            {
                                                "Name": "replenish",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_range",
                        "Groups": [
                            {
                                "Dimension": "origin_range",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_follow",
                        "Groups": [
                            {
                                "Dimension": "origin_follow",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "switch",
                                                "Values": [
                                                    "true"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_tcp_timeout",
                        "Groups": [
                            {
                                "Dimension": "origin_tcp_timeout",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "connect_timeout",
                                                "Values": [
                                                    "56"
                                                ]
                                            },
                                            {
                                                "Name": "connect_timeout_unit",
                                                "Values": [
                                                    "sec"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "origin_http_timeout",
                        "Groups": [
                            {
                                "Dimension": "origin_http_timeout",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "read_timeout",
                                                "Values": [
                                                    "58"
                                                ]
                                            },
                                            {
                                                "Name": "read_timeout_unit",
                                                "Values": [
                                                    "sec"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    },
                    {
                        "Action": "url_auth",
                        "Groups": [
                            {
                                "Dimension": "url_auth",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "auth_type",
                                                "Values": [
                                                    "type_e"
                                                ]
                                            },
                                            {
                                                "Name": "master_secret_key",
                                                "Values": [
                                                    "pk123"
                                                ]
                                            },
                                            {
                                                "Name": "backup_secret_key",
                                                "Values": [
                                                    "bk456"
                                                ]
                                            },
                                            {
                                                "Name": "sign_name",
                                                "Values": [
                                                    "sign"
                                                ]
                                            },
                                            {
                                                "Name": "time_name",
                                                "Values": [
                                                    "ts"
                                                ]
                                            },
                                            {
                                                "Name": "duration",
                                                "Values": [
                                                    "600"
                                                ]
                                            },
                                            {
                                                "Name": "time_format",
                                                "Values": [
                                                    "hex"
                                                ]
                                            },
                                            {
                                                "Name": "algorithm",
                                                "Values": [
                                                    "md5"
                                                ]
                                            },
                                            {
                                                "Name": "rewrite_m3u8",
                                                "Values": [
                                                    "true"
                                                ]
                                            },
                                            {
                                                "Name": "keep_slice_query",
                                                "Values": [
                                                    "true"
                                                ]
                                            },
                                            {
                                                "Name": "m3u8_keep_query",
                                                "Values": [
                                                    "true"
                                                ]
                                            },
                                            {
                                                "Name": "custom_headers",
                                                "Values": [
                                                    "header1",
                                                    "header2"
                                                ]
                                            },
                                            {
                                                "Name": "custom_queries",
                                                "Values": [
                                                    "param1",
                                                    "param2"
                                                ]
                                            },
                                            {
                                                "Name": "signature_rules",
                                                "Values": [
                                                    "secret_key",
                                                    "domain",
                                                    "uri",
                                                    "ip",
                                                    "ua",
                                                    "referer",
                                                    "origin",
                                                    "time_name",
                                                    "header1",
                                                    "header2",
                                                    "param1",
                                                    "param2"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ],
                "Condition": {
                    "IsGroup": true,
                    "Connective": "and",
                    "ConditionGroups": [
                        {
                            "IsGroup": true,
                            "Connective": "and",
                            "ConditionGroups": [
                                {
                                    "IsGroup": false,
                                    "Condition": {
                                        "Object": "always"
                                    }
                                }
                            ]
                        }
                    ]
                }
            },
            "ElseBlock": {
                "SubRules": [],
                "Actions": [
                    {
                        "Action": "redirect_protocol",
                        "Groups": [
                            {
                                "Dimension": "redirect_protocol",
                                "GroupParameters": [
                                    {
                                        "Parameters": [
                                            {
                                                "Name": "status_code",
                                                "Values": [
                                                    "301"
                                                ]
                                            },
                                            {
                                                "Name": "protocol",
                                                "Values": [
                                                    "https"
                                                ]
                                            }
                                        ]
                                    }
                                ]
                            }
                        ]
                    }
                ]
            }
        }
    ]
}
```


<span id="sample-response"></span>
### Sample response
