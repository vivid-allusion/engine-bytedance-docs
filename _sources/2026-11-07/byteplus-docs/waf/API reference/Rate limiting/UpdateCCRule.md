---
title: "UpdateCCRule"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/UpdateCCRule"
---

Edit rate limiting rule, including rule name, request characteristics, and statistical conditions.

<span id=".5rOo5oSP5LqL6aG5"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=UpdateCCRule&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this endpoint and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|ldHWKR">必选</span> `Sample value: UpdateCCRule`

API name. The current API name is `UpdateCCRule`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|FkhNiE">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: --`

Advanced condition configuration. This field does not need to be configured if advanced conditions are not enabled.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The priority of the advanced condition group, used when determining the target position for drag\-and\-drop prioritization in the list.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|LuKlYm">必选</span> `Sample value: -`

List of sub\-rules in the advanced condition group. Each sub\-rule defines specific matching criteria (such as request headers, client IP, and so on) for accurately filtering requests that meet the conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|DBqu8J">必选</span> `Sample value: request.header.clientip`

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

* `request.ja3-hash`: JA3 Hash. (applicable only to the byteplus\-global region)

   Caution: You cannot directly pass generalized forms such as `request.queryargs.*`, `request.header.*`, `request.cookie.*`. A specific Key must be provided.



**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|lG-IrN">必选</span> `Sample value: 12`

Enumeration value of the matching object type, used to specify the matching object type for sub\-rules in advanced conditions. The supported values are as follows:


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

* `23`：request.ja3\-hash.  (Applicable only to the byteplus\-global region)



**Operator ** <span data-label="purple"> Integer  </span><span data-api-tag="require|dyVYpL">必选</span> `Sample value: 2`

Enumeration value of the matching operator, used to specify the matching method for sub\-rules in advanced conditions. The supported values are as follows:


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

* `12`: Contains all of the match set;

* `13`: Does not contain all of the match set;

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

* `25`: Belongs to IP geolocation;

* `26`: Does not belong to IP geolocation;

* `27`: Contains IP threat intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|Vw6znS">必选</span> `Sample value: 0`

