---
title: "ListBotAnalyseProtectRulePriorityAvailable"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListBotAnalyseProtectRulePriorityAvailable"
---

When creating bot statistics protection rules, you must set the rule's priority, and priorities cannot be duplicated. You can call the ListBotAnalyseProtectRulePriorityAvailable API to query available priorities for bot statistics rules.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListBotAnalyseProtectRulePriorityAvailable&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|SGc1Rr">必选</span> `Sample value: ListBotAnalyseProtectRulePriorityAvailable`

API name. The current API name is `ListBotAnalyseProtectRulePriorityAvailable`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|TwftMm">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**Path ** <span data-label="purple"> String  </span><span data-api-tag="require|XYddoc">必选</span> `Sample value: /path`

Request path.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Name of the associated project resource.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|d8_ShE">必选</span> `Sample value: example.volc001.com`

Domain information.



**BotSpace ** <span data-label="purple"> String  </span><span data-api-tag="require|qq60NM">必选</span> `Sample value: BotFrequency`

Bot protection rule data type:


* `BotFrequency`: Rate limiting rule. The corresponding statistic is `access frequency`.

* `BotRepeat`: Statistical protection rule. The corresponding statistic is `number of repetitions` or `repeat ratio`.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

The maximum number of entries per page.



**Page ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Current page number.



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: -`

Specifies the advanced condition group for the query. When provided, it queries the available rule priorities within the specified advanced condition group under this path; if not provided, it queries the available rule priorities within the default group under this path. This parameter is only passed when AccurateGroup validation passes and valid AccurateRules exist.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10000000`

The actual priority corresponding to the advanced condition group. This field is not required when creating a rule; it is only returned when listing advanced condition groups.



**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 167913`

The actual ID corresponding to the advanced condition. This field is not required when creating a rule; it is only used for aggregation display when listing advanced condition groups.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|uJotFQ">必选</span> `Sample value: 1`


* `1`: AND;

* `2`: OR.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|qJoVmS">必选</span> `Sample value: --`

List of sub\-rules in advanced conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|PRTom2">必选</span> `Sample value: request.header.clientip`

The specific object corresponding to the match rule. The supported match objects are as follows:


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


<div data-tips="true" data-tips-type="default">You cannot directly pass generalized forms such as <code>request.queryargs.*</code>, <code>request.header.*</code>, <code>request.cookie.*</code>; you must include a specific Key.</div>




**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|yY73I3">必选</span> `Sample value: 12`

Enumeration value of the matching object type, used to specify the matching object type for sub\-rules in advanced conditions. Supported values are as follows:


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

* `23`：request.ja3\-hash. (applicable only to the byteplus\-global region)



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|o2BgYF">必选</span> `Sample value: 2`

The enumerated value of the match operator, used to specify the matching method for sub\-rules in advanced conditions. The supported values are as follows:


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

* `12`: Contains all match set;

* `13`: Does not contain all match set;

* `14`: Belongs to match set;

* `15`: Does not belong to match set;

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



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|Ctn6dZ">必选</span> `Sample value: 0`

Enumeration value of the matching attribute type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and more;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|j47xTA">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule.


* When the matching object is a generic object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the value to match for the specified Key.

* Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in this field according to the actual matching value.





<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RulePriority ** <span data-label="purple"> Integer[]  </span>`Sample value: [7,8,9]`

Available priorities, sorted in ascending order. 0 represents P0, which is the highest priority.



**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Total number of data items.



**PageSize ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The number of data items contained on one page.



**CurrentPage ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Current page number.



**Count ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The number of data items returned on the current page.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to obtain more information about error codes.
