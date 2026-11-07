---
title: "ListBotAnalyseProtectRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListBotAnalyseProtectRule"
---

Call the ListBotAnalyseProtectRule API to query the details of bot rate limit or statistical protection rules under the specified domain name.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListBotAnalyseProtectRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|I_ed_y">必选</span> `Sample value: ListBotAnalyseProtectRule`

API name. The name of the current API is `ListBotAnalyseProtectRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|EBf_zx">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**Page ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Query page number, default is 1.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the associated project resource.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

Number of items per page, default is 10. Range: 1 ~ 100.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|rgT5Lg">必选</span> `Sample value: example.volc001.com`

The domain name being queried.



**BotSpace ** <span data-label="purple"> String  </span>`Optional` `Sample value: BotFrequency`

Bot protection rule type:


* `BotFrequency`: Rate limiting rule. The corresponding statistical method is `access frequency`.

* `BotRepeat`: Statistical protection rule. The corresponding statistical method is `repeat count` or `repeat ratio`.



**RuleTag ** <span data-label="purple"> String  </span>`Optional` `Sample value: R000000000629`

The unique identifier of the rule, used for precise matching. Its actual numeric value matches the rule `Id`. For example, the rule `R000000000629` corresponds to the rule `Id` value `629`.



**Path ** <span data-label="purple"> String  </span>`Optional` `Sample value: /path`

Protection path, used for fuzzy matching.



**Name ** <span data-label="purple"> String  </span>`Optional` `Sample value: rule1`

Rule name, used for fuzzy matching.


* Must begin with a Chinese character, letter, or number

* Letters, numbers, Chinese characters, period “.”, underscore “_”, and hyphen “\-” are allowed

* Length must be 1–128 characters



**Region ** <span data-label="purple"> String  </span><span data-api-tag="require|9PJ8JP">必选</span> `Sample value: cn-beijing`

The region where the cloud WAF instance is located.


* Asia Pacific (Johor)：ap\-southeast\-1

* Asia Pacific (Jakarta)：ap\-southeast\-3

* China (Hong Kong)：cn\-hongkong

* Edge：byteplus\-global



**ActionTypeKey ** <span data-label="purple"> Integer[]  </span>`Optional` `Sample value: -`

The filter list for protection actions. The default value is an empty array. The supported values are as follows.


* `0`: Observe;

* `1`: Rate limit;  (only applicable when `StatisticalType=1`)

* `2`: Block;

* `6`: JS challenge;

* `7`: CAPTCHA;

* `10`: Proof of work;

* `11`: Dynamic token;

* `12`: Drop.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**CurrentPage ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Current page number.



**Data ** <span data-label="purple"> Object[]  </span>`Sample value: --`

Bot rule details.


**EnableCount ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Number of enabled rules under the current path.



**Path ** <span data-label="purple"> String  </span>`Sample value: /login`

Request path.



**RuleGroup ** <span data-label="purple"> Object[]  </span>`Sample value: -`

The list of rules aggregated by advanced conditions under the current path.


**Group ** <span data-label="purple"> Object  </span>`Sample value: -`

Advanced condition information. If empty, it indicates that there are no advanced conditions under the current path.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Sample value: 10000000`

The actual priority corresponding to the advanced condition group. This field does not need to be included when creating rules; it is only returned when listing advanced condition groups.



**Id ** <span data-label="purple"> Integer  </span>`Sample value: 167913`

The actual ID corresponding to the advanced condition. This field is not required when creating a rule and is only used for aggregation display when listing advanced condition groups.



**Logic ** <span data-label="purple"> Integer  </span>`Sample value: 1`


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span>`Sample value: --`

List of sub\-rules in advanced conditions.


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



**ObjType ** <span data-label="purple"> Integer  </span>`Sample value: 12`

Enumeration value for the type of matching object, used to specify the type of matching object for sub\-rules in advanced conditions. Supported values are as follows:


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

* `25`: Belongs to IP geolocation;