Enumeration value for matching property type. The default is `0` (except for special IP identification scenarios). Supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and so on;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private IP)

   * `21` (identified as public IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|50kLjq">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule. When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key. Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in. For all other operator scenarios, fill in the actual matching value as required.




**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The unique identifier ID of the advanced condition group. It is not required when creating rules and is only used for aggregating related rate limiting rules when displaying the list.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|evmyPw">必选</span> `Sample value: 1`

Logical relationship between subrules in the advanced condition group. Supported values are as follows:


* `1`: AND;

* `2`: OR.




**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 9999999`

Advanced condition priority.

<div data-tips="true" data-tips-type="warning" data-tips-is-title="true">warning</div>


<div data-tips="true" data-tips-type="warning">This parameter does not need to be provided when calling the create or update API.</div>




**CCType ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 0`

Action to execute.


* 0: Observe

* 1: Rate limit

* 2: Block

* 6: JS challenge

* 7: CAPTCHA



**CountTime ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 60`

Statistical duration, unit: seconds. Value range: 5–1,800.



**CronConfs ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value: --`

Details of periodic activation configuration. Required when CronEnable=1.


**Crontab ** <span data-label="purple"> String  </span><span data-api-tag="require|xwFuOT">必选</span> `Sample value: * 18-20 * * 1,2,3,4,5`

crontab expression, must comply with the crontab validation rules of confcenter. The recommended format is `* <startHour>-<endHour> * * <weekList>` (for example, `* 18-20 * * 1,2,3,4,5`). The week configuration within the same rule must remain consistent, and the hour ranges must not overlap.



**PathThreshold ** <span data-label="purple"> Integer  </span><span data-api-tag="require|pBSzMw">必选</span> `Sample value: 500`

Within the scheduled effective period, the overall request threshold for this path. The value range is from `1` to `300000` times.



**SingleThreshold ** <span data-label="purple"> Integer  </span><span data-api-tag="require|roH4nK">必选</span> `Sample value: 50`

Within the scheduled effective period, the request count threshold for a single statistical object. The value range is from `1` to `300000` requests.




**CronEnable ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 0`

Whether to enable periodic activation. Once enabled, the policy can be executed at fixed times each week, and multiple active periods can be configured. The default is disabled, meaning the policy is permanently active.


* 0: Disabled.

* 1: Enabled; periodic activation details must be configured.



**EffectTime ** <span data-label="purple"> Integer  </span><span data-api-tag="require|-o3GHx">必选</span> `Sample value: 100`

Statistics duration, unit: seconds. Value range: 1–86,400.

<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="default">This setting is required when the policy action is <code>block</code>, <code>CAPTCHA</code>, or <code>JS challenge</code>. </div>




**Enable ** <span data-label="purple"> Integer  </span><span data-api-tag="require|QVWqj4">必选</span> `Sample value: 1`

Whether to enable the rule.


* 0: Disabled

* 1: Enabled



**ExemptionTime ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 60`

Policy exemption time. This must be set when the policy action is `CAPTCHA` or `JS challenge`.


* After the request behavior triggers the above protection actions and passes verification, traffic can access the target domain normally within the exemption time.

* After the exemption time expires, if still within the policy restriction duration, WAF will re\-initiate human\-machine verification, JS challenge, or proof of work. Access is allowed only after passing verification.



**Field ** <span data-label="purple"> String  </span><span data-api-tag="require|5vSLkz">必选</span> `Sample value: CLIENTIP`

Statistical object. Supports single or multiple fields, with multiple fields separated by commas. Up to 10 fields are supported. The basic format is `DataType:Value`, for example `HEADER:Authorization`, `COOKIE:PHPSESSID`, `ARGS:device_id`, `CLIENTIP`. The supported values for statistical objects are as follows:


* `CLIENTIP`: Source IP;

* `HEADER:{Header-Name}`: Specified request header (Header\-Name must comply with HTTP header key specifications);

* `ARGS:{ArgName}`: Specified request parameters;

* `COOKIE:{CookieName}`: Specified Cookie;

* `JA3HASH`：JA3 Hash. (Applicable only to the byteplus\-global region)



**Url ** <span data-label="purple"> String  </span><span data-api-tag="require|GOOBOR">必选</span> `Sample value: /test/*`

Request path. Supports wildcard `*`, which can only appear once.



**SingleThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

Threshold for the number of accesses for each statistical object. Value range: 1~300,000.



**RuleTag ** <span data-label="purple"> String  </span>`Optional` `Sample value: F000000001193`

Rule display ID.

<div data-tips="true" data-tips-type="warning">Caution</div>


<div data-tips="true" data-tips-type="warning">This parameter does not need to be provided when calling the create or update interface.</div>




**RulePriority ** <span data-label="purple"> Integer  </span><span data-api-tag="require|_fBMAW">必选</span> `Sample value: 0`

Rule execution priority. The larger the number, the lower the priority.


* 0：P0

* 1：P1

* 2：P2

* 3：P3

* 4：P4

* 5：P5

* 6：P6

* 7：P7

* 8：P8

* 9：P9



**PathThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 100`

Threshold for the number of accesses to the request path. Value range: 1~300,000.



**Name ** <span data-label="purple"> String  </span><span data-api-tag="require|2iOFZa">必选</span> `Sample value: 123`

Rule name.


* Must start with a Chinese character, letter, or number.

* Letters, numbers, Chinese characters, period “.”, underscore “_”, and hyphen “\-” are allowed.

* Length must be 1–128 characters.



**Id ** <span data-label="purple"> Integer  </span><span data-api-tag="require|S49VeN">必选</span> `Sample value: 126217`

ID corresponding to the rule. Take the last 6 digits of "Rule ID" from the console.



**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|lb_z2Y">必选</span> `Sample value: example.volcwaf001.com`

The domain name of the website for which protection rules need to be set.



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, which is the project associated with the current resource. Only projects for which the current identity has permissions can be associated.



**CustomResponsePageID ** <span data-label="purple"> String  </span>`Optional` `Sample value: 123456`

ID of the custom response page. The default value is an empty string, indicating that no custom response page is configured. Before use, ensure that the user has enabled and is authorized to use the corresponding custom response page.



**UpdateTime ** <span data-label="purple"> String  </span>`Optional` `Sample value: 2023-10-09T20:02:42Z`

Most recent update time of the rule, used only for list display.



**WSCdnByteThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 102400`

Byte threshold in WebSocket statistics protection. The value range is from `1` to `10000000`. A value of `0` indicates that this threshold is not configured. When WebSocket statistics protection (`WSCdnEnable` = `1`) is enabled, this field can be configured to enable protection based on byte count. The default value is `0`.



**WSCdnEnable ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 0`

WebSocket statistics protection switch status. Once enabled, at least one of `WSCdnFrameThreshold` or `WSCdnByteThreshold` must be configured, and Cron scheduled configuration cannot be combined. The supported values are as follows:


* `0`: Disabled;

* `1`: Enabled.



**WSCdnFrameThreshold ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Frame threshold in WebSocket statistical protection. The value range is from `1` to `10000`. A value of `0` indicates that the threshold is not configured. When WebSocket statistical protection (`WSCdnEnable` = `1`) is enabled, this field can be configured to enable frame\-based protection.



**WSCdnUnit ** <span data-label="purple"> String  </span>`Optional` `Sample value: KB`

WebSocket byte threshold unit: KB / MB / GB.



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Id ** <span data-label="purple"> Integer  </span>`Sample value: 1`

Rule ID after creation or update.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
