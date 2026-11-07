---
title: "ListCCRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListCCRule"
---

Query the list of rate limiting rules for a specified domain name, displaying rule groups and rule information.

<span id="OlrDraqv"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListCCRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|3lR0bj">必选</span> `Sample value: ListCCRule`

Interface name. The name of the current API is `ListCCRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|CWsGLR">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**CCType ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: [0]`

Action to be performed.


* 0: Observe

* 1: Rate limit

* 2: Block

* 7: Human\-machine verification



**Url ** <span data-label="purple"> String  </span>`Optional` `Sample value: /test/*`

Fuzzy search by request path. Supports wildcard `*`; `*` can appear only once.



**RuleTag ** <span data-label="purple"> String  </span>`Optional` `Sample value: F000000001193`

Exact search by rule ID.



**RuleName ** <span data-label="purple"> String  </span>`Optional` `Sample value: true`

Fuzzy search by rule name.



**PathOrderBy ** <span data-label="purple"> String  </span>`Optional` `Sample value: ASC`

List display order.


* ASC: Sort by request path in ascending order.

* DESC: Sort by request path in descending order.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

The number of rules displayed per page. The default is 10, and the configurable range is 1–100.



**Page ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Query page number. Default is 1.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|uoztJ6">必选</span> `Sample value: example.volcwaf001.com`

The domain name of the website for which protection rules need to be set.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The project name associated with the current resource.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**PageSize ** <span data-label="purple"> Integer  </span>`Sample value: 10`

The number of Rate limiting rule records returned per page.



**CurrentPage ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The page number of the returned Rate limiting rule list, used to indicate the current page position in paginated query results.



