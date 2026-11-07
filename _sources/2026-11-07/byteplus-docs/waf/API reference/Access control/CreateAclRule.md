---
title: "CreateAclRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/CreateAclRule"
---

You can use the CreateAclRule API to create access control rules and manage access for specified IP addresses. You can configure the corresponding Allowlist and Blocklist.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=CreateAclRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the parameters specific to this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|j-gVMw">必选</span> `Sample value: CreateAclRule`

API name. The current API name is `CreateAclRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|oiS_rh">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**AclType ** <span data-label="purple"> String  </span><span data-api-tag="require|h1A2su">必选</span> `Sample value: Block`

Access control rule type.


* Allow: Allowlist

* Block: Blocklist



**Action ** <span data-label="purple"> String  </span>`Optional` `Sample value: observe`

Action to be performed.


* block: Intercept

* observe: Observe



**Advanced ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Whether to set advanced conditions. The default is No.


* 0: No

* 1: Yes



**Enable ** <span data-label="purple"> Integer  </span><span data-api-tag="require|HYFhYF">必选</span> `Sample value: 1`

Whether to enable the rule.


* 0: Disabled

* 1: Enabled



**HostAddType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|1sv7QB">必选</span> `Sample value: 2`

Domain name addition method.


* 2: Add by domain name group

* 3: Add multiple domain names



**IpAddType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|vuRmbT">必选</span> `Sample value: 4`

IP address addition method.


* 2: Add by IP address group

* 3: Add manually (single or multiple addresses)

* 4: Add by geographic location



**Url ** <span data-label="purple"> String  </span><span data-api-tag="require|gRIOOA">必选</span> `Sample value: /path`

Matching path. Supports wildcard `*`, and `*` can only appear once.


* For a specific URL address, for example, to allow `test.com/test.html`, enter `/test.html`.

* For the entire website, enter `/*`.

* For all addresses matching a path prefix, for example, `/test/*`.



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: --`

Advanced conditions; no configuration required if not set.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Priority of the advanced condition group, used to determine the target's position when displaying the list and setting drag\-and\-drop priority.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|IPvQI_">必选</span> `Sample value: -`

List of subrules in the advanced condition group. Each subrule defines specific matching criteria (such as request headers, client IP, and more) to precisely filter requests that meet the conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|4yHCSS">必选</span> `Sample value: request.header.clientip`

The specific object corresponding to the matching rule. Supported matching objects are as follows:


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

* `request.queryargs.{Key}`: Custom request parameter (replace {Key} with the specific parameter name);

* `request.header.{Key}`: Custom request header (replace {Key} with the specific header name);

* `request.cookie.{Key}`: Custom Cookie (replace {Key} with the specific Cookie name);

* `request.ja3-hash`: JA3 Hash; (applicable only to byteplus\-global regions)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">Do not directly pass generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>, <code>response.header.*</code>, or <code>response.body.*</code>. You must provide a specific Key.</div>




**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|BFfrOa">必选</span> `Sample value: 12`

Enumeration value for the matching object type, used to specify the matching object type of subrules in advanced conditions. Supported values are as follows:


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

* `23`：request.ja3\-hash。 (Applicable only to byteplus\-global regions)



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|LYZhbH">必选</span> `Sample value: 2`

Enumeration value for the matching operator, used to specify the matching method for sub\-rules in advanced conditions. Supported values are as follows:


* `0`: greater than;

* `1`: greater than or equal to;

* `2`: equal to;

* `3`: less than;

* `4`: less than or equal to;

* `5`: not equal to;

* `6`: contains substring;

* `7`: does not contain substring;

* `8`: prefix match;

* `9`: prefix does not match;

* `10`: suffix match;

* `11`: suffix does not match;

* `12`: contains all matching sets;

* `13`: does not contain all matching sets;

* `14`: belongs to matching set;

* `15`: does not belong to matching set;

* `16`: regex match;

* `17`: identified as IP;

* `18`: identified as IPv4;

* `19`: identified as IPv6;

* `20`: identified as private IP;

* `21`: identified as public IP;

* `23`: belongs to IP group;

* `24`: does not belong to IP group;

* `25`: belongs to IP location;

* `26`: does not belong to IP location;

* `27`: contains IP intelligence;

* `28`: belongs to ASN;

* `29`: does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|8dtZYp">必选</span> `Sample value: 0`

Enumerated values for matching attribute data types. The default is `0` (except for special IP identification scenarios). The supported values are as follows:


* `0`: Value. Applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and more.

* `5`: IP. Used only for the following IP identification operations:

   * `17` (identify as IP)

   * `18` (identify as IPv4)

   * `19` (identify as IPv6)

   * `20` (identify as private IP)

   * `21` (identify as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|H-wHuJ">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in the actual matching value as required.




**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Unique ID of the advanced condition group. Not required when creating rules; used only for aggregating related rate limiting rules when displaying the list.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|tvU0QL">必选</span> `Sample value: 1`

Logical relationship between subrules in the advanced condition group. Supported values are as follows:


* `1`: AND;

* `2`: OR.




**IpLocationSubregion ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["Anhui","Guangdong"]`

Geographic location codes for subregions in China. Can be filled in when `IpAddType = 4` (add by geographic location).

You can first call the `GetAreaBlockInfo` API, then find the corresponding `AreaCode` for the target region (`AreaName`) in the `CNAreaInfoList` of the response content and enter it.

For example:


* `Beijing`: Beijing

* `Fujian`: Fujian

* `Gansu`: Gansu


<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">Applicable only to BytePlus WAF service; no configuration required when using BytePlus WAF service.</div>




**IpLocationCountry ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["US","JP"]`

Geolocation codes for countries or regions outside the Chinese mainland; can be specified when `IpAddType = 4` (geolocation addition mode).

You can first call the `GetAreaBlockInfo` API, then find the corresponding `AreaCode` for the target region (`AreaName`) in the `OverSeaAreaInfoList` of the response content and enter it.

For example:


* `US`: United States

* `BR`: Brazil

* `JP`: Japan



**Name ** <span data-label="purple"> String  </span><span data-api-tag="require|2WAkCb">必选</span> `Sample value: Access control 1`

Rule name.


* Must start with a Chinese character, letter, or digit.

* Letters, digits, Chinese characters, dot “.”, underscore “_”, and hyphen “\-” are allowed.

* Length must be 1–128 characters.



**Description ** <span data-label="purple"> String  </span>`Optional` `Sample value: Block access from specific IPs.`

Rule description, which can be left empty. If not empty, it must meet the following requirements.


* Must start with a Chinese character, letter, or number

* Letters, numbers, Chinese characters, period “.”, space, underscore “_”, hyphen “\-”, equals sign “=”, English comma “,”, Chinese comma “，” and Chinese period “。” are allowed

* Length must be 0–255 characters



**HostGroupId ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [7436]`

Domain group ID. Required when `HostAddType = 2` (domain group addition mode). Refer to [Query Domain Group](https://docs.byteplus.com/en/docs/waf/ListHostGroup) to obtain the domain group ID.



**HostList ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["example.volcwaf001.com","example.volcwaf002.com"]`

Required when `HostAddType = 3` (multi\-domain addition mode). Supports single or multiple domains.



**IpGroupId ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [6283]`

Required when `IpAddType = 2` (IP address group addition mode); refer to [Query all IP address groups](https://docs.byteplus.com/en/docs/waf/ListAllIpGroups) to obtain the IP address group ID.



**IpList ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["192.1.1.1","192.1.1.2"]`

Required when `IpAddType = 3` (multiple address addition mode); supports single or multiple IP addresses.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the project resource to which it belongs.



**PermitFeature ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: -`

List of allowlist protection rules. If empty, all requests are allowed by default. Once allowed, related requests will no longer be checked by the corresponding rules.

The supported values are as follows:


* `allowlist`: Allow all access.

* `blocklist`: Blocklist.

* `geo_black`: Geographic location access control.

* `api_route`: Unregistered API detection.

* `api_schema`: API protection parameter validation.

* `api_sensitive`: API sensitive information protection.

* `bot_dytoken`: BOT dynamic token.

* `bot_frequency`: BOT frequency limit.

* `bot_repeat`: BOT statistical protection.

* `bot_sequence`: BOT behavior map.

* `user_ua_bot`: BOT custom rule.

* `bot_ua_system`: BOT managed rule.

* `httpflood`: Rate limiting custom rule.

* `vuln_signature`: Vulnerability protection.

* `scan_freqvuln`: High\-frequency scanning.

* `scan_direnum`: Directory traversal.

* `bot_session_protection`: BOT session protection.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**id ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Rule ID after creation or update.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to obtain more information about error codes.

&nbsp;
