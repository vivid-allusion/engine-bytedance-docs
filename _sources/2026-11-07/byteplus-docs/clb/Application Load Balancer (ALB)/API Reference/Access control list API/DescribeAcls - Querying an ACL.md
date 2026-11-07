---
title: "DescribeAcls - Querying an ACL"
product: "Cloud Load Balancer"
product_code: "clb"
source: "https://docs.byteplus.com/en/docs/clb/ALB-DescribeAcls"
---

Call the DescribeAcls API to query the ACL.

<span id=".5L2_55So6K-05piO"></span>
## Instructions


* A maximum of 100 ACLs can be queried in a single API call.

* Submit up to 200 API requests per second.


<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribeAcls&serviceCode=alb&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters



**Action ** <span data-label="purple"> String  </span><span data-api-tag="require|F6-uuV">必选</span>`Example: DescribeAcls`

The interface name. The current API name is `DescribeAcls`.



**Version ** <span data-label="purple"> String  </span><span data-api-tag="require|hCpy93">必选</span> `Example: 2020-04-01`

The interface version. Current API version is `2020-04-01`.



**PageNumber** <span data-label="purple">Integer</span> `optional` `Example: 1`

The page number of the list. Default: 1.



**PageSize ** <span data-label="purple"> Integer </span>`optional` `Example: 10`

Number of rows per page for paginated queries. Valid range: 1 to 100. Default value: 10.



**AclName ** <span data-label="purple">String</span> `optional` `Example: myacl`

ACL name.



**AclIds.N ** <span data-label="purple"> String[] </span>`optional` `Example: AclIds.1=acl-xxxxx & AclIds.2=acl-yyyyy`

List of ACL IDs.



**ProjectName ** <span data-label="purple">String</span> `optional` `Example value: default`

The name of the project to which ACL belongs.



**TagFilters.N.Key ** <span data-label="purple"> String[] </span>`optional` `Example: TagFilters.1.Key=k1&TagFilters.2.Key=k2`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns ACLs tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple"> String[]  </span>`optional` `Example: TagFilters.1.Value.1=v1&TagFilters.1.Value.2=v2&TagFilters.2.Value.1=v3`

Tag value.


* The first N represents the serial number of the tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns ACLs that have any of the specified tag values for that key.

* Separate multiple tag values with an ampersand (&).


<div data-tips="true" data-tips-type="default" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="default">If this parameter is passed in, TagFilters.N.Key must be passed in first.</div>


* <div data-tips="true" data-tips-type="default">Passing an empty string queries for ACLs with an empty tag value.</div>




<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters



**RequestId ** <span data-label="purple"> String  </span>`Example: 20210811152539010225146063030****`

Request ID.



**PageSize ** <span data-label="purple"> Integer  </span>`Example: 20`

The number of rows on the current page.



**PageNumber** <span data-label="purple">Integer</span> `Example: 1`

Current page number.



**TotalCount ** <span data-label="purple"> Integer  </span>`Example: 50`

Total number of qualified ACLs.



**Acls ** <span data-label="purple"> Object[]  </span>`Example: --`

The list of ACLs that meet the specified criteria.


**AclId ** <span data-label="purple"> String  </span>`Example: acl-3cj44nv0jhhxc6c6rrtet****`

ACL ID.



**AclName ** <span data-label="purple"> String </span>`Example: myacl`

ACL name.



**CreateTime ** <span data-label="purple"> String  </span>`Example: 2021-08-11T16:37:37Z`

Creation time of ACL.



**UpdateTime ** <span data-label="purple"> String  </span>`Example: 2021-08-11T16:37:37Z`

Last operation time of ACL.



**AclEntryCount ** <span data-label="purple"> Integer  </span>`Example: 10`

The number of IP entries contained in ACL.



**Listeners ** <span data-label="purple"> String[]  </span>`Example: [ lsn-3tihaugk2y3vj0wt**** , lsn-2fe6fszjgeznk5oxruv0u**** ]`

IDs of listeners associated with ACL.



**Description ** <span data-label="purple"> String  </span>`Example: test`

ACL description.



**ProjectName** <span data-label="purple">String</span> `Example: default`

The name of the project to which ACL belongs.



**Tags ** <span data-label="purple"> Object[] </span>`Example: --`

List of tags bound to the ACL.


**Key ** <span data-label="purple"> String </span>`Example: key`

The tag key of the custom tag.



**Value ** <span data-label="purple"> String </span>`Example: value`

The tag value of the custom tag.




**Status ** <span data-label="purple"> String </span>`Example: Creating`

ACL status.


* Creating

* Active

* Deleting

* Configuring




<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```JSON
GET /?AclIds.1=acl-3cipi5****qps6c6rrsbfr0eb&Action=DescribeAcls&Version=2020-04-01 HTTP/1.1
Host: alb.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/alb/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```JSON
{
    "ResponseMetadata": {
        "RequestId": "202108161840280****52431470309D1E3",
        "Action": "DescribeAcls",
        "Version": "2020-04-01",
        "Service": "alb",
        "Region": "cn-beijing"
    },
    "Result": {
        "RequestId": "2021081618402801****2431470309D1E3",
        "PageNumber": 1,
        "PageSize": 10,
        "TotalCount": 1,
        "Acls": [
            {
                "CreateTime": "2021-08-16T11:22:00Z",
                "UpdateTime": "2021-08-16T11:22:00Z",
                "AclId": "acl-3cipi****qps6c6rrsbfr0eb",
                "AclName": "acl-3cipi****jqps6c6rrsbfr0eb",
                "AclEntryCount": 0,
                "Listeners": []
            }
        ]
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes

If the response body contains an Error field, it indicates the API request failed. This section displays only the error codes of the current API. For more error codes, see [Common error codes](https://docs.byteplus.com/en/docs/clb/Error-codes).


|**Status code** |**Error codes** |**Error message** |**Notes** |
|---|---|---|---|
|400 |InvalidPaging.Malformed |The specified PageNumber or PageSize is malformed. |The format specified for pagination parameter is invalid. |
|400 |LimitExceed.Acl |You've reached the limit on the number of ACLs that you can operate at a time. |The maximum number of ACLs that can be operated in a single request has been reached. |
|400 |LimitExceed.TagFilters.Values |You've reached the limit on the number of tag filter values that you can operate at a time. |You have reached the maximum number of tag values that can be operated on in a single request. |
|400 |InvalidTagFilters.Key.Malformed |The specified TagFilters.Key is malformed. |The specified TagFilters.Key parameter format is invalid. |
|400 |InvalidTagFilters.Value.Malformed |The specified TagFilters.Value is malformed. |The specified TagFilters.Value parameter format is invalid. |
|400 |InvalidTagFilters.Key.Duplicated |The specified TagFilters.Key is duplicated. |The specified TagFilters.Key is duplicated. |
