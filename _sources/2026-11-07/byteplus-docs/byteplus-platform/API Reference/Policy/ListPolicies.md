---
title: "ListPolicies"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listpolicies"
---

Gets a list of policies, including system default policies and user custom policies.

<span id="f7aac165"></span>
## Method

HTTP GET

<span id="2126148c"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListPolicies` |
|Version |String |Yes |`2018-01-01` |
|Scope |String |No |The scope to use for filtering the results. Valid values: `All` |
|Status |Integer |No |Policy status: `active` |
|Limit |Integer |No |Determines the number of records to return. |
|Offset |Integer |No |Determines the starting index. |


<span id="a8a33abf"></span>
## Response parameters


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|PoliciyMetadata |Array of [Policy](https://docs.byteplus.com/en/byteplus-platform/reference/policy) |A list of policies. The `PolicyDocument` field is not included. |
|Limit |Integer |The number of records returned. |
|Offset |Integer |The starting index. |
|Total |Integer |The total number of records. |
