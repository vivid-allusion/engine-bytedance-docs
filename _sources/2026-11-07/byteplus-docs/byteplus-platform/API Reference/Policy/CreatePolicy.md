---
title: "CreatePolicy"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-createpolicy"
---

Creates a user custom policy.

<span id="b3c2a8a2"></span>
## Method

HTTP GET

<span id="fa5ac2fb"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`CreatePolicy` |
|Version |String |Yes |`2018-01-01` |
|PolicyName |String |Yes |Policy name. |
|Description |String |No |Policy description. |
|PolicyDocument |String |Yes |The PolicyDocument in JSON format. Click [here](https://docs.byteplus.com/byteplus-platform/reference/policy#policydocument) for more details. |


<span id="06cb3a70"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|Policy |[Policy](https://docs.byteplus.com/en/byteplus-platform/reference/policy) |A structure containing the details about the new policy. |