* `26`: Does not belong to IP geolocation;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Enumeration value for the matched property data type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span>`Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in. For all other operator scenarios, fill in the actual matching value as required.





**Rules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

List of rules under the current advanced condition group.


**AccurateGroup ** <span data-label="purple"> Object  </span>`Sample value: -`

Advanced condition configuration for the rule, including logical relationships, list of sub\-rules, priority, and other information.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Sample value: 10000000`

The actual priority corresponding to the advanced condition group. This field does not need to be included when creating rules; it is only returned when listing advanced condition groups.



**Id ** <span data-label="purple"> Integer  </span>`Sample value: 167913`

The actual ID corresponding to advanced conditions. This field is not required when creating a rule. It is used for aggregation display when listing advanced condition groups.



**Logic ** <span data-label="purple"> Integer  </span>`Sample value: 1`


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span>`Sample value: --`

List of sub\-rules in advanced conditions.


**HttpObj ** <span data-label="purple"> String  </span>`Sample value: request.header.clientip`

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

* `request.queryargs.{Key}`: Custom request parameter (replace {Key} with the specific parameter name);

* `request.header.{Key}`: Custom request header (replace {Key} with the specific header name);

* `request.cookie.{Key}`: Custom Cookie (replace {Key} with the specific Cookie name);

* `response.header`: Response header;

* `response.body`: Response body;

* `response.code`: Response status code;

* `response.header.content-type`: Response header content\-type;

* `response.header.{Key}`: Custom response header (replace {Key} with the specific header name);

* `response.body.{Key}`: Response body field (replace {Key} with the specific field name);

* `request.ja3-hash`: JA3 Hash; (applicable only to the byteplus\-global region)



**ObjType ** <span data-label="purple"> Integer  </span>`Sample value: 12`

Enumeration value for the type of matching object, used to specify the type of matching object for sub\-rules in advanced conditions. Supported values are as follows:


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

The enumeration value for the matching operator, used to specify the matching method for subrules in advanced conditions. The supported values are as follows:


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

* `16`: Regular expression match;

* `17`: Identify as IP;

* `18`: Identify as IPv4;

* `19`: Identify as IPv6;

* `20`: Identify as private IP;

* `21`: Identified as a public IP;

* `22`: Reserved value;

* `23`: Belongs to an IP group;

* `24`: Does not belong to an IP group;

* `25`: Belongs to an IP geolocation;

* `26`: Does not belong to an IP geolocation;

* `27`: Contains IP intelligence;

* `28`: Belongs to an ASN;

* `29`: Does not belong to an ASN.



**Property ** <span data-label="purple"> Integer  </span>`Sample value: 0`

The enumeration value for the property type of the matching property. The default is `0` (except for special IP identification scenarios). The supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and many others;

* `5`: IP, only used for the following IP identification operations

   * `17` (Identify as IP)

   * `18` (Identify as IPv4)

   * `19` (Identify as IPv6)

   * `20` (Identify as private IP)

   * `21` (Identify as public IP)



**ValueString ** <span data-label="purple"> String  </span>`Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in this field with the actual matching value.





**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Sample value: 10000000`

Priority of the advanced condition. This value can be used to determine the target position when dragging in the list view.



**ActionType ** <span data-label="purple"> Integer  </span>`Sample value: 2`

The action to be executed. The supported values are as follows:


* `0`: Observe;

* `1`: Rate limiting; (only applicable when `StatisticalType=1`)

* `2`: Block;

* `6`: JS challenge;

* `7`: CAPTCHA;

* `10`: Proof of work;

* `11`: Drop.



**EffectTime ** <span data-label="purple"> Integer  </span>`Sample value: 66`

Duration for which the action takes effect, in seconds. Except when `ActionType` is `1` (rate limiting), this field must be filled in when creating or updating rules. The minimum value for code validation in repeated statistics scenarios is 30 seconds.



**Enable ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Enabled status. Supported values are as follows:


* `0`: Disabled;

* `1`: Enabled.



**ExemptionTime ** <span data-label="purple"> Integer  </span>`Sample value: 30`

