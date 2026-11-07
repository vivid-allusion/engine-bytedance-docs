---
title: "UpdateAclRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateAclRule"
---

After access control rules are added, call the UpdateAclRule API to modify API information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateAclRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|0WOzv-">必选</span> `Sample value: UpdateAclRule`

API name. The name of the current API is `UpdateAclRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|5VU64z">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**AclType ** <span data-label="purple"> String  </span><span data-api-tag="require|E938Yg">必选</span> `Sample value: Block`

Access control rule type.


* Allow: Allowlist

* Block: Blocklist



**Action ** <span data-label="purple"> String  </span>`Optional` `Sample value: observe`

Execute an action.


* block: intercept

* observe: observe



**Advanced ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Whether to set advanced conditions. The default is no.


* 0: no

* 1: yes



**Description ** <span data-label="purple"> String  </span>`Optional` `Sample value: Deny specific IP access.`

Rule description.



**Enable ** <span data-label="purple"> Integer  </span><span data-api-tag="require|TvEupj">必选</span> `Sample value: 1`

Whether to enable the rule.


* 0: Disabled

* 1: Enabled



**HostAddType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|P6fAWk">必选</span> `Sample value: 2`

Domain addition method.


* 2: Add domain group

* 3: Add multiple domains



**HostGroupId ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [7436,7515]`

