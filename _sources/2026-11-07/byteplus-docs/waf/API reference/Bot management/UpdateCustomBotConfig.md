---
title: "UpdateCustomBotConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateCustomBotConfig"
---

Call the UpdateCustomBotConfig API to update custom bot rules based on the rule ID, associated domain name, and other information.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateCustomBotConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|yIiePx">必选</span> `Sample value: UpdateCustomBotConfig`

Interface name. The current API name is `UpdateCustomBotConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|33oVRe">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**BotType ** <span data-label="purple"> String  </span><span data-api-tag="require|hWZKkz">必选</span> `Sample value: Bot1`

Bot name.


* Must start with Chinese characters, letters, or digits

* Letters, digits, Chinese characters, period ".", underscore "_", and hyphen "\-" are allowed.

* Length must be 1–128 characters.



**Description ** <span data-label="purple"> String  </span>`Optional` `Sample value: This bot is used for XX and provides XX functionality.`

Description of the bot.


* Must begin with a Chinese character, letter, or digit.

* Letters, digits, Chinese characters, period ".", space, underscore "_", hyphen "\-", equals sign "=", English comma ",", Chinese comma "，", and Chinese period "。" are allowed.

* Length must be 0–255 characters.



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|NmR-8g">必选</span> `Sample value: observe`

Action to perform.


* `observe`: observe

* `block`：block

* `js`: js challenge

* `captcha`: CAPTCHA

* `pow`: proof of work

* `permit`: allow



**Enable ** <span data-label="purple"> Integer  </span><span data-api-tag="require|cvCu2P">必选</span> `Sample value: 1`

Whether to enable this rule.


* 0: Disabled

* 1: Enabled



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|YB3ncJ">必选</span> `Sample value: example.volcwaf001.com`

The protected website domain name whose rule needs to be updated.



**Id ** <span data-label="purple"> Integer  </span><span data-api-tag="require|ra9hQa">必选</span> `Sample value: 923`

The numeric part of the rule's unique identifier (corresponding to `RuleTag`), for example, `RuleTag = K000000041067`, then `Id = 41067`. See [ListCustomBotConfig](https://docs.byteplus.com/en/docs/waf/ListCustomBotConfig) for how to obtain this value.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the project resource to which it belongs.



**Accurate ** <span data-label="purple"> Object  </span><span data-api-tag="require|6JK3IH">必选</span> `Sample value: --`

Advanced configuration details.


**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|plzCjI">必选</span> `Sample value: 1`

Logical relationship between AccurateRules subrules. Supported values are as follows.


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|m7YrgT">必选</span> `Sample value: -`

List of sub\-rules in advanced conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|8rLCr0">必选</span> `Sample value: request.header.clientip`

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


<div data-tips="true" data-tips-type="default">You cannot directly pass generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>; you must provide a specific Key.</div>




**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|5a_xTw">必选</span> `Sample value: 12`

Enumeration value for the match object type, used to specify the match object type of sub\-rules in advanced conditions. Supported values are as follows:


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



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|vp4_W9">必选</span> `Sample value: 2`

Enumeration value for the match operator, used to specify the matching method of sub\-rules in advanced conditions. Supported values are as follows:


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

* `12`: contains all match set;

* `13`: does not contain all match set;

* `14`: belongs to match set;

* `15`: does not belong to match set;

* `16`: regex match;

* `17`: identified as IP;

* `18`: identified as IPv4;

* `19`: identified as IPv6;

* `20`: identified as private IP;

* `21`: identified as public IP;

* `23`: belongs to IP group;

* `24`: does not belong to IP group;

* `25`: belongs to IP geolocation;

* `26`: does not belong to IP geolocation;

* `27`: contains IP intelligence;

* `28`: belongs to ASN;

* `29`: does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|3aykbt">必选</span> `Sample value: 0`

Enumeration value for the matching property type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and many other;

* `5`: IP, only used for the following IP identification operations

   * `17` (Identified as IP)

   * `18` (Identified as IPv4)

   * `19` (Identified as IPv6)

   * `20` (Identified as private IP)

   * `21` (Identified as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|CncflL">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the match object is `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}` and other generalized objects, this field represents the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the match object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in the actual matching value as required.





<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

This API does not have unique response parameters. For more information, see [response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
