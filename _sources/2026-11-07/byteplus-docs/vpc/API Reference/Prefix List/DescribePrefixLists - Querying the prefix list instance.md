---
title: "DescribePrefixLists - Querying the prefix list instance"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists"
---

Call the DescribePrefixLists API to query prefix lists that meet specified conditions.

<span id=".6LCD6K-V"></span>
## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePrefixLists&serviceCode=vpc&version=2020-04-01&groupName=)


<span id=".6K-35rGC5Y-C5pWw"></span>
## Request parameters

The following only details request parameters specific to this API and key common parameters. More information can be found in [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).



**Action ** <span data-label="purple">String </span><span data-api-tag="require|g3DHPN">必选</span> `Example: DescribePrefixLists`

The interface name. The current API name is `DescribePrefixLists`.



**Version ** <span data-label="purple">String </span><span data-api-tag="require|380wSD">必选</span> `Example: 2020-04-01`

The interface version. the current API version is `2020-04-01`.



**PrefixListIds.N ** <span data-label="purple">String </span>`optional` `Example: pl-bp1fg655nh68xyz9****`

The instance ID of the prefix list.


* Parameter \- N: Represents the serial number of the prefix list. The maximum number per call is 100.

* Separate multiple prefix list IDs with ampersands (&).



**PrefixListName ** <span data-label="purple">String </span>`optional` `Example: PrefixList-1`

Name of the prefix list to query.



**IpVersion** <span data-label="purple">String</span> `optional` `Example: IPv4`

IP version of the prefix list. Values:


* IPv4: IPv4 version.

* IPv6: IPv6 version.



**ProjectName ** <span data-label="purple">String </span>`optional` `Example: default`

Select the project to which the prefix list belongs.



**TagFilters.N.Key ** <span data-label="purple">String </span>`optional` `Example: k1`

The tag key.


* N represents the sequence number of a tag key. Values: 1\-10.

* Separate multiple tag keys with &. Multiple tag keys have a logical AND relationship. The query returns Prefix Lists tagged with all the specified keys.

* Duplicate values are not allowed.



**TagFilters.N.Values.N ** <span data-label="purple">String </span>`optional` `Example: v1`

The tag value.


* The first N specifies the serial number of a tag key. Valid values: 1–10.

* The second N represents the serial number of the tag value. Valid values: 1–3. Multiple tag values under the same tag key are combined using a logical OR operation, meaning the query returns Prefix Lists that have any of the specified tag values for that key.

* Separate multiple tag values with ampersands (&).


<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>



* <div data-tips="true" data-tips-type="tip">If this parameter is passed in, <code>TagFilters.N.Key</code> must be passed in first.</div>


* <div data-tips="true" data-tips-type="tip">Passing an empty string queries for Prefix Lists with an empty tag value.</div>




**PageNumber ** <span data-label="purple">Integer </span>`optional` `Example: 1`

Page number of the list. Default: 1.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`optional` `Example: 20`

The number of entries per page in a pagination query. Maximum: 100. Default: 20.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**NextToken ** <span data-label="purple">String </span>`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in pagination queries.


* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.



**MaxResults ** <span data-label="purple">Integer </span>`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.



&nbsp;

<span id=".6L-U5Zue5Y-C5pWw"></span>
## Response parameters

Only the response parameters specific to this API are listed below. More information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).



**RequestId ** <span data-label="purple">String </span>`Example: 2021062415303301022514515207C4****`

Request ID.



**TotalCount ** <span data-label="purple">Integer </span>`Example: 2`

The total number of prefix lists that meet the condition.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. It becomes meaningless when using <code>NextToken</code> and <code>MaxResults</code> for paginated queries.</div>




**PageNumber ** <span data-label="purple">Integer </span>`Example: 1`

The current page number.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**PageSize ** <span data-label="purple">Integer </span>`Example: 10`

The count of entries per page in the current pagination.

<div data-tips="true" data-tips-type="tip" data-tips-is-title="true">tip</div>


<div data-tips="true" data-tips-type="tip">This parameter is scheduled for deprecation. We recommend using <code>NextToken</code> and <code>MaxResults</code> for pagination queries.</div>




