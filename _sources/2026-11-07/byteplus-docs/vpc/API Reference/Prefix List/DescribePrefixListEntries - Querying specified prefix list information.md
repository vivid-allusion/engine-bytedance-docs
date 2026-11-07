---
title: "DescribePrefixListEntries - Querying specified prefix list information"
product: "Virtual Private Cloud"
product_code: "vpc"
source: "https://docs.byteplus.com/en/docs/vpc/DescribePrefixListEntries"
---

Call the DescribePrefixListEntries API to view the prefix entries of the specified prefix list.

## Debug

[去调试](https://api.byteplus.com/api-explorer/debug?action=DescribePrefixListEntries&serviceCode=vpc&version=2020-04-01&groupName=)

## Request parameters

The table below lists only the request parameters unique to this interface and some common parameters. For more information, see [Common parameters](https://docs.byteplus.com/en/docs/byteplus-platform/reference-common-parameters).

**Action ** String必选`Example: DescribePrefixListEntries`

Interface name. The current API name is `DescribePrefixListEntries`.

**Version ** String必选 `Example: 2020-04-01`

Interface version. The current API version is `2020-04-01`.

**PrefixListId ** String必选 `Example: pl-bp1fg655nh68xyz9****`

ID of the prefix list.

You can call the [DescribePrefixLists](https://docs.byteplus.com/en/docs/vpc/DescribePrefixLists) API to query the prefix list ID.

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

Total number of prefix list entries that match the criteria.

> **tip**

> This parameter is scheduled for deprecation. It becomes meaningless when using `NextToken` and `MaxResults` for paginated queries.

**PageNumber ** Integer`Example: 1`

The current page number.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**PageSize ** Integer`Example: 10`

The number of rows on the current page.

> **tip**

> This parameter is scheduled for deprecation. We recommend using `NextToken` and `MaxResults` for paginated queries instead.

**NextToken ** String`Example: caeba0bbb2be03f84eb48b699f0a****`

The pagination token returned by this API call, which marks the position for the next query. An empty return indicates there is no next page.

**PrefixListEntries ** Object[]`Example: -`

A collection of prefix list entries.

**Cidr ** String`Example: 1.1.1.0/24`

CIDR of the prefix entry.

**Description ** String`Example: TestDescription`

Description of the prefix list entry.

**PrefixListId ** String`Example: pl-bp1fg655nh68xyz9****`

ID of the prefix list.

## Request example

```json
GET /?Action=DescribePrefixListEntries&Version=2020-04-01&PrefixListId=pl-bp1fg655nh68xyz9**** HTTP/1.1
Host: vpc.cn-beijing.byteplusapi.com.cn
X-Date: 20251121T094038Z
Authorization: HMAC-SHA256 Credential=Adfks******wekfwe/20251121/cn-beijing/vpc/request, SignedHeaders=host;x-date, Signature=47a7d934ff7b37c03938******cd7b8278a40a1057690c401e92246a0e41085f
```

## Response example

```json
{
    "ResponseMetadata": {
        "RequestId": "20230604110420****100232280022D31",
        "Action": "DescribePrefixListEntries",
        "Version": "2020-04-01",
        "Service": "vpc",
        "Region": "cn-beijing"
    },
    "Result": {
        "NextToken": "caeba0bbb2be03f84eb48b699f0a****",
        "PageNumber": 1,
        "PageSize": 10,
        "PrefixListEntries": [
            {
                "Cidr": "1.1.1.0/24",
                "Description": "TestDescription",
                "PrefixListId": "pl-bp1fg655nh68xyz9****"
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
|400 |DryRunOperation |Exception raised to indicate a successfully authorized action when the DryRun flag is set to true. |This request is set to DryRun action. The action has been authorized but has not been executed. |
|400 |InvalidMaxResults.Malformed |The specified parameter MaxResults is malformed. |The number of queries is invalid. |
|400 |InvalidNextToken.Malformed |The specified parameter NextToken is invalid. |NextToken is invalid for the query. |
|400 |InvalidPage.Malformed |The specified page is malformed. |The specified pagination parameter is invalid. |
|404 |InvalidPrefixList.NotFound |The specified prefix list does not exist. |The specified prefix list does not exist. |
