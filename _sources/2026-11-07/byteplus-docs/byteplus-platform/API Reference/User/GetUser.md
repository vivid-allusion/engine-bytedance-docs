---
title: "GetUser"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-getuser"
---

Gets the information about a specified user.

<span id="30d19c9a"></span>
## Method

HTTP GET

<span id="28bf782e"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`GetUser` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |Username. |


<span id="6807ce67"></span>
## Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|User |[User](https://docs.byteplus.com/en/byteplus-platform/reference/user) |A structure containing the details about the specified user. |
