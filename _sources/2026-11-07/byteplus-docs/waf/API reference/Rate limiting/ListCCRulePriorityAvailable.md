---
title: "ListCCRulePriorityAvailable"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListCCRulePriorityAvailable"
---

Query the list of priorities available for adding or adjusting rate limiting rules under the specified domain and path.

<span id="4ZdzySyI"></span>
## Important note


* Total service API call limit: 1000 QPS

* Single account call limit: 50 QPS


<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListCCRulePriorityAvailable&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The table below lists only the unique request parameters for this API and some common parameters. For more information, see [common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|WLlag-">必选</span> `Sample value: ListCCRulePriorityAvailable`

API name. The name of the current API is `ListCCRulePriorityAvailable`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|ec8H8i">必选</span> `Sample value: 2023-12-25`

API version. The version of the current API is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, used to associate the current resource with a project. Only projects for which the current account has permissions can be associated. To obtain the project name, refer to the `ListProjectResources` API (to get the project resource list), or call the `CreateProject` API to create a new project. The default value is `default`.



**AccurateGroup ** <span data-label="purple"> Object  </span>`Optional` `Sample value: -`

An optional advanced condition group, with the default value being an empty string. Once provided, the system will calculate the available Rate limiting rule priority list based on the same path and advanced condition dimensions.


**AccurateGroupPriority ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The priority of the advanced condition group, used to determine the target position when adjusting priority by dragging in the list display.



**AccurateRules ** <span data-label="purple"> Object[]  </span><span data-api-tag="require|kW1YUn">必选</span> `Sample value: -`

The list of subrules in the advanced condition group, where each subrule defines specific matching criteria (such as request headers, client IP, and more), used to precisely filter requests that meet the conditions.


**HttpObj ** <span data-label="purple"> String  </span><span data-api-tag="require|flSUXF">必选</span> `Sample value: request.header.clientip`

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

* `request.ja3-hash`: JA3 Hash; (applicable only in the byteplus\-global region)

   Caution: You cannot directly pass generalized forms such as `request.queryargs.*`, `request.header.*`, `request.cookie.*`; a specific Key must be provided.



**ObjType ** <span data-label="purple"> Integer  </span><span data-api-tag="require|Cz9LY5">必选</span> `Sample value: 12`

The enumerated value for the object type to match, used to specify the object type for subrule matching in advanced conditions. Supported values are as follows:


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

* `23`：request.ja3\-hash。 (Applicable only to the byteplus\-global region)



**Opretar ** <span data-label="purple"> Integer  </span><span data-api-tag="require|uxzQHD">必选</span> `Sample value: 2`

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

* `23`: Belongs to IP group;

* `24`: Does not belong to IP group;

* `25`: Belongs to IP location;

* `26`: Does not belong to IP location;

* `27`: Contains IP intelligence;

* `28`: Belongs to ASN;

* `29`: Does not belong to ASN.



**Property ** <span data-label="purple"> Integer  </span><span data-api-tag="require|ob7l4G">必选</span> `Sample value: 0`

The enumeration value of the matching attribute data type, with `0` used by default (except for special IP identification scenarios). The supported values are as follows:


* `0`: Value, applicable to most matching object scenarios, such as request protocol, URI, method, request header, client IP, JA3 Hash, and more;

* `5`: IP, only used for the following IP identification operations

   * `17` (identified as IP)

   * `18` (identified as IPv4)

   * `19` (identified as IPv6)

   * `20` (identified as private network IP)

   * `21` (identified as public network IP)



**ValueString ** <span data-label="purple"> String  </span><span data-api-tag="require|H_y0jF">必选</span> `Sample value: 1.1.1.1`

The specific value corresponding to the matching rule. When the matching object is a generalized object such as `request.header.{Key}`, `request.queryargs.{Key}`, or `request.cookie.{Key}`, this field represents the matching value for the corresponding Key. Special note: When the operator (`Opretar`) is `17`, `18`, `19`, `20`, or `21` and the matching object (`HttpObj`) is `request.header.clientip`, this field does not need to be filled in; for all other operator scenarios, fill in the actual matching value as required.




**Id ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

The unique identifier ID of the advanced condition group, which does not need to be provided when creating rules and is only used to aggregate related Rate limiting rules in the list display.



**Logic ** <span data-label="purple"> Integer  </span><span data-api-tag="require|SULBbt">必选</span> `Sample value: 1`

The logical relationship between subrules in an advanced condition group. Supported values are as follows:


* `1`: AND;

* `2`: OR.




**Host ** <span data-label="purple"> String  </span><span data-api-tag="require|yKD73m">必选</span> `Sample value: example.volcwaf001.com`

Specifies the domain name for which the CC protection rule priority list needs to be queried.



**Url ** <span data-label="purple"> String  </span><span data-api-tag="require|0zVYxP">必选</span> `Sample value: /test.html`

Request path. You can specify a specific page path, or match all paths on the entire site or within a specific directory.

The wildcard \* can only appear at the end of the path, for example: `/test.html/*`



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**Count ** <span data-label="purple"> Integer  </span>`Sample value: 3`

The number of available rate limiting rule priorities returned on the current page, which is consistent with the number of elements in the `RulePriority` array.



**CurrentPage ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The page number of the list of available rate limiting rule priorities returned.



**PageSize ** <span data-label="purple"> Integer  </span>`Sample value: 1`

The number of available CC protection rule priorities returned per page during paginated queries.



**RulePriority ** <span data-label="purple"> Integer[]  </span>`Sample value: -`

This field returns a list of available priorities that can be used to add or adjust CC protection rules for the specified domain name and path. The array elements range from `0` to `9` and are sorted in ascending order.



**TotalCount ** <span data-label="purple"> Integer  </span>`Sample value: 5`

The total number of available priorities for adding or adjusting Rate limiting rules under the specified domain and path, used to calculate the total number of pages in pagination scenarios.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) for more information about error codes.
