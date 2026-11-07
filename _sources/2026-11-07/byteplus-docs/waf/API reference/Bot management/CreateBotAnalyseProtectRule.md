---
title: "CreateBotAnalyseProtectRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/CreateBotAnalyseProtectRule"
---

Create a bot analytics protection rule, which applies to two scenarios: bot rate limiting and bot duplicate counting.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Before creating a rule, call the [ListBotAnalyseProtectRulePriorityAvailable](https://docs.byteplus.com/en/docs/waf/ListBotAnalyseProtectRulePriorityAvailable) API to query available rule priorities and avoid conflicts.

* Call limits

   * Service API call total limit: 1000 QPS

   * Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=CreateBotAnalyseProtectRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|DnajvM">必选</span> `Sample value: CreateBotAnalyseProtectRule`

API name. The current API is named `CreateBotAnalyseProtectRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|RIzUGs">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

The name of the resource belonging to the project.



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: --`

No input required if not configured.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10000000`

The actual priority corresponding to the advanced condition group. This field does not need to be provided when creating a rule; it is only returned when displaying the advanced condition group list.



**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 167913`

The actual ID corresponding to the advanced condition. This field does not need to be provided when creating a rule; it is only used for aggregation display when listing advanced condition groups.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|ECjr9P">必选</span> `Sample value: 1`


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|tMOn2l">必选</span> `Sample value: --`

List of subrules in advanced conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|OzerCu">必选</span> `Sample value: request.header.clientip`

The specific object corresponding to the matching rule. Supported matching objects are as follows:


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

* `request.ja3-hash`: JA3 Hash; (applicable only to the byteplus\-global region)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You cannot directly pass generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>; you must include a specific Key.</div>




**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|FyqOB8">必选</span> `Sample value: 12`

Enumeration values for the match object type, used to specify the match object type of sub\-rules in advanced conditions. The supported values are as follows:


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



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|v5yD_q">必选</span> `Sample value: 2`

Enumeration value of the matching operator, used to specify the matching method for subrules in advanced conditions. Supported values are as follows:


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



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|MT7Or6">必选</span> `Sample value: 0`

The enumerated value for the matching property data type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and more;

* `5`: IP, used only for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|gEDUx8">必选</span> `Sample value: 1.1.1.1`

The specific value for the match rule.


* When the match object is a generic object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the match value for the corresponding Key.

* Special note: When the Operator (`Operator`) is `17`, `18`, `19`, `20`, or `21` and the match object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in the actual match value as required.





**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10000000`

The priority of advanced condition goup. It is used only for displaying, not applicable when you create or update a rule.



**ActionType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|wwJ5_T">必选</span> `Sample value: 2`

The action to be executed. The supported values are as follows:


* `0`: Observe;

* `1`: Rate limiting; (only applicable when `StatisticalType=1`)

* `2`: Block;

* `6`: JS challenge;

* `7`: CAPTCHA;

* `10`: Proof of work;

* `11`: Drop.



**EffectTime ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 66`

Duration for which the action takes effect. Except when `ActionType` is `1` (rate limiting), this field must be filled in when creating or updating rules. The valid range is 30–86400 seconds.



**Enable ** <span data-label="purple"> Integer  </span><span data-api-tag="require|kvbdbY">必选</span> `Sample value: 1`

Enabled status. Supported values are as follows:


* `0`: Disabled;

* `1`: Enabled.



**ExemptionTime ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 30`

Exemption time for CAPTCHA challenge, JS challenge, or proof of work, valid range: 30~3600 seconds. 

Required only when `ActionType` is `6` (JS challenge), `7` (CAPTCHA verification), or `10` (proof of work); not required for other actions.



**Field ** <span data-label="purple"> String  </span><span data-api-tag="require|UFi-bU">必选</span> `Sample value: HEADER:X-Forwarded-For,CLIENTIP,COOKIE:token`

The statistical object for the statistical rule. Supports single or multiple fields, with multiple fields separated by commas (up to 10 fields). The field format is divided into two types: enumeration values that do not require a Key and enumeration values that require a Key.


* Enumeration values that do not require a Key include:

   * `CLIENTIP`: Client IP (applicable only when`StatisticalType=1`)

   * `JA3HASH`: JA3 hash value (appicable only to the byteplus\-global region).

* Enumeration values that require a Key include:

   * `HEADER:{Header-Name}`: Specified request header (for example, `HEADER:X-Forwarded-For`);

   * `ARGS:{ArgName}`: Specified request parameters (for example, `ARGS:device_id`);

   * `COOKIE:{CookieName}`: Specified Cookie (for example, `COOKIE:token`).



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|fTbI5T">必选</span> `Sample value: wafexample.com`

The website domain name to be protected.



**Name ** <span data-label="purple"> String  </span><span data-api-tag="require|E8kDtC">必选</span> `Sample value: bot-frequency-login`

Rule name.


* Must start with a Chinese character, letter, or number.

* Letters, numbers, Chinese characters, dot “.”, underscore “_”, and hyphen “\-” are allowed.

* The length must be between 1 and 128 characters.



**Path ** <span data-label="purple"> String  </span><span data-api-tag="require|5FDKoi">必选</span> `Sample value: /login`

The request path to which the rule applies. You can specify a particular page path, match the entire site, or all paths under a directory. The wildcard `*` can only appear at the end of the path.



**PathThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 20`

The overall threshold for the current path. This is effective only when the statistical method is rate limiting (`StatisticalType=1`), and the value range is 1 to 1000.



**RulePriority ** <span data-label="purple"> Integer  </span><span data-api-tag="require|wGGHBF">必选</span> `Sample value: 0`

Rule effective priority under the same path and the same advanced condition. Value range: 0–9. Priorities among different rules must not be duplicated. To query priorities, call [ListBotAnalyseProtectRulePriorityAvailable](https://docs.byteplus.com/en/docs/waf/ListBotAnalyseProtectRulePriorityAvailable).



**SingleProportion ** <span data-label="purple"> Double  </span>`Optional` `Sample value: 0.6`

Threshold for the proportion of a single statistical object. This field is enabled only when `StatisticalType` is `3` (duplicate proportion). In this case, this field must be provided. Value range: `[0, 1)`.



**SingleThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 6`

The threshold for a single statistical object, used only when the statistical method is frequency limit (`StatisticalType=1`). Valid range: 1~1000 times.



**StatisticalDuration ** <span data-label="purple"> Integer  </span><span data-api-tag="require|t15MFJ">必选</span> `Sample value: 60`

Statistical time window, in seconds. The value range varies depending on the statistical scenario:


* Rate limiting scenario（`StatisticalType=1`）: value range is 5–1800 seconds;

* Duplicate counting scenario（`StatisticalType=2` or `StatisticalType=3`）: value range is 1–60 seconds.



**StatisticalType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|NXxFL7">必选</span> `Sample value: 1`

Statistical method. Supported values are as follows:


* `1`: Access frequency;

* `2`: Number of repetitions;

* `3`: Repetition ratio.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Id ** <span data-label="purple"> Integer  </span>`Sample value: 18673`

The rule ID after it is created.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