**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 5`

The total number of rate limiting rules that meet the current filter criteria. Used to calculate the total number of pages or determine if more data is available in pagination scenarios.



**Count ** <span data-label="purple"> Integer  </span>`Sample value: 3`

The number of CC protection rule records returned on the current page that meet the filter criteria.



**policyhandler.ListCCRuleRsp ** <span data-label="purple"> Object[]  </span>`Sample value: -`

The list of rate limiting rules that meet the filter criteria. Each element contains information such as path, rule group, insertion time, total number of rules, and number of enabled rules.


**EnableCount ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The number of rate limiting rules enabled under the current path.



**InsertTime ** <span data-label="purple"> String  </span>`Sample value: 2023-10-09T20:02:42Z`

The time when the Rate limiting rule was first entered into the system for the current path, formatted according to the ISO 8601 standard.



**RuleGroup ** <span data-label="purple"> Object[]  </span>`Sample value: -`

The list of rate limiting rules aggregated by advanced condition group. Each element contains advanced condition group information and the list of rate limiting rules under that group.


**Group ** <span data-label="purple"> Object  </span>`Sample value: -`

Advanced condition group information. If empty, it indicates that there are no advanced condition groups under the current path. Includes information such as the ID of the advanced condition group, the logical relationship between subrules, the list of subrules, and priority.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The priority of the advanced condition group, used to determine the target position when adjusting drag\-and\-drop priority in list displays.



**AccurateRules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

The list of subrules in the advanced condition group. Each subrule defines specific matching criteria (such as request headers, client IP, and more) to precisely filter requests that meet the conditions.


**HttpObj ** <span data-label="purple"> String  </span>`Sample value: request.header.clientip`

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

* `request.ja3-hash`: JA3 Hash; (Applicable only to the byteplus\-global region)

   Note: You cannot directly pass generalized forms such as `request.queryargs.*`, `request.header.*`, `request.cookie.*`. You must include a specific Key.



**ObjType ** <span data-label="purple"> Integer  </span>`Sample value: 12`

The enumeration value for the matching object type, used to specify the matching object type for subrules in advanced conditions. Supported values are as follows:


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

* `23`：request.ja3\-hash. (Applicable only to the byteplus\-global region)



**Opretar ** <span data-label="purple"> Integer  </span>`Sample value: 2`

Enumeration value of the matching operator, used to specify the matching method of sub\-rules in advanced conditions. The supported values are as follows:


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

* `12`: Contains the entire matching set;

* `13`: Does not contain the entire matching set;

* `14`: Belongs to matching set;

* `15`: Does not belong to matching set;

* `16`: Regex match;

* `17`: Identify as IP;

* `18`: Identify as IPv4;

* `19`: Identify as IPv6;

* `20`: Identify as private IP;

* `21`: Identify as public IP;

* `23`: Belongs to IP group;

* `24`: Does not belong to IP group;

* `25`: Belongs to IP geolocation;

* `26`: Does not belong to IP geolocation;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Enumeration value for matching property data type. Default is `0` (except for special IP identification scenarios). The supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and more;

* `5`: IP, only used for the following IP identification operations

   * `17` (Identify as IP)

   * `18` (Identify as IPv4)

   * `19` (Identify as IPv6)

   * `20` (Identify as private IP)

   * `21` (Identify as public IP)



**ValueString ** <span data-label="purple"> String  </span>`Sample value: 1.1.1.1`

The specific value corresponding to the matching rule. When the matching object is `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}` and similar generalized objects, this field represents the matching value for the corresponding Key. Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in. For all other operator scenarios, fill in this field according to the actual matching value.




**Id ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The unique identifier ID of the advanced condition group. This is not required when creating rules and is only used for aggregating related rate limiting rules in list displays.



**Logic ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The logical relationship between subrules in the advanced condition group. Supported values are as follows:


* `1`: AND;

* `2`: OR.




**Rules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

The list of Rate limiting rules under this advanced condition group, including detailed configuration information for each rule.


**AccurateGroup ** <span data-label="purple"> Object  </span>`Sample value: -`

Advanced condition group information. The current path and this condition group have an `AND` relationship. The rule is effective only when the request matches both the path and the condition group.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The priority of the advanced condition group, used to determine the target position when adjusting drag\-and\-drop priority in list displays.



**AccurateRules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of subrules in the advanced condition group. Each subrule defines specific matching conditions (such as request headers, client IP, and more) to precisely filter requests that meet the criteria.


**HttpObj ** <span data-label="purple"> String  </span>`Sample value: request.header.clientip`

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

* `response.header`: Response header;

* `response.body`: Response body;

* `response.code`: Response status code;

* `response.header.content-type`: Response header content\-type;

* `response.header.{Key}`: Custom response header (replace {Key} with the specific header name);

* `response.body.{Key}`: Response body field (replace {Key} with the specific field name);

* `request.ja3-hash`: JA3 Hash; (only applicable to the byteplus\-global region)

   Caution: You cannot directly pass generalized forms such as `request.queryargs.*`, `request.header.*`, `request.cookie.*`, `response.header.*`, or `response.body.*`; a specific key must be provided.



**ObjType ** <span data-label="purple"> Integer  </span>`Sample value: 12`

Enumeration value for the matching object type, used to specify the matching object type for subrules in advanced conditions. Supported values are as follows:


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

* `17`：response.header；

* `18`：response.body；

* `19`：response.code；

* `20`：response.header.content\-type；

* `21`：response.header.{Key}；

* `22`：response.body.{Key}；

* `23`：request.ja3\-hash. (Applicable only to the byteplus\-global region)



**Opretar ** <span data-label="purple"> Integer  </span>`Sample value: 2`

The enumeration value for the matching operator, used to specify the matching method for sub\-rules in advanced conditions. Supported values are as follows:


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

* `22`: Reserved value;

* `23`: Belongs to IP group;

* `24`: Does not belong to IP group;

* `25`: Belongs to IP location;

* `26`: Does not belong to IP location;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span>`Sample value: 0`

The enumeration value for matching attribute data type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span>`Sample value: 1.1.1.1`

The specific value corresponding to the matching rule. When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field indicates the matching value for the corresponding Key. Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in the actual matching value as required.




**Id ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The unique identifier ID of the advanced condition group. This is not required when creating rules and is only used for aggregating related rate limiting rules in list displays.



**Logic ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The logical relationship between sub\-rules in the advanced condition group. Supported values are as follows:


* `1`: AND;

* `2`: OR.




**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The priority of the advanced condition. This value does not need to be specified when creating or updating rules. In list display scenarios, this priority can be used to determine the target position when adjusting priority via drag\-and\-drop.



**CCType ** <span data-label="purple"> Integer  </span>`Sample value: 2`

Action to execute.


* 0: Observe

* 1: Rate limit

* 2: Block

* 6: JS challenge

* 7: Captcha



**CountTime ** <span data-label="purple"> Integer  </span>`Sample value: 60`

Statistics time window. Unit: seconds. Value range: 5~1800.



**CronConfs ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of scheduled configuration entries. Each entry contains a crontab expression, the total path threshold for the time period, and the single object threshold. Returned only when `CronEnable` is `1`.


**Crontab ** <span data-label="purple"> String  </span>`Sample value: * 18-20 * * 1,2,3,4,5`

The crontab expression must comply with the crontab validation rules of confcenter. The recommended format is `* <startHour>-<endHour> * * <weekList>` (for example, `* 18-20 * * 1,2,3,4,5`). The week configuration within the same rule must be consistent, and hour ranges must not overlap.



**PathThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 500`

During the scheduled effective period, the overall request threshold for this path. The value range is from `1` to `300000` times.



**SingleThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 50`

Within the scheduled effective period, the request count threshold for a single statistical object. The value range is from `1` to `300000` requests.




**CronEnable ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Scheduled activation switch. The default value is `0`, which means the rule is always active. After enabling, you must also configure `CronConfs` at the same time. The supported values are as follows:


* `0`: Disabled;

* `1`: Enabled.



**CustomResponsePageID ** <span data-label="purple"> String  </span>`Sample value: 123456`

The unique identifier ID of the custom response page. An empty string indicates that this field is not configured. Before use, ensure that the user has enabled and has permission to use the corresponding custom response page.



**EffectTime ** <span data-label="purple"> Integer  </span>`Sample value: 3600`

Duration for which the action takes effect, in seconds. Value range: 1–86400. When the action is Rate limiting, blocking, CAPTCHA, or JS challenge, it is recommended to explicitly provide this field.



**Enable ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The switch status of the rule. The supported values are as follows:


* `0`: Off;

* `1`: On.



**ExemptionTime ** <span data-label="purple"> Integer  </span>`Sample value: 300`

The exemption time for human verification or JS challenge, in seconds, with a value range of 1 to 3600. After passing verification within the exemption time, the user can access normally; after the exemption time ends, if still within the restriction period, verification will be triggered again.



**Field ** <span data-label="purple"> String  </span>`Sample value: CLIENTIP`

Statistics field. Supports a single field or multiple fields, with multiple fields separated by commas. Up to 10 fields are allowed. The basic format is `DataType:Value`, for example, `HEADER:Authorization`, `COOKIE:PHPSESSID`, `ARGS:device_id`, `CLIENTIP`. Supported statistics field values are as follows:


* `CLIENTIP`: Source IP;

* `HEADER:{Header-Name}`: Specified request header (Header\-Name must comply with HTTP header key specifications);

* `ARGS:{ArgName}`: Specified request parameter;

* `COOKIE:{CookieName}`: Specified Cookie;

* `JA3HASH`：JA3 Hash. (Applicable only to the byteplus\-global region)



**Host ** <span data-label="purple"> String  </span>`Sample value: example.volcwaf001.com`

The website domain name to be protected. Before calling, ensure that this domain name has been added to the current WAF instance.



**Id ** <span data-label="purple"> Integer  </span>`Sample value: 12345`

The unique identifier ID of the rate limiting rule.



**Name ** <span data-label="purple"> String  </span>`Sample value: Product detail page Rate limiting rule`

The name of the Rate limiting rule must meet the following requirements:


* Must begin with a Chinese character, letter, or digit.

* Chinese characters, letters, digits, English period (.), underscore (_), and hyphen (\-) are allowed.

* Length must be between 1 and 128 characters.



**PathThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 1000`

The total request threshold under the current path, in requests, with a value range of `1` to `300000`.



**RulePriority ** <span data-label="purple"> Integer  </span>`Sample value: 0`

The priority of the rule, with a value range from `0` to `9`. Among them, `0` is the highest priority, and `9` is the lowest priority. Supported values are as follows.


* `0`: Highest priority;

* `1`: Priority 1;

* `2`: Priority 2;

* `3`: Priority 3;

* `4`: Priority 4;

* `5`: Priority 5;

* `6`: Priority 6;

* `7`: Priority 7;

* `8`: Priority 8;

* `9`: Lowest priority.



**RuleTag ** <span data-label="purple"> String  </span>`Sample value: 123456`

The display ID of the rule. This field does not need to be included when creating or updating a rule, and is only used in list display scenarios.



**SingleThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The threshold for a single statistical object. The value range in external documentation is 1 to 300000, in requests.



**UpdateTime ** <span data-label="purple"> String  </span>`Sample value: 2023-10-09T20:02:42Z`

The time when the rule was last updated, used only in list display scenarios.



**Url ** <span data-label="purple"> String  </span>`Sample value: /test.html`

Request path. You can specify a specific page path, or match all paths on the entire site or within a directory.

The wildcard \* can only appear at the end of the path, for example: `/test.html/*`



**WSCdnByteThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 1`

WebSocket byte threshold. Value range: 1~10000000.

A value of 0 indicates not configured.



**WSCdnEnable ** <span data-label="purple"> Integer  </span>`Sample value: 0`

The switch status for WebSocket statistics protection. After enabling, you must configure at least one of `WSCdnFrameThreshold` or `WSCdnByteThreshold`, and Cron scheduled configuration cannot be used in combination. Supported values are as follows:


* `0`: Disabled;

* `1`: Enabled.



**WSCdnFrameThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 1`

WebSocket frame threshold. Value range: 1–10000.

0 indicates not configured.



**WSCdnUnit ** <span data-label="purple"> String  </span>`Sample value: KB`

WebSocket byte threshold unit: KB / MB / GB.





**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Total number of rules under the current path.



**Url ** <span data-label="purple"> String  </span>`Sample value: /test.html`

Request path.




<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