**NextToken ** <span data-label="purple">String </span>`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.



**PrefixLists ** <span data-label="purple">Object[] </span>`Example: -`

Collection of VPC prefix lists.


**PrefixListId ** <span data-label="purple">String </span>`Example: pl-bp1fg655nh68xyz9****`

ID of the VPC prefix list.



**PrefixListName ** <span data-label="purple">String </span>`Example: PrefixList-1`

Name of the VPC Prefix List.



**Description ** <span data-label="purple">String </span>`Example: PrefixList_Common`

Description of the VPC prefix list.



**IpVersion ** <span data-label="purple">String </span>`Example: IPv4`

IP version of the prefix list.



**MaxEntries ** <span data-label="purple">Integer </span>`Example: 10`

The maximum number of entries allowed for the prefix list.



**AssociationCount ** <span data-label="purple">Integer </span>`Example: 5`

Number of resources associated with the prefix list.



**Cidrs ** <span data-label="purple">String[] </span>`Example: 1.XX.XX.0/24`

CIDR block information of the prefix list.



**Status ** <span data-label="purple">String </span>`Example: Available`

Status of the prefix list. Values:


* Available

* Creating

* Deleting

* Pending: Modifying.



**ProjectName ** <span data-label="purple">String </span>`Example: default`

The name of the project to which the prefix list belongs.



**Tags ** <span data-label="purple">Object[] </span>`Example: -`

Tag information of the prefix list.


**Key ** <span data-label="purple">String </span>`Example: k1`

The tag key.



**Value ** <span data-label="purple">String </span>`Example: v1`

The tag value.




**CreationTime ** <span data-label="purple">String </span>`Example: 2017-12-05T22:40:00+08:00`

Creation time of the VPC prefix list.



**UpdateTime ** <span data-label="purple">String </span>`Example: 2017-12-05T22:40:00+08:00`

The modified time of the VPC prefix list.




&nbsp;

<span id=".6K-35rGC56S65L6L"></span>
## Request examples

```json
GET /?Action=DescribePrefixLists&Version=2020-04-01&NextToken=caeba0bbb2be03f84eb48b699f0a****&MaxResults=50 HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20250804T033538Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20250804/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```


<span id=".6L-U5Zue56S65L6L"></span>
## Response examples

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePrefixLists",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "PrefixLists": [
            {
                "Tags": [
                    {
                        "Key": "k1",
                        "Value": "v1"
                    }
                ],
                "Cidrs": [
                    ""
                ],
                "Status": "Available",
                "IpVersion": "IPv4",
                "MaxEntries": 10,
                "UpdateTime": "2017-12-05T22:40:00+08:00",
                "Description": "PrefixList_Common",
                "ProjectName": "default",
                "CreationTime": "2017-12-05T22:40:00+08:00",
                "PrefixListId": "pl-bp1fg655nh68xyz9****",
                "PrefixListName": "PrefixList-1",
                "AssociationCount": 5
            }
        ],
        "RequestId": "2021062415303301022514515207C4****"
    }
}
```


<span id=".6ZSZ6K-v56CB"></span>
## Error codes


|Status code |Error codes |Error message |Notes |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of query results is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter.IpVersion |The specified IP version is not supported. |The specified IP Address type is not supported. |
|400 |InvalidTagFilter.Disorder |The specified index order of tag filter is malformed. |The index order format of the specified tag filter is invalid. |
|400 |InvalidTagFilterKey.Malformed |The specified parameter tag filter key is invalid. |The tag filter key is invalid. |
|400 |InvalidTagFilterValue.Malformed |The specified parameter tag filter value is invalid. |The tag filter value is invalid. |
|400 |LimitExceeded.PrefixListId |You've reached the limit on the number of prefix list IDs that you can describe. |The maximum allowed number of Prefix List IDs for a single query has been reached. |
|400 |LimitExceeded.TagFilterKey |You've reached the limit on the number of tag keys that you can filter. |You have reached the maximum number of filter tag keys that can be specified in a single request. |
|400 |LimitExceeded.TagFilterValue |You've reached the limit on the number of tag values that you can filter. |The maximum number of filter tag values that can be specified in a single request has been reached. |
