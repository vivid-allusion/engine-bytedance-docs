---
title: "UpdateRole"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-updaterole"
---

Updates information for a specified role, such as the name, trust policy, and description.

<span id="5538fc12"></span>
## Method

HTTP GET

<span id="212e5d94"></span>
## Request parameter


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`UpdateRole` |
|Version |String |Yes |`2018-01-01` |
|RoleName |String |Yes |The new role name. |
|TrustPolicyDocument |String |No |The new trust policy. |
|DisplayName |String |No |The new display name. |
|Description |String |No |The new description. |
|MaxSessionDuration |Integer |No |The new maximum session duration. The value ranges from `3,600` to `43,200` (in seconds) |


<span id="845af476"></span>
## Response parameter

None.
