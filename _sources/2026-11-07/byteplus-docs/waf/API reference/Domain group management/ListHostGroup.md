---
title: "ListHostGroup"
product: "Web Application Firewall"
product_code: "waf"
source: "https://docs.byteplus.com/en/docs/waf/ListHostGroup"
---

The ListHostGroup API is used to query domain name group information, including details of domain names within the group and associated rule IDs. Supports querying details of the associated domain name group based on domain name, domain name group name, domain name group ID, and more.

<span id=".6K-35rGC6K-05piO"></span>
## HTTP request


* Method: POST

* URL: https://waf.byteplusapi.com/?Action=ListHostGroup&Version=2023\-12\-25


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following table lists only the request parameters specific to this API and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

<span id="Query"></span>
### Query



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|rB3wgz">必选</span> `Sample value: ListHostGroup`

API name. The current API name is `ListHostGroup`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|dlsfGC">必选</span> `Sample value: 2023-12-25`

API version. The current API version is `2023-12-25`.



<span id="Body"></span>
### Body



**ProjectName ** <span data-label="purple"> String  </span>`Optional` `Sample value: default`

Project name, default is "default". The current resource is associated with the corresponding project, and only projects for which the current identity has permission can be associated. For how to obtain the project name, refer to ListProjectResources.



**HostFix ** <span data-label="purple"> String  </span>`Optional` `Sample value: volcwaf.com`

Domain name information to query.



**HostGroupID ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 7515`

Domain name group ID.



**ListAll ** <span data-label="purple"> Boolean  </span>`Optional` `Sample value: true`

Whether to return all domain name groups and their name information. Returned by default.


* true: Returned

* false: Not returned



**NameFix ** <span data-label="purple"> String  </span>`Optional` `Sample value: priority protected domain name`

Domain name group name to query, supports fuzzy matching.



**Page ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Query page number. The default is 1.



**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

Number of items per page, default is 10. Range is 1 ~ 100.



**RuleTag ** <span data-label="purple"> String  </span>`Optional` `Sample value: F00000000****`

Rule ID associated with the domain name group, which can be obtained using the access control query API.



**TimeOrderBy ** <span data-label="purple"> String  </span><span data-api-tag="require|FWtKkT">必选</span> `Sample value: DESC`

List display order.


* ASC: Sort by update time in ascending order

* DESC: Sort by update time in descending order



<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**HostGroupList ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value: --`

Details of the domain name group list.


**Description ** <span data-label="purple"> String  </span>`Optional` `Sample value: Used for batch association with the blocklist.`

Domain name group description.



**HostCount ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 2`

Number of domain names contained in the domain name group.



**HostGroupId ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 7515`

Domain name group ID.



**HostList ** <span data-label="purple"> String[]  </span>`Optional` `Sample value: ["volcwaf.com","www.testwaf.com"]`

Domain names in the domain name group.



**Name ** <span data-label="purple"> String  </span>`Optional` `Sample value: priority protected domain name`

Domain name group name.



**RelatedRules ** <span data-label="purple"> Object[]  </span>`Optional` `Sample value: --`

Associated rule list.


**RuleName ** <span data-label="purple"> String  </span>`Optional` `Sample value: block_rule`

Rule name.



**RuleTag ** <span data-label="purple"> String  </span>`Optional` `Sample value: F00000000****`

Rule ID.



**RuleType ** <span data-label="purple"> String  </span>`Optional` `Sample value: Block`

Rule type.


* Allow: Allowlist

* Block: Blocklist




**UpdateTime ** <span data-label="purple"> String  </span>`Optional` `Sample value: 2024-10-25T16:05:57+08:00`

Domain name group update time.




**PageSize ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 10`

Maximum number of items per page.



**CurrentPage ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 1`

Current page number.



**TotalCount ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 15`

Total number of rules under the current domain name.



**Count ** <span data-label="purple"> Integer  </span>`Optional` `Sample value: 5`

Current data count.



<span id=".6ZSZ6K-v56CB"></span>
## Error codes

You can visit [Common error codes](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-error-codes) to get more information about error codes.
