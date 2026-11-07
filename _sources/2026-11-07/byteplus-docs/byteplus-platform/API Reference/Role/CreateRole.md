---
title: "CreateRole"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-createrole"
---

Creates a role.

<span id="9a57c3ad"></span>
## Method

HTTP GET

<span id="65ea6a06"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`CreateRole` |
|Version |String |Yes |`2018-01-01` |
|TrustPolicyDocument |String |Yes |The role's trust policy. |
|RoleName |String |Yes |Role name. |
|DisplayName |String |Yes |The role's display name. |
|Description |String |No |Role description. |
|MaxSessionDuration |int |No |The maximum session duration of the role. The value ranges from `3,600` to `43,200` (in seconds). |


<span id="8ffd1c02"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|Role |[Role](https://docs.byteplus.com/en/byteplus-platform/reference/role) |A structure containing the details about the new role. |