Exemption time for CAPTCHA, JS challenge, or proof of work, in seconds. Only required when `ActionType` is `6` (JS challenge), `7` (human verification), or `10` (proof of work); not required for other actions.



**Field ** <span data-label="purple"> String  </span>`Sample value: HEADER:X-Forwarded-For,CLIENTIP,COOKIE:token`

The statistical object for the statistical rule. Supports single or multiple fields, with multiple fields separated by commas (up to 10 fields). The field format is divided into two types: enumeration values that do not require a Key and enumeration values that require a Key.


* Enumeration values that do not require a Key include:

   * `CLIENTIP`: Client IP (applicable only when`StatisticalType=1`)

   * `JA3HASH`: JA3 hash value (appicable only to the byteplus\-global region).

* Enumeration values that require a Key include:

   * `HEADER:{Header-Name}`: Specified request header (for example, `HEADER:X-Forwarded-For`);

   * `ARGS:{ArgName}`: Specified request parameters (for example, `ARGS:device_id`);

   * `COOKIE:{CookieName}`: Specified Cookie (for example, `COOKIE:token`).



**Host ** <span data-label="purple"> String  </span>`Sample value: wafexample.com`

The website domain name to be protected.



**Id ** <span data-label="purple"> Integer  </span>`Sample value: 18673`

Rule ID.



**Name ** <span data-label="purple"> String  </span>`Sample value: bot-frequency-login`

The name of the rule. It must start with a Chinese character, letter, or digit. Chinese characters, letters, digits, periods (`.`), underscores (`_`), and hyphens (`-`) are allowed. The length range is 1–128 characters.



**PassRatio ** <span data-label="purple"> Double  </span>`Sample value: 0`

JS challenge or CAPTCHA pass rate. Displayed only when `ActionType` is `6` (JS challenge), `7` (CAPTCHA), or `10` (proof of work).



**Path ** <span data-label="purple"> String  </span>`Sample value: /login`

Specify the request path to which the rule applies. You can enter a specific page path, or match all paths for the entire site or within a particular directory. The wildcard `*` can only appear at the end of the path.



**PathThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 20`

The overall threshold for the current path. This parameter is effective only when the statistical method is rate limit (`StatisticalType=1`). The value range is 1 to 1000.



**RulePriority ** <span data-label="purple"> Integer  </span>`Sample value: 0`

Priority of the rule, with a value range from `0` to `9`. Where `0` is the highest priority, and `9` is the lowest priority.



**RuleTag ** <span data-label="purple"> String  </span>`Sample value: R000000018673`

Rule display ID. The display ID for rate limit rules is in the format `R000000018673`, and the display ID for duplicate statistics rules is in the format `S000000018674`.



**SingleProportion ** <span data-label="purple"> Double  </span>`Sample value: 0.6`

The proportion threshold for a single statistical object. This parameter is enabled and required only when the statistical method is duplicate proportion (`StatisticalType`=3). The value range is [0, 1).



**SingleThreshold ** <span data-label="purple"> Integer  </span>`Sample value: 6`

The threshold for a single statistical object. This is only effective when the statistical method is rate limiting (`StatisticalType`=1). The value range is 1 to 1000.



**StatisticalDuration ** <span data-label="purple"> Integer  </span>`Sample value: 60`

Statistical time window, in seconds. Required for creation and update. The value range for rate limiting is 5 to 1800, and for duplicate statistics is 1 to 60.



**StatisticalType ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Statistical method. Supported values are as follows:


* `1`: Access frequency;

* `2`: Number of repetitions;

* `3`: Repetition ratio.



**UpdateTime ** <span data-label="purple"> String  </span>`Sample value: 2023-10-09T20:02:42Z`

Most recent update time, returned only when displaying the list.





**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Total number of rules under the current path.




**PageSize ** <span data-label="purple"> Integer  </span>`Sample value: 10`

Maximum number of items per page.



**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 15`

Total number of items.



**Count ** <span data-label="purple"> Integer  </span>`Sample value: 5`

Number of items on the current page.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to get more information about error codes.
