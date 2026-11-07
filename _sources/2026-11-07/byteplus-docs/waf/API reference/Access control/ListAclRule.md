---
title: "ListAclRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListAclRule"
---

The ListAclRule API is used to query detailed information about access control rules. You must specify whether the rule type to be queried is a Blocklist or an Allowlist.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListAclRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|gp5cGF">必选</span> `Sample value: ListAclRule`

API name. The current API name is `ListAclRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|Zo4Ie2">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**AclType ** <span data-label="purple"> String  </span><span data-api-tag="require|PfvpHn">必选</span> `Sample value: Block`

Access control rule data type.


* Allow: Allowlist

* Block: Blocklist



**Action ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["observe"]`

Action to execute.


* block: Intercept

* observe: Observe



**DefenceHost ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["example.volcwaf002.com"]`

The list of domains to query.



**Enable ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [1]`

The enable status of the rule.


* 0: Disabled

* 1: Enabled



**Page ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Query page number. The default is 1.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

Number of items per page. The default is 10. The range is 1 ~ 100.



**RuleName ** <span data-label="purple"> String  </span>`Optional` `Sample value: Access control 1`

Rule name, supports fuzzy search.



**RuleTag ** <span data-label="purple"> String  </span>`Optional` `Sample value: B000000116869`

Unique rule identifier, supports exact search.



**TimeOrderBy ** <span data-label="purple"> String  </span>`Optional` `Sample value: ASC`

List display order.


* ASC: Sorted by update time in ascending order, with the most recently updated items at the top of the list.

* DESC: Sorted by update time in descending order, with the most recently updated items at the bottom of the list.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the associated project resource.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Rules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of ACL rules, where each element represents a specific ACL rule.


**AccurateGroup ** <span data-label="purple"> Object  </span>`Sample value: -`

Advanced conditions. This field is not required if not configured.


**accurateRules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of sub\-rules in advanced conditions. Each sub\-rule defines specific matching criteria, including matching object, data type, operator, property, and matching value.


**HttpObj ** <span data-label="purple"> String  </span>`Sample value: request.header.clientip`

The specific object corresponding to the matching rule. The supported matching objects are as follows:


* `request.schema`: Request protocol;

* `request.uri`: Request URI;

* `request.method`: Request method;

* `request.path`: Request path;

* `request.queryargs`: request parameters;

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


<div data-tips="true" data-tips-type="default">Generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>, <code>response.header.*</code>, and <code>response.body.*</code> cannot be passed directly; a specific Key must be provided.</div>




**ObjType ** <span data-label="purple"> Integer  </span>`Sample value: 12`

Enumeration value of the matching object type, used to specify the matching object type of sub\-rules in advanced conditions. The supported values are as follows:


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

* `23`：request.ja3\-hash。 (applicable only to byteplus\-global regions)



**Opretar ** <span data-label="purple"> Integer  </span>`Sample value: 2`

The enumeration value of the matching operator, used to specify the matching method for sub\-rules in advanced conditions. Supported values are as follows:


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

* `12`: Contains all matching sets;

* `13`: Does not contain all matching sets;

* `14`: Belongs to matching set;

* `15`: Does not belong to matching set;

* `16`: Regex match;

* `17`: Identified as IP;

* `18`: Identified as IPv4;

* `19`: Identified as IPv6;

* `20`: Identified as private IP;

* `21`: Identified as public IP;

* `23`: Belongs to IP address group;

* `24`: Does not belong to IP address group;

* `25`: Belongs to IP geolocation;

