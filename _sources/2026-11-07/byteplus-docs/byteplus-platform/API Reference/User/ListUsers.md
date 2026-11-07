---
title: "ListUsers"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-listusers"
---

Gets a list of users.

<span id="41f00ccf"></span>
## Method

HTTP GET

<span id="1bad9652"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`ListUsers` |
|Version |String |Yes |`2018-01-01` |
|Query |String |No |The fuzzy query of the username and email. |
|Limit |Integer |Yes |Determines the number of records to return. |
|Offset |Integer |Yes |Determines the starting index. |


<span id="9b7284e0"></span>
## Response parameters


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|UserMetadata |Array of [User](https://docs.byteplus.com/en/byteplus-platform/reference/user) |A list of users. |
|Limit |int |The number of records returned. |
|Offset |int |The starting index. |
|Total |int |The total number of records. |
