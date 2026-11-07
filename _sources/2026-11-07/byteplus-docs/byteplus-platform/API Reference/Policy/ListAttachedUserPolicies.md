---
title: "ListAttachedUserPolicies"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listattacheduserpolicies"
---

Gets a list of policies that are attached to a specified user, including system default policies and user custom policies.

<span id="fb3ba5eb"></span>
## Method

HTTP GET

<span id="92b790b4"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListAttachedUserPolicies` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |Username. |


<span id="9e98cbae"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|AttachedPolicyMetadata |Array of [AttachedPolicy](https://docs.byteplus.com/en/byteplus-platform/reference/attachedpolicy) |A list of policies that are attached to the specified user. |
