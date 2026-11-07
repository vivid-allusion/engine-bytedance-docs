---
title: "ListEntitiesForPolicy"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listentitiesforpolicy"
---

Gets a list of users and roles that a specified policy is attached to.

<span id="66457c04"></span>
## Method

HTTP GET

<span id="4ee51b32"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListEntitiesForPolicy` |
|Version |String |Yes |`2018-01-01` |
|PolicyName |String |Yes |Policy name. |
|PolicyType |String |Yes |Policy type: `System` |
|EntityFilter |String |No |This parameter is used to filter results. Its valid values are: `All` |
|Limit |Integer |No |Determines the number of records to return. |
|Offset |Integer |No |Determines the starting index. |


<span id="7d3335ce"></span>
## Response parameters


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|PolicyUsers |Array of [PolicyUser](https://docs.byteplus.com/en/byteplus-platform/reference/policyuser) |A list of users that the policy is attached to. Returned when `EntityFilter` is set to `All` or `User`.<br><br>***Note***: Currently, `All` is not supported. |
|PolicyRoles |Array of [PolicyRole](https://docs.byteplus.com/en/byteplus-platform/reference/policyrole) |A list of roles that the policy is attached to. Returned when `EntityFilter` is set to `All` or `Role`.<br><br>***Note***: Currently, `All` is not supported. |
