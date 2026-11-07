---
title: "UpdateUser"
product: "BytePlus Billing Console"
product_code: "byteplus-platform"
source: "https://docs.byteplus.com/en/docs/byteplus-platform/reference-updateuser"
---

Updates information for a specified user.

<span id="5b4d87fb"></span>
## Method

HTTP GET

<span id="cab93022"></span>
## Request parameters


|**Parameter** |**Data Type** |**Required (Yes/No)**  |**Description** |
|---|---|---|---|
|Action |String |Yes |`UpdateUser` |
|Version |String |Yes |`2018-01-01` |
|UserName |String |Yes |The name of the to\-be\-updated user. |
|NewUserName |String |No |The new username. |
|NewDisplayName |String |No |The new display name. |
|NewMobilePhone |String |No |The new phone number with a county calling code. For example: `+65 80000000`. |
|NewEmail |String |No |The new email. |
|NewDescription |String |No |The new user description. |


Response parameter


|**Parameter** |**Data Type** |**Description** |
|---|---|---|
|User |[User](https://docs.byteplus.com/en/byteplus-platform/reference/user) |A structure containing the details about the updated user. |
