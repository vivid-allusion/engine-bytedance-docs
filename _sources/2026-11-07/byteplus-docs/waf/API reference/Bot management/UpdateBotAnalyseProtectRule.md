---
title: "UpdateBotAnalyseProtectRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateBotAnalyseProtectRule"
---

Update existing Bot statistical protection rules. Applicable to both Bot frequency limit and Bot duplicate statistics scenarios.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateBotAnalyseProtectRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this interface and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|sAXR3N">必选</span> `Sample value: UpdateBotAnalyseProtectRule`

API name. The current API name is `UpdateBotAnalyseProtectRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|mPYeMC">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the project resource to which it belongs.



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: --`

Advanced conditions. If not configured, this field does not need to be provided.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10000000`

The actual priority corresponding to the advanced condition group. This field does not need to be included when creating rules; it is only returned when listing advanced condition groups.



**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 167913`

The actual ID corresponding to advanced conditions. This field does not need to be included when creating rules; it is only used for aggregation display when listing advanced condition groups.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|CKSIlA">必选</span> `Sample value: 1`


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|sWaj4B">必选</span> `Sample value: --`

List of sub\-rules in advanced conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|BBYxv0">必选</span> `Sample value: request.header.clientip`

The object to which the matching rule applies. Supported matching objects are as follows:


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

* `request.ja3-hash`: JA3 Hash; (applicable only to the byteplus\-global region)


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">You cannot directly pass generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>; a specific Key must be included.</div>




**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|E3L11q">必选</span> `Sample value: 12`

Enumerated values for matching object types, used to specify the matching object type for sub\-rules in advanced conditions. Supported values are as follows:


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



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|yUn9IR">必选</span> `Sample value: 2`

Enumeration value of the matching operator, used to specify the matching method for sub\-rules in advanced conditions. Supported values are as follows:


* `0`: Greater than;

* `1`: Greater than or equal to;

* `2`: Equal to;

* `3`: Less than;

* `4`: Less than or equal to;

* `5`: Not equal to;

* `6`: Contains substring;

* `7`: Does not contain substring;

* `8`: Prefix match;

* `9`: Does not match prefix;

* `10`: Suffix match;

* `11`: Does not match suffix;

* `12`: Contains all items in the matching set;

* `13`: Does not contain all items in the matching set;

* `14`: Belongs to the matching set;

* `15`: Does not belong to the matching set;

* `16`: Regex match;

* `17`: Is recognized as an IP address;

* `18`: Is recognized as an IPv4 address;

* `19`: Is recognized as an IPv6 address;

* `20`: Is recognized as a private IP address;

* `21`: Is recognized as a public IP address;

* `23`: Belongs to the IP group;

* `24`: Does not belong to the IP group;

* `25`: Belongs to the IP location;

* `26`: Does not belong to the IP location;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|lORWjG">必选</span> `Sample value: 0`

Enumeration value of the matching attribute type. By default, `0` is used (except for special IP identification scenarios). The supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|I3HorW">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}` and similar generalized objects, this field indicates the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field is not required; for all other operator scenarios, fill in the actual matching value as required.





**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10000000`

The actual priority corresponding to the advanced condition group. This field does not need to be included when creating rules; it is only returned when listing advanced condition groups.



**ActionType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|HWeNyW">必选</span> `Sample value: 2`

The action to be executed. The supported values are as follows:


* `0`: Observe;

* `1`: Rate limiting; (only applicable when `StatisticalType=1`)

* `2`: Block;

* `6`: JS challenge;

* `7`: CAPTCHA;

* `10`: Proof of work;

* `11`: Drop.



**EffectTime ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 66`

Duration for which the action takes effect, in seconds. Except when `ActionType` is `1` (rate limiting), this field must be provided when creating or updating a rule. The valid range is 30–86400 seconds.



**Enable ** <span data-label="purple"> Integer  </span><span data-api-tag="require|giDVwF">必选</span> `Sample value: 1`

Enablement status. Supported values are as follows:


* `0`: Disabled;

* `1`: Enabled.