* `26`: Does not belong to IP geolocation;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Enumeration value for the matching property type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span>`Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field indicates the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in the actual matching value as required.




**id ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The actual ID corresponding to advanced conditions. This does not need to be included when creating, but is used for aggregation display in the list view.



**logic ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Logical relationship:


* 1: AND

* 2: OR




**Action ** <span data-label="purple"> String  </span>`Sample value: block`

Action to execute:


* block: Intercept

* observe: Observe



**AddSrc ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Reserved field, no actual meaning.



**Advanced ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Whether to enable advanced conditions:


* 0: Disabled

* 1: Enabled



**ClientIp ** <span data-label="purple"> String  </span>`Sample value: IPLIST_DEMO`

Client IP information to which the rule applies.



**Description ** <span data-label="purple"> String  </span>`Sample value: ACL rule example`

Rule description.



**Enable ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Whether to enable this rule:


* 0: Disabled

* 1: Enabled



**Host ** <span data-label="purple"> String  </span>`Sample value: www.example.com`

The domain to which the rule applies.



**HostAddType ** <span data-label="purple"> Integer  </span>`Sample value: 2`

Domain addition method


* 2: Domain group

* 3: Manually enter one or more domains



**HostGroupId ** <span data-label="purple"> Integer[]  </span>`Sample value: [8561]`

When the domain name addition method (`HostAddType`) is `2` (domain group addition method), returns the list of domain group IDs.



**HostGroups ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of detailed domain group information returned when the domain addition method (`HostAddType`) is `2` (domain group addition method).


**HostGroupId ** <span data-label="purple"> Integer  </span>`Sample value: 8561`

The unique ID of the domain group. When the domain addition method for the ACL rule (`HostAddType`) is `2` (domain group addition), this is the domain group ID returned in the detailed information of the domain group.



**Name ** <span data-label="purple"> String  </span>`Sample value: FooName`

The name of the domain group. When the domain addition method for the ACL rule (`HostAddType`) is `2` (domain group addition), this is the domain group name returned in the detailed information of the domain group.




**HostList ** <span data-label="purple"> String[]  </span>`Sample value: ["www.example.com"]`

When the domain addition method (`HostAddType`) is `3` (multiple domain addition mode), the returned domain list contains multiple domains for which the ACL rule is effective.



**ID ** <span data-label="purple"> Integer  </span>`Sample value: 259227`

The unique identifier of the ACL rule, used to uniquely identify each rule.



**IpAddType ** <span data-label="purple"> Integer  </span>`Sample value: 3`

IP addition method. The supported values are as follows.


* `2`: IP address group;

* `3`: Multiple IPs;

* `4`: Geolocation.



**IpGroupId ** <span data-label="purple"> Integer[]  </span>`Sample value: [17401]`

When the IP addition method (`IpAddType`) is `2` (IP address group addition mode), the returned list contains the IDs of the IP address groups.



**IpGroups ** <span data-label="purple"> Object[]  </span>`Sample value: -`

When the IP addition method (`IpAddType`) is `2` (IP address group addition mode), this returns the detailed information list of IP address groups, where each element contains the IP address group ID and name.


**IpGroupId ** <span data-label="purple"> Integer  </span>`Sample value: 17401`

The unique ID of the IP address group. When the IP addition method for the ACL rule (`IpAddType`) is `2` (IP address group addition mode), this is the IP address group ID returned in the detailed information of the IP address group.



**Name ** <span data-label="purple"> String  </span>`Sample value: AllowIPGroup001`

The name of the IP address group, used to identify the group. This field is returned when the IP addition method (`IpAddType`) is `2` (IP address group addition mode).




**IpList ** <span data-label="purple"> String[]  </span>`Sample value: ["1.1.1.1"]`

When the IP addition method (`IpAddType`) is `3` (multiple IP addition mode), the returned IP or CIDR list specifies the client IP range for which the ACL rule is effective.



**IpLocationCountry ** <span data-label="purple"> String[]  </span>`Sample value: ["US"]`

Field returned when `IpAddType` is `4` (geolocation addition mode), containing the list of country codes used in geolocation mode. Code samples are taken from the AreaCode field in OverSeaAreaInfoList returned by the `GetAreaBlockInfo` interface.



**IpLocationSubregion ** <span data-label="purple"> String[]  </span>`Sample value: ["Beijing"]`

Field returned when `IpAddType` is `4` (geolocation addition mode), containing the list of sub\-region codes where the rule is effective. Code samples are taken from the AreaCode field in CNAreaInfoList returned by the `GetAreaBlockInfo` interface.

Applicable only to BytePlus WAF service; not effective when using BytePlus WAF service.



**Name ** <span data-label="purple"> String  </span>`Sample value: AclAllowRuleDemo`

The name of the ACL rule, used to identify the meaning or purpose of each rule.



**PermitFeature ** <span data-label="purple"> String[]  </span>`Sample value: ["allowlist"]`

List of protection rules allowed by the allowlist. If empty, it means all are allowed by default. After allowing, related requests will no longer be checked by the corresponding rules.

Supported values are as follows:


* `allowlist`: All access allowed;

* `blocklist`: Blocklist;

* `geo_black`: Geographic access control;

* `api_route`: Unregistered API detection;

* `api_schema`: API parameter validation;

* `api_sensitive`: API sensitive information protection;

* `bot_dytoken`: BOT dynamic token;

* `bot_frequency`: BOT frequency limit;

* `bot_repeat`: BOT statistical protection;

* `bot_sequence`: BOT behavior map;

* `user_ua_bot`: BOT custom rule;

* `bot_ua_system`: BOT managed rule;

* `httpflood`: CC custom rule;

* `vuln_signature`: Vulnerability protection;

* `scan_freqvuln`: High\-frequency scanning;

* `scan_direnum`: Directory traversal;

* `bot_session_protection`: BOT session protection



**PrefixSwitch ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Reserved field, no actual meaning.



**RuleTag ** <span data-label="purple"> String  </span>`Sample value: B000000227102`

Rule display ID.



**UpdateTime ** <span data-label="purple"> String  </span>`Sample value: 2023-10-09T20:02:42Z`

Rule update time.



**Url ** <span data-label="purple"> String  </span>`Sample value: /demo/path`

Path where the rule is effective.




**Count ** <span data-label="purple"> Integer  </span>`Sample value: 5`

The number of ACL rules actually returned on the current page.



**CurrentPage ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The page number of the current returned result, used to indicate which page the data is on in a paginated query.



**PageSize ** <span data-label="purple"> Integer  </span>`Sample value: 10`

The number of ACL rules returned per page.



**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 10`

Total number of ACL rules matching the query criteria, used to calculate the total number of pages or determine if more data is available in pagination scenarios.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to get more information about error codes.
