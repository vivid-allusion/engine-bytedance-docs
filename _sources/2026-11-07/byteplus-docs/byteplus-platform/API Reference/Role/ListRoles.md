---
title: "ListRoles"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listroles"
---

Gets a list of roles.

<span id="cdeba397"></span>
## Method

HTTP GET

<span id="6e3bea2d"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListRoles` |
|Version |String |Yes |`2018-01-01` |
|Limit |Integer |No |Determines the number of records to return. |
|Offset |Integer |No |Determines the starting index. |


<span id="114d4d04"></span>
## Response parameters


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|RoleMetadata |Array of [Role](https://docs.byteplus.com/en/byteplus-platform/reference/role) |A list of roles. |
|Limit |Integer |The number of records returned. |
|Offset |Integer |The starting index. |
|Total |Integer |The total number of records. |
