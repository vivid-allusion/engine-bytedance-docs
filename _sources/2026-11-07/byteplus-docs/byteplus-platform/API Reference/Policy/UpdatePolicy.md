---
title: "UpdatePolicy"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-updatepolicy"
---

Updates a user custom policy.

<span id="c2c969b4"></span>
## Method

HTTP GET

<span id="19e78ab6"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`UpdatePolicy` |
|Version |String |Yes |`2018-01-01` |
|PolicyName |String |Yes |The name of the to\-be\-updated policy. |
|NewPolicyName |String |No |The new policy name. |
|NewPolicyDocument |String |No |The new PolicyDocument. |
|NewDescription |String |No |The new policy description. |


<span id="41ad1ed4"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|Policy |[Policy](https://docs.byteplus.com/en/byteplus-platform/reference/policy) |A structure containing the details about the updated policy. |
