---
title: "GetRole"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-getrole"
---

Gets the information about a specified role.

<span id="3d4404cf"></span>
## Method

HTTP GET

<span id="5a723277"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`GetRole` |
|Version |String |Yes |`2018-01-01` |
|RoleName |String |Yes |Role name. |


<span id="550a9495"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|Role |[Role](https://docs.byteplus.com/en/byteplus-platform/reference/role) |A structure containing the details about the specified role. |