**ExemptionTime ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 30`

Exemption time for CAPTCHA challenge, JS challenge, or proof of work, in seconds. Required only when `ActionType` is `6` (JS challenge), `7` (CAPTCHA challenge), or `10` (proof of work); not required for other actions.



**Field ** <span data-label="purple"> String  </span><span data-api-tag="require|ROGEWX">必选</span> `Sample value: HEADER:X-Forwarded-For,CLIENTIP,COOKIE:token`

The statistical object for the statistical rule. Supports single or multiple fields, with multiple fields separated by commas (up to 10 fields). The field format is divided into two types: enumeration values that do not require a Key and enumeration values that require a Key.


* Enumeration values that do not require a Key include:

   * `CLIENTIP`: Client IP (applicable only when`StatisticalType=1`)

   * `JA3HASH`: JA3 hash value (appicable only to the byteplus\-global region).

* Enumeration values that require a Key include:

   * `HEADER:{Header-Name}`: Specified request header (for example, `HEADER:X-Forwarded-For`);

   * `ARGS:{ArgName}`: Specified request parameters (for example, `ARGS:device_id`);

   * `COOKIE:{CookieName}`: Specified Cookie (for example, `COOKIE:token`).



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|8beP5n">必选</span> `Sample value: wafexample.com`

The website domain name to be protected.



**Id ** <span data-label="purple"> Integer  </span><span data-api-tag="require|Pfrbxq">必选</span> `Sample value: 18673`

Rule ID.



**Name ** <span data-label="purple"> String  </span><span data-api-tag="require|n1744U">必选</span> `Sample value: Bot frequency limit rule for login interface`

Rule name.


* Must start with a Chinese character, letter, or number.

* Letters, numbers, Chinese characters, dot “.”, underscore “_”, and hyphen “\-” are allowed.

* The length must be between 1 and 128 characters.



**Path ** <span data-label="purple"> String  </span><span data-api-tag="require|c7wZW7">必选</span> `Sample value: /login`

Specifies the request path to which the rule applies. You can enter a specific page path, match all paths on the site, or all paths under a directory. The wildcard `*` can only appear at the end of the path.



**PathThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 20`

The overall threshold for the current path. This is effective only when the statistical method is frequency limiting (`StatisticalType=1`), and the value range is 1 to 1000.



**RulePriority ** <span data-label="purple"> Integer  </span><span data-api-tag="require|h4hCYU">必选</span> `Sample value: 0`

Rule activation priority. Value range: 0–9. The priority values of different rules must not be duplicated. To query available priorities, call [ListBotAnalyseProtectRulePriorityAvailable](https://docs.byteplus.com/en/docs/waf/ListBotAnalyseProtectRulePriorityAvailable).



**SingleProportion ** <span data-label="purple"> Double  </span>`Optional` `Sample value: 0.6`

Proportion threshold for a single statistical object. Enabled only when `StatisticalType` is `3` (duplicate proportion); this field must be provided in that case. The value range is `[0, 1)`.



**SingleThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 6`

Threshold for a single statistical object. Used only when the statistical type is rate limiting (`StatisticalType=1`). Value range: 1–1000.



**StatisticalDuration ** <span data-label="purple"> Integer  </span><span data-api-tag="require|loRpRG">必选</span> `Sample value: 60`

Statistical time window, in seconds. The value range varies depending on the statistical scenario:


* Rate limiting scenario（`StatisticalType=1`）: value range is 5–1800 seconds;

* Duplicate counting scenario（`StatisticalType=2` or `StatisticalType=3`）: value range is 1–60 seconds.



**StatisticalType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|8LHNb-">必选</span> `Sample value: 1`

Statistical method. The supported values are as follows:


* `1`: Access frequency;

* `2`: Number of repetitions;

* `3`: Repetition ratio.



**UpdateTime ** <span data-label="purple"> String  </span>`Optional` `Sample value: 2023-10-09T20:02:42Z`

Most recent update time. This field does not need to be included when creating or updating  rules; it is only returned in the listing interface. 



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This interface has no unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more error code information.
