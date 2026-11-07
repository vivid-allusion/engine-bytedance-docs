---
title: "ListCustomBotConfig"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListCustomBotConfig"
---

Call the ListCustomBotConfig API to query custom bot rules for a specified domain name.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListCustomBotConfig&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|a2C12N">必选</span> `Sample value: ListCustomBotConfig`

API name. The current API name is `ListCustomBotConfig`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|9lfZwG">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**Page ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Query page number. Default is 1.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

The maximum number of entries per page. Value range: 1~100, default is 10.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the associated project resource.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|_OcZKU">必选</span> `Sample value: example.volcwaf001.com`

Domain name information.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**CurrentPage ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Current page number.



**PageSize ** <span data-label="purple"> Integer  </span>`Sample value: 10`

Maximum number of entries per page.



**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 15`

Total number of entries matching the query criteria.



**Count ** <span data-label="purple"> Integer  </span>`Sample value: 5`

Current data count.



**Data ** <span data-label="purple"> Object[]  </span>`Sample value: --`

Description.


**BotType ** <span data-label="purple"> String  </span>`Sample value: Bot1`

Bot name.



**Description ** <span data-label="purple"> String  </span>`Sample value: This bot is used for XX and has XX functionality.`

Rule description.



**Action ** <span data-label="purple"> String  </span>`Sample value: observe`

Action to perform.


* `observe`: observe

* `block`：block

* `js`: js challenge

* `captcha`: CAPTCHA

* `pow`: proof of work

* `permit`: allow



**Enable ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Whether to enable this rule.


* 0: Disabled

* 1: Enable



**UpdateTime ** <span data-label="purple"> String  </span>`Sample value: 2023-10-10T14:59:29+08:00`

Rule update time.



**Advanced ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Whether to enable advanced configuration.


* 0: Disabled.

* 1: Enabled.



**RuleTag ** <span data-label="purple"> String  </span>`Sample value: K00000004****`

Tag of the rule.



**Accurate ** <span data-label="purple"> Object[]  </span>`Sample value: --`

Advanced configuration details.


**Logic ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Logical relationship between AccurateRules sub\-rules. Supported values are as follows.


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span>`Sample value: -`

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

Enumeration value for the type of matching object, used to specify the matching object type for sub\-rules in advanced conditions. Supported values are as follows:


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

The enumeration value of the matching property data type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (Identified as IP)

   * `18` (Identified as IPv4)

   * `19` (Identified as IPv6)

   * `20` (Identified as private IP)

   * `21` (Identified as public IP)



**ValueString ** <span data-label="purple"> String  </span>`Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, it must be filled in according to the actual matching value.





**Id ** <span data-label="purple"> Integer  </span>`Sample value: 41067`

The actual count value of the rule's unique identifier (corresponding to `RuleTag`), for example, `RuleTag = K000000041067`, then `Id = 41067`.




<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
