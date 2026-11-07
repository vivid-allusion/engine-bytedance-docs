---
title: "ListAttachedRolePolicies"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listattachedrolepolicies"
---

Gets a list of policies that are attached to a specified role, including system default polices and user custom policies.

<span id="ff1121d1"></span>
## Method

HTTP GET

<span id="657a5b29"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListAttachedRolePolicies` |
|Version |String |Yes |`2018-01-01` |
|RoleName |String |Yes |Role name. |


<span id="3c853a3d"></span>
## Response parameters


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|AttachedPolicyMetadata |Array of [AttachedPolicy](https://docs.byteplus.com/en/byteplus-platform/reference/attachedpolicy) |A list of policies that are attached to the specified role. |
