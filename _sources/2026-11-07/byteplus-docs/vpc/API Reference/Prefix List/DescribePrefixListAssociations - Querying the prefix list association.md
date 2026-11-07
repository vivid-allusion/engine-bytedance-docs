---
title: "DescribePrefixListAssociations - Querying the prefix list association"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribePrefixListAssociations"
---

Call the DescribePrefixListAssociations API to query the resources associated with a specified prefix list.

## Instructions

* When multiple request parameters are passed in, the system queries based on these parameters and returns Prefix Lists that match all conditions. If no matching Prefix Lists are found, an empty value is returned.

* If none of the optional request parameters are provided, the query will be performed under the current logged\-in account and return all Prefix Lists belonging to this account.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePrefixListAssociations&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选 `Example: DescribePrefixListAssociations`

Interface name. The current API name is `DescribePrefixListAssociations`.

**Version ** String必选 `Example: 2020-04-01`

The interface version. The current API version is `2020-04-01`.

**PrefixListId ** String必选 `Example: pl-bp1fg655nh68xyz9****`

Prefix List ID.

You can call the [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to query the Prefix List ID.

**ResourceType ** String`optional` `Example: VpcRouteTable`

Associated resource type, valid values:

* VpcRouteTable: Route table.

* VpcSecurityGroup: Security group.

* TrRouteTable: Route table of the transit router.

* TrRoutePolicyTable: Route policy table of the transit router.

**PageNumber ** Integer`optional` `Example: 1`

Page number of the list. Default: 1.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`optional` `Example: 20`

The number of rows per page for paginated queries. Maximum: 100. Default: 20.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`optional` `Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token that is used to mark the position in paginated queries.

* If left blank, the query starts from the beginning.

* Provide the `NextToken` returned from a previous call to this API, the query continues from that pagination position.

**MaxResults ** Integer`optional` `Example: 50`

The number of query results. Default: 10. Maximum: 100.

## Response parameters

Only the response parameters specific to this API are listed below. For more information, see [Response structure](https://docs.byteplus.com/en/docs/byteplus-platform/reference-request-response).

**RequestId ** String`Example: 2021062415303301022514515207C4****`

Request ID.

**TotalCount ** Integer`Example: 2`

Total number of prefix list's associated resources that match the criteria.

> **tip**

> This parameter is scheduled for deprecation. It becomes meaningless when using `NextToken` and `MaxResults` for paginated queries.

**PageNumber ** Integer`Example: 1`

Current page number.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`Example: 10`

The number of rows on the current page.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates no next page.

**PrefixListAssociations ** Object[]`Example: -`

VPC prefix list association collection.

**ResourceId ** String`Example: vtb-bp1drpcfz9srr393h****`

Associated resource ID.

**ResourceType ** String`Example: VpcRouteTable`

The type of associated resources.

## Request example

```json
GET /?Action=DescribePrefixListAssociations&Version=2020-04-01&PrefixListId=pl-0b78hw45f****&ResourceType=VpcRouteTable HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePrefixListAssociations",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "PageNumber": 1,
        "PageSize": 10,
        "PrefixListAssociations": [
            {
                "ResourceId": "vtb-bp1drpcfz9srr393h****",
                "ResourceType": "VpcRouteTable"
            }
        ],
        "RequestId": "2021062415303301022514515207C4****",
        "TotalCount": 2
    }
}
```

## Error codes

|Status code |Error codes |Error message |Description |
|---|---|---|---|
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun. The action is authorized but not executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of queries is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|400 |InvalidParameter.ResourceType |The specified type of resource is not supported. |The specified resource type is not supported. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified Prefix List does not exist. |