Domain group ID. When `HostAddType = 2` (domain group addition method), this field must be filled in. Refer to [query domain group](https://docs.byteplus.com/en/docs/waf/ListHostGroup) to obtain the domain group ID.



**HostList ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["*.4399.com","www.test.com"]`

Domain name information, must be specified when `HostAddType = 3` (multi\-domain addition mode), and at least two domain names must be provided.



**ID ** <span data-label="purple"> Integer  </span><span data-api-tag="require|vpc2s2">必选</span> `Sample value: 126217`

The rule ID to be edited, which can be obtained via [Query access control rules](https://docs.byteplus.com/en/docs/waf/ListAclRule).



**IpAddType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|Yiln--">必选</span> `Sample value: 4`

IP address addition method.


* 2: IP address group addition

* 3: Manual addition (single or multiple addresses)

* 4: Geographic location addition



**IpGroupId ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [6283,7515]`

IP address group ID. Required when `IpAddType = 2` (IP address group addition mode). Refer to [query all IP address groups](https://docs.byteplus.com/en/docs/waf/ListAllIpGroups) to obtain the IP address group ID.



**IpList ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["192.1.**.**","192.2.**.**"]`

IP addresses, must be specified when `IpAddType = 3` (multi\-address addition mode), and at least two IP addresses must be provided.



**IpLocationCountry ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["US","JP"]`

Geolocation code for subregions in China. This field can be filled in when `IpAddType = 4` (geolocation addition method).

You can first call the `GetAreaBlockInfo` API, and then find the `CNAreaInfoList` in the response. Locate the target region (`AreaName`) and enter the corresponding `AreaCode`.

For example:


* `Beijing`: Beijing

* `Fujian`: Fujian

* `Gansu`: Gansu


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Applicable only to BytePlus WAF service. No configuration is required when using BytePlus WAF service.</div>




**IpLocationSubregion ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["Anhui","Guangdong"]`

Geolocation codes for countries or regions outside the Chinese mainland, can be specified when `IpAddType = 4` (geolocation addition method).

You can first call the `GetAreaBlockInfo` API, and then find the target region (`AreaName`) and its corresponding `AreaCode` in the `OverSeaAreaInfoList ` of the response, and fill it in.

For example:


* `US`: United States

* `BR`: Brazil

* `JP`: Japan



**Name ** <span data-label="purple"> String  </span><span data-api-tag="require|phmoOl">必选</span> `Sample value: Access Control 1`

Rule name.


* Must start with a Chinese character, letter, or digit

* Letters, digits, Chinese characters, period '.', underscore '_', and hyphen '\-' are allowed

* Length must be 1–128 characters



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: --`

Details of advanced conditions.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The priority of the advanced condition group, used to determine the target position when dragging for priority in the list display.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|RmiGVW">必选</span> `Sample value: -`

List of sub\-rules in the advanced condition group. Each sub\-rule defines specific matching criteria (such as request headers, client IP, and more) for precisely filtering requests that meet the conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|Zgh46g">必选</span> `Sample value: request.header.clientip`

The specific object corresponding to the matching rule. The supported matching objects are as follows:


* `request.schema`: Request protocol;

* `request.uri`: Request URI;

* `request.method`: Request method;

* `request.path`: Request path;

* `request.queryargs`: Request parameters;

* `request.header`: Request header;

* `request.header.ua`: Request User\-Agent;

* `request.header.refer`: Request referer;

* `request.header.cookie`: Request Cookie header;

* `request.header.content-length`: Request body length;

* `request.header.content-type`: Request body format;

* `request.header.x-forwarded-for`：X\-Forwarded\-For；

* `request.header.clientip`: Client IP;

* `request.queryargs.{Key}`: Custom request parameters (replace {Key} with the specific parameter name);

* `request.header.{Key}`: Custom request header (replace {Key} with the specific header name);

* `request.cookie.{Key}`: Custom Cookie (replace {Key} with the specific Cookie name);

* `request.ja3-hash`: JA3 Hash; (applicable only to the byteplus\-global region)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Do not directly pass generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>, <code>response.header.*</code>, or <code>response.body.*</code>; you must include a specific Key.</div>




**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|ICE8Xp">必选</span> `Sample value: 12`

Enumeration value for the match object data type, used to specify the match object data type for sub\-rules in advanced conditions. Supported values are as follows:


* `0`：request.schema；

* `1`：request.uri；

* `2`：request.method；

* `3`：request.path；

* `4`：request.queryargs；

* `5`：request.header；

* `6`：request.header.ua；

* `7`：request.header.refer；

* `8`：request.header.cookie；

* `9`：request.header.content\-length；

* `10`：request.header.content\-type；

* `11`：request.header.x\-forwarded\-for；

* `12`：request.header.clientip；

* `13`：request.queryargs.{Key}；

* `14`：request.header.{Key}；

* `15`：request.cookie.{Key}；

* `23`：request.ja3\-hash。 (Applicable only to the byteplus\-global region)



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|sUx3PT">必选</span> `Sample value: 2`

The enumeration value of the matching operator, used to specify the matching method for subrules in advanced conditions. Supported values are as follows:


* `0`: Greater than;

* `1`: Greater than or equal to;

* `2`: Equal to;

* `3`: Less than;

* `4`: Less than or equal to;

* `5`: Not equal to;

* `6`: Contains substring;

* `7`: Does not contain substring;

* `8`: Prefix match;

* `9`: Prefix does not match;

* `10`: Suffix match;

* `11`: Suffix does not match;

* `12`: Contains all matching set;

* `13`: Does not contain all matching set;

* `14`: Belongs to matching set;

* `15`: Does not belong to matching set;

* `16`: Regex match;

* `17`: Identified as IP;

* `18`: Identified as IPv4;

* `19`: Identified as IPv6;

* `20`: Identified as private IP;

* `21`: Identified as public IP;

* `23`: Belongs to IP group;

* `24`: Does not belong to IP group;

* `25`: Belongs to IP location;

* `26`: Does not belong to IP location;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|-pm_AX">必选</span> `Sample value: 0`

Enumeration value for the property data type to match. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most match object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|2myePI">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the match object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the match object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, it must be filled in according to the actual matching value.




**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The unique identifier ID of the advanced condition group. It is not required when creating rules and is only used for aggregating related Rate limiting rules in the list display.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|J9jIOK">必选</span> `Sample value: 1`

The logical relationship between subrules in an advanced condition group. Supported values are as follows:


* `1`: AND;

* `2`: OR.




**Url ** <span data-label="purple"> String  </span><span data-api-tag="require|genTSb">必选</span> `Sample value: /path`

Matching path. Wildcard `*` is supported, and `*` can appear only once.


* For a specific URL address, for example, to allow `test.com/test.html`, enter `/test.html`.

* For the entire website, enter `/*`.

* For all addresses matching a certain path prefix, for example, `/test/*`.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project resource name.



**PermitFeature ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: -`

List of protection rules allowed by the allowlist. If empty, all are allowed by default. After allowing, related requests will no longer be checked by the corresponding rules.

Supported values are as follows:


* `allowlist`: Allow all access;

* `blocklist`: Blocklist;

* `geo_black`: Geographic access control;

* `api_route`: Unregistered API detection;

* `api_schema`: API protection parameter validation;

* `api_sensitive`: API sensitive information protection;

* `bot_dytoken`: BOT dynamic token;

* `bot_frequency`: BOT frequency limit;

* `bot_repeat`: BOT statistics protection;

* `bot_sequence`: BOT behavior map;

* `user_ua_bot`: BOT custom rule;

* `bot_ua_system`: BOT managed rule;

* `httpflood`: CC custom rule;

* `vuln_signature`: Vulnerability protection;

* `scan_freqvuln`: High\-frequency scanning;

* `scan_direnum`: Directory traversal;

* `bot_session_protection`: BOT session protection.



&nbsp;

<span id="3Itjc4Uw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id="q98adxVP"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to obtain more information about error codes.
